---
layout: post
title: "Cutout Assistant: ベクトルアートのアンチエイリアリング解除を支援するツール"
title_en: "Cutout Assistant"
date: 2016-05-10 19:19:03 +0900
date_formatted: 2016年5月10日
comments: true
categories: [Graphics]
---


{% img center /images/post-images/cutout-assistant/before-after.png %}

ラスタライズされたベクトルアートは、背景から切り出したり、特定の領域の色を変えたりする加工を綺麗に行うのが意外と難しいものです。
この理由は、アンチエイリアシングにより、異なる色の隣り合った領域間に中間色が生成されてしまう為です。
グラデーションの存在も邪魔になります。
解決法の一つはアンチエイリアシングを解除をすることで、その方法の一つは減色を行うことですが、あまり良い結果にはなりません(下図)。

{% img center /images/post-images/cutout-assistant/bad.png %}

アンチエイリアシングにより上部のエッジが数段階の色で表現されてしまっています。
この原因は、ある箇所の色が離れた箇所の中間色を近似するのに用いられてしまうことです。
そこで、隣接した領域の色のみを用いることにより、この現象を起こりにくくした[減色ツールを作ってみました](https://cdn.rawgit.com/yvt/cutout-assistant/0.1.1/index.html)。

ソースコードは[GitHub](https://github.com/yvt/cutout-assistant)に上げてあります。
プルリクエスト大歓迎です。

使い方
------

1. キャンバスに画像ファイルをドラッグします。右側にはその時点の出力画像、左側にはそれと入力画像の差分が表示されます。
2. 画像上の点をクリックすると、そのピクセルの色に近い隣接した部分が同じ色で塗りつぶされます。
3. 右クリックか、あるいはスクリーンショットを撮るなどして保存して下さい。

