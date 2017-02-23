---
layout: post
title: "Nisra Hackathon 2017"
date: 2017-02-23 11:44:02 +0800
comments: true
categories:
---
# Nisra Hackathon 2017 心得

### 前言

由於去年的Nisra Hackathon不小心在ㄆㄆ家睡過頭xDD，所以今年決定來雪恥www，
今年的獎金也蠻豐碩的第一名有一萬元，希望藉由黑客松來籌畢旅的基金 哈哈。


## 正文
這次的黑客松在參賽前就想好題目了，剛好因為研究所的計劃要做一個LBGM，所以想說來做一個LBGM版的小精靈遊戲，這個題目是受到Google在2015年彩蛋（是能在Google Maps上玩小精靈）的啟發，但當時好像只Web版而已，沒有真正的Loaction Base，有此想說如果用React Native來做一個，應該蠻有挑戰的。

當年彩蛋的截圖

![alt text](https://camo.githubusercontent.com/3df8af60dfc1dafbdb0125081704c7c5baa512aa/68747470733a2f2f63646e302e746e7763646e2e636f6d2f77702d636f6e74656e742f626c6f67732e6469722f312f66696c65732f323031352f30332f476f6f676c654d6170735061634d616e2d373330783334332e706e67 "當年彩蛋的截圖")

###  小精靈規則簡介與遊戲構想
玩家為小精靈，
遊戲中會出現鬼魂，
被鬼魂碰到的話就輸了。
迷宮為使用者所在地圖，
豆子會出現在街道上，玩家吃了豆子會得分。
大力丸會出現在特殊地點（lbs），
大力丸提供小精靈一小段時間，可以反過來吃掉鬼魂。鬼魂在這段時間內會變成深藍色，會往反方向逃逸，而且比平常的移動速度慢。當鬼魂被吃掉時，它的眼睛還在，會飛回鬼屋，並再生而回復正常的顏色。

最後的遊戲積分可以轉換成金錢
金錢可以購買skin

遊戲積分可以分享到社群

運動的里程數當做成就

達成一定成就可以拿錢

### 技術選用
由於以前有摸過[Mapbox][1]，而且[Mapbox Studio][2]的高度客制化功能剛好是我要的，因此地圖選擇使用Mapbox。

[React Native][3]的部分因為他真的很強大，在不偷跑的情況下要在短短的兩天內做出一個可以看的App，使用它真的會方便許多。

豆子的產生是由銓哥用C++程式寫的，主要原理是先在地圖道路上選兩個點，然後由其中一點向另一點不停打點。由於如果要在全地圖打點有點麻煩，所以我們一開始的考量就是只在輔大的地圖上打點就好，這些點算是Hard Code哈哈。

配色的啟發是在黑客松前幾天剛好在medium上看到一篇在講 [Color trend 2016/2017][4]

[1]:https://www.mapbox.com/
[2]:https://www.mapbox.com/studio/
[3]:http://facebook.github.io/react-native/
[4]:https://medium.muz.li/color-trend-2016-2017-c40e34f08f2c#.bhrqrvors

## 成果

實際在校園裡遊玩的螢幕錄影

![alt text](https://github.com/KevinHu2014/Pacman/blob/master/screenshots/demo.gif?raw=true "Demo")


Zoom in 地圖

![alt text](https://github.com/KevinHu2014/Pacman/blob/master/screenshots/01.png?raw=true "Demo")

Zoom out 地圖

![alt text](https://github.com/KevinHu2014/Pacman/blob/master/screenshots/02.png?raw=true "Demo")

## 遊戲玩法

在地圖的右下角有三個按鈕，從上到下分別是**磁鐵**、**定位回中心**與**地圖縮放**。

**磁鐵**: 是用來吸收玩家附近的豆子，我們改良了經典的小精靈的玩法

**定位回中心**:  由於地圖是可以滑動的，怕玩家在滑動後位子會跑掉，因此設計了這個按鍵，讓地圖可以迅速回到中心（以使用者的位置為中心）。

**地圖縮放**: 我們只設定了兩種zoom level


## 心得
這次非常感謝老楊與銓哥兩位夥伴陪我這個係邊參加黑客松，雖然最後只拿到第三名，但已滿足哈哈哈。 要用React Native做遊戲真的不容易，尤其是沒有什麼遊戲引擎可以用，要什麼新增什麼酷炫功能都要自己來。

![alt text](https://s10.postimg.org/w4jprbi4p/16251219_120300001783519418_1984515907_o.jpg "第三名")
