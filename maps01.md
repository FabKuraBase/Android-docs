# API Keyの取得

## 証明書のフィンガプリントの取得

まず、Googke Maps API Keyを発行するために、開発で使用しているMacのフィンガプリントの取得をおこないます。

    $  keytool -list -v -keystore ~/.android/debug.keystore

![map0101](img-map01/map01.png)


## Google API Consoleにログイン

https://code.google.com/apis/console/?pli=1

にログインします。