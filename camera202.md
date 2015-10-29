# CameraManager

## Cameraの取得

Camera2では、CameraManagerを用いてCameraをOpenします。
まず、最初にCameraManagerを用いて、カメラを取得します。Cameraには、フロントカメラやバックカメラが存在しています。今回は、バックカメラを取得します。

MainActivity.java
```java
package utsunomiya.gclue.com.camerasample;

import android.app.Activity;
import android.content.Context;
import android.graphics.SurfaceTexture;
import android.os.Bundle;
import android.util.Log;
import android.util.Size;
import android.view.Menu;
import android.view.MenuItem;
import android.view.Surface;
import android.view.TextureView;
import android.hardware.camera2.*;
import android.view.View;
import android.view.Window;
import android.view.WindowManager;
import android.hardware.camera2.params.StreamConfigurationMap;
import android.hardware.camera2.CameraCharacteristics;
import java.util.Arrays;

public class MainActivity extends Activity implements TextureView.SurfaceTextureListener {

    /** TextureView */
    private TextureView mTextureView;
    /** SurfaceTexture */
    private SurfaceTexture mSurfaceTexture;
    /** Surface */
    private Surface mSurface;
    /** Log用のTag */
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

## サイズの取得　

バックカメラを取得したら、今度は、利用可能なサイズを取得します。



| 配列の番号 |Nexus5 | 2:0 | 3:0 |
| -- | -- | -- | -- |
| 0 | 1280x960 | 2:2 | 3:2 |
| 1 | 1280x768 | 2:3 | 3:3 |
| 0:4 | 1:4 | 2:4 | 3:4 |
| 0:5 | 1:5 | 2:5 | 3:5 |
| 0:6 | 1:6 | 2:6 | 3:6 |
| 0:7 | 1:7 | 2:7 | 3:7 |
| 0:8 | 1:8 | 2:8 | 3:8 |
| 0:9 | 1:9 | 2:9 | 3:9 |
| 0:10 | 1:10 | 2:10 | 3:10 |
size[0]1280x960
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[1]1280x768
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[2]1280x720
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[3]1024x768
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[4]800x600
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[5]800x480
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[6]720x480
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[7]640x480
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[8]352x288
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[9]320x240
10-30 03:48:10.663  21761-21761/utsunomiya.gclue.com.camerasample I/CAMERA﹕ size[10]176x144