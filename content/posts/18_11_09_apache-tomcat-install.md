---
title: "安裝Apache Tomcat Server(for Mac OS)"
date: 2018-11-09T11:07:48+08:00
draft: false
categories: [Java Web/Spring]
tags: [Apache Tomcat Server]
---

## Download Apache Tomcat 8(Version 8.0.53)

目前穩定版本，Release Data：2018/06/29。

* https://tomcat.apache.org/download-80.cgi

下載Version8.0.53的`.zip`或`.tar.gz`，下載後解壓縮出一個`apache-tomcat-8.0.53`的資料夾。

![下載.zip或.tar.gz](/18_11_09_apache-tomcat-install/001.png)

## Start/Stop Apache Tomcat Server

### Step1：將解壓縮後的apache-tomcat-8.0.53資料夾移至`/usr/local`目錄下

```bash
# 預設apache-tomcat-8.0.53資料夾位置在下載資料夾中
$ sudo mv ~/Download/apache-tomcat-8.0.53 /usr/local
```

### Step2：新增symbolic link在`/Library`目錄下

```bash
$ sudo ln -s /usr/local/apache-tomcat-8.0.53 /Library/Tomcat
```

### Step3：更改此symbolic link的使用者權限

```bash
# [username]更改為自己的username
$ sudo chown -R [username] /Library/Tomcat
```

### Step4：設定bin目錄下的所有shell scripts有被執行的權限

```bash
$ sudo chmod +x /Library/Tomcat/bin/*.sh
```

### Step5：開啟/關閉Tomcat Server服務

```bash
# 開啟Tomcat Server服務
$ /Library/Tomcat/bin/startup.sh

# 關閉Tomcat Server服務
$ /Library/Tomcat/bin/shutdown.sh
```

開啟瀏覽器，網址輸入[http://localhost:8080](http://localhost:8080)，出現以下畫面即代表開啟服務成功。

![開啟Tomcat Server](/18_11_09_apache-tomcat-install/002.png)

`Tips`

如果要查看`Server Status`、`Manager App`、`Host Manager`這些功能，需要新增管理者的角色權限。

* 先shutdown server
* 編輯/Library/Tomcat/conf/tomcat-users.xml

內容最下方有一段註解的：

```xml
<role rolename="tomcat"/>
<role rolename="role1"/>
<user username="tomcat" password="<must-be-changed>" roles="tomcat"/>
<user username="both" password="<must-be-changed>" roles="tomcat,role1"/>
<user username="role1" password="<must-be-changed>" roles="role1"/>
```

但刪掉註解後，依舊無法使用Web Manager App的功能。

因此需要新增角色，在檔案中加入下面的內容(上段註解無需打開)：

```xml
<role rolename="admin-gui"/>
<role rolename="admin-script"/>
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
# [username]、[password]為自定帳號密碼
<user username="[username]" password="[password]" roles="manager-gui,manager-script,manager-jmx,manager-status,admin-script,admin-gui"/>
```

存檔後再start server，就可以使用`Server Status`、`Manager App`、`Host Manager`管理server了。

### Reference
---
* http://tonytsai1984.blogspot.com/2016/09/mac-os-x-tomcat-9.html