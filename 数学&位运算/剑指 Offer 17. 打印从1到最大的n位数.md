## 题目描述
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。


## 解决思路
n位十进制数，从1开始，一共有10^n-1种可能，直接return即可。考虑大数越界问题，本题即为0~9的n位全排列问题，可采取的思路是：

1. 为了避免数字开头出现0，先把首位first固定，first取值范围为1～9。
2. 用digit表示要生成的数字的位数，本题要从1位数一直生成到n位数，对每种数字的位数都生成一下首位，所以有个双重for循环。
3. 生成首位之后进入递归生成剩下的digit-1位数，从0-9中取值。
4. 递归的中止条件为已经生成了digit位的数字，即index==digit，将此时的数num转为int加到res结果中。


## 代码
```python
def printNumbers(self, n: int) -> List[int]:
        def dfs(index, num, digit):
            if index == digit:
                res.append(int(''.join(num)))
                print(int(''.join(num)))
                return
            for i in range(10):
                num.append(str(i))
                dfs(index + 1, num, digit)
                num.pop()
        res = []
        for digit in range(1, n + 1):
            for first in range(1, 10):
                num = [str(first)]
                dfs(1, num, digit)
        return res

```
