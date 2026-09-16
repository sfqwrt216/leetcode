# 列表

列表也是从下标0开始的

## 移除列表

[203. 移除链表元素 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-linked-list-elements/description/)

![image-20260915111521256](Linked list.assets\image-20260915111521256.png)

### 伪代码

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    #Optional的意思是创建的head可以是指定的ListNode类型，也可以是None
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        
        dummyhead = ListNode(0)#定义一个虚拟的头结点
        dummyhead.next = head #指向链表的头节点
        cur = dummyhead#用来遍历链表
        
        while  cur.next != None:
            if cur.next.val == val:
                cur.next = cur.next.next
            else:
                cur = cur.next
        head = dummyhead.next
        return head
```

思路：

创建一个虚拟头指针指向head，因为如果head也是target的话删除的时候一定要知道前一个头指针是什么





##  设计列表





```python
class ListNode:
    def __init__(self, val: int = 0, next: "ListNode" = None):
        self.val = val      # 节点值
        self.next = next    # 指向下一个节点，默认 None


class MyLinkedList:

    def __init__(self): # 初始化列表
        self.size=0
        self.head=ListNode(0,None)
        

    def get(self, index: int) -> int: #获取下标index的值
        if index<0 or index>=self.size:
            return -1
        
        cur =self.head
        for _ in range(0,index+1): #循环到index取出来 +是右边开的边界
            cur=cur.next
        return cur.val


    def addAtHead(self, val: int) -> None: # 把val这个值插入到第一个元素之前作为新头节点

        self.addAtIndex(0, val)
        

    def addAtTail(self, val: int) -> None: # 把val这个值插入到最后一个元素之前作为末尾节点

        self.addAtIndex(self.size, val)

    def addAtIndex(self, index: int, val: int) -> None:#把val插入到下标index之前
        if index>self.size:
            return 
        index = max(0, index) #也有可能是负数
        self.size += 1
        cur=self.head
        for _ in range(0,index): #index 的节点之前那么就正好 右开就是index 指到上一个节点
            cur=cur.next 

        to_add=ListNode(val,cur.next) #这里是创造新加的节点的值以及指向下一个指针
        cur.next=to_add #把index上一个的next指向 to_add
        

    def deleteAtIndex(self, index: int) -> None: #三处下标
        if index < 0 or index >= self.size:
            return
        self.size -= 1
        pred = self.head
        for _ in range(index):
            pred = pred.next
        pred.next = pred.next.next

 


# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```



