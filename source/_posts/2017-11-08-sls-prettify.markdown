---
layout: post
title: "宅學習批改器"
date: 2017-11-08 11:04:39 +0800
comments: true
categories: python
---

## 前言

由於當助教改作業的流程很繁瑣（我hen懶），所以就寫了一個工具幫助自己簡化流程。

首先，學生會在一個名為宅學習的平臺上撰寫作業，寫完後存檔會得到一個unique的URL，接著將這個URL貼到臉書課程社團的作業繳交貼文之留言處。
然後助教在改作業時，就要點擊留言的網址，切換瀏覽器分頁，看完作業再關閉切換下一個。 所以改一份作業大概是三次點擊，假設修課人數有六十人… 大約就是180次的點擊🙄

## 正文

作業繳交貼文留言的格式如下
![](https://s8.postimg.org/l7cervb39/2017-11-21_11.57.01.png)

讓我們開啟瀏覽器的開發人員工具來檢視

![](https://s8.postimg.org/9jicwuodx/2017-11-22_12.00.10.png)


程式碼如下
``` html
<span class="UFICommentBody">
  <a class="" dir="ltr" target="_blank"
   href="https://l.facebook.com/l.php?u=https%3A%2F%2Fsls.weco.net%2Fnode%2F28539&amp;h=ATOzewHOmxTiqORjcKQalUU4Q5Xc4M09fgfLDk7-4-Sf9BvMfqBoHTYK26mHWWKEyjnB8rhkhbF4kMWcAY64HgbYfbv_r5wggX01rVFusbyQ3zTEkl9QBauQ7zYEErTPtwSeRZZDtZf7x3E51A"rel="nofollow"
  >
   https://sls.weco.net/node/28539
  </a>
</span>
```

我們關注的會是這串連結

```
https://sls.weco.net/node/28539
```

而我們先將作業繳交貼文留言的程式碼複製貼上到 `data.html`的檔案裡，再寫一隻爬蟲`parse.py`去爬我們要的資訊
<!--more-->
``` python
# -*- coding: utf-8 -*-
# parse.py

# function import BeautifulSoup
from bs4 import BeautifulSoup

# genetic import codecs
import codecs

# 讀檔
f = codecs.open("data.html", 'r', 'utf-8')

```
透過 `soup.select('span[class=UFICommentBody] a')`會回傳所有class 為 `UFICommentBody`之 `<span>`下的 `<a>`。由於結果不只一筆，所以回傳的是一個陣列。透過`for`去走訪它，而我們需要的只有 `<a>` tag 裡的文字，因此用 `.get_text()` 去取得文字。

``` python

s = ""

for child in soup.select('span[class=UFICommentBody] a'):
    s = s + "\"" + child.get_text() + "\","

print(s)
```
輸出結果

```
output

"https://sls.weco.net/node/28888","https://sls.weco.net/node/28889","https://sls.weco.net/node/28890","https://sls.weco.net/node/28874"......
```
拿到這些連結後，我們只要再透過iFrame就能將所有的作業連結都呈現在同一頁了。

``` HTML
// index.html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>SLS Prettify</title>

</head>
<body>
  <script language="javascript" type="text/javascript" src="scripts.js"></script>
</body>
</html>
```

``` javascript
// script.js
var i = 0;
var arr = ["https://sls.weco.net/node/28888","https://sls.weco.net/node/28889","https://sls.weco.net/node/28890","https://sls.weco.net/node/28874","https://sls.weco.net/node/28891","https://sls.weco.net/node/28892","https://sls.weco.net/node/28894","https://sls.weco.net/node/28900","https://sls.weco.net/node/28901","https://sls.weco.net/node/28902","https://sls.weco.net/node/28905","https://sls.weco.net/node/28906","https://sls.weco.net/node/28903","https://sls.weco.net/node/28907","https://sls.weco.net/node/28908","https://sls.weco.net/node/28909","https://sls.weco.net/node/28910","https://sls.weco.net/node/28911","https://sls.weco.net/node/28912","https://sls.weco.net/node/28913","https://sls.weco.net/node/28914","https://sls.weco.net/node/28915","https://sls.weco.net/node/28916","https://sls.weco.net/node/28917","https://sls.weco.net/node/28918","https://sls.weco.net/node/28919","https://sls.weco.net/node/28921","https://sls.weco.net/node/28893","https://sls.weco.net/node/28922","https://sls.weco.net/node/28923","https://sls.weco.net/node/28924","https://sls.weco.net/node/28926","https://sls.weco.net/node/28925","https://sls.weco.net/node/28928","https://sls.weco.net/node/28920","https://sls.weco.net/node/28929","https://sls.weco.net/node/28930","https://sls.weco.net/node/28927","https://sls.weco.net/node/28933","https://sls.weco.net/node/28934","https://sls.weco.net/node/28931","https://sls.weco.net/node/28935","https://sls.weco.net/node/28936","https://sls.weco.net/node/28937","https://sls.weco.net/node/28939","https://sls.weco.net/node/28938","https://sls.weco.net/node/28940","https://sls.weco.net/node/28941","https://sls.weco.net/node/28942","https://sls.weco.net/node/28944","https://sls.weco.net/node/28943","https://sls.weco.net/node/28945","https://sls.weco.net/node/28946","https://sls.weco.net/node/28947","https://sls.weco.net/node/28948","https://sls.weco.net/node/28949","https://sls.weco.net/node/28950","https://sls.weco.net/node/28951","https://sls.weco.net/node/28952","https://sls.weco.net/node/28953","https://sls.weco.net/node/28954","https://sls.weco.net/node/28955","https://sls.weco.net/node/28956","https://sls.weco.net/node/28958","https://sls.weco.net/node/28959","https://sls.weco.net/node/28960","https://sls.weco.net/node/28961",];
while(i<arr.length){
    var Frame = document.createElement("Iframe");
    Frame.src = arr[i];
    Frame.width = "90%";
    Frame.height = "500px";
    document.body.appendChild(Frame);
    i=i+1;
    }


```
[範例網頁](http://hsiangyu.com/SLS_Prettify/)


目前流程為：

把複製程式碼貼到`data.html` => 執行`parse.py`=>將輸出結果貼到`script.js`=>打開網頁`index.html`

但這樣的流程還是有點繁瑣，不過自動化，所以我寫了一個shell script來自動化（執行`parse.py`=>將輸出結果貼到`script.js`=>打開網頁`index.html`）這部分的流程。

``` bash
#run.sh

#!/bin/bash

#將parse.py 的執行結果輸出到 output.txt中
python3 parse.py > output.txt
#把第二行刪掉
sed -i '' '2d' scripts.js
#在第一行的後面 加入 output.txt 的內容
sed -i '' '1 r output.txt' scripts.js
#開啟瀏覽器
open index.html

```
簡化後的流程：

把複製程式碼貼到`data.html` => 執行`run.sh`

簡化超多的xDDDD

## 心得
透過這次的寫工具讓我再次體會到`偷懶使人進步`xDDD，剛好透過這次的機會學會了一點shell script，也體會到自動化的強大，將繁瑣的事情交給電腦吧!
