# 题目描述
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

示例:
```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

# 解决思路
暴力，n^2的计算；

需要注意的是要求返回索引，不是返回元素，因此不能先排序；

输入元素中可能有负数，因此将值跟target比对想加速处理的想法也不要有；

# 提交代码
```cpp
#include <algorithm> 
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> result={0,0};
        //sort(nums.begin(),nums.end());
        int flag =0;
        int j=0;
        for(int i=0;i<nums.size();i++){
            //if(nums[i]>target)
            //    continue;
            for(int j=i+1;j<nums.size();j++){
                //if(nums[j]>target)
                //    continue;
                if(nums[i]+nums[j]==target){
                    result[0]=i;
                    result[1]=j;
                    flag=1;
                    break;
                }
            }
            if(flag==1)
                return result;
        }
        result={};
        return result;
    }
};
```
