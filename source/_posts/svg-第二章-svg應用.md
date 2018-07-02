---
title: svg -第二章-svg進階基礎(1)
date: 
cover: /img/svg-第二章/SVG_logo.svg
author: 
  nick: Joseph 
tags: 
 - svg  
 - Joseph
---

##### 延續上次解到起屁臉大大為我們講解的svg基礎之後，我們就要稍稍進入到一點更進階的基礎了。我們將要瞭解到漸層、模式、文字、變形的進階基礎。大家打開你的編輯器，我們要開始了。

## 漸層

##### 好的首先我先來看看結果吧！
<p data-height="265" data-theme-id="0" data-slug-hash="NzojzE" data-default-tab="html,result" data-user="josephwu" data-embed-version="2" data-pen-title="svg-linearGradient" class="codepen">See the Pen <a href="https://codepen.io/josephwu/pen/NzojzE/">svg-linearGradient</a> by JosephWu (<a href="https://codepen.io/josephwu">@josephwu</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

##### 你會想哇！這是怎麼做，我就來一步步的拆解程式碼吧！

##### 首先呢！！我們一樣在最外層給他一個svg屬性，定義他是個svg的作用範圍，並給他一個400X400可視區域的大小,

```html
<svg width='400' height='400'>
   
</svg>
```

##### 接著放入defs,用來定義裡面的檔案是可以被重複引用的

#### linearGradient、radialGradient

##### 接下來就來到我們的重頭戲，`<linearGradient>`和`<radialGradient>`，我們可以用`linearGradient`來定義一個       **線性漸層**和`radialGradient`來定義一個**放射狀的漸層**,並需要給`linearGradient`一個id,id在一個網頁中是唯一的,但是可以被不同元件重複使用。

##### 要填入`<stop>`來指定顏色的範圍,`<stop>`裡面的屬性`offset`是顏色的節點，使用百分比的設定，`stop-color`可以設定節點的顏色。

```html
<defs>
    <linearGradient id="left" x1="0%" y1="0%" x2="0%" y2="100%" gradientUnits="userSpaceOnUse">
      <stop offset="0%" stop-color="#eee" />
      <stop offset="30%" stop-color="#000" />
    </linearGradient>
    <linearGradient id="right" x1="0" y1="0" x2="1" y2="1">
      <stop offset="30%" stop-color="#d00" />
      <stop offset="90%" stop-color="#fc0" />
    </linearGradient>
</defs>
```

##### 並且在`<linearGradient>`中可以用***線性漸層***x1,x2,y1,y2、***放射狀漸層***cx,cy,r,fx,fy來決定漸層色的起點和終點,皆以%為單位,也可以簡略不寫

```html
<defs>
    <linearGradient id="right" x1="0" y1="0" x2="1" y2="1">
      <stop offset="30%" stop-color="#d00" />
      <stop offset="90%" stop-color="#fc0" />
    </linearGradient>
  </defs>
  <rect width="120" height="120" x="10" y="10" stroke="#000" fill="url(#right)" />
  <rect width="120" height="120" x="140" y="10" stroke="#000"  fill="url(#right)" />
</defs>
```

<p data-height="265" data-theme-id="0" data-slug-hash="bKzRQd" data-default-tab="html,result" data-user="josephwu" data-embed-version="2" data-pen-title="svg-linearGradient2" class="codepen">See the Pen <a href="https://codepen.io/josephwu/pen/bKzRQd/">svg-linearGradient2</a> by JosephWu (<a href="https://codepen.io/josephwu">@josephwu</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

##### 並且可以使用***xlink:href***屬性，他可以將漸層的屬性和`stop`節點的屬性，引入到另一個漸層中，我們就不用在另一個漸層中建立許多`stop`節點。

<p data-height="265" data-theme-id="0" data-slug-hash="vrbJEw" data-default-tab="html,result" data-user="josephwu" data-embed-version="2" data-pen-title="svg-linearGradient3" class="codepen">See the Pen <a href="https://codepen.io/josephwu/pen/vrbJEw/">svg-linearGradient3</a> by JosephWu (<a href="https://codepen.io/josephwu">@josephwu</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

#### radialGradient

##### radialGradient和linearGradient大同小異，只是差在radialGradient是一個點向外發散，並且在radialGradient用cx,cy,r來決定漸層位置與大小,這邊的cx,cy,r一樣是百分比或是小數點

```html
<defs>
      <radialGradient id="Gradient1">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
      <radialGradient id="Gradient2" cx="0.25" cy="0.25" r="0.25">
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
      </radialGradient>
  </defs>
 
  <rect x="10" y="10" rx="15" ry="15" width="100" height="100" fill="url(#Gradient1)"/>
  <rect x="140" y="10" rx="15" ry="15" width="100" height="100" fill="url(#Gradient2)"/>
```
<p data-height="265" data-theme-id="0" data-slug-hash="bKzraq" data-default-tab="html,result" data-user="josephwu" data-embed-version="2" data-pen-title="svg-radialGradient" class="codepen">See the Pen <a href="https://codepen.io/josephwu/pen/bKzraq/">svg-radialGradient</a> by JosephWu (<a href="https://codepen.io/josephwu">@josephwu</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

##### 另一個差異為fx、fy，決定的是漸層的中心點

![svg放射性漸層](https://developer.mozilla.org/@api/deki/files/352/=SVG_Radial_Grandient_Focus_Example.png)

使用fx、fy可以決定漸層的中心點在哪，呈現光源位置不同的感覺

```html
<radialGradient id="Gradient2" cx=".5" cy="0.5" r="0.5" fx='.3' fy='.33'>
        <stop offset="0%" stop-color="red"/>
        <stop offset="100%" stop-color="blue"/>
</radialGradient>
```
<p data-height="265" data-theme-id="0" data-slug-hash="pKGrOL" data-default-tab="html,result" data-user="josephwu" data-embed-version="2" data-pen-title="svg-radialGradient-fx,fy" class="codepen">See the Pen <a href="https://codepen.io/josephwu/pen/pKGrOL/">svg-radialGradient-fx,fy</a> by JosephWu (<a href="https://codepen.io/josephwu">@josephwu</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

##### 經過了一連串漸層svg的tag與屬性的修煉，總算可以抵達終點了？

##### 不不不，等等? 還有兩個重要的屬性，***spreadMethod***與***gradientUnits***還沒講到，先喝杯茶，來完成最後兩個屬性吧！

### spreadMethod

##### spreadMethod指的是漸層的擴散方式，分成了pad、reflect、repeat這三種方式，pad就是按照預設的方式擴散、reflect就是鏡射、repeat就是重複，我們來看看效果如何吧！
##### spreadMethod經過測試似乎只在radialGradient有效果

<p data-height="265" data-theme-id="0" data-slug-hash="gKqGMx" data-default-tab="html,result" data-user="josephwu" data-embed-version="2" data-pen-title="svg-radialGradient-spreadMethod" class="codepen">See the Pen <a href="https://codepen.io/josephwu/pen/gKqGMx/">svg-radialGradient-spreadMethod</a> by JosephWu (<a href="https://codepen.io/josephwu">@josephwu</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### gradientUnits

#### gradientUnits是用來表示漸層是套用在哪個定位上，objectBoundingBox是預設值，表示套用在要顯示漸層的物件上，而userSpaceOnUse表示套用在整個svg的可視區域上,以下為範例可以看看。
#### linearGradient套用gradientUnits="userSpaceOnUse"後，整個漸層渲染從svg位置(0,0)的地方往下延伸，所以y1="300"代表從可視區域300px的，地方開始漸層才看得見，對比原本在物件上的漸層只要設定1即為100%即可完全顯示漸層。

```html
 <linearGradient id="GradientLeft" x1="" x2="0" y1="300" y2="0" gradientUnits="userSpaceOnUse">
     <stop id="stop1" offset="0%" stop-color='#000'/>
    <stop id="stop2" offset="50%" stop-color='#b00'/>
   <stop id="stop3" offset="100%" stop-color='#cc0'/>
    </linearGradient>
```
<p data-height="265" data-theme-id="0" data-slug-hash="PaVOJL" data-default-tab="html,result" data-user="josephwu" data-embed-version="2" data-pen-title="svg-linearGradient-gradientUnits" class="codepen">See the Pen <a href="https://codepen.io/josephwu/pen/PaVOJL/">svg-linearGradient-gradientUnits</a> by JosephWu (<a href="https://codepen.io/josephwu">@josephwu</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

##### 參考資料
[MDN SVG教學](https://developer.mozilla.org/zh-TW/docs/Web/SVG/Tutorial)
[SVG 完整教學 31 天](http://www.oxxostudio.tw/articles/201410/svg-tutorial.html)
[卡斯伯-SVG 漸層沒想到是這樣的做法](https://wcc723.github.io/svg/2014/06/05/svg-linear-gradient/)














