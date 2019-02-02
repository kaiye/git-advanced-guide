# 分支操作流示例

![&#x6765;&#x6E90; https://yq.aliyun.com/articles/280233](../.gitbook/assets/gitflow.png)

```text
# 查看所有本地与远程分支
git branch -a               # gba
​
# 新建分支 feature/v1，并切换过去
git checkout -b feature/v1  # gcb feature/v1
​
# 在本地 feature/v1 分支上，拉取远程 master 分支合并进来
git pull origin master      # ggl master
​
# 开发过程中将 feature/v1 分支推至 origin 同名分支
git push origin feature/v1  # ggp
​
# feature/v1 开发完成后，切换回 master 分支，将其修改合并进来
git checkout master         # gco master
git merge feature/v1        # gm feature/v1
​
# 在 master 分支上，删除已完成合并的分支 feature/v1
git branch -d feature/v1    # gbd feature/v1
​
# 删除远程 feature/v1 分支
git push origin --delete feature/v1 # gp -d origin feature/v1
```

