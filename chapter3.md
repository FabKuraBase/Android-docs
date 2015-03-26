# アプリの種類

Androidでは、画面のあるアプリケーションを開発する場合は、Activityで開発する。Acivity以外に、画面のない常駐型のアプリケーションを開発可能なServiceや、データへのアクセス用のContentsProvider、AndroidからのBroadcastを取得するためのBroadcast Recieverが存在しています。

![](pre0301.jpg)

## Activity



MainActivity.java
```java
package com.gclue.activitysample;

import android.os.Bundle;
import android.support.v7.app.ActionBarActivity;
import android.view.Menu;
import android.view.MenuItem;


public class MainActivity extends ActionBarActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```
