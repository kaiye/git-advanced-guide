# Git Alias Cheat Sheet

## 1、设置 git log alias

`git log` 是一个十分强大的命令，使用以下命令可以查看每次提交的文件修改列表，和分支变化的图形信息。

```shell
git log --name-status --oneline --graph
```

但作为一个地球人，我们是很难记住这些复杂选项的，查手册也是相当费时，这里就需要用到 `git alias` 的用法。我们可以通过以下语句，配置出一个 `git ls` 的命令，以实现相同的效果。

```shell
git config --global alias.ls 'log --name-status --oneline --graph'

# 运行新命令即可查看效果
git ls
```

## 2、ZSH Git Plugin Alias

如果你使用了 `zsh`（参考《[全新 Mac 安装指南（编程篇）](https://github.com/kaiye/kaiye.github.com/issues/2)》 ），那么开启 [zsh git plugin](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugin:git) 后，你将会直接获得一大群好用的 git alias。

| Alias       | Command                                                                                                    | Remark                                       |
| ----------- | ---------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| `grv`       | `git remote -v`                                                                                            | 查看远程分支列表                             |
| **`gf`**    | `git fetch`                                                                                                |                                              |
| **`gl`**    | `git pull`                                                                                                 |                                              |
| `gup`       | `git pull --rebase`                                                                                        |                                              |
| **`gupa`**  | `git pull --rebase --autostash`                                                                            |                                              |
| `glum`      | `git pull upstream master`                                                                                 |                                              |
| **`grb`**   | `git rebase`                                                                                               |                                              |
| **`gm`**    | `git merge`                                                                                                |                                              |
| `gba`       | `git branch -a`                                                                                            |                                              |
| `gsu`       | `git submodule update`                                                                                     | 更新子仓库                                   |
| **`gst`**   | `git status`                                                                                               |                                              |
| **`gaa`**   | `git add -all`                                                                                             | 将当前版本库所有改动提交至暂存区             |
| **`gp`**    | `git push`                                                                                                 |                                              |
| `ggp`       | `git push origin "${*}"`                                                                                   | 可指定分支或标签名，默认当前分支             |
| `ggsup`     | `git branch --set-upstream-to=origin/$(git_current_branch)`                                                | 当前分支与远程同名分支关联                   |
| **`gcmsg`** | `git commit -m`                                                                                            |                                              |
| **`gco`**   | `git checkout`                                                                                             |                                              |
| **`gcb`**   | `git checkout -b`                                                                                          | 从当前分支新建并转向新分支                   |
| **`glol`**  | `git log --graph --pretty='%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'`   | 格式化版本号、提交时间、作者信息的日志       |
| `gwip`      |  | 将当前新增与改动的文件做一次临时提交         |
| `gunwip`    |                                               | 从上一次 gwip 恢复                           |
| **`grhh`**  | `git reset HEAD --hard`                                                                                    |                                              |
| `gclean`    | `git clean -df`                                                                                            |                                              |
| `gpristine` | `git reset --hard && git clean -dfx`                                                                       | 注意 .gitignore 里的 node_modules 也会被清除 |
| `gsta`      | `git stash save`                                                                                           |                                              |
| `gstl`      | `git stash list`                                                                                           |                                              |
| `gstp`      | `git stash pop`                                                                                            |                                              |
| `gtv`       |                                                                                       |                                              |
| `gdct`      |                                              | 当前最近 tag 版本信息                        |
| `gca!`      | `git commit -v -a --amend`                                                                                 | 将当前修改追加至上一次提交，并修改提交记录   |

**注：本书所有章节中 git 命令行代码中，会在行内注释中标注对应的 zsh alias 用法。**
