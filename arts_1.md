第一周作业

1. leetcode, NO.1 Two Sum
	```python
	class Solution(object):
		def twoSum(self, nums, target):
			"""
			:type nums: List[int]
			:type target: int
			:rtype: List[int]
			"""
			result = []
			for i, first_value in enumerate(nums):
				for j, next_value in enumerate(nums[i+1:],start=i+1):
					if first_value + next_value == target:
						result.append(i)
						result.append(j)
						return result
	```
	做了第一道题目，准备以后按顺序刷。看了下solution，里面还有用java的hushmap 来做的，因为hashtable的查找效率高，用空间换时间。
2.  review
	 这周看了些django event的文章。
	 事情的起因是这样的，我们想在 django 前端某个地方有更新的时候去触发 jenkins job, 但又不想用 django 后台来做，占用资源，于是想让 jenkins 去轮询，又觉得轮询太笨，想用事件来处理，在我们现在的django系统里没有用事件。
	 看了下django的signals和channels，signals的事件处理好像也只能放在django的后台来做，不能和其他的应用程序交互。channels貌似可以，支持websocket, django 应该可以通过websocket和其他应用程序交互，但这样的话不也要保持一个websocket的长连接在那里么？还看了下gerrit trigger，也是通过ssh 连接到gerrit的某个端口，gerrit会把事件发往这个端口。看来应用之间的交互底层实现要么就是轮询，要么就是长连接了吧？
	又看了用kafka做event sourcing，它的cosumer和事件中心之间的连接也是基于TCP协议，自己实现的一种协议。
	 在连接上纠缠跑偏了很长时间，看一篇文章里说django出现的时候是十几年前，那时候网页大部分都是静态的，mvc也刚刚出现，正热门，ajax也刚出现，用的地方都不过，过了这么多年，和应用的交互越来越频繁，而很多以前完全想象不到的技术也出现了，django这种通过view提交request，又通过response把结果返回给view的方式已经落后了，因为这种同步的方式当request特别多的时候，就会造成反应变慢甚至停滞。是这样的，我们现在的django系统用的人也不多，大概几百人吧，具体数字我也不清楚，但是去调用另一个系统的api更新的时候5秒钟刷新一次都支持不了，要改到30s刷新一次才能工作。
	 但在我们的系统里怎么用事件我还不清楚，因为我们的每个事件要传很多的数据给jenkins，这种event sourcing可以存储这么多的数据吗？
	 写的有点乱，因为我自己都还稀里糊涂。