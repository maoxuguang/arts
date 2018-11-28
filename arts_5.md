1. leetcode No.4 Median of Two Sorted Arrays

   ```python
   class Solution(object):
       def findMedianSortedArrays(self, nums1, nums2):
           """
           :type nums1: List[int]
           :type nums2: List[int]
           :rtype: float
           """
           m = len(nums1)
           n = len(nums2)
           if (m > n):
               tmp = nums1
               nums1 = nums2
               nums2 = tmp
               tmp = m
               m = n
               n = tmp
           imin = 0
           imax = m
           halfLen = (m+n+1)/2
           while(imin <= imax):
               i = (imin+imax)/2
               j = halfLen -i
               if i < imax and nums1[i]<nums2[j-1]:
                   imin = i + 1
               elif i > imin and nums1[i-1] > nums2[j]:
                   imax = i-1
               else:
                   if i == 0:
                       maxLeft = nums2[j-1]
                   elif j == 0:
                       maxLeft = nums1[i-1]
                   else:
                       maxLeft = max(nums1[i-1],nums2[j-1])
                   if (m+n)%2 == 1:
                       return maxLeft
                   
                   if i == m:
                       minRight = nums2[j]
                   elif j == n:
                       minRight = nums1[i]
                   else:
                       minRight = min(nums1[i],nums2[j])
                   
                   return (maxLeft+minRight)/2.0
   ```


2. Tips

   yum的priority值越小优先级越高，比如1的优先级最高，99的优先级最低。