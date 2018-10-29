---
title: "使用Github Pages架設Hugo靜態blog"
date: 2018-10-29T09:50:03+08:00
draft: false
categories: [Text Editing/Blog/Github]
tags: [Github, Hugo]
---

Github除了可以使用Git Server儲存code之外，也可當作靜態網頁的Server，所以可作為個人靜態網頁或blog，但僅能使用git指令上傳修改檔案，而且只能顯示「靜態」網頁內容。

### 操作步驟分為兩部分(使用MacOS)

1. 在本地端架設Hugo個人網站(blog)
2. 部署至Github上成為個人Github pages

## 第一部分：在本地端架設Hugo個人網站(blog)
Hugo為open source的靜態網頁框架產生器，可快速建立個人網站或blog。

### Step1：使用terminal安裝Homebrew
Homebrew為open source的軟體套件管理工具，可簡化在Mac上安裝或卸載套件的過程。

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Step2：使用terminal安裝Hugo

```bash
brew install hugo
```

### Step3：使用Hugo創建新網站
到想要的目錄下，創建Hugo新網站。

```bash
# [website-name]為自定網站資料夾名稱
hugo new site [website-name]
cd [website-name]
```

創建完成後，可在terminal看到以下畫面：
![成功建立Hugo網站](/18_10_29_github-pages-hugo/001.png)

cd至該網站資料夾內，可看到內部資料夾結構如下：
![Hugo內部資料夾結構](/18_10_29_github-pages-hugo/002.png)

### Step4：更換主題(Theme)
[官網](https://themes.gohugo.io/)提供許多網站主題，若找到合適的即可使用git clone下載該主題。

在官網主題內找尋喜歡的主題，並點選進去：
![進入主題github](/18_10_29_github-pages-hugo/003.png)

複製該主題的git網址，並使用git clone下載至`themes`資料夾中：
![複製git網址](/18_10_29_github-pages-hugo/004.png)

cd至網站資料夾內的`themes`資料夾中：
```bash
cd themes
git clone [該主題git網址]
```

### Step5：編輯config.toml檔案
config.toml檔案在根目錄下，使用sublime或其他文字編輯器進行修改，由於之後會將此Hugo個人網站部署至Github上，因此`baseURL`需配置為Github pages的網址，而theme為更換剛剛Step4下載的主題資料夾名稱。

```text
baseURL = "https://[個人Github帳號].github.io/"   # [個人Github帳號]需改為Github帳號
languageCode = "zh-tw"
title = "[My New Hugo Site]"   # [My New Hugo Site]為自定網站名稱
theme = "[Theme dir name]"   # [Theme dir name]為主題資料夾名稱
```

### Step6：建立新文章(post)
在根目錄下輸入以下指令建立新文章。

```bash
hugo new posts/[post name].md   # [post name]為自定文章檔案名稱
```

按下enter後，則可以在terminal看到以下建立成功畫面：
![成功建立新文章](/18_10_29_github-pages-hugo/005.png)

若建立成功，則可以在目錄下的`/contents/posts`資料夾中，看見剛剛新增的文章檔案(.md檔)，使用文字編輯器修改此md檔。

```text
---
title: "[New Post]"   # [New Post]為自定文章標題
date: 2018-10-29T11:06:37+08:00
draft: false   # 原本為true，改為false
---

[此處可輸入文章內容]
```

文章使用markdown語法編輯，未來建立文章皆使用Step6這個方式，`draft`記得改為false。

若文章中有使用圖片，圖片檔案放入根目錄中的`/static`資料夾內。

### Step7：本地端執行測試
以上步驟即可完成Hugo網站的大致雛形，若想看成品，可在本地端使用terminal先執行測試(在根目錄下)。

```bash
hugo serve -D
```

打開瀏覽器，輸入網址[http://localhost:1313/](http://localhost:1313/)，可看到如下畫面：
![Hugo網站創建完成](/18_10_29_github-pages-hugo/006.png)

## 第二部分：部署至Github上成為個人Github pages
Github提供靜態網站的server，使用者可將靜態網站上傳上去，作為Github pages，一隻帳號僅有一個主頁，這個部分將操作部署剛剛創建好的Hugo網站至Github上。

### Step1：在Github上新增一個新repository
repository name取名為`[Github帳號].github.io`。

### Step2：在Hugo網站根目錄下建立/public資料夾
使用terminal在根目錄下輸入以下指令，執行完後會在根目錄下產生一個`public`資料夾。

```bash
hugo
```

### Step3：在/public資料夾內初始化git並連結到Github pages
先至Github將剛新增repo的git網址複製下來(如第一部分Step4第二張圖)。

```bash
cd public

# 初始化git
git init
git remote add origin [貼上剛複製好的repo git URL]
git remote -v   # 檢查origin名稱是否有遠端連結到該git URL

# 建立第一個commit
git add .
git commit -m "Initial commit"
git push -u origin master
```

`Hint`

有時候在操作`git push`指令時，系統常常會告訴你要設定好要push去哪個分支，產生類似以下的錯誤。

```bash
git push

fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

	git push --set-upstream origin master
```

若今天在push時加入`-u`這個參數：

```bash
git push -u origin master
```

`-u`這個參數為表示設定upstream(上游)，以上述例子來看，`-u`設定下去後，就會把`origin/master`設定為本地`master`分支的upstream，下次要再執行`git push`指令而不加任何參數時，預設值則會知道是要將master這個分支推往origin這個遠端節點。

### Step4：查看個人Github pages
上個步驟push完成後，打開瀏覽器輸入網址https://[Github帳號].github.io/，就可以看到自己的Github pages了。

* Hugo建立的網站要連結至Github pages，需在`public`資料夾下進行push，往後若網站進行修改後，則需在根目錄下先執行`hugo`指令，在cd至public資料夾中進行commit與push。

* 另外，若想要將Hugo網站整個資料夾上傳到Github另一個repo，也是可以的，上傳過程中遇到資料夾重複上傳的warning可自動忽略。

### Reference
-----
* https://gohugo.io/
* https://medium.com/@chs_wei/%E5%9C%A8-github-%E9%83%A8%E7%BD%B2-hugo-%E9%9D%9C%E6%85%8B%E7%B6%B2%E7%AB%99-9c40682dfe40
* https://gitbook.tw/chapters/github/using-github-pages.html
* https://gitbook.tw/chapters/github/push-to-github.html