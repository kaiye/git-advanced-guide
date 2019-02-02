# 如何为不同项目配置不同的提交用户？

#### 1、git config user

假如你在 Github 上有个人项目，而公司项目存放在公司内网 gitlab 上，如何为这两种不同类型的项目配置不一样的提交用户呢？

Git 全局的用户配置文件存放在 `~/.gitconfig` 中，我们可以通过以下命令设置全局默认的用户名和邮箱。

```text
git config --global user.name "<Your Name>"
git config --global user.email "<Your Email>"
```

如果需要为某一个项目配置不同的用户，则可以进入到项目对应的目录下，使用以下命令。它会在项目根目录的 `.git/config` 文件中保存这些配置信息：

```text
git config user.name "<Another Name>"
git config user.email "<Another Email>"
```

#### 2、Conditional Includes

在 git 2.13 版本中，增加了 [conditional includes](https://git-scm.com/docs/git-config#_includes) 配置，可以创建多个 gitconfig 文件，并针对不同的根目录使用不同的配置文件。例如，以下全局配置文件 `~/.gitconfig` 中包含以下用户配置信息，当项目 clone 在 `~/dev/` 目录下时，会自动使用另外一份配置文件：

```text
[user]
    name = Your Name
    email = your_email@example.com
[includeIf "gitdir:~/dev/"]
    path = .gitconfig-dev
```

以下是 `~/.gitconfig-dev` 文件的配置：

```text
[user]
    name = Another Name
    email = another_email@example.com
```

**注意：强烈建议将 global user 配置为你的 Github ID，避免默认提交中有效用户信息的缺失，导致 Github contributions 不准确。同时，不设置为公司邮箱，可以避免邮箱信息泄露。**  


