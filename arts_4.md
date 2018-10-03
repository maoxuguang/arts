1. leetcode No.3 Longest substring without repeating characters

   ```python
   class Solution(object):
       def lengthOfLongestSubstring(self, s):
           """
           :type s: str
           :rtype: int
           """
           unique = []
           max_length = 0
           length =  len(s)
           i=0
           j=0
           while (i<length and j<length):
               if s[j] in unique:
                   unique.remove(s[i])
                   i=i+1
               else:
                   unique.append(s[j])
                   j=j+1
                   max_length = max_length if max_length > len(unique) else len(unique)
           return max_length
   ```

   仍然是第三道题目，换了种解法，用时92ms，比之前的暴力破解法性能提高很多。是看了solution之后做的，希望后面能越做越好。

   2. review

      <http://rgalen.com/agile-training-news/2016/4/24/backlog-refinement-are-you-doing-it-right>

      读这篇文章是因为和同事关于grooming 颗粒度的争论，这篇文章主张每个item grooming的时间不超过5分钟，然后grooming 也可以迭代，不要要求在一次grooming里把一个item分析彻底，而是争取每次迭代大家都对这个item有个进一步的认识。多次迭代也给了大家熟悉和思考这个item的时间。

      主张grooming的速度优先于thoughtfulness.

      我觉得这个想法太理想化了，这样会增加很多开会的次数，会让team干活的时间碎片化，而且还要求team开会的效率比较高，大家在每一次会议上参与度都很高才会有效果，不然大家只会抱怨会变多了。

   3. tips 

   4. share

      关于grooming的颗粒度的争论

      同事认为我们grooming的时候讨论的太细，会影响设计。颗粒度细的好处是会把需求澄清的非常清楚，风险依赖也会提前分析出来，而且每个人都对这个item比较了解，会比较可控。

      颗粒度大可以提高设计的灵活和成员的能动性，但有可能导致risk, dependency 被漏掉。增加了项目的风险。

