---
layout: default
permalink: intro.html
title: ihower 的 Git 教室
---

## Git 簡介

版本控制系統是當代軟體開發所不可或缺的工具，而 Git 是其中最先進和熱門、且為開放原始碼的分散式版本控制系統(DVCS)。

Git 是由 Linux Torvalds 所發明，一開始的目的是為了管理 Linux Kernel 原始碼，他於2005/4 開始開發，2005/6 開始管理  Linux Kernel，2005/12 就釋出了 1.0 版。

因其分散式、效能好、本地存取、無痛分支的特性，而普遍適合各種開發流程，近年來受到多數人喜愛。使用 Git 的專案包括：Linux Kernel, Apache, Debian, Drupal, Eclipse, Fedora, Gnome, KDE, Perl, PHP, PostgreSQL, Ruby on Rails, Node.js, JQuery, YUI... 等等。諸如 Google, facebook, Microsoft, Twitter, Linkedin, NetFlix 等公司皆有使用 Git 作為版本控制系統。

不同於傳統 Delta 儲存方式，記錄每次檔案變更，開分支需要建立副本。Git 使用 DAG (Directed acyclic graph) 的儲存方式，利用有向無環圖來記錄 metadata 建構出 snapshots，相同內容只會有一份記錄。開分支也只是建立參考。Git 的內部原理，下一章會進一步介紹。這裡讀者只要有一個概念，理解 Git 最好的方法，就是用圖論中的節點(node)和指標(points)來思考，所有*Git*的指令操作，都是在操作這些節點，新增、修改、刪除、變更指標。

<blockquote class="twitter-tweet"><p>finally figuring out that git commands are strangely named graph manipulation commands--creating/deleting nodes, moving pointers around</p>&mdash; Kent Beck (@KentBeck) <a href="https://twitter.com/KentBeck/status/42657237986054144" data-datetime="2011-03-01T18:47:32+00:00">March 1, 2011</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

![Git graph example](images/intro-1.png)

## Git 安裝

### 安裝步驟 (Ubuntu)

在 Ubuntu 上安裝 Git

	sudo apt-get install git-core

	git config --global user.name "Your Name"
	git config --global user.email "your@email.com"
	git config --global color.ui true
	
	git config --global core.editor vi 
	或 git config --global core.editor gedit
	
安裝 GUI

    sudo apt-get install gitg
	或 sudo apt-get install gitk
	
> Github 上的安裝文件 [http://help.github.com/linux-set-up-git/](http://help.github.com/linux-set-up-git/)


### 安裝步驟 (Windows)

Windows 的 Git 請安裝 [msysgit](http://code.google.com/p/msysgit/)。如果是透過 RailsInstaller 安裝，則已經附帶安裝好了。請參考以下步驟產生 SSH key：

    $ c:\RailsInstaller\Git\bin\ssh-keygen.exe -t rsa -C "your_email@example.org"

接著用文字編輯器打開 "%homedrive%%homepath%\.ssh\id_rsa.pub" 的內容，即是你的 Public SSH key。

> 如果需要 GUI 介面，可以加裝 [http://code.google.com/p/tortoisegit/](http://code.google.com/p/tortoisegit/)，記得進 Settings 修改 Git path 至 C:\RubyInstall\Git\bin 即可。可以參考這份[投影片](http://www.slideshare.net/jason8301/tortoisegit-intro-in-traditional-chinese)。

Windows 平台上還有一件要注意的事情，就是對於換行字元的處理與 Unix/Mac 平台不同，會讓 Git 誤判成有修改，因此需要多以下設定：


    $ git config --global core.autocrlf true
    $ git config --global core.safecrlf true


> Github 上的安裝文件 [http://help.github.com/win-set-up-git/](http://help.github.com/win-set-up-git/)

### 安裝步驟 (Mac)

如果是透過 [Homebrew](http://mxcl.github.com/homebrew/) 安裝的話：

    $  brew install git
    
> Github 上的安裝文件 [http://help.github.com/mac-set-up-git/](http://help.github.com/mac-set-up-git/)
	
### 產生 SSH Key

因為 Git 的伺服器大多使用 SSH public/private key 來做認證，請用以下步驟產生 SSH Key。稍後會用 [Github](http://github.com) 練習。

	ssh-keygen -t rsa -C "your_email@youremail.com"
	cat ~/.ssh/id_rsa.pub
	複製下來貼到 Github 帳號 -> Account Settings -> SSH Keys 裡
	這樣在 Github 開專案，就可以 push 和 pull 下來了。
		
### 其他參考步驟

一些好用的 git alias，請編輯 ~/.gitconfig

     [alias]
        co = checkout
        ci = commit
        st = status
        br = branch -v
        rt = reset --hard
        unstage = reset HEAD
        uncommit = reset --soft HEAD^
        l = log --pretty=oneline --abbrev-commit --graph --decorate
        amend = commit --amend
        who = shortlog -n -s --no-merges
        g = grep -n --color -E
        cp = cherry-pick -x
	    nb = checkout -b
	     
        # 'git add -u' handles deleted files, but not new files
        # 'git add .' handles any current and new files, but not deleted
        # 'git addall' now handles all changes
        addall = !sh -c 'git add . && git add -u'

        # Handy shortcuts for rebasing
        rc = rebase --continue
        rs = rebase --skip
        ra = rebase --abort
        
命令列(Bash)提示，請編輯 ~/.bashrc

    function git_branch {
      ref=$(git symbolic-ref HEAD 2> /dev/null) || return;
      echo "("${ref#refs/heads/}") ";
    }

    function git_since_last_commit {
      now=`date +%s`;
      last_commit=$(git log --pretty=format:%at -1 2> /dev/null) || return;
      seconds_since_last_commit=$((now-last_commit));
      minutes_since_last_commit=$((seconds_since_last_commit/60));
      hours_since_last_commit=$((minutes_since_last_commit/60));
      minutes_since_last_commit=$((minutes_since_last_commit%60));
    
      echo "${hours_since_last_commit}h${minutes_since_last_commit}m ";
    }

    PS1="[\[\033[1;32m\]\w\[\033[0m\]] \[\033[0m\]\[\033[1;36m\]\$(git_branch)\[\033[0;33m\]\$(git_since_last_commit)\[\033[0m\]$ " 
	
### 參考資料

* [Why Git is Better than X](http://thkoch2001.github.com/whygitisbetter/)
* [用 Git 表示台北捷運](http://gugod.org/2009/12/git-graphing/)