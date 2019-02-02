# Git Stash 与 gwip

## 1、如何在不提交修改的前提下，执行 pull 或分支切换的操作？

我见过最圡方法是，将修改的文件 copy 到 git 仓库之外的目录临时存放，pull 或分支切换操作完成之后，再 copy 回来。

**拷贝覆盖文件的做法，一是效率不高，二是可能会遗漏潜在的冲突。**

事实上，如果你的 git 版本大于 2.10，那么只需以下一行命令就能自动完成 git stash -&gt; git pull -&gt; git stash pop 的操作。

```text
git pull --rebase --autostash # gupa
```

## 2、git stash

在当前任务未完成前，我们可能需要执行本地与远程分支的同步或本地不同分支的 merge 操作。这时候如果将未完成修改的文件直接 commit，会导致 log 中记录许多无效的 commit 和 merge 记录。

git stash 可以将当前工作状态（WIP，work in progress）临时存放在 stash 列表中，待 pull / merge 操作完成后，再从 stash 中重新应用这些修改。

以下是 git stash 常用命令：

```text
# 查看 stash 列表中已暂存了多少 WIP
git stash list              # gstl
​
# 添加当前 WIP
# -u 参数表明新增的文件也一起 stash
git stash -u save 'message' # gsta -u

# 恢复上一次的 WIP 状态，并从列表中移除
git stash pop               # gstp

# 恢复指定编号的 WIP，同时从列表中移除
git stash pop stash@{num}   # gstp 0
​
# 恢复指定编号的 WIP，但不从列表中移除
git stash apply stash@{num} # gstaa 0
```

**注：如果 git stash 的文件刚好被其他提交修改过了，那么在 pop 时会自动将修改过的文件标记为 conflict 状态。需要注意的是，pop 出来的文件，是 --theirs 而非 --ours。**

## 3、gwip 与 gunwip

Stash 的记录只保存在本地，如果需要在不同电脑间（例如公司和家里）同步临时性的修改，则无法通过 git stash 完成。

Git 社区中有一条约定是，在 commit 中通过 **wip** 关键词表示，这是一次 **work in progress** 的临时提交。借助 zsh git alias，我们可以通过一组 `gwip` 和 `gunwip` 命令来实现同步。

其实现原理是，gwip 提交了特定的 commit message（即，`--wip-- [skip ci]`），gunwip 判断如果上一次提交为 gwip 提交，则自动进行 reset，以下是 alias 的细节。

```text
alias gunwip='git log -n 1 | grep -q -c "\-\-wip\-\-" && git reset HEAD~1'
alias gwip='git add -A; git rm $(git ls-files --deleted) 2> /dev/null; git commit --no-verify -m "--wip-- [skip ci]"'
```

