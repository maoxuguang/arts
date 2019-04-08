1. algorithm

   NO.5 Longest Palindromic Substring 用动态规划重写了一遍，代码只有10几行，可读性是之前版本的100倍😂不过用时5000多毫秒，还要再优化

   ```python
   class Solution(object):
       def longestPalindrome(self, s):
           """
           :type s: str
           :rtype: str
           """
           if len(s) == 0:
               return s
           n = len(s)
           max = 0
           result = s[0]
           dp = [[0]*n for _ in range(n)]
           for m in range(n):
               dp[m][m] = 1
               
           for i in range(2,n+1):
               for j in range(0,n):
                   k = i+j-1
                   if k < n:
                       if i == 2:
                           dp[j][k] = 1 if s[j] == s[k] else 0
                       else:
                           dp[j][k] = 1 if dp[j+1][k-1] and s[j] == s[k] else 0
                       if dp[j][k] and k-j+1 > max:
                           max = k-j+1
                           result = s[j:k+1]
           return result
   ```

2. review

   <https://www.cloudbees.com/blog/taming-jenkins-json-api-depth-and-tree>

   这篇文章主要是讲怎么通过depth和tree参数，从jenkins api 返回指定的数据。可以通过tree这个参数指定你想要的element和field. subelement可以嵌套。

   ```
   tree=keyname[field1,field2,subkeyname[subfield1]] 
   ```

   在网上查到的结果好像是还可以指定返回的条目。但没查到怎样指定field的值来查询。后来是用xpath实现的。

   ```python
   jenkins_api_url = jenkins_url+"api/xml?&tree=jobs[builds[*]]&xpath=/hudson/job/build[building='true' and fullDisplayName[contains(text(),'" + job_name + "')]]&wrapper=builds"
   ```

3. tip

   通过jquery的addClass()更新circle class失败。通过下面方法更新成功。可能和我们现在用的jquery版本有关

   ```javascript
   $("#status_circle").attr("class",status);
   ```

4. share

   python 初始化二维数组:

   ```python
   dp = [[0]*n for _ in range(n)]
   ```

   这行代码刚看有点蒙，还google了下，其实稍微分析下就明白了。最外层的是一个列表推导，相当于:

   ```python
   dp = []
   for _ in range(n):
       dp.append([0]*n)
   ```

   在python中字符串，列表，元组与一个整数N相乘，返回一个其所有元素重复N次的同类型对象。

