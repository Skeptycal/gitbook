---
layout: default
permalink: index.html
title: ihower 的 Git 教室
---

部落格文章
===

<ul>
<li><a href="http://ihower.tw/blog/archives/6704/">Git rebase 和 merge 合併操作示範錄影</a></li>
<li><a href="http://ihower.tw/blog/archives/5691">如何建立一個沒有 Parent 的 Git branch</a></li>
<li><a href="http://ihower.tw/blog/archives/5436">我的 Git 偏好設定</a></li>
<li><a href="http://ihower.tw/blog/archives/5140">Git flow 開發流程 </a></li>
<li><a href="http://ihower.tw/blog/archives/2622">Git 版本控制系統 (3) 還沒 push 前可以做的事</a></li>
<li><a href="http://ihower.tw/blog/archives/3843">使用 git rebase 避免無謂的 merge</a></li>
<li><a href="http://ihower.tw/blog/archives/2620">Git 版本控制系統 (2) 開 branch 分支和操作遠端 repo. </a></li>
<li><a href="http://ihower.tw/blog/archives/2591">Git 版本控制系統 (1)</a></li>
<li><a href="http://ihower.tw/blog/archives/1733">Github 分散式版本控制的殺手級應用</a></li>
</ul>

另外，我在[Ruby on Rails 實戰聖經](http://ihower.tw/rails3)一書中也有一篇[Git簡介](http://ihower.tw/rails3/git)。

上手指令集
======

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

產生 SSH Key，做為 Github 認證之用

	ssh-keygen -t rsa -C "your_email@youremail.com"
	cat ~/.ssh/id_rsa.pub
	複製下來貼到 Github 帳號 -> Account Settings -> SSH Keys 裡
	這樣在 Github 開專案，就可以 push 和 pull 下來。