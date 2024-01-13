---
title: "移動方法を切り替える"
---
:::message
Unreal Engine Version : 5.3.2
:::

# ワープ移動を左スティックでできるように

![](https://storage.googleapis.com/zenn-user-upload/3fb6735fd010-20240113.png)

# VRPawnに切り替え処理を追加

マクロ（繰り返し使用できるノードの塊）を作成します。

![](https://storage.googleapis.com/zenn-user-upload/ea512a8de800-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/f130c6506133-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/ad7569edb547-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/8b7529cd0deb-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/c79f293db950-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/7e59d10c95e5-20240113.png)

移動モードの切り替え処理を作成します。
イベントグラフで右クリックしてイベントを作成します。

![](https://storage.googleapis.com/zenn-user-upload/22baf7a3dfce-20240113.png)

下記のように実装します。

![](https://storage.googleapis.com/zenn-user-upload/4cc729bfbaae-20240113.png)


作成したマクロを配置します。

![](https://storage.googleapis.com/zenn-user-upload/060cd3314e5e-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/276260980dfa-20240113.png)


@[blueprintue](https://blueprintue.com/render/m8rz227_/)


![](https://storage.googleapis.com/zenn-user-upload/51a655711afd-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/91377d06f2f4-20240113.png)

@[blueprintue](https://blueprintue.com/render/dutn9a81/)


# 切り替えのUIを作成

![](https://storage.googleapis.com/zenn-user-upload/dfdc7e5994e5-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/2490dc8133d7-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/0fe4f57e382d-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/c99394373ce5-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/d0951ab16e54-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/9182245a94af-20240113.png)

下記のように実装します。
![](https://storage.googleapis.com/zenn-user-upload/ef7cf6fde37e-20240113.png)





@[blueprintue](https://blueprintue.com/render/_ob0k8w0/)
