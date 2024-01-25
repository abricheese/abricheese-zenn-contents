---
title: "掴めるものを増やす"
---
:::message
Unreal Engine Version : 5.3.2
:::

# Actorを作成する

コンテンツドロワーを開きます。
![](https://storage.googleapis.com/zenn-user-upload/6d9118d788a5-20240113.png)

フォルダーを作成します。
![](https://storage.googleapis.com/zenn-user-upload/3c00de7d8ecc-20240113.png)

図のような構成になるようにフォルダーを作成します。
![](https://storage.googleapis.com/zenn-user-upload/f3096f43b570-20240113.png)

フォルダーは数字→アルファベット順に並ぶため、先頭に数字を入れておくと意図した順番に配置できるので便利です。

ブループリントを作成します。
![](https://storage.googleapis.com/zenn-user-upload/304534ddbfd2-20240113.png)

親クラスはActorを選択します。
![](https://storage.googleapis.com/zenn-user-upload/f0710b37b9ad-20240113.png)

名前を［BP_GrabbableObj］に設定します。
![](https://storage.googleapis.com/zenn-user-upload/ffc65943ccfd-20240113.png)

### 命名規則の参考ページ

https://github.com/Allar/ue5-style-guide

作成した\[BP_GrabbableObj\]をダブルクリックして編集画面を開きます。
![](https://storage.googleapis.com/zenn-user-upload/af2b2005a657-20240113.png)

# 掴めるようにする

![](https://storage.googleapis.com/zenn-user-upload/4908df3ba5ee-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/383ea7ecd4bd-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/725e154fb2cf-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/24009520f6c3-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/797bb36b7ba9-20240113.png)

下記のような親子関係になるようにします。
![](https://storage.googleapis.com/zenn-user-upload/c0bc54af87ec-20240113.png)


コンパイルして保存します。
![](https://storage.googleapis.com/zenn-user-upload/6bf3a0373fcf-20240113.png)


# Actorを配置する


![](https://storage.googleapis.com/zenn-user-upload/dd6c4fb2d336-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/8dc6e1502801-20240113.png)

## 編集画面でのカメラ操作
- 右クリック + マウス移動 ： カメラの回転
- マウスホイール回転 ： カメラの前後移動
- 右クリック + W/A/S/D/Q/Eキー ： カメラの前後左右上下移動

## 編集画面でのオブジェクトの操作
- Wキー ： 移動に切り替え
- Eキー ： 回転に切り替え
- Rキー ： 拡大縮小に切り替え
- 移動・回転・拡大縮小はスナップで一定値ずつ動かすこともできる
- Endキー ： オブジェクトを着地させる

![](https://storage.googleapis.com/zenn-user-upload/5565923879ad-20240113.png)

## VRプレビューで掴んでみる

VRプレビューを実行して、動作を確認してみましょう。

https://youtu.be/HjD9wfnS7Hg


# 物理挙動を有効化する

![](https://storage.googleapis.com/zenn-user-upload/f70e378c6f3c-20240113.png)





# 掴んだ時の挙動を変更する


![](https://storage.googleapis.com/zenn-user-upload/d7cb0caab6ba-20240113.png)



