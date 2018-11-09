---
title: "［MySQL］安裝與介面化工具(for Mac OS)"
date: 2018-11-08T22:54:39+08:00
draft: false
categories: [Web Back-end Development]
tags: [MySQL]
---

## Download MySQL Community Server

社群版本，開源免費，但不提供官方技術支援。

* https://dev.mysql.com/downloads/mysql/

## Open/Stop MySQL Server

* 左上角蘋果圖示 --> 系統偏好設定 --> MySQL
* 進入操作頁面後，就可以開與關MySQL Server

## Terminal Command

### 增加路徑至$PATH(iTerm2+Oh My Zsh)

```bash
# 進入並編輯.zshrc檔案
$ vim ~/.zshrc

# 增加以下敘述，增加後儲存離開
export PATH="/usr/local/mysql/bin:$PATH"

# 關掉terminal，重新打開，輸入以下指令查看$PATH是否有mysql執行路徑
$ echo $PATH
```

如此一來，即可在terminal上直接使用`mysql`開頭的指令了。

### 進入MySQL

若MySQL下載5.7以上的版本，則安裝包一開始會設定好root初始的密碼(亂數，下載後需複製)。

```bash
# 若root沒有設定密碼
$ mysql -u root
# 若root有設定密碼，會跳出輸入密碼的提示，輸入密碼後進入
$ mysql -u root -p
```

### 重新設定密碼

```bash
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'New Password';
```

### 選擇資料庫

```bash
mysql> use mysql;
```

### 刷新MySQL

```bash
mysql> flush privileges;
```

### 離開MySQL

```bash
mysql> quit
```

## Mac用介面化工具

* [Sequel Pro](https://www.sequelpro.com/)

### Reference
---
* https://goo.gl/NpZNQA