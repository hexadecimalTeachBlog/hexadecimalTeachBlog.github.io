---
title: 精神時光屋第一周 todolist 心得
date: 2018-06-11 10:24:28
author: 
  nick: 解到起屁臉 
tags: 
 - 解到起屁臉 
 - react
 - styled-components
---
不囉嗦先來看網址
[成果](https://protected-reaches-93253.herokuapp.com/)
[github](https://github.com/aiko3310/The-F2E-week1-todolist)

在進度裡這次使用到的有 react, styled-components, react-router, material-ui

我自己在這禮拜寫是挺趕的，從周四才開始寫

畢竟也是第一次實戰react，有很多地方不是很熟，覺得只是copy+paste的程度而已

不過在做的時候發現使用Styled-components更多彈性的作法

使得每一個Component都可以提供更多的彈性

例如

`margin:0 0 0 20px`

改寫成

`margin:${props=>props.mg || "initial"}`

這樣寫就能更在jsx標籤裡使用mg這個方法 只要指定mg="屬性值" 就可以隨時調整magin的值了

另外material-ui在date-picker上居然不支援safiri!!!!

雖然我還是繼續用就是了

本來安排的進度還有用mobx做狀態的管理，無奈技術力還不足，無法了解mobx的寫法

期待之後再慢慢補上了