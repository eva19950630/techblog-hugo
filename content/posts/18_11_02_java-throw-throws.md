---
title: "［Java］異常處理機制：throw與throws"
date: 2018-11-02T21:31:53+08:00
draft: false
categories: [Basic Programming Language]
tags: [Java]
---

## throw
用於丟出一個異常物件。

語法：寫於程式語句中。

throw [例外物件變數];

舉例：throw new Exception("這是例外錯誤！");

## throws
用於宣告此method會丟出哪些Exception，表示此method可能會發生哪些例外，加s意指可以同時使用多個Exception子類別修飾方法。

語法：寫於宣告method的地方。

舉例：public void function() throws Exception {...}

### 上述兩者差異
* 寫的地方不同：`throw`寫在語句中；`throws`寫在函數頭。
* 執行可能性：若編譯過程中執行`throw`則表示一定發生異常；而`throws`只是宣告該method可能發生異常，但不一定會發生這些異常。

## 配合使用try catch
Coding時，盡可能在可能出現異常的地方，使用`try{...}catch{...}`來捕捉(發現)異常並進行處理。

發現異常後，一定要在`catch{...}`內進行異常發生時的處理。

如果有在method內寫throw語句丟出異常，盡量在函數頭加上throws進行聲明，若真的發生異常，則會將異常交給上層呼叫此異常方法進行處理(通常在`catch{...}`內)。

`Example`

```java
public class test {
	public static void main (String[] args) {
		try {
			score(101);
		} catch (Exception e) {
			System.out.println(e.getMessage());
		}
	}

	public static void score(int num) throws Exception {
		if (num > 100)
			throw new Exception("Over");
	}
}
```

`Tips`

如果有使用到繼承時，若父類別某個method有throws某些例外，子類別欲重新定義該方法，可以throws父類別該方法宣告的某些例外，但不可throws父類別方法中「未宣告」的例外。

### Reference
---
* http://jhengjyun.blogspot.com/2010/06/java-throwthrows.html
* https://hk.saowen.com/a/3759f3e723abe683f4b20f65bec494c26b097467c095b77de2b0b1778eee8b5e
* https://www.javaworld.com.tw/jute/post/view?bid=29&id=282977
* https://openhome.cc/Gossip/Java/Throw.html