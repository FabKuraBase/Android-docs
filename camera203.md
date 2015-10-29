# Cameraをオープン


MainActivity.java
```java
package utsunomiya.gclue.com.camerasample;

import android.app.Activity;
import android.content.Context;
import android.graphics.SurfaceTexture;
import android.os.Bundle;
import android.util.Log;
import android.util.Size;
import android.view.Surface;
import android.view.TextureView;
import android.hardware.camera2.*;
import android.hardware.camera2.params.StreamConfigurationMap;
import android.hardware.camera2.CameraCharacteristics;

public class MainActivity extends Activity implements TextureView.SurfaceTextureListener {

    /**
     * TextureView
     */
    private TextureView mTextureView;
    /**
     * SurfaceTexture
     */
    private SurfaceTexture mSurfaceTexture;
    /**
     * Surface
     */
    private Surface mSurface;
    /**
     * CameraSize
     */
    private Size mCameraSize;
    /**
     * Log用のTag
     */
    private static final String TAG = "CAMERA";


    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // TextureViewをactivity_mainから取り込み
        mTextureView = (TextureView) findViewById(R.id.camera_texture_view);
        // TextureViewのリスターを設定
        mTextureView.setSurfaceTextureListener(this);
        // SurfaceTextureのインスタンスを取得
        mSurfaceTexture = mTextureView.getSurfaceTexture();
    }

    // StateCallback
    CameraDevice.StateCallback mStateCallback = new CameraDevice.StateCallback()
    {
        @Override
        public void onDisconnected(CameraDevice device){
            Log.i(TAG, "onDisconnected");

        }

        @Override
        public void onError(CameraDevice device, int error){
            Log.i(TAG, "onError");

        }

        @Override
        public void onOpened(CameraDevice device){
            Log.i(TAG, "onOpened");

        }
    };

    @Override
    public void onSurfaceTextureAvailable(SurfaceTexture surface, int width, int height) {

        Log.i(TAG, "onSurfaceTextureAvailable");

        mSurfaceTexture = surface;
        mSurface = new Surface(mSurfaceTexture);

        try {
            CameraManager manager = (CameraManager) getSystemService(Context.CAMERA_SERVICE);
            for( String cameraId: manager.getCameraIdList()){

                Log.i(TAG, "cameraId:" + cameraId);

                // 取得したCameraIdからキャラスタリスチクスを取得
                CameraCharacteristics characteristics = manager.getCameraCharacteristics(cameraId);

                // Frontカメラの場合
                if (characteristics.get(CameraCharacteristics.LENS_FACING) == CameraCharacteristics.LENS_FACING_FRONT)
                {
                    Log.i(TAG, "FrontCamera");

                    // Mapを取得
                    StreamConfigurationMap map = characteristics.get(CameraCharacteristics.SCALER_STREAM_CONFIGURATION_MAP);

                    // サイズの一覧を取得
                    Size[] mOutputSize = map.getOutputSizes(SurfaceTexture.class);
                    for (int i = 0; i < mOutputSize.length; i++) {
                        Log.i(TAG, "size[" + i + "]" + mOutputSize[i].toString());
                    }

                    // カメラサイズ0番目をGlobalな関数に格納
                    mCameraSize = map.getOutputSizes(SurfaceTexture.class)[0];

                    // カメラをオープン
                    manager.openCamera(cameraId, mStateCallback, null);
                }
                // Backカメラの場合
                else if (characteristics.get(CameraCharacteristics.LENS_FACING) == CameraCharacteristics.LENS_FACING_BACK)
                {
                    Log.i(TAG, "BackCamera");
                }
            }
        }
        catch (Exception e) {
            Log.i(TAG, "Error:"+e);
        }
    }

    @Override
    public void onSurfaceTextureSizeChanged(SurfaceTexture surface, int width, int height) {
        Log.i(TAG, "onSurfaceTextureSizeChanged");

    }

    @Override
    public boolean onSurfaceTextureDestroyed(SurfaceTexture surface) {
        Log.i(TAG, "onSurfaceTextureDestroyed");

        return false;
    }

    @Override
    public void onSurfaceTextureUpdated(SurfaceTexture surface) {
        Log.i(TAG, "onSurfaceTextureUpdated");

    }
}
```