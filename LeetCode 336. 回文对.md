# 题目描述
给定一组 互不相同 的单词， 找出所有不同 的索引对(i, j)，使得列表中的两个单词， words[i] + words[j] ，可拼接成回文串。

示例 1：
```
输入：["abcd","dcba","lls","s","sssll"]
输出：[[0,1],[1,0],[3,2],[2,4]] 
解释：可拼接成的回文串为 ["dcbaabcd","abcddcba","slls","llssssll"]
```
示例 2：
```
输入：["bat","tab","cat"]
输出：[[0,1],[1,0]] 
解释：可拼接成的回文串为 ["battab","tabbat"]
```

# 解决思路

# 暴力求解代码
暴力求解复杂度是O(n^2*m)，m是拼接后的字符串的平均大小，以下代码超时；
```cpp
#include <vector>
class Solution {
public:
    int comparision(string s){
        int i=0;
        int j=s.size()-1;
        while(i<s.size()/2){
            if(s[i]!=s[j]){
                return 0;
            }
            i++;
            j--;
        }
        return 1;
    }

    vector<vector<int>> palindromePairs(vector<string>& words) {
        vector<vector<int>> result;
        string s;
        vector<int> a(2);
        for(int i=0;i<words.size();i++){
            for(int j=0;j<words.size();j++){
                if(j==i){
                    continue;
                }
                if(words[i]=="" && words[j]==""){
                    a[0]=i;
                    a[1]=j;
                    result.push_back(a);
                    continue;
                }
                if(words[i]==""){//words[j]!=""
                    if(words[j].size()==1){
                        a[0]=i;
                        a[1]=j;
                        result.push_back(a);
                        continue;
                    }
                    if(comparision(words[j])==1){
                        a[0]=i;
                        a[1]=j;
                        result.push_back(a);
                        continue;
                    }
                }
                if(words[j]==""){//words[i]!=""
                    if(words[i].size()==1){
                        a[0]=i;
                        a[1]=j;
                        result.push_back(a);
                        continue;
                    }
                    if(comparision(words[i])==1){
                        a[0]=i;
                        a[1]=j;
                        result.push_back(a);
                        continue;
                    }
                }
                s=words[i]+words[j];
                if(comparision(s)==1){
                    a[0]=i;
                    a[1]=j;
                    result.push_back(a);
                }
            }
        }
        return result;
    }
};
```
