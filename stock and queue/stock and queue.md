# 栈和队列

**1.判断栈是否为空使用  if not self.stock_in   而不是直接  if  self.stock_in==0 ，因为队列和栈都们本质上是一个容器（集合），而不是数字**

由于栈结构的特殊性，⾮常适合做对称匹配类的题⽬  

2. 定义栈和队列：

   ```python
   #栈的定义;
   	stock_in =[] 
       
       return self.stock_out[-1] #从右边开始输出
       
   #队列的定义：
       queue = deque() 
       return self.queue[0]    #从左边开始输出
   
   
   队列的常见函数
   #deque() 是 Python 中的“双端队列”
   #它支持在队列的两端快速添加和删除元素
   #1.创建deque队列
   queue = deque()
   #2.从右端添加元素 
   queue.append(1)
   queue.append(2)
   print(queue)#deque([1,2])
   #3.从左端添加元素
   queue.appendleft(0)
   print(queue)#deque([0,1,2])
   #4.从右端删除元素
   queue.pop()#删除并返回右边元素2
   #5.从左端删除元素
   queue.popleft()#删除并返回左边元素0
   #6. 直接获取队列的首值
   return self.queue[0]            
   
   ```

   



## 用栈实现队列

[232. 用栈实现队列 - 力扣（LeetCode）](https://leetcode.cn/problems/implement-queue-using-stacks/solutions/632369/yong-zhan-shi-xian-dui-lie-by-leetcode-s-xnb6/)



![image-20260928162830390](stock and queue.assets/image-20260928162830390.png)

### 伪代码

```python
class MyQueue:

    def __init__(self):
        self.stock_in =[]  #定义队列中进来的元素储存
        self.stock_out=[]  # 定义队列中出去的元素储存
        

    def push(self, x: int) -> None:
        self.stock_in.append(x)
        

    def pop(self) -> int: 
        if not self.stock_out : ##
            while self.stock_in:
                self.stock_out.append(self.stock_in.pop())
        return self.stock_out.pop()        


    def peek(self) -> int:
        # 复用 pop 的倒腾逻辑，但不要真正弹出 
        if not self.stock_out:
            while self.stock_in:
                self.stock_out.append(self.stock_in.pop())
        
        # 直接返回输出栈的最后一个元素（即栈顶），不调用 pop()
        return self.stock_out[-1]
        

    def empty(self) -> bool:
                # 只有当两个栈都为空时，整个队列才算空
        return  not self.stock_in  and not self.stock_out  # not  ==0


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```





### 思路 

用两个栈一个存储一个用来翻转

push实现： 直接append到stock_in当中

pop实现：把stock_in全部pop到stock_out当中

peek实现：和popo同理，不同在于        return self.stock_out[-1]

empty实现：直接判断即可

### 易错点：

**判断栈是否为空使用  if not self.stock_in   而不是直接  if  self.stock_in==0 ，因为队列和栈都们本质上是一个容器（集合），而不是数字**

### 知识点



### 重写一遍之后还会犯的错

























## 用队列来实现栈

[225. 用队列实现栈 - 力扣（LeetCode）](https://leetcode.cn/problems/implement-stack-using-queues/description/)

![image-20260928174933822](stock and queue.assets/image-20260928174933822.png)

### 伪代码

```python


class MyStack:

    def __init__(self):
        self.queue = deque()
        

    def push(self, x: int) -> None:
        n=len(self.queue)
        self.queue.append(x)
        for _ in range(0,n):#从左边推出来，然后再加进去就实现了先入后出，要出的话就是出的最后加进来的那个
            self.queue.append(self.queue.popleft())
        

    def pop(self) -> int:    
        return self.queue.popleft()       
   

    def top(self) -> int: #返回栈顶元素，但是不要改变栈的顺序
        return self.queue[0]            

    def empty(self) -> bool:
        return not self.queue       


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```



### 思路 

**用一个队列来实现栈，就是先把元素放进去，再循环把前面的一个一个从队伍尾部加进去**

### 易错点：

### 知识点：

```python
#deque() 是 Python 中的“双端队列”
#它支持在队列的两端快速添加和删除元素
#1.创建deque队列
queue = deque()
#2.从右端添加元素
queue.append(1)
queue.append(2)
print(queue)#deque([1,2])
#3.从左端添加元素
queue.appendleft(0)
print(queue)#deque([0,1,2])
#4.从右端删除元素
queue.pop()#删除并返回右边元素2
#5.从左端删除元素
queue.popleft()#删除并返回左边元素0
#6. 直接获取队列的首值
return self.queue[0]            

```



### 重写一遍之后还会犯的错





















## 有效的括号

[20. 有效的括号 - 力扣（LeetCode）](https://leetcode.cn/problems/valid-parentheses/description/)

![image-20260928191828720](assets/image-20260928191828720.png)



### 伪代码

```python
#第一种写法  右括号当键
from collections import deque
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2 == 1: #能直接结束，实现时间降低
            return False
        
        stack=[]  # 创建一个空栈
        mapping ={")":"(","]":"[","}":"{"}          #创建一个映射字典，左边是键右边是值

        for ch in s:
            if ch in mapping: #右括号就直接开始判断

                if not stack or stack[-1] !=mapping[ch]: #用[] 而不是（）
                    return False
                stack.pop()

            else: #左括号就存入栈当中
                stack.append(ch)
                
        return not stack #还有（（的情况
    
    
#第二种写法   左括号当键
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2 == 1:
            return False

        stack = []
        mapping = {"(": ")", "[": "]", "{": "}"}

        for ch in s:
            if ch in mapping:
                stack.append(mapping[ch]) #左括号存入开始对比
            else:
                if not stack or stack.pop()!=ch:
                    return False
        return not stack
```



### 思路 

定义一个pair也就是字典类型，先把左边的括号存入栈（先进后出）当中，然后存完之后利用字典的特性， 从右括号开始（中间开始配对），判断栈顶是不是和右括号是一对键值

![image-20260928202154487](assets/image-20260928202154487.png)

****

### 易错点：

1.为什么不能从两边开始配对，要从中间开始： s = "()[]{}" 这种情况就不满足呀

3.能否用队列去实现



代码上：

```python
            if ch in pairs: #这里是判断的键而不是值
```

### 知识点：

```python
     由于栈结构的特殊性，⾮常适合做对称匹配类的题⽬
    
    pairs = {
            ")": "(",
            "]": "[",
            "}": "{",
        }

# 这样算是定义了字典 左边是键右边是值  						11111




if ch in pairs: #这里是判断的键而不是值
    
    
    
    写代码三部曲：
    1.看看能不能有些情况不用去执行，直接判断即可
    2.每次做完一定要对原始数据进行处理  stack.pop（）
```



### 重写一遍之后还会犯的错



















## 删除字符串中的所有相邻重复项

[1047. 删除字符串中的所有相邻重复项 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)



![image-20260928205336646](assets/image-20260928205336646.png)





### 伪代码

```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        stack=[]

        for ch in s :
            if stack and ch == stack[-1]:
                stack.pop()
            else:
                stack.append(ch)
        return "".join(stack)
```



### 思路 

对于相邻元素，你append之前就判断是否和stack【-1】是否一样即可

****

### 易错点：

​      if stack and ch == stack[-1]:   一定要注意是否为空，为空就完蛋了，力扣还是很多判断极限的地方

### 知识点：

```python
"-".join(["c", "a"])      # "c-a"
", ".join(["a", "b", "c"]) # "a, b, c"
"".join(["a", "b", "c"])   # "abc"
" ".join(["hello", "world"]) # "hello world"

```



### 重写一遍之后还会犯的错





## 逆波兰表达式求值

[150. 逆波兰表达式求值 - 力扣（LeetCode）](https://leetcode.cn/problems/evaluate-reverse-polish-notation/description/)



### 伪代码

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        
        mapping={ "+": add,"-":  sub , "*":mul, "/":lambda x, y: int(x / y)}
        stack=[]
        for ch in tokens:
            if ch in {"+","-","*","/"} :
                num1=stack.pop()
                num2=stack.pop()
                num3=mapping[ch](num2,num1)
                stack.append(num3)
            else :
                stack.append(int(ch))   #tokens中的都是字符串不是数字所以要转一下
        return stack.pop()      


```



### 思路 

用mapping定义，这样就实现了两个数之前的操作可以冬动态“”+”或者“”-”然后pop两次实现求值

****

### 易错点：

1.左右操作数别写反

2.tokens中的都是字符串，而不是数组所以要转一下  int(ch)

### 知识点：

```python

#11.python函数中的add和sub和mul用法：
add(a,b)
sub(a,b)s
mul(a,b)


#2.lambda
lambda：定义一个短小的函数懒得再去定义函数了

```

![image-20260928214648669](assets/image-20260928214648669.png)

### 重写一遍之后还会犯的错









### 伪代码

```python

```



### 思路 

****

### 易错点：

### 知识点：

```python
 

```



### 重写一遍之后还会犯的错