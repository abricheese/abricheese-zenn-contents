---
title: "エフェクトをシーケンサーで使う"
---
:::message
Unreal Engine Version : 5.5.0
:::

# Cascade（レガシー）

Unreal Engineのスターターコンテンツに入っているエフェクトは、2024/12/1現在、旧式のCascadeで作られています。

これをシーケンサー上に配置して、任意のタイミングで起動してみます。

コンテンツドロワーから、P_Explosionをドラッグアンドドロップして配置します。

![](https://storage.googleapis.com/zenn-user-upload/4c73458bbe08-20241201.png)

配置したP_Explosionをさらにアウトライナーからシーケンサー上にドラッグアンドドロップして、シーケンサーに追加します。

![](https://storage.googleapis.com/zenn-user-upload/c31de4e71ce5-20241201.png)

シーケンサーのP_Explosionの横の＋ボタンから、「FXシステムトグルトラック」を選択します。

![](https://storage.googleapis.com/zenn-user-upload/81a8d031a713-20241201.png)

エフェクトを再生させたいタイミングにキーを追加すると、任意のタイミングでエフェクトを再生できるようになります。

![](https://storage.googleapis.com/zenn-user-upload/b5bceec99093-20241201.png)

# Niagara

現行のエフェクトシステムであるNiagaraを使います。

コンテンツドロワーにて作業用のフォルダーを作成し、右クリックメニューから「Niagaraシステム」を選択します。

![](https://storage.googleapis.com/zenn-user-upload/529be418dda5-20241201.png)

作成元のテンプレートやサンプルの一覧が表示されるので、「FountainLightweight」を選択して「作成」をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/761e818d6748-20241201.png)

名前を「NS_Fountain」として、ドラッグアンドドロップして配置します。
※NSはNiagara Systemの略

![](https://storage.googleapis.com/zenn-user-upload/11b667f4a1f5-20241201.png)

配置したNS_Fountainをさらにアウトライナーからシーケンサー上にドラッグアンドドロップして、シーケンサーに追加します。

![](https://storage.googleapis.com/zenn-user-upload/f965a368ce78-20241201.png)

シーケンサーのNS_Fountainの横の＋ボタンから、「NiagaraComponent0」を選択します。

![](https://storage.googleapis.com/zenn-user-upload/0ea28417d8de-20241201.png)

さらにNiagaraComponent0の横の＋ボタンから、「Niagaraシステムのライフタイムサイクルトラック」を選択します。

![](https://storage.googleapis.com/zenn-user-upload/c9f8cedce526-20241201.png)

ライフサイクルの左端を掴んで動かすと、エフェクト再生の開始位置を変更できます。

![](https://storage.googleapis.com/zenn-user-upload/761982c43063-20241201.png)

エフェクト再生の終了位置を変更するには、終了させたいフレーム位置に移動して「右クリック＞編集＞セクションの右側をトリム」を選択します。

![](https://storage.googleapis.com/zenn-user-upload/296006920e4c-20241201.png)