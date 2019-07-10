1. algorithm

2. review

3. tips git basic commands

   当你在自己的分支更新了某些东西，此时又需要切换到其他分支去pull更新查看代码，而你又不确定你在自己分支更新的东西最后是否会提交，但是又不能丢弃，因为还需要继续在上面工作。这时候可以通过git stash将

   修改暂存，完成插入的工作后再将更新pop出来。

   ```bash
   git stash
   git checkout master
   git pull
   git stash pop
   ```

   删除远程分支

   ```bash
   git branch --delete --remotes <remote>/<branch>
   git branch -dr <remote>/<branch> # Shorter
   ```

4. share

