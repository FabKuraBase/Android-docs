# Viewでの描画処理

## WindowとView

Androidでは、Activityを継承したクラスは、Windoowを保持する。WindowにViewを貼り付ける事で、描画関連の処理をおこなう事ができる。

![](chapter5/pre0501.png)

Viewクラスを継承したクラスは、Window.setContentView() または、Window.addContentView()で、Windowに貼り付けられる。

## 新規プロジェクトの作成

[File]-[New Project]を選択し、新しいプロジェクトを作成する。

![](chapter5/pre0502.png)

Application nameを設定し、[Next]ボタンを押す。

![](chapter5/pre0503.png)

Minimum SDKのAPIバージョンを設定する。

![](chapter5/pre0504.png)

ActivityはBlack Activityを選択する。

![](chapter5/pre0505.png)

![](chapter5/pre0506.png)
