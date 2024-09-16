---
title: "第22回UE5ぷちコン 技術的な振り返り① ～マテリアル：電光掲示板編～"
emoji: "🕌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["UnrealEngine", "UnrealEngine5", "UE5","UE5ぷちコン","XRm鹿児島"]
published: true
---

# この記事について
株式会社ヒストリア様主催の[第22回UE5ぷちコン](https://historia.co.jp/ue5petitcon22)に参加した技術的な振り返りを記録したものです。

今回ははじめてXRミートアップ鹿児島のメンバーと一緒にチームを組んで参加してみました。

## 提出した作品

https://www.youtube.com/watch?v=L5rYlT0Atkk

## ツイートまとめ

https://togetter.com/li/2431939

## その他の技術的な振り返り記事
～作成中～

# この記事で紹介するもの
スコア表示のために電光掲示板を作成したので、作成手順を記録しておきます。

![](https://storage.googleapis.com/zenn-user-upload/0e7c0d5c798d-20240916.png)

締め切り直前で時間がない中での作業だったので、超手抜きの雑仕様なのはご了承ください。
電光掲示板っぽいというだけで、よく見ると正しい表示ではないので、正しい表示方法をお求めの方は下記のような記事をご覧ください。

https://limesode.hatenablog.com/entry/2017/12/15/222643

# コンポーネント構造
電光掲示板はスタート&ゴール地点の乗降場のActorの中に作りました。
~~（Actor名が雑なのは許して…）~~

電光掲示板っぽい形をCubeで作り、その上にWidgetで作ったUIを重ねました。
![](https://storage.googleapis.com/zenn-user-upload/0a88f6ffb4ed-20240916.png)

余談ですが、[使用したアセット](https://www.unrealengine.com/marketplace/ja/product/amusement-park-1)の乗降場にはコースターが走る側に屋根がついておらず、電光掲示板をつける場所がありませんでした。
そのため、乗降場のメッシュをFBXでエクスポート→Blenderで開き、屋根以外の不要な箇所を削除、UEに取り込んで土台部分はCubeで代用するという荒業で何とかしました。
（Blenderでモデリングはできないけど、なんとか頂点の削除だけはできた…）
これでコースターが走る部分には柵や階段がない状態にできました。
![](https://storage.googleapis.com/zenn-user-upload/2bbabb981c93-20240916.png)

# 電光掲示板っぽいUI
この記事の本題です。

UIの階層構造はこんな感じ。
大きく2つに分かれていて、文字を表示する部分と文字の上に粒々感を出すテクスチャを重ねる部分で構成されています。
![](https://storage.googleapis.com/zenn-user-upload/3e91bb7a6aab-20240916.png)

文字だけ表示するとこんな感じ。
真っ黒な背景色のボーダーの下に、うっかり超ハイスコアが出たとき用のおまじないスケールボックスを挟み、TextBlockを入れています。
（横にスクロールするアニメーションを入れているので、スケールボックスなしでもよかったかも？）
フォントは[こちら](http://jikasei.me/font/jf-dotfont/)の「JFドットjiskan24」をお借りしました。（商用利用/再配布OKなフォント）
![](https://storage.googleapis.com/zenn-user-upload/949b4baa1745-20240916.png)

粒々のテクスチャ部分だけを表示して拡大するとこんな感じ。
![](https://storage.googleapis.com/zenn-user-upload/d2366447fda2-20240916.png)

使用したテクスチャはこちら。
[みつまめ杏仁さんのブログ](https://limesode.hatenablog.com/entry/2017/12/15/222643)を参考に、ペイントソフト（Krita）で作りました。
16×16pxのサイズのキャンバスを黒塗りして、中に上下左右に1pxずつ余白ができるように14×14pxの丸い消しゴムで消して透明部分を作りました。
![](https://storage.googleapis.com/zenn-user-upload/27905316fafb-20240916.png)

こちらのテクスチャをImageの中のBrush>Imageの項目にセットし、TilingをBothに設定してタイリング（テクスチャの繰り返し）をさせることで粒々感を出します。
![](https://storage.googleapis.com/zenn-user-upload/dcc92318143a-20240916.png)

粒々の密度はスケールボックス&サイズボックスの組み合わせで調整しました。
（この組み合わせは負荷が大きいので、あまり使いすぎない方がいいらしい）
キャンバスパネル内でのスケールボックスの大きさをボーダーと同じ大きさ（今回はサイズX:700、サイズY:200）に設定し、サイズボックスでのWidth/Height Overrideをそれぞれ4倍の数値（今回は2800と800）に設定してみました。
![](https://storage.googleapis.com/zenn-user-upload/e9549aa10632-20240916.png)
![](https://storage.googleapis.com/zenn-user-upload/6f252a782849-20240916.png)


# アニメーション
電光掲示板っぽく、かつ目立つように、下記のようなスライドイン→点滅→スライドアウトのアニメーションを作ってみました。
![](https://storage.googleapis.com/zenn-user-upload/0e1f2cc12cc1-20240916.gif)

アニメーションはTextBlockの親の方のスケールボックスに対してTransformとOpacityを変更して作成しました。

Transformは等速直線運動を、Opacityは一瞬でオンオフを切り替えたかったので、各時間にキーを打った後、キーを右クリックしてTransformは「リニア」を、Opacityは「定数」を選択しました。
![](https://storage.googleapis.com/zenn-user-upload/36c6f8ce4d1d-20240916.png)

背景部分からはみ出した文字列は表示させないため、ボーダーのClippingを「Clip to Bounds」に変更しました。
![](https://storage.googleapis.com/zenn-user-upload/797543f6f5ba-20240916.png)

![](https://storage.googleapis.com/zenn-user-upload/e540ea012302-20240916.png)

# おわりに
VRゲームで空中に極力UIを表示したくない宗派なので、締め切り直前の焦る気持ちの中、なんとかそれっぽいものは作れました。~~（困ったらWidget芸）~~
現実の電光掲示板では、UIの粒々部分は光るor光らないのどちらかのはずですが、今回のものはそこまで細かい実装をしていません。なので、粒の半分は光っているけど半分は黒いままになっていることもある、なんちゃって仕様になっております。
この辺サクッと解決できる方法がありましたら、優しく教えてください。

# 参考ページ

https://at.sachi-web.com/font_electronic-billboards.html

https://limesode.hatenablog.com/entry/2017/12/15/222643