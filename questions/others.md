# 其他问题汇总（中文乱码）

#### 1、set-upstream 同步

设置本地分支与远程分支保持同步，在第一次 git push 的时候带上 `-u` 参数即可

```text
git push origin master -u 
```

#### 2、解决文件名中文乱码

git 默认将非 ASCII 编码的目录与文件名以八进制编码展示，使用以下命令可支持中文目录与文件名的显示。

```text
git config --global core.quotepath off
```



