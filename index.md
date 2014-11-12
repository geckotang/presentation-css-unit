# CSSの様々な単位

[@GeckoTang](http://twitter.com/GeckoTang)

---

全ての場所で使えるものや、一部のCSS関数内で使える単位など、CSSではとても多くの単位を扱うことができます。
px以外の単位を状況に応じて、使いこなせるようになりましょう。

---

## %

&lt;percentage&gt;型

- パーセンテージ。何かしらを基準とした値。単位ではないけど一応。
- gradientとかに置いては、gradientを指定した要素の幅や高さを基準とした割合。
- ``widthプロパティ``や``marginプロパティ``、``paddingプロパティ``においては、その要素の親要素の幅を基準とした割合となる。
- 以外に間違えがちだが、margin-top: 100%;としたからといって、その要素の高さ分の上マージンが確保されるわけではない。

---

## px

&lt;length&gt;型

- pixel
- 画面解像度に依存し、72dpiの解像度であれば72pxが2.54cmになり、96dpiであれば96pxが2.54cmになります。
- 相対的な単位ではありますが、実際は絶対的な単位として使用されています。

---

## em

&lt;length&gt;型

- 親、祖先のフォントサイズを基準とした単位。（ただし，印刷の分野では文字“M”の幅）
- 例えば10pxが指定された要素の子要素に、1emを指定すると10px相当の文字サイズになる。もし0.1emにすれば1px相当のサイズになる。
- ※まぁChromeは10px相当以下にはなりませんが。

---

## ex

&lt;length&gt;型

- emの成り立ち自体は、Mの高さを基準としたものだったのにたいして、xの高さ（x-height）を1としたもの。
- 多くのフォントは1ex = 0.5emになってる様子。
- あんまりつかわない。

---

## rem

&lt;length&gt;型

- ルート要素（たとえばhtml）のフォントサイズを基準とした単位。
- remは親要素のフォントサイズが変わったとしても、ルート要素のフォントサイズが変わらない場合変化しない。

```css
html { font-size: 62.5%; } /* 10px相当 */
ul { font-size: 0; }
ul > li { font-size: 1.6rem; } /* 16px相当 */
```

このようにフォントサイズを0にして、子要素内はもとに戻す。みたいな事ができる。

---

## ch

&lt;length&gt;型

- 現在のフォントの``0``の幅。
- Chromeが未サポート。FirefoxとIE9は対応している。

---

## <small>cm、mm、q、in、pt、pc、mozmm</small>

&lt;length&gt;型

絶対的な単位。使わない。

- ``cm``: センチメートル 1cm = 10mm
- ``mm``: ミリメートル 10mm = 1cm
- ``q``: 四分ミリメートル 1q = (1÷40)cm
- ``in``: インチ 1in = 2.5cm
- ``pt``: ポイント 1pt = 1/72in = 0.3528mm
- ``pc``: パイカ 1pc = 12pt
- ``mozmm``: ディスプレイ解像度によらず、正確に 1 ミリメートルを描画しようとするらしい。

``mozmm``はFirefoxの実験的な実装だが、なぜかSafariも対応している。

---

## vw、vh

&lt;length&gt;型

- viewport widthとviewport height
- ``vw``: ビューポートの幅に対する割合の単位
- ``vh``: ビューポートの高さ対する割合の単位
- 例えば画面幅が320pxであれば、100vwは320px、10vwは32pxとなる。

http://caniuse.com/#search=vw

------

## vmin、vmax

&lt;length&gt;型

- ``vw``と``vh``に関連するものとして、``vmin``と``vmax``が存在する
- ``vmin``: ビューポートの幅と高さのうち、値が小さい方に対する割合
- ``vmax``: ビューポートの幅と高さのうち、値が大きい方に対する割合
- 過去に、仕様書で``vmin``を``vm``として定義していたが、いまは``vmin``になっている。

------

### パーセンテージとの違い。

> 例えば画面幅が320pxであれば、100vwは320px、10vwは32pxとなる。

- ここだけみれば、パーセンテージと同じに見えます。
- しかし、``widthプロパティ``のパーセンテージは、親要素（その要素を包括する要素）の幅を基準にした割合なので、かならずしもビューポート＝親要素の幅ではありません。
- なので、ビューポートを基準として、何かを操作したい場合は``vw``や``vh``を使うと幸せになるでしょう。

------

### 対応ブラウザ

- ほとんどのブラウザで使うことはできる。
- IE9からはvwとvh、そしてvminに対応していますが、vmaxに関してはIE11からの対応です。
- そして、Androidは4.4以降からそれぞれの単位に対応しています。残念。
- しかし、Chrome 38ではメディアクエリの式の中ではvw、vhが使えない。困る。

 http://hail2u.net/blog/webdesign/aspect-ratio-feature.html

---

## deg、grad、rad、turn

&lt;angle&gt;型
 
- rotateやskew関数などで使う単位。
- ``deg``: 度。1周は360度。
- ``grad``: gradian（グラジアン）円の全周は 400 gradian。
- ``rad``: ラジアン。 円の全周は 2π ラジアン。
- ``turn``: 回転数（ turn ）。 円の全周は 1 回転。

http://www.w3.org/TR/css-values/#angles

---

## s、ms

&lt;time&gt;型

- transition-durationなどで使える単位。
- ``s``: 秒。100sは100秒
- ``ms``: ミリ秒。100msは100ミリ秒
- ちなみに、transition-durationの初期値は``0s``となり、``transition-duration: 0;``とした場合、Firefoxにおいては厳密に評価し、無効な値となり、機能しません。ほかブラウザでは機能することもありますが、めんどくさくても``s``をつけましょう。

http://www.w3.org/TR/css-values/#time-value

---

## Hz、kHz

&lt;frequency&gt;型

- 話し声の高さのような、周波数を表すためのもの。
- ``Hz``: ヘルツ単位の周波数を表す。例： 0Hz、1500Hz、10000Hz
- ``kHz``: キロヘルツ単位の周波数を表す。例： 0kHz、1.5kHz、10kHz
- 対応しているプロパティがそもそも存在しない。
- 過去には、声のピッチなどを定義するために導入され、非推奨になり、仕様として再度復帰。

https://developer.mozilla.org/ja/docs/Web/CSS/frequency

<small>Operaがバージョンによっては [pichプロパティ](http://www.htmq.com/style/pitch.shtml) で使えるらしい。でも今は...Blin(ry</small>

---

## dpi、dpcm、dppx

&lt;resolution&gt;型

- メディアクエリの式で使える単位。
- デバイスの解像度を表すもの。
- ``dpi``: 1インチあたりのドット数。1インチは 2.54 cm なので、1dpi ≈ 2.54dpcm です。
- ``dpcm``: センチメートルあたりのドット数 を表します。1インチは 2.54 cm なので、 1dpcm ≈ 0.39dpi です。
- ``dppx``: ピクセル（px）あたりのドット数を表します。CSS の inch と CSS の px の比率は 1.96 で固定なので、1dppx は 96dpi と同じです。

https://developer.mozilla.org/ja/docs/Web/CSS/resolution

---

## 参考

- [CSS Values and Units Module Level 3](http://www.w3.org/TR/css-values/)
- [length - CSS | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/Length)
- [CSS には vw, vh, vmin, vmax という単位がある](http://dev.classmethod.jp/ria/html5/css-length-viewport/)
- [CSSの単位](https://w3g.jp/css/guide/units)
- [Android units – pixels, density, dpi, dip, dp, dps, sp, sip](http://blog.edwinevans.me/?p=131)
