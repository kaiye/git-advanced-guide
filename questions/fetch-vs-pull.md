# fetch pull merge rebase 的关系

## 1、我应该用 git pull 还是 git fetch？

`pull` 与 `fetch` 的关系是：

```text
git pull = git fetch + merge
git pull --rebase = git fetch + rebase
```

## 2、merge 和 rebase 有什么区别？

如果有疑问，推荐去玩一下本书前言提到的 [Learn Git Branching](https://learngitbranching.js.org) 游戏。

主要的差异是：

* rebase 改变了时间线，而 merge 没有；
* rebase 扁平化时间线后，历史记录变得更加简单和直观。

**二者的选择只是个人倾向性问题，底线建议是，不要改变 origin 仓库的时间线，避免找不到背锅侠。**



