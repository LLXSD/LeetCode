## 题目描述
一个整型数组 nums 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。


## 解决思路
题解：先对所有数字进行一次异或，在异或结果中找到任意为 1 的位，这表示这两个只出现一次的数字在这个位取值不同，根据这一位对所有的数字进行分组，相同的数字在这一位取值相同，一定会被分到一个组中，在每个组内进行异或操作，得到两个数字。 

## 代码
```python
from functools import reduce
class Solution:
    def singleNumbers(self, nums: List[int]) -> List[int]:
        x=reduce(lambda x,y:x^y,nums)
        bit=0
        for i in range(31+1):
            if (1<<i) & x:
                bit=i
        ans1,ans2=0,0
        for i in range(len(nums)):
            if (1<<bit) & nums[i]:
                ans1^=nums[i]
            else:
                ans2^=nums[i]
        return [ans1,ans2]


```
