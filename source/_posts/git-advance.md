---
title: Git 進階
date: 2019-08-13 11:00:57
tags:
  - git
categories:
  - git
---
## git fetch v.s. git pull
`git fetch`: 下載新版的意思，但並沒有做 merge 的動作
`git pull`：下載新版並同時做 merge 的動作。簡單來說就是等於 `git fetch` 加上 `git merge` 到本地分支

一般不推薦直接使用 `git pull`，因為當下載的新版本出問題時，因為`git pull`會直接 merge，而導致無法看到新版本可能出現的問題．

## upstream
本地分支透過設定 upstream ，可開始追蹤指定的遠端分支，一旦設定好後，不論 push 或 pull，都不需再打上遠端的分支名稱。

    $ git branch --set-upstream origin 指定分支名

另外也可以取消追蹤遠端分支，使用 `--unset-upstream` 即可

    $ git branch --unset-upstream