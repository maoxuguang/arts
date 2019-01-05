1. leetcode no. 5 Longest palindromic substring

   1500ms, 我尽力了...

   ```python
   class Solution(object):
       def longestPalindrome(self, s):
           """
           :type s: str
           :rtype: str
           """
           max_str = ""
           max = 0
           for i in range(len(s)):
               j = len(s)-1
               while j >= i:
                   if s[j] == s[i]:
                       if j-i+1 <= max:
                           break
                       m = i+1
                       n = j-1
                       while m < n:
                           if s[m] == s[n]:
                               m = m+1
                               n = n-1
                           else:
                               if s[m] not in s[:m] and s[m] not in s[m+1:]:
                                   if m-1 >= 0 and m+1 < len(s) and s[m-1] != s[m+1]:
                                       j = m-1
                                       break
                               if s[n] not in s[:n] and s[n] not in s[n+1]:
                                   if n-1 >=0 and n+1 < len(s) and s[n-1] != s[n+1]:
                                       j = n-1
                                       break
                               j = j-1
                               break
                       if m>=n:
                           l = j-i+1
                           if l >= max:
                               max = l
                               max_str = s[i:j+1]
                               next = len(s)-i-1
                               if max >= next:
                                   return max_str
                               break
                           else:
                               j = j-1
                   else:
                       j = j-1
           return max_str
                   
   ```

2. review

   https://stackoverflow.com/questions/32557920/what-are-type-hints-in-python-3-5

   这是上次被报了个bug, 调用对象的方法时对象为空，群里有同学建议用typing.optional，注释类型，这是查到的资料。里面说了三种方式来辅助做静态检查:

   special comments

   function anotation

   stub file

   但是我还是不是太清楚怎么发现我的这种错误，要动手试一下

3. tips

   git checkout specific file or folder

   ```
   git checkout -- path/to/file
   ```

   主要是这个 -- 的意思，是为了区分branch和file name相同的情况，比如你要更新某个文件A，但你有个branch名字也是A，那加了 -- 后就会更新A这个文件，而不是checkout到A这个分支。

