# 如何撤销修改？

修改包含四种情况，需单独区分。

## 1、新建的文件和目录，且从未提交至版本库

此类文件的状态为 `Untracked files` ，撤销方法如下：

```shell
git clean -fd . # gclean .
```

其中，`.` 表示当前目录及所有子目录中的文件，也可以直接指定对应的文件路径，以下其他情况类似。

## 2、提交过版本库，但未提交至暂存区的文件（未执行 git add）

此类文件的状态为 `Changes not staged for commit`，撤销方法：

```shell
git checkout . # gco .
```

## 3、已提交至暂存区的文件

此类文件的状态为 `Changes to be committed`，撤销方法：

```shell
git reset . # grh .
```

执行之后文件将会回到以上的 1 或者 2 状态，可继续按以上步骤执行撤销，若 git reset 同时加上 `--hard` 参数（alias 为 `grhh`），将会把修改过的文件也还原成版本库中的版本。

## 4、已提交至版本库（执行了 git commit）

每次提交都会生成一个 commit hash，通过以下命令可查阅 hash id 并将其回滚：

```shell
git log # glol
git reset <commit_hash> # grh 
```

如果需要「回滚至上一次提交」，可直接使用以下命令：

```shell
git reset head~1 # grh head~1
```

执行之后，再按照 1 或者 2 状态进行处理即可，如果回滚之后的代码同时需要提交至 origin 仓库（即回滚 origin 线上仓库的代码），需要使用 `-f` 强制提交参数，且当前用户需要具备「强制提交的权限」。

## 5、如果回滚了之后又不想回滚了怎么办？

如果是以上的情况 1 或者 2，只能歇屁了，因为修改没入过版本库，无法回滚。

如果是情况 4，回滚之后通过 git log 将看不到回滚之前的 commit hash，但可通过 `git reflog` 命令（所有记录过的 commit hash）找到回滚之前的 commit hash，然后 `git reset <commit_hash>` 。

## 6、git reset 与 revert 的区别

二者都是做回滚操作，不同之处在于：`reset` 直接将 head 指向了回滚的记录，丢弃了这条记录之后所有的提交时间线，而 `revert` 不会改变已有的时间线，通过新增提交记录将项目还原到之前的某次提交时的状态。
