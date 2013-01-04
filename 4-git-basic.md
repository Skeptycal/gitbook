---
layout: default
permalink: basic.html
title: ihower 的 Git 教室
---

本章介紹 Git 的本地操作指令，不需要網路即可操作。

## Git 基本操作

Git 是分散式的，表示你不需要伺服器，在本地端就有完整的*Repository*。

### 建立、新增、修改、遞交

從頭建立 Repository：

	mkdir sandbox





### Staging Area

一個 Git 目錄裡，可以分成三種區域：

* 目前工作目錄 Working tree
* 暫存準備遞交區 Staging Area
* 儲存庫 Repository

![Staging area](images/basic-1.png)

而 Working tree 裡的檔案有四種狀態：

![Staging area](images/basic-2.png)

* 沒有被追蹤的檔案 Untracked files
* 有修改、還沒準備要被遞交 Changes not staged for commit
* 有修改、準備要被遞交的檔案(在Staging Area) Changes to be commtted
* 已經被遞交的檔案 Commtted

Staging Area 算是 Git 獨有的功能，有什麼好處呢?

* Working tree 可能很亂，包含了想要 commit 的內容和不相關的實驗修改等

只 commit 部分檔案：

	touch a.rb







### revert (還原 commit 記錄)

### Tag 下標籤

	git tag foo

### 歷史紀錄

	git log

### 比較差異 Diff

	git diff <SHA1> 拿 Working Tree 比較
### 砍掉 untracked 檔案

	git clean -n 列出打算要清除的檔案

### 忽略不需要追蹤的檔案


	編輯 .gitignore (屬於專案的設定，會 commit 出去)








> Git 預設的 branch 叫做*master*



### 四種合併方式

#### 1. Straight merge 預設的合併模式





切換 working tree 的 branch 時，如果有檔案在 staging area 或是 modified，會無法切換。





