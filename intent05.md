# Intentを作成する


Intentを呼び出す手段

- 明示的なIntent起動
- 暗黙的なIntent起動

があります。明示的なIntent起動では、パッケージ名とクラス名を指定します。明示的なIntentでは、アクション名を指定します。

明示的
```java
Intent selectIntent = new Intent();
selectIntent.setClassName("com.example.intentcooperationsample","com.example.intentcooperationsample.MyActivity");
startActivityForResult(selectIntent, 1);
```
暗黙的
```java
Uri uri = Uri.parse("http://www.gclue.com/");
Intent browserIntent = new Intent(Intent.ACTION_VIEW,uri);
startActivity(browserIntent);
```


