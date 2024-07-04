---
title: "シネカメラを動かす"
---
:::message
Unreal Engine Version : 5.3.2
:::

# 2台目のシネカメラを追加する
「アウトライナー」でシネカメラ（Cine Camera Actor）を右クリックし、複製します。
（複製することで、1台目のカメラで設定した追跡とフォーカスの設定をそのまま引き継げます。）
![](https://storage.googleapis.com/zenn-user-upload/f00f38d8981d-20240704.png)

複製したシネカメラをシーケンサーに追加します。
![](https://storage.googleapis.com/zenn-user-upload/818c5e1b04fa-20240704.png)


# カメラカットに2台目のシネカメラを追加する

![](https://storage.googleapis.com/zenn-user-upload/1e6bd6845a35-20240704.png)

カメラカットが2台のカメラに分割されました。
![](https://storage.googleapis.com/zenn-user-upload/4fa10f57e99d-20240704.png)


# シネカメラをシーケンサーで移動させる
撮影したい位置・画角を決め、1個目のキーを追加します。
![](https://storage.googleapis.com/zenn-user-upload/36ba65f12892-20240704.png)

移動後のフレーム位置に合わせ、画角を移動先の位置に変更し、キーを追加します。
![](https://storage.googleapis.com/zenn-user-upload/cc9f449fba45-20240704.png)


