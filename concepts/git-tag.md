# Git Tag 与 Describe

Git tag 常用于发布版本的标注，可以理解为 tag 是对某一次 commit hash 的别名设置。需要注意的是，git tag 的同步与删除，需要显式地指定其名称。

## 1、查看 tag 列表

```shell
# 列出所有本地 tag
git tag
​
# 过滤出 v2. 开头的 tag
git tag -l 'v2.*'
​
# 使用管道输出 tag 列表，避免进入 visual 模式
git tag | sort -V # gtv
```

## 2、新增 tag

Tag 包含两种，一种是轻量 tag，只设置别名，另外一种为附注 tag，能包含这个 tag 的作者和额外的备注信息。

```shell
# 创建一个名为 v0.0.1 的轻量 tag
git tag v0.0.1
​
# 创建一个名为 v1.0.0 的附注 tag
git tag -a v1.0.0 -m 'tag description'
​
# 将 tag 推送至远程
git push origin v1.0.0 # ggp v1.0.0
```

## 3、删除 tag

```shell
# 删除本地 tag
git tag -d v1.0.0
​
# 删除远程 tag
git push origin -d v1.0.0 # gp origin :v1.0.0
```

## 4、语义化版本与 git describe

清晰的 tag 版本信息，不但有助于发布版本的选择和回滚，同时能十分方便的查看到分支的版本提交进度。

```shell
git describe master --tags
```

假如以上命令输出为：v1.1.0-kaiye-gitbook-2-g51e992f

它表明，本地 master 分支当前 commit hash 为 `51e992f`，距离上一次的 tag 版本 `v1.1.0-kaiye-gitbook` 之间已有 `2` 次提交。

如果需要知道本地与远程最近发布的一次 tag 版本是什么，直接运行 `gdct` 即可。

```shell
alias gdct='git describe --tags `git rev-list --tags --max-count=1`'
```