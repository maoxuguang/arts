arts 第三周

1. leetcode 3. longest substring without repeating characters

   ```python
   class Solution(object):
       def lengthOfLongestSubstring(self, s):
           """
           :type s: str
           :rtype: int
           """
           if len(s)==1:
               return 1
           result_list = []
           for i in range(len(s)):
               for j,item in enumerate(s[i+1:],start=i+1):
                   if item in s[i:j]:
                       result_list.append(j-i)
                       break
                   else:
                       if j+1 == len(s):
                           result_list.append(j-i+1)
           return max(result_list) if result_list else 0
   ```

   唉，每次都想着先用暴力破解再优化，结果就是陷在暴力破解的思路里不可自拔...

2. review 

   https://smartbear.com/blog/test-and-monitor/api-performance-problems/

   想查点API监控的资料，这个只是讲了API监控的重要性，API把各个互相依赖的应用连接起来，没讲怎么做，讲怎么做的文章还要填个人和公司信息才能看，讨厌

3. tips python中的三元运算符

   ```python
   if result_list:
       return max(result_list)
   else:
       return 0
   ```

   ```python
   return max(result_list) if result_list else 0
   ```

4. share

   这周的clean code活动，改进一个函数update_feature，这个函数有180行左右，里面不仅其实不仅有update的功能，还有create feature的功能，所以有些地方代码有冗余，比如create的时候已经生成了实例，还要为update把各个属性再赋值一遍，在create的时候不会删除模块，但在update的时候会，这样生成和更新的功能放在一块，看起来会有些奇怪，不那么易读。

   我试图把生成和更新的功能分开，但也不是那么好分，比如在create的时候只添加模块，不删除模块，我想把添加模块的功能抽出来放在一个函数，给生成和更新调用，但如果添加失败，生成和更新的异常处理是不一样的。

   生成的时候，如果模块添加失败，只需要把已经生成的模块的分之给删掉就好了，如果是更新的时候添加模块失败，还需要把删除的模块再添加回feature.

   感觉就是打断了骨头连着筋，很难拆分啊。

   感觉每次的share都写的是我碰到的问题，我根本就解决不了，我要好好读耗哥的专栏了....

   记得不是很准确了，明天回公司了再看下。