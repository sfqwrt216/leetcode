[704. 二分查找 - 力扣（LeetCode）](https://leetcode.cn/problems/binary-search/)

本地资料："D:\代码随想录PDF全集V3.0\1.《代码随想录》数组（V3.0）.pdf"

![二分查找代码](Array.assets/image-20260908230516870.png)

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left=0
        right=len(nums)-1
        while left<=right:
          middle =left+(right-left) // 2
          if nums[middle] > target:
            right=middle-1
          elif nums[middle] <target:
            left=middle+1
          else: return middle
        return -1
```

解题心得：

           c++转python，还没学完python，第一次写python，导致很多地方语法不太会 比如c++的（）是python的： 以及缩进代替，并使用 `/` 计算中点，导致下标不是整数

 还有数组nums是【】引用

![二分查找代码](Array.assets/image-20260908233445233.png)

这个while也要对齐1
