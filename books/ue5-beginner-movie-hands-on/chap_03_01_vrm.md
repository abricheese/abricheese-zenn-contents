---
title: "VRMを入れて動かす"
---
:::message
Unreal Engine Version : 5.5.0
:::
# VRMとは

VRMは（主に）人型のキャラクターを扱えるファイル形式です。
キャラクターの腕や足など体の動き（アニメーション）を付けられる他、ファイル内に登録されている表情を切り替えることもできます。

https://vrm.dev/vrm/vrm_about/

# VRMモデルを用意する

Unreal Engineに取り込むVRMモデルを用意します。
今回はVRoid Hubで配布されているサンプルを使用します。
（利用規約に問題ないか確認してください）

![](https://storage.googleapis.com/zenn-user-upload/262b04ebf0a4-20241130.png)

https://hub.vroid.com/characters/2843975675147313744/models/5644550979324015604

## その他のVRM入手先の例
上記VRoid Hubの他にも、各種配布・販売サイトや、VRMモデル作成ツールがあるので、お好きなモデルを探してみてください！
（モデルやサービス毎の利用規約に気をつけてください）

### VRM作成ツール

https://avatarmaker.vket.com/

https://vroid.com/studio


### 販売サイト

https://booth.pm/ja/search/VRM

# VRM4UでVRMモデルをUnreal Engineに取り込む

## VRM4Uとは
UnrealEngineで動作する、VRMファイルのインポート用プラグインです。
[はるべえ](https://x.com/ruyo_h)さんという方が個人で開発・サポートしています。

公式ドキュメント：

https://ruyo.github.io/VRM4U/

ライセンス情報：

https://github.com/ruyo/VRM4U?tab=readme-ov-file#%E3%83%A9%E3%82%A4%E3%82%BB%E3%83%B3%E3%82%B9

開発支援の投げ銭はこちら：

https://ruyo.booth.pm/items/1707224

## VRM4Uを使う
下記の公式ドキュメントページを見ながら作業して、Unreal EngineプロジェクトにVRM4Uプラグインを追加し、モデルを読み込みます。

https://ruyo.github.io/VRM4U/01_quick-start/

https://ruyo.github.io/VRM4U/01_look/

# アニメーションさせる

## ControlRigを使う

公式ドキュメント：

https://ruyo.github.io/VRM4U/06_controlrig/

https://ruyo.github.io/VRM4U/07_controlrig_morph/

コンテンツドロワー＞設定＞プラグインコンテンツを表示にチェックを入れる
![](https://storage.googleapis.com/zenn-user-upload/4e685cf3cc15-20241201.png)

/Plugins/VRM4U/Util/Actor/latestにあるCR_VRoidSimpleUE5Allを作業フォルダーにコピーする
![](https://storage.googleapis.com/zenn-user-upload/3109ee155c6b-20241201.png)

（中略、公式ドキュメントをご参照ください。）

プロパティ変更時に自動でキーを打つ設定がオススメです。
![](https://storage.googleapis.com/zenn-user-upload/1c461da41748-20241201.png)


# (参考)VRChat向けのモデルを使う場合

https://ruyo.github.io/VRM4U/04_vrchat/

# (参考)揺れもの

`Kawaii PhysicsはUnrealEngine4,5用に作成した疑似物理プラグインです。
髪、スカート、胸などの揺れものを「かんたんに」「かわいく」揺らすことができます。`（公式ドキュメントより）

![](https://github.com/pafuhana1213/Screenshot/raw/master/KawaiiPhysics1.gif)

https://github.com/pafuhana1213/KawaiiPhysics