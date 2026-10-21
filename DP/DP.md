

# 动态规划

### 动态规划五部曲

1.**确定dp数组以及下标的含义**     比如爬到第i层楼梯，有dp[i]种⽅法  

2.**确定递推公式**        					如dp[i] = dp[i - 1] + dp[i - 2]  

3.dp数组如何初始化  

4.确定遍历顺序  

5.举例推导dp数组  

### 递归

1.什么时候结束也就是终止条件

2.什么时候return

3.要python在自己的函数里面调用自己，需要加self.





### Debug

找问题的最好⽅式就是把dp数组打印出来，看看究竟是不是按照⾃⼰思路推导的  

### 定义二维数组

```python
        dp = [[0] * n for _ in range(m)] # 定义一个m行 n列的二维数组   但是mn不能交换位置的
```

<img src="./assets/image-20261021103815640.png" alt="image-20261021103815640" style="zoom:150%;" />





## 1.斐波那契数  

https://leetcode.cn/problems/fibonacci-number/

![image-20260922160931702](DP.assets/image-20260922160931702.png)



### 伪代码

```python
						1.递归法      				时间复杂度O(2^n)    空间复杂度： O(n)
class Solution:
    def fib(self, n: int) -> int:
        if n<2:  
            return n
        return self.fib(n-1)+self.fib(n-2)

        
        
        				2.常规代码法：           时间复杂度O(n)    空间复杂度： O(n)
        class Solution:
    def fib(self, N: int) -> int:

        if N <= 1:
            return N
        dp = [0] * (N + 1)    #空间复杂度在这 
        dp[0] = 0
        dp[1] = 1
        
        for i in range(2, N + 1): #时间复杂度在这
            dp[i] = dp[i - 1] + dp[i - 2] 
        return dp[N]
    
    
    					3.节约空间代码法：           时间复杂度O(n)    空间复杂度： O(1)
				
class Solution:
    def fib(self, n: int) -> int:
        if n < 2:
            return n
            
        dp = [0] * 30
        dp[0] = 0
        dp[1] = 1
        for i in range(2, n + 1):
            								# 正确的滚动更新
            dp[0], dp[1] = dp[1], dp[0] + dp[1]
            
        return dp[1] 
```

### 思路：

### 易错点：

1.要python在自己的函数里面调用自己，需要加self.

### 知识点：

这是递归的入门题： 递归有两个要素



### 时间复杂度

![image-20261020103216801](./assets/image-20261020103216801.png)

### 再写一遍犯的错





## 爬楼梯

