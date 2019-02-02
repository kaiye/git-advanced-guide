# Git Alias

#### 1、设置 git log alias

`git log` 是一个十分强大的命令，使用以下命令可以查看每次提交的文件修改列表，和分支变化的图形信息。

```text
git log --name-status --oneline --graph
```

但作为一个地球人，我们是很难记住这些复杂选项的，查手册也是相当费时，这里就需要用到 git alias 的用法。我们可以通过以下语句，配置出一个 `git ls` 的命令，以实现相同的效果。

```text
git config --global alias.ls 'log --name-status --oneline --graph'
```

#### 2、Zsh git plugin alias

如果你使用了 `zsh`（参考《[全新 Mac 安装指南（编程篇）](https://github.com/kaiye/kaiye.github.com/issues/2)》 ），那么开启 [zsh git plugin](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugin:git) 后，你将会直接获得一批好用的 git alias：

* `grv` 即 git remote -v
* `gf` 即 git fetch，拉取远程更新
* `gl` 即 git pull，与 fetch 的区别可以理解为，pull = fetch + merge
* `gup` 即 git pull --rebase，通常 rebase 比默认 pull 少一次 merge 记录
* `gupav` 即 git pull --rebase --autostash -v
* `glum` 即 git pull upstream master
* `gsu` 即 git submodule update
* `gst` 即 git status
* `gaa` 即 git add -all，将当前版本库所有改动提交至暂存区
* `gp` 即 git push，本地分支提交至远程仓库
* `gcmsg` 即 git commit -m
* `gco` 即 git checkout
* `glol` 格式化版本号、提交时间、作者信息的 git log
* `gwip` 临时提交版本
* `gunwip` 从当前分支的上一次临时提交版本恢复修改，与 `gwip` 成对使用
* `grhh` 即 git reset HEAD --hard，重置当前所有未提交的修改
* `gclean` 即 git clean -df，清除当前所有不在版本库的文件
* `gpristine` 即 git reset --hard && git clean -dfx，注意 .gitignore 里的 node\_modules 也会被清除
* `gsta` 即 git stash save
* `gstl` 即 git stash list
* `gstp` 即 git stash pop
* `gtv` 即 git tag \| sort -V

