# Cameraへのオーバーレイ

CameraにViewをOverlayしてみます。


MainActivity.java
```java
package utsunomiya.gclue.com.camerasample;

import android.app.Activity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuItem;
import android.view.ViewGroup;
import android.view.Window;
import android.view.WindowManager;

public class MainActivity extends Activity {

    /** LOGCAT用のTAG. */
    private static final String TAG = "CAMERA_ACTIVITY";

    /** Camera用のSurfaceView. */
    private static CameraView mCameraView;

    /** OverlayするView. */
    private static MyView mView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        getWindow().addFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN);
        requestWindowFeature(Window.FEATURE_NO_TITLE);

        mCameraView = new CameraView(this);
        setContentView(mCameraView);

        mView = new MyView(this);
        addContentView(mView, new ViewGroup.LayoutParams(ViewGroup.LayoutParams.WRAP_CONTENT, ViewGroup.LayoutParams.WRAP_CONTENT));
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.menu_main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_settings) {
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
}

```

MyView.java
```java
package utsunomiya.gclue.com.camerasample;

/**
 * Created by sasakiakira on 15/10/30.
 */
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Paint;
import android.view.MotionEvent;
import android.view.View;

class MyView extends View {

    private int x;
    private int y;

    /**
     * コンストラクタ
     *
     * @param context
     */
    public MyView(Context context) {
        super(context);
        setFocusable(true);
    }

    /**
     * 描画処理
     */
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);

        // 描画するための線の色を設定.
        Paint mPaint = new Paint();
        mPaint.setStyle( Paint.Style.FILL );
        mPaint.setARGB( 255, 255, 255, 100 );

        // 長方形を描画.
        canvas.drawRect( x, y, x + 100, y + 100, mPaint );
    }

    /**
     * タッチイベント
     */
    public boolean onTouchEvent(MotionEvent event) {

        // X,Y座標の取得
        x = (int)event.getX();
        y = (int)event.getY();

        // 再描画の指示
        invalidate();

        return true;
    }
}
```