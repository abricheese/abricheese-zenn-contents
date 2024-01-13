---
title: "スムーズ移動できるように"
---
:::message
Unreal Engine Version : 5.3.2
:::
# 新規入力を作成
![](https://storage.googleapis.com/zenn-user-upload/dbcaacd4807e-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/bb9159864cb8-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/034a48d7f2ce-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/2df7d0fa7624-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/8b4bd4fa965b-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/f66de64d0265-20240113.png)

Meta Questのコントローラーの左手のスティック操作をしたときにIA_SmoothMoveが呼び出されるようにします。
![](https://storage.googleapis.com/zenn-user-upload/7389a3e9c663-20240113.png)

このままではVRテンプレートのデフォルトの回転操作（左スティック左右）とバッティングしてしまうので、回転操作を右スティック左右へ変更します。
（FPSゲームの標準的な操作方法に準拠）

![](https://storage.googleapis.com/zenn-user-upload/dbc4d7e0697c-20240113.png)


# Pawnの編集

![](https://storage.googleapis.com/zenn-user-upload/eb638a97982b-20240113.png)

UE標準の移動機能を使いたいので、VRPawnの親クラスをCharacterに変更します。
- Pawn ： プレイヤーが操作できる機能を持ったクラス
- Character ： Pawnの子クラスで、Pawnの機能に加えて移動などの機能が備わっている

![](https://storage.googleapis.com/zenn-user-upload/2e6d6ddcf2ea-20240113.png)

このままでは回転が上手くできないので、[Use Controller Rotation Yaw]のチェックをオフにします。

![](https://storage.googleapis.com/zenn-user-upload/b57e8ad5c8f9-20240113.png)


左スティックでの入力処理を実装します。

![](https://storage.googleapis.com/zenn-user-upload/341cc1709836-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/bc31d3260a4a-20240113.png)

@[blueprintue](https://blueprintue.com/render/s5yqc2tw/)

## 地面の高さに対して高すぎるので調整する

![](https://storage.googleapis.com/zenn-user-upload/62eb98996241-20240113.png)


## アイテムを掴んだ時にうまく移動できないのを修正する
VRPawnのコリジョンと掴んだもののコリジョンが反応してしまうため、うまく移動できないことがあります。
今回はVRPawnのコリジョンを小さくすることで解消します。

![](https://storage.googleapis.com/zenn-user-upload/56a864e4ebcf-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/0b95ed64b44e-20240113.png)


