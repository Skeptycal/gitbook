---
layout: default
permalink: tips.html
title: ihower 的 Git 教室
---

## Git Tips

### 其他更多指令

git archivegit bisectgit blamegit grepgit showgit gcgit format-patch, send-email, am

### git pull --rebase

使用 git pull --rebase 可以避免無謂的 merge 節點，讓線圖變乾淨http://ihower.tw/blog/archives/3843
git pull 何時用 merge? 何時用 rebase?
修改比較多，預期會有 conflict，用 merge	是不是一開始就應該開 feature branch 來做呢?修改範圍較小，不太預期有 conflict，建議可以用 --rebase
但是如果採用 git flow 利用 branches，就可以大幅降低無謂 merge 情形!