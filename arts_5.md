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


2. review

   https://stackoverflow.com/questions/21047524/how-does-swapping-of-members-in-the-python-tuples-a-b-b-a-work-internally

   算法题目的答案和皓哥的专栏里编程范式的文章都提到了下面这个式子：

   ```python
   a, b = b, a
   ```

   想了解原理，看了下爆栈上的解释，python会把赋值等号的右边先存在stack上，然后交换，然后赋值给等号左边。还不是太明白。

3. Tips

   yum的priority值越小优先级越高，比如1的优先级最高，99的优先级最低。

4. share python中的生成器(generator)

   前些天参加同事的培训，他讲了生成器，说生成器的优势是速度快，节省内存空间，今天看了下，计算0到10000000的和，速度好像差不了多少，内存空间倒是节省了。在网上查到的某个文章里说运行下面这段代码会卡死，但我运行起来也超快，秒级:

   ```python
   l = range(100000000)
   
       for i in l:
           pass
   ```



   看了下wiki, 生成器可以让函数作为迭代器工作。

   ```
   Generator functions allow you to declare a function that behaves like an iterator, i.e. it can be used in a for loop.
   ```

   有两个优势，一个是简化的代码，因为迭代器要有iter和next函数，非常繁琐，而生成器可以非常方便的用简洁的代码构建迭代器。

   另一个优势是性能的提升，因为生成器本质上还是迭代器，而迭代器是惰性计算，用到某个值才会去计算，不会像列表要先把所有的值都加载到内存。
