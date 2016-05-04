---
layout: post
title: "簡単にアニメーション化できるパイチャートをCSSオンリーで描画する"
title_en: "Pure CSS3 Pie/Arc, Fully Animatable"
date: 2016-05-04 21:50:28 +0900
date_formatted: 2016年5月4日
comments: true
categories: [Web]
---

{% img /images/post-images/pure-css-pie/ss.png %}

今開発しているWebサービスで使うために、CSSだけでパイチャートを作成してみました。
CSSでパイチャートを描画するのは以前から行われてきましたが、今回作成したものは角度の制御にCSS3 Animations/Transitionsが適用可能で、従来手法と異なり不連続点が無く、簡単に滑らかなアニメーションを付加できるという特徴があります。

`transform: rotate()` により2個の半円を回転させ、重ね合わせることで任意の角度のパイチャートを描画するという[方法](https://www.smashingmagazine.com/2015/07/designing-simple-pie-charts-with-css/)は以前から知られていました。
しかし、2個の半円を重ねる方法では180°未満の角度の円弧を表せないため、角度が180°になる点で背景色と前景色を入れ替えるという方法を取らざるを得ません。CSS3 Transitionsで角度をアニメーションさせる場合には、角度が180°未満かどうかをJSで毎フレーム確認する必要があり、大変不便です。そもそもCSS3 Transitionsベースのアニメーションを制御するために毎フレームJSを実行するのは本末転倒です。

今回作成したものは、目的の角度とその二分角で `transform: rotate()` を適用し、さらに `overflow: hidden` を駆使することにより、こうした不連続点を生じることなくパイチャートを実現することができます。

[JSFiddle](https://jsfiddle.net/yvtjp/3e5g2gd6/3/)で動作デモをご覧になれます。
ソースコード(SCSS)と、そのまま使えるコンパイル済みCSSファイルをMITライセンスで[GitHub](https://github.com/yvt/pure-css-pie/releases)にて配布中です。

使用方法
--------

基本的な使い方は[JSFiddleのエントリ](https://jsfiddle.net/yvtjp/3e5g2gd6/3/)を参考にして下さい。
JSFiddleではCSSクラスにより角度を制御していますが、角度を直接指定したい場合には以下のようにします。

```js
/**
 * <code>pie</code>の円弧の角度を設定する。
 * @param pie 設定対象の円弧のHTML要素。
 * @param angle 円弧の角度を [0, 360] の範囲で指定する。
 */
function setAngle(pie, angle) {
    $(pie).find(".pcp-rot.full").css("transform", `rotate(${+angle}deg)`);
    $(pie).find(".pcp-rot.half").css("transform", `rotate(${angle / 2}deg)`);
}
```

注: css関数の第二引数にはECMAScript 2015の[テンプレート文字列](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/template_strings)機能を使用して値を指定しています。古いブラウザをターゲットとする場合は、文字列連結に置き換えてください。
