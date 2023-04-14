## 题目描述
如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，
[2,3,4] 的中位数是 3
[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

void addNum(int num) - 从数据流中添加一个整数到数据结构中。

double findMedian() - 返回目前所有元素的中位数。



## 解决思路
**思路1**

建立一个最大堆，若有奇数个，则pop n/2下取整次，堆顶即为所求；若有偶数个，则pop n/2下取整-1次，记录堆顶，再pop一次，记录堆顶，两次记录值取平均。此思路超时。


```python
class MedianFinder:
    def __init__(self):
        self.max_heap=[]

    def addNum(self, num: int) -> None:
        self.max_heap.append(num)
        i=len(self.max_heap)
        while i>1:
            parent=math.floor(i/2)
            if self.max_heap[parent-1]>=self.max_heap[i-1]:
                break
            else:
                self.max_heap[parent-1],self.max_heap[i-1]=self.max_heap[i-1],self.max_heap[parent-1]
                i=parent

    def findMedian(self) -> float:
        def max_heap(nums:List[int],i):
            #同上
        nums=list(self.max_heap)
        n=len(nums)
        if n%2==1:
            k=math.floor(n/2)
            for i in range(k):
                nums[0],nums[len(nums)-1]=nums[len(nums)-1],nums[0]
                nums.pop()
                max_heap(nums,1)
            return float(nums[0])
        else:
            k=math.floor(n/2)-1
            for i in range(k):
                nums[0],nums[len(nums)-1]=nums[len(nums)-1],nums[0]
                nums.pop()
                max_heap(nums,1)
            num1=nums[0]
            nums[0],nums[len(nums)-1]=nums[len(nums)-1],nums[0]
            nums.pop()
            max_heap(nums,1)
            num2=nums[0]
            return (num1+num2)/2



```


**题解**

建立两个堆，一个最大堆，一个最小堆，最小堆最多比最大堆元素数多一，至少跟最大堆元素数一致。如此，若二者个数相加共有奇数个，则最小堆堆顶元素即为所求；若二者个数相加共有偶数个，则两个堆顶元素取平均即为所求。

```python
def __init__(self): 
        self.max_heap=[] #left
        self.min_heap=[] #right

    def addNum(self, num: int) -> None:
        def max_heap(nums:List[int],i):
            #同上
        def min_heap(nums:List[int],i):
            #同上
        def max_heapfly():
            i=len(self.max_heap)
            while i>1:
                parent=math.floor(i/2)
                if self.max_heap[parent-1]>=self.max_heap[i-1]:
                    break
                else:
                    self.max_heap[parent-1],self.max_heap[i-1]=self.max_heap[i-1],self.max_heap[parent-1]
                    i=parent
        def min_heapfly():
           #同上
        if self.min_heap ==[]:
            self.min_heap.append(num)
        else:
            if num<self.min_heap[0]: #max
                self.max_heap.append(num)  #先根据大小关系加，数目不合法再调整
                max_heapfly()
                if len(self.max_heap)>len(self.min_heap):
                    self.min_heap.append(self.max_heap[0]) 
                    min_heapfly()
                    self.max_heap[0]=self.max_heap[-1]
                    self.max_heap.pop()
                    max_heap(self.max_heap,1)
            else: #min
                self.min_heap.append(num)
                min_heapfly()
                if len(self.min_heap)-len(self.max_heap)>1:
                    self.max_heap.append(self.min_heap[0])
                    max_heapfly()
                    self.min_heap[0]=self.min_heap[-1]
                    self.min_heap.pop()
                    min_heap(self.min_heap,1)
        #print(self.min_heap,self.max_heap)

    def findMedian(self) -> float:
        if len(self.min_heap)==len(self.max_heap):
            return (self.min_heap[0]+self.max_heap[0])/2
        else:
            return self.min_heap[0]

```