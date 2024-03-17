---
title: "MRハッカソン2024振り返り"
emoji: "🐲"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["UnrealEngine", "UnrealEngine5", "UE5", "MR","MRHack"]
published: true
---
# はじめに
この記事は「[MR Hackathon 2024](https://osaka-driven-dev.connpass.com/event/310577/)」に参加した振り返りの記事です。
今回は[鮫さん](https://twitter.com/aym_same)と二人で[XRミートアップ鹿児島チーム](https://twitter.com/xrm_kagoshima)を組み参加しました！
ハッカソン初挑戦でした。

https://osaka-driven-dev.connpass.com/event/310577/

# 作ったもの
タツノオトシゴとハンドトラッキングで触れ合ったり、指に掴まってくれたりするMRアプリです。

（実際はMRで現実空間内にタツノオトシゴが表示されるのですが、Metaのセキュリティの関係でパススルー映像を録画できなかったので、撮影時は見やすいように＆後で背景を合成できるようにグリーンバックにしています。）

https://twitter.com/abricheese/status/1769280688476258471

現実のタツノオトシゴもしっぽで海藻や仲間の首に掴まってとてもかわいいです！！
こんな感じで自分の指にも掴まってくれるととてもかわいいだろうなぁという夢をかなえるべく、今回このようなMRアプリを作りました！！！

https://twitter.com/abricheese/status/1769329033878331472

# 結果
[ホログラム株式会社](https://ho-lo.jp/)さまより「ホログラム賞」をいただきました！！
ありがとうございます！！！
![](https://storage.googleapis.com/zenn-user-upload/c7e3002e7151-20240317.png)


# 実装振り返り
後で同じようなアプリを作るときに参考になるように、どのように作ったかを記録しておきます。

## 環境
- Windows 10
- Unreal Engine 5.3.2（Launcher版）
- Meta Quest3（PC Link）
- [MetaXRプラグインver.62.0](https://developer.oculus.com/downloads/package/unreal-engine-5-integration/)

今回はMRアプリということで、Quest3のパススルーを使いました。
指にタツノオトシゴが掴まるという演出のため、ハンドトラッキングも使用しました。

UEでQuest3のパススルーやハンドトラッキングを使うにはMetaXRプラグインを使う必要があり、エンジンはLauncher版とOculusブランチを自分でビルドする2つの方法がありますが、今回は手軽にLauncher版を使いました。

スタンドアロン向けに作った方が体験がしやすいのですが、今回は開発期間が短かったためPC VR向けに作りました。
（そのせいでパススルーの映像を録画できないという問題が発生しました……）

## Oculus（Meta）のサンプルいろいろ
今回年度末の繁忙期とちょうど重なってしまい、開発期間が1日半しか取れなかったため、できるだけ省力化するためにOculusのサンプルをベースに作成しました。

GitHubにOculusの各種サンプルが公開されており、それぞれの目的ごとに細かく分けられていてとても便利です。

https://github.com/oculus-samples?q=unreal&type=all&language=&sort=

今回は下記のサンプルを参考にしました。

### ハンドトラッキング

https://github.com/oculus-samples/Unreal-HandSample

ハンドトラッキングはちゃんと動きましたが、なぜか手のマテリアルが正しく表示されませんでした。（マテリアルが壊れているときに表示されるデフォルトのグレー格子模様になっていました）

### パススルー

https://github.com/oculus-samples/Unreal-PassthroughSample

こちらはなぜかパススルー映像が歪んで正しく表示されませんでした。

### オクルージョン

https://github.com/oculus-samples/Unreal-OcclusionSample

オクルージョンのサンプルが欲しかったというより、パススルーのサンプルとしてほしかったため試しました。こちらのパススルーはちゃんと機能していました。
ただし、オクルージョンはなぜか機能しませんでした。~~どうしてメインの機能はどれも正しく機能しないのか……~~
あとこちらも手のマテリアルが正しく表示されていませんでした。

### ハンドトラッキングを使ったミニゲームの実例

https://github.com/oculus-samples/Unreal-HandGameplay

結局これをベースに実装しました。ハンドトラッキングを使ったいくつかのミニゲームが実装されたサンプルです。

これを使った理由は、他のサンプルではハンドトラッキング用の手のSkeltal Meshがどこで実装されているのか見つけることができなかったからです。
指にタツノオトシゴを掴まらせる都合上、手のボーン情報が欲しかったのですが、他のサンプルでは見つかりませんでした。

サンプルのミニゲーム部分は必要なかったのですべてマップから削除しました。（無情……）

## パススルーの資料

https://speakerdeck.com/41h0_shiho/questprodeyou-bou-karapasusuru-and-aitoratukingu

使用したサンプルにはパススルーが実装されていなかったため、パススルーについてはこちらの資料を基に実装しました。
手順通りにいくつかのプロジェクト設定を変えるなどすれば簡単にパススルー対応できました！

## 実装
### Oculusアプリの設定
ハンドトラッキング・パススルーをPC Linkで使用する際は、下記の設定が必要です。
![](https://storage.googleapis.com/zenn-user-upload/a3669ecb3e3b-20240317.png)

### 手でタツノオトシゴを触ったり掴まらせたり
Pawn側の実装です。

まず正直に告白すると、手にコリジョンを入れられませんでした……。
以前[タツノオトシゴXR](https://twitter.com/xrm_kagoshima/status/1742524727649030426)の時にUEのVRテンプレートの手のメッシュにコリジョンを追加した際は、「Enable Per Poly Collision」をTrueにすればコリジョンを有効化できていた記憶なのですが、今回はなぜかうまくいきませんでした……。

![](https://storage.googleapis.com/zenn-user-upload/8efd4c0ac4d2-20240317.png)
↑VRテンプレートの手

VRテンプレートの手がSkeltal Mesh Componentなのに対して、今回使ったテンプレートの手がPoseable Mesh Componentだったことが影響していそうな気がします。（詳しい方いたら教えてください！）

そのため、各指先にSphere Collisionを配置してそれっぽく見せています。
時間があれば手のひらや各関節にも追加したかったのですが、時間が足りずに断念しました。

手の各指にタツノオトシゴに触る用のSphere Collision（コリジョンプリセットはBlock All）と、掴まる判定をするためのSphere Collision（コリジョンプリセットはタツノオトシゴのしっぽのコリジョンとのみオーバーラップするものを新規に作成した）を配置しました。

![](https://storage.googleapis.com/zenn-user-upload/a1fc60bf2f79-20240317.png)

コリジョンの親ソケットにPoseableMeshの各ボーンを指定するのですが、なぜか初期状態でPoseableMeshのSkeltal Meshに何も指定されておらずボーンを選べなかったので、「OculusHand_L」と「OculusHand_R」を左手右手にそれぞれ設定しました。

![](https://storage.googleapis.com/zenn-user-upload/3ced54b010a9-20240317.png)

掴まる判定をするためのSphere Collisionは、独立したActorを作成してChild ComponentでPawnの指にアタッチしました。
そして同じ指に複数のタツノオトシゴが掴まってしまうことがないように、タツノオトシゴのコリジョンに反応したときに呼ばれてコリジョンをオフにする関数を作りました。（本当はインターフェイス使った方がいいところだけど手抜き）
Pawn側に処理を作らずに独立したActorにしたのは、タツノオトシゴ側でコリジョンが反応したときにOther Actorに対してこのコリジョンオフの処理を呼ぶだけで済むためです。（Pawnに実装すると、どの指に触れたのかの判定が必要になって面倒）

![](https://storage.googleapis.com/zenn-user-upload/b4a1b2664a14-20240317.png)

### タツノオトシゴが触られるときの物理アニメーションや手に掴まる仕組み
タツノオトシゴ側の実装です。
こちらもいろいろとうまくいかなくて力技で解決しました……。

まずはコンポーネント周り。
通常状態と手に掴まっている状態の物理アニメーションの切り替えがうまくいかなかったため、通常用と掴まり用でそれぞれ2組のコンポーネントを作りました。

![](https://storage.googleapis.com/zenn-user-upload/d65356825eb2-20240317.png)

掴まっている状態のものは、手の回転をYaw回転だけ伝えるようにしたり回転にラグを持たせるために、Spring Arm Componentを噛ませています。
![](https://storage.googleapis.com/zenn-user-upload/bbbb553f175a-20240317.png)

通常状態のものはしっぽが指のコリジョンに触れたかどうかを判定するためのSphere CollisionをSkeltal Meshの尻尾にアタッチしています。

あらかじめ掴まり用のSkeltal MeshはHidden in GameをTrueにして非表示にしておき、指のコリジョンに触れた時に呼ばれるイベントで通常用のSkeltal MeshとHidden in Gameとコリジョンを入れ替えました。

![](https://storage.googleapis.com/zenn-user-upload/2d9ab1bc3579-20240317.png)

物理アニメーションに関して、使用したタツノオトシゴのボーン構造がお腹付近にrootがあり、そこから上半身と下半身に分かれている構造だったため、指に掴まっているしっぽの先端部分以外に物理アニメーションを適用させる方法が分りませんでした。
そのため、掴まっている状態の時は上半身のみの物理アニメーション適用になりました。

![](https://storage.googleapis.com/zenn-user-upload/ddc48552b917-20240317.png)


物理アニメーションの設定は、[以前タツノオトシゴXRでやった](https://www.docswell.com/s/abricheese/5JLM4V-ue_kyushu01#p11)のと同じような方法で実装しました。
一部違う部分としては、掴まれている状態の時は上半身のみに物理アニメーションを適用しました。~~というか今気づいたけどこれはじめから両方のSkeltal Meshに物理アニメーション適用させててもいいんじゃないか？~~
締め切り30分前に実装した部分なのでムダが多いですね……。

![](https://storage.googleapis.com/zenn-user-upload/c2b58bbad1a9-20240317.png)

指に掴まっているときのアニメーションがなかったので、下記の方法を参考にしてしっぽが丸まっている状態の1フレームだけを抜き出したアニメーションシーケンスを作成しました。

https://forums.unrealengine.com/t/topic/774474/2

これをアニメーションブループリントの「Layered blend per bone」で通常状態のアニメーションとブレンドして、しっぽの先だけ丸まった状態を維持するようにしました。

![](https://storage.googleapis.com/zenn-user-upload/f9d16d96735b-20240317.png)

指に掴まるときの挙動は、「Attach Actor to Actor」で、各指に配置したコリジョンのActorにタツノオトシゴをアタッチさせることで実現しました。

ただしこれだけでは手を動かしたときに即座にタツノオトシゴも追従することになり、海中に漂っている浮遊感が表現できませんでした。

その解決策として、手の移動量に応じてタツノオトシゴの角度を変えてあげることで、引っ張られている感を表現することができました。

![](https://storage.googleapis.com/zenn-user-upload/2d71655440ee-20240317.png)

その他細かなこだわりとしては、マップ上に大量に配置したタツノオトシゴが同時に同じアニメーションをすると不自然でした。
そのため初期状態でアニメーションのPlay Rateを0にしておき、Begin Playからランダムな秒数だけDelayを挟んでPlay Rateを1にすることで、アニメーションのタイミングがバラバラになるようにしてみました。
（本当はアニメーションの開始位置をランダムにしたかったのだけれど、実装方法が分からず……今回は直接アニメーションシーケンスをSkeltal Meshに設定していたけど、アニメーションBPで実装すればできるのだろうか？）

![](https://storage.googleapis.com/zenn-user-upload/a698e2d5277c-20240317.png)

# おわりに
今回ハッカソン初挑戦でどんなものか知りたくて参加してみました。
ちょうど年度末の繁忙期と重なってしまい作業が1日半しかできず、なかなかにスリリングなイベントでした。

手にタツノオトシゴが掴まる仕組みを実装し始めたのが締め切り1時間を切っていたときで、そこから大量のバグが出て心折れかけましたが、なんとか見せられるものができました。

相方の鮫さんにおしゃれな体験動画を作ってもらう予定でしたが全然間に合わずに非常に申し訳ないことをしました。
それでも限られた時間で本物のタツノオトシゴを背景にパススルーで体験している動画を撮影してくれて大変感謝してます！

https://twitter.com/jun_mh4g/status/1769267100252778987

最後になりますが、運営スタッフの皆様、スポンサーの皆様、応援してくださった皆様のおかげで楽しいイベントになりました！
ありがとうございます！！
来年も楽しみです！！！