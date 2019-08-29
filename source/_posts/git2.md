---
title: Git 入門(二)
date: 2018-12-22 12:24:32
tags:
  - git
categories:
  - git
---

刪掉 commit: `git revert<commit id>`

移到指定 commit 狀態: `git reset` (用於快速移除 debug 時的一堆 `console.log.()`)

- `-mixed`: 預設模式，只丟掉暫存區的檔案，工作目錄上的檔案不會被動到
- `-soft`: 暫存區和工作目錄下的檔案都不會被動到，僅移動 commit 點而已
- `-hard`全部回到原狀態，不論暫存區還是工作目錄下的檔案都會被丟掉

實際上 `git reset` 指令**並不是真的刪除或是重新設定 Commit**，只是**前往**到指定的 Commit

**git reset v.s. git checkout**
https://stackoverflow.com/questions/3639342/whats-the-difference-between-git-reset-and-git-checkout

---

**git stash**: 可將將現在更改部分存入 stack(另外自己可看的暫存區)，達成不用 commit 就可以切換別的 branch
`git stash list`:查看 stash 內的列表
`git stash apply`:拿出 stash 內的東西，後面加上 `<stash id>`可指定拿出的東西

---

**cherry-pick** :拉別的分支的 commit(可用於要修復不同分支的共同 bug)

    $ git cherry-pick <commit-id>

---

**git rebase**:重整 commit(類似 merge)
**rebase v.s. merge**

1. 比 `git merge`乾淨(將 commit 的線整理整齊)
2. rebase 方式 Git 不會特別做出一個專門用來合併的 Commit(被 rebase 忽略的 commit 並不會被刪除，仍然還會在 log 上，只是已經沒有分支指向他，也就是**失去指標**)

※但要小心使用，rebase 回原先長出來的那個分支，因為 rebase 指令等於是**修改歷史**，不應該隨便對已經 push 出去給別人內容進行 rebase，因為這很容易造成其它人的困擾
「rebase」=「re」+「base(branch 長出的源頭)」，類似「重新定義分支的參考基準」的意思。

使用時機:
通常在**還沒有 Push**出去，但感覺得有點亂或太瑣碎的 Commit，可先使用 Rebase 分支來整理完再推出去。但對於已 push 出去的內容，非必要的話請盡量不要使用 rebase。

---

#### rebase v.s. reset v.s. revert

|        | 改變歷史紀錄 |
| ------ | ------------ |
| rebase | 是           |
| reset  | 是           |
| revert | 否           |

---

`git tag`: 幫 commit 加標籤
通常在開發軟體有完成特定的里程碑，例如軟體版號 1.0.0 或是 beta-release 之類的，這時候就很適合使用標籤做標記。
