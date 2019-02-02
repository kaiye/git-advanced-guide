# Git Tag

Git tag 常用于发布版本的标注，可以理解为 tag 是对某一次 commit hash 的别名设置。需要注意的是，git tag 的修改需要显式地指定其名称。

#### 1、查看 tag 列表

```text
# 列出所有本地 tag
git tag
​
# 过滤出 v2. 开头的 tag
git tag -l 'v2.*'
​
# 即 gtv，使用管道输出可不进入 visual 模式
git tag | sort -V 
```

#### 2、新增 tag

Tag 包含两种，一种是轻量 tag，只设置别名，另外一种为附注 tag，能包含这个 tag 的作者和额外的备注信息，更多请查看《[Git 基础 - 打标签](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)》

```text
# 创建一个名为 v0.0.1 的轻量tag
git tag v0.0.1
​
# 创建一个名为 v1.0.0 的附注 tag
git tag -a v1.0.0 -m 'tag description'
​
# 将 tag 推送至远程
git push origin v1.0.0
```

#### 3、删除 tag

```text
# 删除本地 tag
git tag -d v1.0.0
​
# 删除远程 tag
git push origin --delete v1.0.0
```

