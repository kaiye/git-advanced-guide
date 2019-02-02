# origin 与 upstream

Git 是一个去中心化的版本管理工具，这意味着一个 Git 仓库，既可以没有远程仓库，也可以有多个远程仓库，其中默认的远程仓库我们称之为 `origin`。

在 Github 上，我们可以 fork 任意开源项目到个人 ID 下，当我们把个人 ID 下的仓库 clone 到本地时，除了默认的 origin 仓库外，我们还需要配置一个 upstream 仓库，指向原始的开源项目地址，保证可以定期同步源仓库的更新。

注：upstream 只是一个命名约定，你可以换成任意的命名。

## 1、查看远程仓库列表

```text
# 查看远程仓库列表
git remote -v           # grv

# 查看具体仓库细节
git remote show origin  # gr show origin
```

## 2、添加 upstream 仓库信息

```text
git remote add upstream <git_repository_url> # gra upstream
```

## 3、删除 upstream 仓库信息

```text
git remote remove upstream # grrm upstream
```

