# 如何配置 git merge tool？

当文件进入冲突状态时，需要一个好用的 git merge tool 来解决冲突。

当前版本的 vscode 虽然能标注 git conflict 状态，但还未能实现 three-way merge 功能（\#[5770](https://github.com/Microsoft/vscode/issues/5770)），文本以老牌对比工具 Beyond Compare 为例，介绍如何配置 git merge tool。

#### 1、命令行中的配置

首先从 Beyond Compare 菜单中选择 **Install Command Line Tools**，然后运行以下配置命令：

```text
git config --global merge.tool bc3
git config --global mergetool.bc3 trustExitCode true
git config --global mergetool.keepBackup false # 关闭生成 .orig 备份文件
```

设置完成后，即可使用 Beyond Compare Text Merge 功能打开待解决冲突的文件：

```text
git mergetool <文件名>
```

#### 2、Three-way Merge 界面

在 Beyond Compare 的 merge 界面中，「上左」与「上右」面板为合并发生冲突的两次提交版本，「上中」为前次历史版本，「下方」为合并后的代码。

「下方」面板中，「红色！」表示当前行代码发生了冲突，点击「蓝色⇨」或「紫色⇨」，可以分别选择上方需要的代码。合并完成后，保存并关闭窗口，文件会被自动标记为已解决状态，添加至暂存区。

![](http://upload-images.jianshu.io/upload_images/1255999-8547bb372609d92f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3、Source Tree 中的配置

打开 Source Tree，配置外部对比、合并工具为 Beyond Compare。

![](http://upload-images.jianshu.io/upload_images/1255999-90c2d1451c8b9c29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在 SourceTree 中右键选中冲突的文件，使用指定工具解决冲突

![](http://upload-images.jianshu.io/upload_images/1255999-6714daef610ea375.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

