# Cherry Pick 的使用场景

当你需要将某些特定的 commit，合并进当前分支时，可以使用该命令。

**cherry-pick 时，极其容易发生冲突。一般来说，如果项目中使用了规范的 git 分支操作流，那么基本上不会用到 cherry-pick。**

但如果出现了以下三种情况，则可能会使用到。

* 需求发布窗口发生变更，某个特性需要从版本中单独拎出来，放入另外的迭代中；
* 同一分支中某些特性改错了，但提交更新次数过多，需要选中某些历史提交，再次合并至 head；
* 项目最开始的基准分支切错了，后续需要重新切基准分支，并将错误分支上的提交记录移植到正确分支上。

```shell
# cherry-pick 指定 commit，可同时传入多个 commit
git cherry-pick <commit_hash>   # gcp
​
# 放弃 cherry-pick
git cherry-pick --abort         # gcpa
​
# cherry-pick 多个 commit 时，解决冲突后继续下次合并
git cherry-pick --continue      # gcpc
```
