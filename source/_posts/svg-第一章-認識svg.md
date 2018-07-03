---
title: svg -第一章-認識svg
date: 2018-06-14 15:22:15
cover: https://upload.cc/i1/2018/07/02/SsbxMu.png
author: 
  nick: 解到起屁臉 
tags:
 - svg
 - 解到起屁臉
---
相信各位在學習前端的路上一定都對svg這個名詞不陌生
最基礎的就是在logo不使用png,而使用svg的方式了

但我們要來開始了解svg

什麼是svg?
他能夠做什麼?

他是一種針對能讓網頁呈現向量圖的一種[xml](https://developer.mozilla.org/en-US/docs/XML_introduction)的語言
講到向量圖，就不得不介紹一下向量圖跟點陣圖的差異了

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/Bitmap_VS_SVG.svg/1200px-Bitmap_VS_SVG.svg.png" width="300" />

透過上圖，我們可以很清楚明白的了解到，左側的唯一般的點陣圖，他是由 "點" 所組成的
右側的向量圖，他是由一種數學運算的方式紀錄圖片內容，也就是說，他沒有解析度的概念
可以隨意地縮放圖片的尺寸

它還有什麼優點?

1.它在裡面還可以在塞圖片，如jpg svg等等
2.可以有文字物件
3.可以被用DOM來抓取，做一些動畫等等
4.圖層的觀念，寫後面的code屬性會蓋在前一層上

### 有了對svg有個基礎的認識之後，讓我們繼續吧

<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg"><rect width="100%" height="100%" fill="blue" /><text x="50%" y="60%" font-size="30" text-anchor="middle" fill="white">我是SVG</text></svg>

```html
<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
  <rect width="100%" height="100%" fill="blue" />
  <text x="50%" y="60%" font-size="30" text-anchor="middle" fill="white">我是SVG</text>
</svg>
```
可以看到上面的code

我們可以看到 我們用svg的標籤把我們所需要的東西全部都包起來

然後我們使用了version 去定義了svg版本為1.1

然後用[baseProfile=full](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/baseProfile)去定義了了我們所需要的配置

又定義了[xmlns="http://www.w3.org/2000/svg"](https://developer.mozilla.org/en-US/docs/Web/SVG/Namespaces_Crash_Course)這個命名空間

以上這些，雖然不寫也沒差，不過根據MDN的文件，保險起見，還是定義一下

做完上述，我們可以把它存成image.svg，然後可使用object、iframe、img、或css裡的background-image引用，如

```html
<object data="image.svg" type="image/svg+xml" />
<iframe src="image.svg"></iframe>
<image src="image.svg"></image>
```
### 了解svg的定位系統

svg是使用座標系統來定位的

剛剛上面的範例可以看的到，我下了X及Y這兩種屬性，來去定位它的位置

![svg網格](https://developer.mozilla.org/@api/deki/files/78/=Canvas_default_grid.png)

讓我們繼續看下去
<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 100 100"><rect x="20" y="20" width="100" height="100" fill="blue"/></svg>

```html
<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 100 100">
<rect x="20" y="20" width="100" height="100" fill="blue"/>
</svg>
```
從上面的例子中 我們開了一個200X200的畫布
```html
<svg width="200" height="200" ...
```
又使用了rectˊ這個標籤，在svg裡面就是方塊的標籤，x,y起點為20，寬跟高為100像素，並用fill這個屬性填滿藍色
```html
<rect x="20" y="20" width="100" height="100" fill="blue"/>
```
這時候一定會問說，阿為什麼右鍵檢查明明就200*200，騙我

因為我們使用了viewBox這個屬性

x跟y起點為0，開了100 X 100的區域，被放到 200 X 200的畫布上，所以就有放大兩倍的效果

[打開你的codepen玩玩看R](https://codepen.io/)

### 剛剛都講到了fill，讓我們來填充它吧!

#### 填充與邊框屬性

fill屬性我們剛剛已經知道了 就一個fill="你要什麼顏色就填什麼"

然後我們可以透過fill-opacity="0.5" 來去調整它的透明度

<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg"><text x="40" y="40" width="100" height="100">這種若隱若現的感覺</text><rect x="20" y="20" width="100" height="100" fill="blue" fill-opacity="0.5" /></svg>

```html
  <text x="40" y="40" width="100" height="100">這種若隱若現的感覺</text>
  <rect x="20" y="20" width="100" height="100" fill="blue" fill-opacity="0.5" />
```
邊框stroke屬性

<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg"><rect width="100" height="100" stroke-width=5 stroke="blue" fill="#07B492" /></svg>

```html
<rect width="100" height="100" stroke-width=5 stroke="blue" fill="#07B492" />
```
從上述的利子可以看到，我們建立了一個5px寬的藍色邊框

storke="你要什麼顏色"

storke-width="你要多寬"

繪製邊框當然不只這些屬性

<svg width="160" height="280" xmlns="http://www.w3.org/2000/svg" version="1.1"><polyline points="40 60 80 20 120 60" stroke="black" stroke-width="20" stroke-linecap="butt" fill="none" stroke-linejoin="miter"/><polyline points="40 140 80 100 120 140" stroke="black" stroke-width="20" stroke-linecap="round" fill="none" stroke-linejoin="round"/><polyline points="40 220 80 180 120 220" stroke="black" stroke-width="20" stroke-linecap="square" fill="none" stroke-linejoin="bevel"/></svg>

```html
  <polyline points="40 60 80 20 120 60" stroke="black" stroke-width="20"

      stroke-linecap="butt" fill="none" stroke-linejoin="miter"/>

  <polyline points="40 140 80 100 120 140" stroke="black" stroke-width="20"

      stroke-linecap="round" fill="none" stroke-linejoin="round"/>

  <polyline points="40 220 80 180 120 220" stroke="black" stroke-width="20"

      stroke-linecap="square" fill="none" stroke-linejoin="bevel"/>
```
這邊有三個一樣長的線段
stroke-linecap 控制終點的形狀(看左右兩頭) 提供三種屬性: butt round square

butt就是已跟線的終點一樣長的邊框(切齊)，這個是預設，如果你要這樣的話不寫也沒差

round 提供以圓角形式來做結束

square 跟 butt 差不多，但是稍微長一點

stroke-linejoin 屬性，用來控制兩條邊框線段之間，用什麼方式連接。(看轉角的地方)

一樣有三種屬性: miter round bevel

miter 直角(預設)
round 圓角
bevel 轉角為斜切

當然 我們更進一步 可以將邊框變成你想要的虛線

<svg width="200" height="150" xmlns="http://www.w3.org/2000/svg" version="1.1"><path d="M 10 75 Q 50 10 100 75 T 190 75" stroke="black" stroke-linecap="round" stroke-dasharray="5,10,5" fill="none"/></svg>

```html
<path ... stroke-dasharray="5,10,5" />
```

可以看到說 這個stroke-dasharray的方法就是 

第一個數字為5px實線，緊接著10px的空白，然後又接著5px的實線，用逗號來做分隔，然後一直循環

所以它的寫法為
```html
<path ... stroke-dasharray="實線,空白,實線 ...." />
```
當然，如果你想寫更複雜的虛線，你可以在後面繼續延伸下去


### 讓我們用CSS來操作它吧!

在CSS裡 我們要怎麼對svg做操作呢?

我們要使用我們剛剛上面所說的一切屬性來對它做操作
它的標籤就跟你平常在寫有點不一漾

<style>#MyRect { stroke: black; fill: red; } #MyRect:hover,#MyRect:focus{stroke: blue; fill: green;}</style><svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1"><rect x="10" height="180" y="10" width="180" id="MyRect"/><text x=60 y=100 fill="white">滑鼠過我看看</text></svg>

```html
<style>
#MyRect { 
  stroke: black; 
  fill: red; 
} 

#MyRect:hover,
#MyRect:focus{
  stroke: blue; 
  fill: green;
}
</style>

<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <rect x="10" height="180" y="10" width="180" id="MyRect"/>
  <text x=60 y=100 fill="white">滑鼠過我看看</text>
</svg>
```

可以看到，我們遵循著svg的規範，去製作我們想要的任何效果

如果你已經會了CSS跟HTML，相信這對你來說並沒有太大的難度

今天的介紹介到這裡，我們下次見d(`･∀･)b

