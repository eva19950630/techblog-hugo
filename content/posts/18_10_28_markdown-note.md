---
title: "Markdown筆記"
date: 2018-10-28T20:27:16+08:00
draft: false
categories: [Text Editing/Blog/Github]
tags: [Markdown]
---

## 一般文字(Text)
test

## 標題(Title)
```markdown
# test1.1
## test1.2
### test1.3
#### test1.4
##### test1.5
###### test1.6
```

`Example`

# test1.1
## test1.2
### test1.3
#### test1.4
##### test1.5
###### test1.6

## 引用文字(Blockquote)
```markdown
> test2
```

`Example`

> test2

## 粗體/斜體/刪除線
```markdown
# 粗體
**test3.1**
__test3.2__
# 斜體
*test4.1*
_test4.2_
# 刪除線
~~test5~~
```

`Example`

**test3.1**

__test3.2__

*test4.1*

_test4.2_

~~test5~~

## 無序列點
```markdown
* test6.1
* test6.2
* test6.3

- test6.4
- test6.5
- test6.6
```

`Example`

* test6.1
* test6.2
* test6.3

- test6.4
- test6.5
- test6.6

## 有序列點
```markdown
1. test7.1
2. test7.2
3. test7.3
```

`Example`

1. test7.1
2. test7.2
3. test7.3

## 巢狀列點
```markdown
1. test8.1
   1. test8.1.1
   2. test8.1.2
2. test8.2
   * test8.2.1
   * test8.2.2
```

`Example`

1. test8.1
   1. test8.1.1
   2. test8.1.2
2. test8.2
   * test8.2.1
   * test8.2.2

## Code
```markdown
`test9`

```html
<head>
    <title>test10</title>
</head>
(```)
# 括號()去掉
```

`Example`

`test9`

```html
<head>
    <title>test10</title>
</head>
```

## 連結(Link)
```markdown
# 符號皆為半型
[test11](https://www.google.com/)
test12，連結至Google(https://www.google.com/)
```

`Example`

[test11](https://www.google.com/)

test12，連結至Google(https://www.google.com/)

## 分隔線
```markdown
***
----
- - -
```

`Example`

***
----
- - -

## 表格(Table)
```markdown
名稱 | 說明
---------- | ----------
test13.1 | about test13.1
test13.2 | about test13.2
test13.3 | about test13.3
```

`Example`

名稱 | 說明
---------- | ----------
test13.1 | about test13.1
test13.2 | about test13.2
test13.3 | about test13.3

## 圖片(Image)
```markdown
![Alt text](/path/to/img.jpg)

# hugo blog需將圖片放置static資料夾中，資料夾內可自由新增其他子資料夾
![test14](/18_10_28_markdown-note/test14.jpg)

# 也可直接使用<img>標籤，即可調整長寬
<img src="/18_10_28_markdown-note/test14.jpg" width="300" height="300"></img>
```

`Example`

![test14](/18_10_28_markdown-note/test14.jpg)

<img src="/18_10_28_markdown-note/test14.jpg" width="300" height="300"></img>

## 跳脫字元
```markdown
# 下方這些符號插入後會產生效果，為了不顯示效果，在下方符號前面插入反斜線(\)，即可顯示原符號
# \ ` * _ {} [] () # + - . !

\*test15\*
```

`Example`

\*test15\*

### Reference
------
* https://markdown.tw/
* https://ithelp.ithome.com.tw/markdown/