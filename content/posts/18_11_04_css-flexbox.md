---
title: "［CSS3］Flexbox"
date: 2018-11-04T21:20:00+08:00
draft: false
categories: [Web Front-end Development]
tags: [CSS]
---

網頁前端設計時，時常遇到排版區塊的問題，目前有許多排版框架(如：Bootstrap)可以使用並快速排版，而其實CSS3提供了一個很好的排版模型：`flexbox`，這讓我們在排版介面時更加快速與彈性，而且能輕鬆進行響應式設計(RWD)，在各大瀏覽器也幾乎都支援，因此`flexbox`是近年來愈來愈多人在使用的排版模型。

## Layout Box Model

首先先了解flexbox的佈局模型，才能較快上手flexbox，根據[W3C](https://www.w3.org/TR/css-flexbox-1/#box-model)的文章，flexbox的佈局模型如下圖：

![flexbox佈局模型](/18_11_04_css-flexbox/001.png)

從上圖可以觀察到：

* 最外層有一個`flex container`包覆著內層兩個`flex item`的元件區塊：
   * 意指當要使用flexbox時，需在所有要排版的元件區塊最外層包覆著一個容器，並給定flex效果，讓這個容器內所有元件區塊皆有flex效果。
* 最外層容器具有水平軸(main axis)、垂直軸(cross axis)、水平的起點與終點(main start、main end)、垂直的起點與終點(cross start、cross end)、水平尺寸(main size)與垂直尺寸(cross size)。

因此透過上圖，flexbox的模型概念可以了解成：

在一個有flex效果的父元件容器(container)當中，裝載著各個區塊子元件(items)，而每個item擺放的位置可透過設定main與cross去劃分位置，將各個區塊擺到相對應的位置上。

以下將分別介紹父元件容器(container)與子元件區塊(items)可應用的屬性。

## 父元件容器(container)

### display

在最外層容器一定要設定有flex效果，其內部子元件才會跟著有flex效果。使用display屬性設定，有兩種方式：

* `display: flex`：類似display: block，後方元素會強迫換行，但子元件有更多彈性的設定。
* `display: inline-flex`：類似display: inline-block，意思即一個display: flex外包覆一個display: inline的屬性，後方元素不會換行。

```css
.flex-container {
	display: flex | inline-flex;
}
```

### flex-direction

設定內部子元件的「排列方向」(主軸方向)。

預設值為**先由左到右，再從上到下**，總共有四種排列方式可以設定：

* `flex-direction: row`：預設值，先由左到右，再從上到下。
* `flex-direction: row-reverse`：與row相反。
* `flex-direction: column`：先從上到下，再由左到右。
* `flex-direction: column-reverse`：與column相反。

![flex-direction排列方式示意圖](/18_11_04_css-flexbox/002.png)

```css
.flex-container {
	display: flex;
	flex-direction: row | row-reverse | column | column-reverse;
}
```

### flex-wrap

設定內部子元件在父元件有限寬度內「是否換行」。

因為當container設定為flex屬性後，內部子元件則預設以**不換行**的方式進行排列，彈性撐滿整個容器。而flex-wrap有三種方式可以設定：

* `flex-wrap: nowrap`：預設值，單行(不換行)。
* `flex-wrap: wrap`：多行。
* `flex-wrap: wrap-reverse`：多行，但內容元件反轉。

![flex-wrap設定方式示意圖](/18_11_04_css-flexbox/003.png)

```css
.flex-container {
	display: flex;
	flex-wrap: nowrap | wrap | wrap-reverse;
}
```

### flex-flow

為上述`flex-direction`與`flex-wrap`的**縮寫**，可同時設定這兩者的屬性。

語法：flex-flow: [flex-direction屬性] [flex-wrap屬性];

* [flex-direction屬性]、[flex-wrap屬性]分別給定對應的屬性值。

`Example`

```css
.flex-container {
	flex-flow: column wrap;
}
```

### justify-content

設定內部子元件的「水平對齊」位置。

最上面提到flexbox的佈局模式，有水平的起點與終點(main start、main end)兩個端點，因此可透過justify-content設定內部元件的水平對齊位置，總共有五種對齊方式：

* `justify-content: flex-start`：預設值，對齊最左邊的main start位置。
* `justify-content: flex-end`：對齊最右邊的main end位置。
* `justify-content: center`：水平置中。
* `justify-content: space-between`：平均分配內容元素，最左邊與最右邊元素會分別貼齊main start與main end位置。
* `justify-content: space-around`：平均分配內容元素，各元素的間距也平均分配。

![justify-content設定示意圖](/18_11_04_css-flexbox/004.png)

```css
.flex-container {
	display: flex;
	justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

### align-items

設定內部子元件的「垂直對齊」位置(元件排列為「單行」適用)。

與上述`justify-content`相反，一樣是根據佈局模式垂直起點與終點(cross start、cross end)來對齊相對應位置，總共有五種對齊方式：

* `align-items: flex-start`：對齊最上面的cross start位置。
* `align-items: flex-end`：對齊最下面的cross end位置。
* `align-items: center`：垂直置中。
* `align-items: stretch`：預設值，所有內容元素整個撐開在容器的有限高度內。
* `align-items: baseline`：以所有內容元素的基線(baseline)作為對齊標準。下圖每個元件內「文字大小」不同，因此以文字的底部作為基線。

![align-items設定示意圖](/18_11_04_css-flexbox/005.png)

```css
.flex-container {
	display: flex;
	align-items: flex-start | flex-end | center | stretch | baseline;
}
```

### align-content

設定內部子元件的「垂直對齊」位置(元件排列為「多行」適用)。

與上述`align-items`類似，只是為設定多行元件的垂直對齊位置，總共有六種對齊方式：

* `align-content: flex-start`：對齊最上面的cross start位置。
* `align-content: flex-end`：對齊最下面的cross end位置。
* `align-content: center`：垂直置中。
* `align-content: space-between`：第一行元素對齊最上面cross start位置，最後一行元素對齊最下面cross end位置。
* `align-content: space-around`：每行平均分配間距。
* `align-content: stretch`：預設值，所有內容元素整個撐開在容器的有限高度內。

![align-content設定示意圖](/18_11_04_css-flexbox/006.png)

```css
.flex-container {
	display: flex;
	flex-wrap: wrap;
	align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

## 子元件區塊(items)

### order

設定各個子元件的「排列順序」。

與`flex-wrap`不同的是，`order`可**個別**定義子元件的順序。

![order設定示意圖](/18_11_04_css-flexbox/007.png)

```html
<div class="flex-container" style="display: flex">
  <div style="order: 5">1</div>
  <div style="order: 3">2</div>
  <div style="order: 4">3</div>
  <div style="order: 2">4</div>
  <div style="order: 1">5</div>
</div>
```

### flex-grow

設定子元件是否具有「伸展性」，配值為一個**數值**，預設值為「0」，表示不會進行任何伸展變化，設定「1」以上的數值則會在容器有限空間內相對應比例分配伸展長度，但不可設定為負值。

適用於子元件沒有設定長度時。

![flex-grow設定示意圖](/18_11_04_css-flexbox/008.png)

```html
<div class="flex-container" style="display: flex; width: 500px;">
  <div style="flex-grow: 0">1</div>
  <div style="flex-grow: 1">2</div>
  <div style="flex-grow: 5">3</div>
</div>
```

### flex-shrink

設定子元件是否具有「壓縮性」，配值為一個**數值**，預設值為「1」，設定「0」則不會進行任何壓縮變化，設定「1」以上的數值則會在容器有限空間內相對應比例分配長度，但不可設定為負值。

適用於子元件有設定長度時。

![flex-shrink設定示意圖](/18_11_04_css-flexbox/009.png)

```html
<div class="flex-container" style="display: flex; width: 500px;">
  <div style="flex-shrink: 1; width: 200px;">1</div>
  <div style="flex-shrink: 1; width: 200px;">2</div>
  <div style="flex-shrink: 0; width: 200px;">3</div>
  <div style="flex-shrink: 1; width: 200px;">4</div>
  <div style="flex-shrink: 1; width: 200px;">5</div>
</div>
```

### flex-basis

設定子元件的「基本大小」，可使用不同的單位值(例如：px)，預設值為「0」，若沒有設定此屬性則會直接採用`flex-grow`屬性，也可以設定為auto，表示以子元素本身的基本大小作為基準。

![flex-shrink設定示意圖](/18_11_04_css-flexbox/010.png)

```html
<div class="flex-container" style="display: flex; width: 500px;">
  <div style="flex-basis: 0;">1</div>
  <div style="flex-basis: 0;">2</div>
  <div style="flex-basis: 300px;">3</div>
  <div style="flex-basis: 0;">4</div>
  <div style="flex-basis: 100px;">5</div>
</div>
```

### flex

為上述三者`flex-grow`、`flex-shrink`、`flex-basis`的**縮寫**，可同時設定這三者的屬性。

語法：flex: [flex-grow屬性] [flex-shrink屬性] [flex-basis屬性];

* [flex-grow屬性]、[flex-shrink屬性]、[flex-basis]分別給定對應的屬性值。

通常這三個屬性都是適用在製作不同版面大小的元件時，可以透過伸展與壓縮來達到元件不會跑掉的目的，因此如果下方例子第三個區塊將flex-shrink設定為「0」，在壓縮畫面大小的時候，其元件大小依舊為原本設定的大小，不會更動。

![flex設定示意圖](/18_11_04_css-flexbox/011.png)

```html
<div class="flex-container" style="display: flex; width: 500px;">
  <div style="flex: 2 1 0">1</div>
  <div style="flex: 1 1 0">2</div>
  <div style="flex: 0 0 300px">3</div>
</div>
```

### align-self

設定與`align-items`相似，其設定種類也一樣(flex-start、flex-end、center、stretch、baseline)，但不同的是，`align-self`可針對某一元件做設定，因此若一開始父元件有設定`align-items`，當子元件設定`align-self`，則會直接覆寫原本父元件所設定的屬性。

![align-self設定示意圖](/18_11_04_css-flexbox/012.png)

```html
<div class="flex-container" style="display: flex; align-items: stretch;">
  <div>1</div>
  <div style="align-self: center;">2</div>
  <div style="align-self: flex-end;">3</div>
</div>
```

### Reference
---
* https://www.w3.org/TR/css-flexbox-1/#box-model
* https://www.w3schools.com/css/css3_flexbox.asp
* https://wcc723.github.io/css/2017/07/21/css-flex/
* https://www.oxxostudio.tw/articles/201501/css-flexbox.html
* https://dotblogs.com.tw/leo_codespace/2018/05/02/154954