---
title: Git 入門(一)
date: 2018-12-21 11:19:50
tags:
  - git
categories:
  - git
---

### 為何要用 Git ?

1. 不需人為比對檔案差異
2. 不須手動備份
3. 不用怕犯錯

---

工作目錄(Working Directory)
`git add` =========> 暫存區 (Staging Area)
`git commit` ======> 儲存庫 (Repository)

---

顯示目前狀態: `git status`

看版本差異: `git diff`

- +`<file>` 工作目錄 v.s 暫存區
- +`--cache` 暫存區 v.s 儲存庫
- +`HEAD` 工作目錄 v.s 儲存庫

---

看過去 commit 的紀錄: `git log` (按 `q`退出指令)
`git log --oneline --graph` :較為精簡易看
`git blame <file name>` : 可以查看該檔案每一行是誰改的，也可看到更改時間

---

切換 branch 或 commit: `git checkout`
**切換到過去某個 commit 點: 可以實現回到過去某個 commit 點在開 branch**
`git checkout -- <file>` : 只看檔案不看 branch

---

PR: `git pull <remote name> <branch name>` 或 `git pull`
Push: `git push <remote name> <branch name>` 或 `git push`
※ origin 為 遠端分支

---

**有用指令**
`git add file -p` : 分段 add

---

Commit: `git commit -m message`
**commit message 非常重要，可以永久留下我們做了什麼的訊息，對於 revert 或 reset 來說較方便**
因為 branch 只是指向某個 Commit 的指標，刪除這個指標並不會造成那些 Commit 消失
若在 code 不能跑或做到一半時，必須 commit 或切換 branch

1. 可以在 message 中加上 temp，之後再修改 commit 訊息: `git commit -amend -m 新訊息` (修改後 commit id 會改變)
   ※amend只能修改最後一次 commit 訊息
   ※注意: 修改 commit 要在 push 前
   ※commit id 用 HA-1（Secure Hash Algorithm 1）演算法所計算的結果，通常用前 7 位
2. 用 `git stash` (看 {%post_link git2%})

---

HEAD: 現在 commit 的位置
HEAD 是一個「指向某一個分支的指標」，你以把 HEAD 當做「目前所在的分支」看待。
`HEAD^`:上次 commit
`HEAD^2`或 `HEAD^^` 或 `HEAD~2`: 上上次 commit (越之前的會越複雜，建議直接用 commit id 比較好，也盡量不要用`~`)

---

### 大忌: rewrite history

如果你已經 push 出去了，請千萬不要做 rewrite history 的動作。
請正確善用 **undo changes**/**rewrite history**的功能，要確保完整整齊的 code，才能 push 出去給別人 pull
