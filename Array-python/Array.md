# 二分查找



### 总结：二分查找俩个必须条件，  1.有序 2.不重复

[704. 二分查找 - 力扣（LeetCode）](https://leetcode.cn/problems/binary-search/)

本地资料："D:\代码随想录PDF全集V3.0\1.《代码随想录》数组（V3.0）.pdf"

![二分查找代码](Array.assets/image-20260908230516870.png)

### 伪代码如下：

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

### 解题心得：

           c++转python，还没学完python，第一次写python，导致很多地方语法不太会 比如c++的（）是python的： 以及缩进代替，并使用 `/` 计算中点，导致下标不是整数还有数组nums才是【】引用

这个while也要对齐

![二分查找代码](Array.assets/image-20260908233445233.png)





# 搜索插入位置



[35. 搜索插入位置 - 力扣（LeetCode）](https://leetcode.cn/problems/search-insert-position/description/)

![image-20260909230631522](Array.assets/image-20260909230631522.png)

### 伪代码如下

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left=0 
        right=len(nums)-1
        while left<=right:
            middle=left+(right-left) // 2
            if nums[middle]>target:
                right=middle-1
            elif nums[middle]<target:
                left=middle+1
            else : return middle
        return left
```

### 解题心得

这次二分法忘记了  while left<=right:这一行代码了，看了一下题解发现了，把这个补充好之后问题就迎刃而解了，一开始没写这一行的时候我还在想  

 return left该怎么返回去呢

# 在排序数组中查找元素的第一个和最后一个位置

[34. 在排序数组中查找元素的第一个和最后一个位置 - 力扣（LeetCode）](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)

![image-20260910095724381](Array.assets/image-20260910095724381.png)

### 伪代码如下

```python
#核心思路：  找到target的左边界 ，在找到target+1的左边界 就简化到了二分查找一个值，只是改一小点东西即可
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        #1.target不存在数组中
        #2.target存在数组中，在数组中间
        
        #寻找第一个大于等于value的函数并且是左边界   继续二分法查找左边界左边界左边界左边界左边界
        def searchFirst(value: int) -> int:
            left=0
            right=len(nums)-1
            while left<=right:
                middle = left + (right - left) // 2
                if nums[left]<value:    #没找到就一直+1
                    left=left+1
                else:#nums[left]>=value  找到了左边界就一直让right缩到left=right最核心的就是这个函数是找左边界的
                    right=right-1
            return left
            
        first=searchFirst(target) #寻找左边界
        if first==len(nums) or nums[first] != target:  #因为left=0，往右边开始缩，所以不要考虑左边界 1.target比数组里的都大，2.target可能在数组中间
            return [-1,-1]
        last=searchFirst(target+1)-1   #找到比target大的左边界，但是要减去1因为不是target，只是比target大一点
        return [first,last]

```



### 解题心得

​       找到target的左边界 ，在找到target+1的左边界-1 就是要的答案了

思路：可以先找到左边界，在二分的基础上直接修改，左边界要保证nums[left]<value 所以找到了之后就不满足nums[left]<value了所以left就停在了左边界    

​        else:#nums[left]>=value找到左边界之后就一直让right减小直到完成while循环的条件     整个核心构造就是searchFirst函数的实现



# X的平方根

[69. x 的平方根 - 力扣（LeetCode）](https://leetcode.cn/problems/sqrtx/description/)

### 伪代码如下

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        l=0
        r=x
        while l<=r:
            middle=l+(r-l)//2
            
            if middle*middle==x:
                return middle
            elif middle*middle<x:  #middle*middle>x之后 l已经不再开始动了 l一直停下来了，但是直接return放不下去
                l=middle+1
            else : #middle*middle>x
                r=middle-1
        return r              #所以为什么这里返回的是r，是因为middle*middle>x之后r一直往左边缩，直到r<l
```



### 解题如下

思路：注意返回值是R  L直到middle*middle<x就再也没动过了，等到r来找L





# 有效的完全平方数

### 伪代码：

```python
class Solution:
        def isPerfectSquare(self, num: int) -> bool:
            left=0
            right=num
            while left<=right:
                mid=left+(right-left)//2
                if mid*mid==num:
                    return  True
                if mid*mid<num:
                    left=mid+1
                elif mid*mid>num:
                    right=mid-1
            return False
        

        
```

### 解题思路

思路：就是和上一道题x的平方根一样去搜索直到完成while的破坏条件  不同的是返回的是True和False而不是其他的数值了

# 移除元素

### 总结：双指针：原地执行

[27. 移除元素 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-element/)

本地资料："D:\代码随想录PDF全集V3.0\1.《代码随想录》数组（V3.0）.pdf"

![image-20260909223437532](Array.assets/image-20260909223437532.png)





### 伪代码如下

```python
#慢指针slow作为新数组nums的指针 
#快指针fast作为寻找值等于val的指针


class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow=0
        fast=0
        while fast<len(nums):
            if nums[fast]!=val:   #找到不等于val的之后 slow+1 也就是找到多少个和val不相等的值
                nums[slow]=nums[fast]   #把不是val的值传递到新数组里
                slow=slow+1
            fast=fast+1
        return slow

```



### 解题心得：

注意他是用如下方案检验你的代码的，k是删除完元素的数组nums的长度 ，并且nums是更新过的，这个函数调用的外部nums，不存在值传递的东西

![image-20260909224200483](Array.assets/image-20260909224200483.png)





# 删除有序数组的重复项

### 伪代码如下

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        slow=1
        fast=1

        while fast<len(nums):
            if nums[fast] !=nums[fast-1] :#如果不相同就直接存下来因为fast是从1开始的所以和fast-1比较，
                nums[slow]=nums[fast]
                slow=slow+1

            fast=fast+1

        return slow  #因为这个后面就是要多少个，所以slow和fast不能从0开始            明天试试从0开始并且num【0】从第一个if开始就判断过了
        
```

```python
#这份代码能通过但是你有没有想过 slow从0开始，万一数组是【1,1,1,1】满足不了条件，你也能通过吗？

class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        slow=0
        fast=0
        while fast<len(nums):
            if fast+1 ==len(nums):
                if nums[fast]!=nums[fast-1]:
                  nums[slow]=nums[fast]
                  slow=slow+1                   
            elif(fast+1<len(nums) and nums[fast]!=nums[fast+1]):
                nums[slow]=nums[fast]
                slow=slow+1
            fast=fast+1

        return slow
```

### 思路：

1.比较的时候向前看，不然最后一个边界不好处理

 if nums[fast] !=nums[fast-1] :#如果不相同就直接存下来因为fast是从1开始的所以和fast-1比较， 为什么是 是从第nums【1】个开始比较并且和前一个比较，就是因为如果fast和fast+1比较的话，到倒数第二个如果fast和fast+1不重复，那么你也存不了fast+1了

# 移动零

[283. 移动零 - 力扣（LeetCode）](https://leetcode.cn/problems/move-zeroes/description/)

### 伪代码

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        slow=0
        fast=0
        temp=0
        while fast<len(nums):
            if nums[fast]!=0:
                temp=nums[slow]
                nums[slow]= nums[fast] # 可以直接让slow数组和fast数组交换，反正slow本来就没有值 fast之后反正要舍弃
                nums[fast] =temp
                slow=slow+1
            fast=fast+1


 # nums[left], nums[right] = nums[right], nums[left]可以用这句代码区执行两个数值置换，并且不用temp完成了少量内存
```



### 思路：      

  nums[left], nums[right] = nums[right], nums[left]可以用这句代码区执行两个数值置换，并且不用temp完成了少量内存









# 比较含退格的字符串

[844. 比较含退格的字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/backspace-string-compare/solutions/451606/bi-jiao-han-tui-ge-de-zi-fu-chuan-by-leetcode-solu/)

### 伪代码：

```python
class Solution:
    def backspaceCompare(self, S: str, T: str) -> bool:
        index_s=len(S)-1
        index_t=len(T)-1
        skips=skipt=0
                                        #有一个还有值就要让他死在这个循环返回false
        while index_s>=0 or index_t>=0 : #走完index等于0之后在函数末尾会执行index-1的操作 ，所以要用or不是and

            #找到要对比的下标 或者都找不到了  
            while index_s>=0:
                if S[index_s] =="#":
                    skips=skips+1
                    index_s=index_s-1
                elif skips>0:
                    skips=skips-1
                    index_s=index_s-1
                else : #index_s这个是找到要对比的值
                    break
            while index_t>=0:
                if T[index_t] =="#":
                    skipt=skipt+1
                    index_t=index_t-1
                elif skipt>0:
                    skipt=skipt-1
                    index_t=index_t-1
                else : #index_t这个是找到要对比的值
                    break

            if index_s >= 0 and index_t >= 0: #如果都没到达边界 就进行对比   1 and 1
                if S[index_s] != T[index_t]:
                    return False
            elif index_s >= 0 or index_t>= 0:   #  其中有一个人小于0 另一个不小于0 那么就返回false
                #这个就是经过查找下一个要对比的值之后一个没有了一个还有    ++ 两种情况01 10   00是0那么就不会执行false++ 
                 # if index_s<0 or index_t<0:  有三种情况 01 10 00  但是00不要执行false是执行true         0指的是判断
                return False
            
            index_s=index_s-1
            index_t=index_t-1



            #要是0 or 0就跳出了最外层while返回了true  return 是while循环跳出之后
        return True
```



### 思路：

1.首先就是要倒序读取，添加一个新变量skip来记录有多少个# 并且要跳多少回

2.两个字符串同时进行一个对比，每一次外层循环去寻找是否要进行对比

3. 两个判断： index_s >= 0 and index_t >= 0:  都有值的话就直接进行对比，index_s >= 0 or index_t>= 0 要是一个又有一个没那么就直接返回False  ，index_s在内层循环可能会改变
4. 可能在第二个判断的时候 已经有两个 index是-1了然后到时候在跳出外层while进行return true



