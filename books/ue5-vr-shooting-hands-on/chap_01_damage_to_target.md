---
title: "的に弾が当たったときだけ色が変わるようにする（ダメージ処理）"
---
:::message
Unreal Engine Version : 5.3.2
:::

## 的に弾が当たったときだけ色が変わるようにする

実は現在の\[BP_Target\]の実装では、的に弾以外の一部のオブジェクトが衝突した際にも色が変わるようになってしまっています。
（一番最初にできるだけ簡単に\[PrintString\]を呼び出す実装にしたかったので、このようになっています。。）

「[スムーズ移動できるように](https://zenn.dev/abricheese/books/ue5-vr-shooting-hands-on/viewer/chap_01_smooth_move)」にて移動方法を追加したことにより、スムーズ移動で的に接触すると色が変わるようになってしまいました。

今回はそこを修正します。

今までの実装では、\[BP_Target\]の\[On Component Hit\]を使用して接触判定を行ってましたが、今回はUnreal Engine標準のダメージ処理を使用し、的が弾からダメージを受けたときだけ色を変えるように修正します。

## 弾にダメージを与える処理を追加

![](https://storage.googleapis.com/zenn-user-upload/db373438c0e2-20240113.png)

![](https://storage.googleapis.com/zenn-user-upload/ca52a82888c7-20240113.png)

@[blueprintue](https://blueprintue.com/render/exvt4d3b/)

## 的がダメージを受けたときだけ色を変えるように

\[BP_Target\]を下記のように実装します。

![](https://storage.googleapis.com/zenn-user-upload/f4e1bd627e79-20240113.png)

@[blueprintue](https://blueprintue.com/render/3c6tgo18/)

