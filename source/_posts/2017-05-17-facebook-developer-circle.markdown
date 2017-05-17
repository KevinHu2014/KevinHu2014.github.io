---
layout: post
title: "Facebook Developer Circle Taipei"
date: 2017-05-17 23:50:47 +0800
comments: true
categories: meetup
---
## 前言
由於本公司的產品大量使用到Facebook的服務，所以就翹課來參加了首次在台灣舉辦的**Facebook Developer Circle : Taipei** 的開發者聚會，這次的活動是舉辦在CHOCOLABS 的辦公室。


[![18489614_1326777600732946_7004909634724846760_o.jpg](https://s11.postimg.org/im1dmayrn/18489614_1326777600732946_7004909634724846760_o.jpg)](https://postimg.org/image/bvkwcvblr/)
## 正文

此次的主題主要有三個

+ ReactVR - Jeremy Lu
+ Self-Serve Facebook Ads w/ Marketing API - Clement Tang (Project Manager from 91APP)
+ F8 Highlights - Guannan Pu (Strategic Partnership Manager from Facebook)

### [ReactVR](https://facebook.github.io/react-vr/)
Jeremy Lu 的介紹淺顯易懂，
首先在講**ReactVR**前要先提**WebVR**

WebVR簡單來說就是能在web browser上直接觀看VR內容

那要能達到這樣的功能，首先要先來定義統一的規則

這樣各家廠商實作時才有標準可以依循，確保同一份內容能正確呈現在不同平台上

而規格定義了WebVR API 和 Hand Position API

目前實作這些規格的廠商少了ㄧ家（Safari , Apple）

現況下兩大主流的WebVR框架為
+ Mozilla 的 Aframe
+ Facebook 的 ReactVR

high level ---------> low level

react-aframe -> Arame -> {ThreeJS|WebGL|WebVR}

ReactVR -> OVRUI -> {ThreeJS|WebGL|WebVR}

**兩者的比較**（擷取自[amberroy的留言](https://github.com/facebook/react-vr/issues/18#issuecomment-267622361)）

+ React VR apps are written in JavaScript, with JSX tags that are transpiled into JS. A-Frame apps use HTML, with custom HTML tags (whether this is advantage or disadvantage depends if you want to code in JS or HTML :) although A-Frame components are built with JavaScript.

+ React VR is based on the React core (in production use since 2011, open sourced in 2013) and A-Frame is written from scratch (mid-to-late 2015). So contributing back to a-frame is not possible since they have different underlying implementations.

+ React VR is build on top of React Native, with a JS runtime for WebVR, while aframe-react is a very thin layer on top of A-Frame to bridge with React JS.

ReactVR 的優勢是基本上只要你會React 或是 ReactNative 就能無痛立即開發

總結來說VR至少還要2~5年才成熟

## Self-Serve Facebook Ads w/ Marketing API

這部分由於我本身沒有接觸過Facebook的廣告，所以就沒有特別紀錄

詳細的請直接參考[投影片](https://speakerdeck.com/clementtang/self-serve-facebook-ads-with-marketing-api)

## F8 Highlights

這裡主要提兩個跟公司有正相關的服務

首先是 [**Account Kit**](https://developers.facebook.com/docs/accountkit)

這項服務主要是讓用戶只需使用電話號碼或電子郵件地址就能快速註冊並登入您的應用程式，完全無需密碼。它不但可靠、容易使用，並且提供另一個註冊應用程式的選擇。

在前年F8的時候就提出了，不過我目前還是觀望中，不知道是否真的如圖中的show case那麼厲害。
[![18552931_1327014974042542_1341671821_o.jpg](https://s15.postimg.org/sg7y8nuh7/18552931_1327014974042542_1341671821_o.jpg)](https://postimg.org/image/3mye80bgn/)

另一項是 [** Places Graph **](https://developers.facebook.com/docs/places)

這基本上可以看成是Geocoding的服務，

使用時機像是如果你今天使用[Google Places API](https://developers.google.com/places/?hl=zh-tw)的時候，常常遇到這樣的問題
>  Google Places API for iOS 擷取之地點位置時所使用的任何地圖都是 Google 地圖。

或是你使用Mapbox 的Geocoding
> The results from geocoding with the mapbox.places mode must be displayed on a Mapbox map...

這樣的限制使得你無法在地圖上使用其他地圖的Geocoding服務

但現在有了Facebook Places Graph 的服務

你能輕鬆為你的地圖擴充打卡建議點



## 後記

這次的開發者聚會真的是受益良多，也感謝主辦單位提供場地與食物
[![18486041_10154609245768595_8209573010552021913_n.jpg](https://s27.postimg.org/nrmclq5xv/18486041_10154609245768595_8209573010552021913_n.jpg)](https://postimg.org/image/4zahi59jj/)
