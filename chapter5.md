# Viewでの描画処理

## WindowとView

Androidでは、Activityを継承したクラスは、Windoowを保持する。WindowにViewを貼り付ける事で、描画関連の処理をおこなう事ができる。

![](chapter5/pre0501.png)

Viewクラスを継承したクラスは、Window.setContentView() または、Window.addContentView()で、Windowに貼り付けられる。

## 独自のViewを作成する

