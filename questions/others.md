# 其他问题汇总

## 1、解决文件名中文乱码

git 默认将非 ASCII 编码的目录与文件名以八进制编码展示，使用以下命令可支持中文目录与文件名的显示。

```text
git config --global core.quotepath off
```

## 2、set-upstream 同步

设置本地分支与远程分支保持同步，在第一次 git push 的时候带上 `-u` 参数即可，或使用 `ggsup` alias 进行关联。

```text
git push origin master -u # gp -u
```

## 3、怎样修改 commit message？

如果你需要批量修改历史时间线中的记录，最好的办法是使用 `git rebase -i`，这里有份详细的指南《[Git-工具-重写历史](https://git-scm.com/book/zh/v2/Git-工具-重写历史)》。

如果只想修改上一次的提交的日志信息，使其符合团队规范（如社区广泛使用的 [AngularJS Git Commit Message Conventions](https://gist.github.com/stephenparish/9941e89d80e2bc58a153) 或 [gitmoji](https://github.com/carloscuesta/gitmoji/)），可使用

```text
git commit --amend # gc!
```

## 4、merge 和 rebase 有什么区别？

如果有疑问，推荐去玩一下本书前言提到的 [Learn Git Branching](https://learngitbranching.js.org) 游戏。

**主要的区别是 rebase 改变了时间线，而 merge 没有；rebase 扁平化时间线后，历史记录变得更加简单和直观。**

二者的选择只是个人倾向性问题，底线建议是，不要改变 origin 仓库的时间线，避免找不到背锅侠。

## 5、我应该用 git pull 还是 git fetch？

`pull` 与 `fetch` 的关系是：

```text
git pull = git fetch + merge
git pull --rebase = git fetch + rebase
```

## 6、操作符 ^ 和 ~ 什么区别？

二者都是向上回溯提交记录的位置选择符，默认值为 1。`^` 用于分支路径选择，`~` 用于提交记录选择。例如 `git checkout v1^~^` 等同于：

```text
git checkout v1 # gco v1
git checkout head~3 # gco head~3
```

一般来说，记住 `head~N` 之类的用法即可，它表示当前 head 指针往回移 N 位。

## 7、git push origin :master 是个什么鬼操作？

喔，要小心了，这个操作有点类似 `rm -rf /` ，用于删除远程 master 分支。原因是 push 命令中的 `:` 参数分隔符前面可以选任意分支，如果留空，则表示删除的意思。

```text
# 表示将本地 dev 分支的前一个版本推至远程 master
git push origin dev^:master
```

所以一个好的习惯是，在 git 后台设置 protect 好 master，并且在 push 时，不要使用强制参数 `-f`。

## 8、如何快速生成 .gitignore 文件？

```text
# 安装 gi 命令，来自 https://github.com/joeblau/gitignore.io
echo "function gi() { curl -L -s https://www.gitignore.io/api/\$@ ;}" >> ~/.zshrc && source ~/.zshrc

# 往项目中追加 node ignore file
gi node >> .gitignore
```

