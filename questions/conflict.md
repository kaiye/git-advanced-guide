# 遇到冲突了怎么解决？

两个分支进行合并时（通常是 git pull 时），可能会遇到冲突，同时被修改的文件会进入 `Unmerged` 状态，需要解决冲突。

#### 1、最快的办法

大部分时候，「最快解决冲突」的办法是：使用当前 HEAD 的版本（ours），或使用合并进来的分支版本（theirs）。

```text
# 使用当前分支 HEAD 版本，通常是冲突源文件的 <<<<<<< 标记部分，======= 的上方
git checkout --ours <文件名>
​
# 使用合并分支版本，通常是源冲突文件的 >>>>>>> 标记部分
git checkout --theirs <文件名>
​
# 标记为解决状态加入暂存区
git add <文件名>
```

#### 2、最普通的办法

用编辑器打开冲突的源文件进行修改，可能会发生遗留，且体验不好，通常需要借助 git mergetool 命令。

在 Mac 系统下，运行 `git mergetool <文件名>` 可以开启配置的第三方工具进行 merge，默认的是 FileMerge 应用程序，还可以配置成 [Beyond Compare](http://www.scootersoftware.com/support.php?zz=kb_vcs_osx#git) 体验更佳。

#### 3、好的习惯

有三个好的习惯，可以减少代码的冲突：

* 在开始修改代码前先 `git pull` 一下；
* 将业务代码进行划分，尽量不要多个人在同一时间段修改同一文件；
* 通过 [Gitflow 工作流](http://www.ituring.com.cn/article/56870) 也可以提升 git 流程效率，减少发生冲突的可能性。

#### 4、最复杂的情况

如果你的项目周期比较长，还应该养成「定期 rebase 的习惯」，`git pull --rebase` 可以让分支的代码和 origin 仓库的代码保持兼容，同时还不会破坏线上代码的可靠性。

它的大概原理是，先将 origin 仓库的代码按 origin 的时间流在本地分支中提交，再将本地分支的修改记录追加到 origin 分支上。如果发生冲突，则可以即时的发现问题并解决，否则到项目上线时再解决冲突，可能会发生额外的风险。

rebase 大概的操作步骤如下：

```text
# 将当前分支的版本追加到从远程 pull 回来的节点之后
git pull --rebase
​
# 若发生冲突，则按以上其他方法进行解决，解决后继续
git rebase --continue
​
# 直到所有冲突得以解决，待项目最后上线前再执行
git push origin
​
# 若多次提交修改了同一文件，可能需要直接跳过后续提交，按提示操作即可
git rebase --skip
```

需要注意的是，rebase 默认以 [bog-standard flattening](https://stackoverflow.com/questions/11863785/make-git-pull-rebase-preserve-merge-commits/11863842) 模式将提交的时间线进行扁平化处理，如果希望保留两个版本的合并记录，可以使用 `git pull --rebase=preserve` 参数。你也可以将该参数设置为全局配置：

```text
git config --global pull.rebase preserve
```

