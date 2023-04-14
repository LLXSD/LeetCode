## 题目描述
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

## 解决思路
基于归并排序，考虑并的过程。

用「算贡献」的思想在合并的过程中计算逆序对的数量的时候，只在 lPtr 右移的时候计算，是基于这样的事实：当前 lPtr 指向的数字比 rPtr 小，但是比 R 中 [0 ... rPtr - 1] 的其他数字大，所以这里就贡献了 rPtr 个逆序对。


## 代码
```python
def mergeSort(self, nums, tmp, l, r):
        if l >= r:
            return 0
        mid = (l + r) // 2
        inv_count = self.mergeSort(nums, tmp, l, mid) + self.mergeSort(nums, tmp, mid + 1, r) 
	   #递归调用，计算局部的逆序对的个数，归并时计算更大范围的逆序对的个数
        i, j, pos = l, mid + 1, l #pos是为了排序用的
        while i <= mid and j <= r:
            if nums[i] <= nums[j]:
                tmp[pos] = nums[i]
                i += 1
                inv_count += (j - (mid + 1)) #只有当左侧元素更小时，才会更新inv_count
            else:
                tmp[pos] = nums[j]
                j += 1
            pos += 1
        for k in range(i, mid + 1):  #左侧元素有剩余，即左侧剩余元素大于右侧已排好序的全部元素
            tmp[pos] = nums[k]
            inv_count += (j - (mid + 1))  #此时j=r+1
            pos += 1
        for k in range(j, r + 1):    #右侧元素大于左侧已排好序的全部元素
            tmp[pos] = nums[k]
            pos += 1
        nums[l:r+1] = tmp[l:r+1]
        return inv_count
    def reversePairs(self, nums: List[int]) -> int:
        n = len(nums)
        tmp = [0] * n
        return self.mergeSort(nums, tmp, 0, n - 1)


```