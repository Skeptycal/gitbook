---
layout: default
permalink: index.html
title: ihower 的 git 課程
---

[投影片下載](files/ihower-git.pdf)
======

指令集
======

安裝 Git

	sudo apt-get install git-core

	git config --global user.name "Your Name"
	git config --global user.email "your@email.com"
	git config --global color.ui true
	
	git config --global core.editor vi 
	或 git config --global core.editor gedit
	
安裝 GUI
    sudo apt-get install gitg
	或 sudo apt-get install gitk
	
一些好用的 git alias，編輯 ~/.gitconfig

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
        
指令列提示，編輯 ~/.bashrc

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

產生 SSH Key

	ssh-keygen -t rsa -C "your_email@youremail.com"
	cat ~/.ssh/id_rsa.pub
	複製下來貼到 Github 帳號 -> Account Settings -> SSH Keys 裡