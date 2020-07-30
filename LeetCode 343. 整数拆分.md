# 题目描述
给定一个正整数 n，将其拆分为至少两个正整数的和，并使这些整数的乘积最大化。 返回你可以获得的最大乘积。

示例 1:

输入: 2

输出: 1

解释: 2 = 1 + 1, 1 × 1 = 1。

示例 2:

输入: 10

输出: 36

解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36。

说明: 你可以假设 n 不小于 2 且不大于 58。

# 解决思路
基本思想是动态规划，将大小为n的数看成是长为n的线段。选择合适位置切分为两段，比较两段长度值乘积和对右侧段进一步执行切分后的结果与左侧段乘积的大小，返回max;

1<=i<(n/2+1): max[i*(n-i), i*integerBreak(n-i)]

为了进一步降低运行时间，将其优化为带备忘录的自顶向下的实现方式；

# 提交代码
```cpp
class Solution {
public:
    int result[59];
    int integerBreak(int n) {
        int max=0;
        if(n==1){
            return 1;
        }
        int now=0;
        int temp=0;
        for(int i=1;i<n/2+1;i++){
            if(result[n-i]!=0){
                temp=i*result[n-i];
            }
            else{
                result[n-i]=integerBreak(n-i);
                temp=i*result[n-i];
            }
            if(i*(n-i)<temp){
                now=temp;
            }
            else{
                now=i*(n-i);
            }
            if(max<now){
                max=now;
            }
        }
        return max;
    }
};
```
