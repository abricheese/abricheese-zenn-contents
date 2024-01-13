---
title: "特定のエリアに入ったら的が出現する"
---
:::message
Unreal Engine Version : 5.3.2
:::

# 的が起き上がるアニメーションを作る
Unreal Engineには今回のやり方の他にもBlenderなどで作成したアニメーションを再生する機能がありますが、今回はTimelineを使った疑似的なアニメーションを使用します。

## Cubeのピボット位置を変更

![](https://storage.googleapis.com/zenn-user-upload/b92e5f4d3dbe-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/60e32665b03b-20240113.png)

## 的の動く向きがわかるようにArrowを追加する
![](https://storage.googleapis.com/zenn-user-upload/52d45221cc14-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/36481a2eff07-20240113.png)

## Timelineを使った疑似アニメーションを作成する
下記のように実装します。
![](https://storage.googleapis.com/zenn-user-upload/1d13cc19e276-20240113.png)

タイムラインは下記のように実装します。
![](https://storage.googleapis.com/zenn-user-upload/d19bee0bf6bf-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/6a21fd4a6804-20240113.png)


Begin Play（Actor生成時に呼ばれるイベント）の最後で試しに呼んでみます。
![](https://storage.googleapis.com/zenn-user-upload/643781c9a58b-20240113.png)

動作確認で問題なければ、テスト用の実装は削除します。

![](https://storage.googleapis.com/zenn-user-upload/39ff43872bef-20240113.png)


@[blueprintue](https://blueprintue.com/render/kt4hrzit/)


# エリアに入ったことを検知するActorを作る

## Actorの作成
![](https://storage.googleapis.com/zenn-user-upload/8c52caf56a8c-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/f0710b37b9ad-20240113.png)


![](https://storage.googleapis.com/zenn-user-upload/1992a83403cb-20240113.png)

## Pawnがエリアに入ったときの処理を実装
![](https://storage.googleapis.com/zenn-user-upload/0e98f78fcfcf-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/5d43ca381151-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/177e5e13c72d-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/b58c0e6ed64c-20240113.png)

下記のように実装します。
![](https://storage.googleapis.com/zenn-user-upload/3456b12122fc-20240113.png)


@[blueprintue](https://blueprintue.com/render/pn_4qzng/)


## マップに配置する

![](https://storage.googleapis.com/zenn-user-upload/8a0476f4b3fc-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/3d51793ee211-20240113.png)