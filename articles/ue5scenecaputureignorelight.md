---
title: "[UE5]Scene Capture 2Dでライティングの影響を受けないように"
emoji: "🌃"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["UnrealEngine", "UnrealEngine5", "UE5"]
published: true
---
# はじめに
この記事では、Scene Capture 2Dを使ってゲーム内の撮影をする際に、ライティングの影響を受けないようにする方法を説明します。
暗いマップでも撮影した画像が真っ黒にならずにすみます。

また、この方法ではVR（r.ForwardShading=True）でも動作しました。
他にもググると[ポスプロで行う方法](https://www.reddit.com/r/unrealengine/comments/13lf2uy/unlit_capture_using_a_scene_capture_component_2d/)も出てきましたが、こちらはVRでは使えませんでした。

実際に撮影した画像はこんな感じ。
ライティングがなくなるので、見た目はチープになります。
また、空は暗いままです。

![](https://storage.googleapis.com/zenn-user-upload/a6c321340816-20241001.png)

# 環境
- Windows11
- UE5.3.2

# やり方
撮影用のScene Capture 2D **Actor**を用意して、詳細タブからScene Capture > Advanced > Hidden Show Flags > Lighting のチェックを外します。

![](https://storage.googleapis.com/zenn-user-upload/fad42df0e39e-20241001.png)

これにより、Scene Capture 2Dでライティングの影響を受けずに撮影することが可能です。

![](https://storage.googleapis.com/zenn-user-upload/d317f16b6932-20241001.png)

比較として、Show Flag変更前はこんな感じでした。

![](https://storage.googleapis.com/zenn-user-upload/e2812405de1d-20241001.png)

余談ですが、Show Flagには他にも様々な項目があり、キャラクター/背景だけ抜き出したいなどの用途でも使えるようです。（未検証）

:::message alert
Scene Capture 2D **Component**を独自のBPクラスに追加してShow Flagを変更しても、パッケージングすると正しく機能しません。
:::

フォーラムの下記あたりで議論されていますが、これはEpicとしては仕様のようで直す気はないみたいです。

https://forums.unrealengine.com/t/scenecapture2d-show-flags-not-available-in-blueprint/304175/13

https://forums.unrealengine.com/t/scene-capture-show-flags-not-working-after-packing-game/482570

試したところ、Scene Capture 2D **Actor**を継承してShow Flagを変更したものを用意しておき、他のBPから動的にスポーンさせることは可能でした。

# 検証用プロジェクト作成手順
需要があるか分かりませんが、記事を書くための検証用にサードパーソンテンプレを使ったプロジェクトの作成手順を記録しておきます。

1. DirectionalLightのIntensityを0.3にする
![](https://storage.googleapis.com/zenn-user-upload/ac1666770f85-20241001.png)

1. Scene Capture 2D Actorを配置して、Scene Capture > Capture SourceをFinal Color(LDR) in RGBにする
![](https://storage.googleapis.com/zenn-user-upload/94ae84221046-20241001.png)

1. Scene Capture > Advanced > Hidden Show Flags > Lightingをオフにする

1. BP_ThirdPersonCharacterにテスト用の撮影機能を追加する
（BeginPlayの後ろに追加した、Capture Every Frameがオンになっているので、Capture Sceneは呼ばなくて良かったかも）
![](https://storage.googleapis.com/zenn-user-upload/6c492877db57-20241001.png)
参考記事：

https://historia.co.jp/archives/16883/

-----
皆様の応援が投稿のモチベーションになります。

記事が参考になりましたら、ぜひ♡ボタンを押したり、記事の拡散、X(Twitter)のフォローなどしていただけますと嬉しいです。
