1. leetcode no. 5 Longest palindromic substring

   还没做出来...下面这个做法有两个case跑不过...

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
               for j in range(len(s)-1,-1,-1):
                   if s[j] == s[i]:
                       m = i+1
                       n = j-1
                       while m < n:
                           if s[m] == s[n]:
                               m = m+1
                               n = n-1
                           else:
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
                       continue
           return max_str
                   
               
                   
                   
   ```
