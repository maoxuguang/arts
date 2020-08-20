1. algorithm

2. review

3. tips git cherry-pick 一个分支上的的所有commit

   ```shell
   # Find the range of commits you wish to re-add to your branch.
   # then use cherry-pick to add them back to the branch
   git cherry-pick start..end
   
   # If you wish to include the start commit as well add the ^
   # This will result in a cherry-pick of the start commit included as well 
   git cherry-pick start^..end
   ```

   不过用这个命令一次cherry-pick多个commit, push到review后每个commit 还是分开的。迷惑。

4. share awk 基本用法

   awk由模式（pattern）和动作（action）组成。

   ```shell
   awk '/^$/{print "this is a blank line"}' filename
   ```

   单引号中间是awk命令，//之间是模式，{}之间是动作。

   ```shell
   awk -F"," '{print $3}' filename
   ```

   -F是改变分隔符的。