[70. 爬楼梯 - 力扣（LeetCode）](https://leetcode.cn/problems/climbing-stairs/description/)

![image-20260922161500270](DP.assets/image-20260922161500270.png)





### 伪代码

```python
 									1.递归法（不可用 ）  --时间复杂度O(2^n)    空间复杂度： O(n)
class Solution:
    def climbStairs(self, n: int) -> int:

        if n==1: return 1
        if n==2 : return 2
        return self.climbStairs(n-1)+self.climbStairs(n-2)
            
        
 									2.常规代码法：           时间复杂度O(n)    空间复杂度： O(n)
class Solution:
    def climbStairs(self, n: int) -> int:
        if n<=2:
            return  n  #一定要进行这个初始情况判定
        dp=[0]*(n+1)
        dp[1]=1
        dp[2]=2
        if n<=1:
            return n
        
        for i in range(3,n+1):
            dp[i]=dp[i-1]+dp[i-2]
        return dp[n]
            
            
            						3.节约空间代码（只用dp【1】 和dp 【2】）   时间复杂度O(n)    空间复杂度： O(1)
class Solution:
    def climbStairs(self, n: int) -> int:
        dp=[0,1,2] 
        dp[1]=1
        dp[2]=2
        if n<=1:
            return n
        
        for i in range(3,n+1):
            dp[1],dp[2]=dp[2],dp[1]+dp[2]
        return dp[2]

```

### 思路：

变种的斐波那契数  ， 比如10阶台阶 = 8阶的时候+9阶的时候 的值  ，  你说8阶不可以 8+1+1 和 8 +2 两种呢， 因为8+1的时候再+1中间有9的过程了



### 易错点

1.初始化数组

再用代码法的时候，记得 初始化数组不然不能调用

```python
        dp=[0,1,2]   去初始化一个数组，
    
    # 创建长度为 n+1 的列表，初始值全为 0
        dp = [0] * (n + 1)
```









## 最小花费爬楼梯

[746. 使用最小花费爬楼梯 - 力扣（LeetCode）](https://leetcode.cn/problems/min-cost-climbing-stairs/description/)

![image-20260929201511148](./assets/image-20261020152154719.png)

### 伪代码

```python
											1.递归法 时间复杂度
class Solution:
    def minCostClimbingStairs(self, cost: list[int]) -> int:
        dp=[0]*(len(cost)+1) #楼顶数量是len(cost)+1  也就是cost后面的那个  这里是几个不是下标   要求的是下标是dp【len（cost）】也就是cost数组接触不到的天花板
        dp[0]=0
        dp[1]=0

        for i in range(2,len(cost)+1):  #走到cost+1位置需要的最少的花费
            dp[i]=min(dp[i-1]+cost[i-1],dp[i-2]+cost[i-2])
        return dp[len(cost)]

        
       									2.常规代码法  -使用
class Solution:
    def minCostClimbingStairs(self, cost: list[int]) -> int:
        dp=[0]*(len(cost)+1)#一共len（） 但是下标是从0 到len（cost）+1的
        dp[0]=0
        dp[1]=0

        for i in range(2,len(cost)+1):
            dp[i]=min(dp[i-1]+cost[i-1],dp[i-2]+cost[i-2])
        return dp[len(cost)]
            

									3. 节约时间复杂度法 
class Solution:
    def minCostClimbingStairs(self, cost: list[int]) -> int:

        dp=[0,0,0]

        for i in range(2,len(cost)+1): #要计算的下标是 len（cost） 所以右边界要+1
            dp[2]=min(dp[1]+cost[i-1],dp[0]+cost[i-2])
            dp[0]=dp[1]
            dp[1]=dp[2]

        return dp[1]
            

```



### 思路 

****

### 易错点：

1. 它是指当你站在第i台阶，口袋花了多少钱

![image-20261020161517287](./assets/image-20261020161517287.png)

`dp[i]` 代表的是**“你站在第 i 个台阶上时，你口袋里最少已经花了多少钱”**

![image-20261020162831308](./assets/image-20261020162831308.png)





2.

```python
            dp[0]=dp[1]
            dp[1]=min(dp[1]+cost[i-1],dp[2]+cost[i-2]) ❌️❌️❌️❌️  这样不就自己调用自己了吗
        
        
        
            dp[2]=min(dp[1]+cost[i-1],dp[0]+cost[i-2])  ✅️✅️✅️
            dp[0]=dp[1]
            dp[1]=dp[2]
```







### 知识点：



```python
 

```













## 62不同路径

[62. 不同路径 - 力扣（LeetCode）](https://leetcode.cn/problems/unique-paths/)

![image-20261021095910889](./assets/image-20261021095910889.png)





###  思路

**二维数组法：**

1.先初始化，第一行第一列全为1 

2.从第二行第二列开始遍历 ：  dp[i][j] = dp[i - 1][j] + dp[i][j - 1]

​	

**一维数组法：**

（dp【i】 表示的上一行的结果，）

1.先初始化第一行 全为1 

2.从第二行的第二列开始   dp[j]=dp[j]+dp[j-1]

**易错点**：dp[j-1] 从第二列开始存在 ，那		j-1		的值是多少  ，就是继承的上一行的dp【0】的值吗，没有改变都是1

### 伪代码

```python
										1.递归法（二维数组）  时间复杂度 O(m × n)  空间复杂度O(m × n)
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp=[[0]*n for _ in range(0,m)] #记住如何定义二维数组  m行n列
        
        for i in range(0,n): #列填充 初始化第一行全是 1
            dp[0][i]=1
        for i in range(0,m): #行填充 初始化第一列也全是1
            dp[i][0]=1

        for i in range(1, m):#行  
            for j in range(1, n):#列
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]


        return dp[m - 1][n - 1]
										
        								2.递归法（一维数组法） 时间复杂度： O(m × n)  空间复杂度： O(n)
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp=[1]*n #定义一维数组

        for i in range(1,m):
            for j in range(1,n):
                dp[j]=dp[j]+dp[j-1]
        return dp[-1]

        
        
```





## 不同路径II（没提交）

[63. 不同路径 II - 力扣（LeetCode）](https://leetcode.cn/problems/unique-paths-ii/description/)

![image-20261021103003668](./assets/image-20261021103003668.png)





###  思路

..**常规递归法 时间复杂度O(n × m)， 空间复杂度O(n × m)，**

1.定义二维数组 

2.给第一行和第一列初始化为1 ，碰到障碍后面的全部break

3.从第二列第二行开始遍历  **dp[i][j]=dp[i][j-1]+dp[i-1][j]**



**节约空间复杂度的代码 时间复杂度： O(n × m)，空间复杂度： O(m)**

就是每个dp【j】都是上一行的数值， dp[j-1]是左边的数值

1.定义一个n列的一维数组

2.初始化第一行 dp[i]=1，碰到障碍直接break

3.遍历每行每列，如果碰到障碍。直接dp【j】=0 如果j！=0 （不是第一列）  dp[j]=dp[j]+dp[j-1]



**易错点**：dp[j-1] 从第二列开始存在 ，那		j-1		的值是多少  ，就是继承的上一行的dp【0】的值吗，没有改变都是1

****



### 伪代码

```python
									1.常规递归法 时间复杂度O(n × m)， 空间复杂度O(n × m)，
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: list[list[int]]) -> int:
        m=len(obstacleGrid)
        n=len(obstacleGrid[0])
        dp=[[0]* n for i in range(0,m)]

        #初始化
        for i in range(0,n):
            if obstacleGrid[0][i] ==1:
                break
            else :dp[0][i]=1
		#初始化
        for i in range(0,m):
            if obstacleGrid[i][0] ==1:
                break
            else : dp[i][0]=1
        
        for i in range(1,m):#m行  按照行填充
            for j in range(1,n):#n列
                if obstacleGrid[i][j] == 1:
                    dp[i][j] = 0     # 障碍格不可达
                else : 
                    dp[i][j]=dp[i][j-1]+dp[i-1][j]
        return dp[m-1][n-1]


								2. 节约空间复杂度的代码 时间复杂度： O(n × m)，空间复杂度： O(m)
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: list[list[int]]) -> int:
        m=len(obstacleGrid)
        n=len(obstacleGrid[0])

        #定义一维数组 长度为n列
        dp=[0]*n 

        #初始化第一行
        for i in range(0,n):
            if obstacleGrid[0][i]==1:#有障碍
                break
            else: 
                dp[i]=1

           #开始遍历 
        for i in range(1,m):
            for j in range(0,n):
                if obstacleGrid[i][j]==1:
                    dp[j]=0
                elif j!=0:
                    dp[j]=dp[j]+dp[j-1]
        return dp[-1]
    
    
    
    
    
       							#我改成这样行吗 else :
                    dp[j]=dp[j]+dp[j-1]
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: list[list[int]]) -> int:
        m=len(obstacleGrid)
        n=len(obstacleGrid[0])

        #定义一维数组 长度为n列
        dp=[0]*n 

        #初始化第一行
        for i in range(0,n):
            if obstacleGrid[0][i]==1:#有障碍
                break
            else: 
                dp[i]=1

        for i in range(1,m):
            for j in range(1,n):
                if obstacleGrid[i][j]==1:
                    dp[j]=0
                else :
                    dp[j]=dp[j]+dp[j-1]
        return dp[-1]

```











##整数拆分

[343. 整数拆分 - 力扣（LeetCode）](https://leetcode.cn/problems/integer-break/description/)

![image-20261021161220030](./assets/image-20261021161220030.png)



###  思路

**当前dp【i】 就是 i 的最大整数拆分**

![image-20261021162235638](./assets/image-20261021162235638.png)

### 伪代码

```python
class Solution:
    def integerBreak(self, n: int) -> int:
        dp=[0]*(n+1)
        dp[2]=1

        for i in range(3,n+1):
            for j in range(1,i//2+1):
                # 方案一：只拆成两个数 (j 和 i-j)，不再继续拆分
                option1= j*(i-j)
                #方案二：把 (i-j) 继续拆分，利用之前算好的 dp 表
                option2 = j*dp[i-j]

                dp[i]=max(dp[i],option1,option2)#因为遍历了所有的，dp[i]只取max

        return dp[n]
```











## 96不同的二叉搜索树

[96. 不同的二叉搜索树 - 力扣（LeetCode）](https://leetcode.cn/problems/unique-binary-search-trees/)

![image-20261021163636243](./assets/image-20261021163636243.png)



###  思路

dp[i] ： 1到i为节点组成的⼆叉搜索树的个数为dp[i] 



在这里n为3 以 1为头结点的话 i=3 j=1  左子树0 颗  右子树 2颗 

​					以 2为头结点的话 i=3 j=2  左子树1 颗  右子树 1颗 

​					以 3为头结点的话 i=3 j=3  左子树2颗  右子树 0颗 

**所以可以推导出递归公式**			

​					以 i 为头结点的话			  左子树j-1 颗  右子树 i-j颗   想加为  i- 1           j-1 +  i-j 

![image-20261021163820355](./assets/image-20261021163820355.png)



### 伪代码

```python
class Solution:                  #时间复杂度： O(n^2)   空间复杂度： O(n)
    def numTrees(self, n: int) -> int:
        dp=[0]*(n+1)
        dp[0]=1# 空树也是一棵树
        for i in range(1,n+1):#从1开始到n的      dp【i】的二叉树数量
            for j in range(1,i+1):#从1到 i 种情况的头结点  以j为头节点的二叉树种类
                dp[i]+=dp[j-1]*dp[i-j] #以j为头节点左子树有j-1个元素，右子树有i-j个

        return dp[n]


```









## 二维数组背包

**dp格子含义 `dp[i][j]`**：代表从 `0` 到 `i` 个物品中任取，放进容量为 `j` 的背包里，能获得的最大价值

所以第一列背包能容纳重量为0 就全是0  ，然后 第一行背包从0 到 0 任取物品也是0





**递推公式**：   第一个表示不选物品i （根本就没碰第 i  个物品）  第二个表示选物品 i 然后j减去这个物品的重量 +物品价值

```python
   dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i])
```



**初始化的表格**



![image-20261021194013162](./assets/image-20261021194013162.png)



**最终填满的表格**

![image-20261021202939362](./assets/image-20261021202939362.png)

### 伪代码

```python
							# n为物品的数量  bagweight表示背包的容量

n, bagweight = map(int, input().split())

weight = list(map(int, input().split()))
value = list(map(int, input().split()))

dp = [[0] * (bagweight + 1) for _ in range(n)] #定于二维数组

for j in range(weight[0], bagweight + 1): #第一行初始化  从物品0 容量开始放物品0的价值
    dp[0][j] = value[0]

for i in range(1, n):#从第二行开始 表示物品 
    for j in range(0,bagweight + 1):#从第一列开始 表示容量
        if j < weight[i]:
            dp[i][j] = dp[i - 1][j] #不取
        else:
            dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]) # 不取    取

print(dp[n - 1][bagweight])

```



## 一维数组背包



1.**dp[j]含义：：****dp[j]表示：容量为j的背包，所背的物品价值可以最⼤为dp[j]**          和之前一样直接拷贝上一层的值即可







**2.递推公式：** 

第一个表示不选这个物品，所以直接把上面一层的结果记录下来    可以参考上面的二维图来理解

第二个表示选这个物品 ，所以还是这样

```python
dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
```





**3.一维背包得倒序排序**

![image-20261021202413405](./assets/image-20261021202413405.png)

1.倒序的时候 算dp【2】的时候 **dp【1】初始化为0** 所以 0+15 ==15 



### 初始化表格

![image-20261021211501502](./assets/image-20261021211501502.png)



### 最终数组

![image-20261021211536889](./assets/image-20261021211536889.png)

### 伪代码

```python
n, bagweight = map(int, input().split())
weight = list(map(int, input().split()))
value = list(map(int, input().split()))

dp = [0] * (bagweight + 1)  # 创建一个动态规划数组dp，初始值为0

dp[0] = 0  # 初始化dp[0] = 0,背包容量为0，价值最大为0

for i in range(n):  # 应该先遍历物品 也就是行 
    for j in range(bagweight, weight[i]-1, -1):  # 1.倒序遍历背包容量     2.weight[i]-1  是因为前面的都不需要判断，想放都放不了了
        dp[j] = max(dp[j], dp[j - weight[i]] + value[i]) # 取 ， 不取

print(dp[bagweight])

```

