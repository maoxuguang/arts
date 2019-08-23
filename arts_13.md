1. algorithm

2. review

   <https://stackoverflow.com/questions/11214908/closing-files-in-openpyxl/11215839>

   这是查openpyxl什么时候保存退出的时候查到的:

   ```
   Fundamentally we read an excel workbook into memory from a file which is closed afterwards, make updates, if we don't save it, the changes presumably are lost, if we save it, the file is closed after writing.
   ```

   这个答案还提供了一个很好的解决问题的思路，就是看源码。

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

4. share x-step 8i 配置

   ```
   1. cpri目录中除了set up文件还有很多其他文件stimulus的时候用到，拷贝整个目录
   2. 代码中通过系统提示符判断x-step cli是否执行成功，这个8i的系统提示符和代码中的不一样，通过命令修改
   3. program device用到了bin文件，拷贝bin目录和lib目录
   ```


