# 题目描述
给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和。

提示：
```
num1 和num2 的长度都小于 5100
num1 和num2 都只包含数字 0-9
num1 和num2 都不包含任何前导零
```
你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式

# 解决思路
从较短的字符串的末位开始，跟另一个字符串对应位置字符求和，这里需要将字符转成整型，int(ch)+48;

为了解决添位导致的字符串长度增加的问题，预先在较长的字符串前面拼接“0000”，输出时需要将前导0删除；

需要注意的地方是访问两个数组对应值时的下标以及操作结果字符串的下标；

# 提交代码
```cpp
#include <string>
class Solution {
public:
    string addStrings(string num1, string num2) {
        if(num1.length()==0 && num2.length()==0){
            return "";
        }
        if(num1.length()==0)
            return num2;
        if(num2.length()==0)
            return num1;

        string result;
        int flag=0;
        if(num1.length()<num2.length()){
            result="0000"+num2;
            int temp=0;
            for(int i=num1.length()-1;i>=0;i--){
                temp=int(num1[i])-48+int(num2[num2.length()-num1.length()+i])-48+flag;
                if(temp<=9){
                    result[i+4+num2.length()-num1.length()]=char(temp+48);
                    flag=0;
                }
                else{
                    result[i+4+num2.length()-num1.length()]=char(temp-10+48);
                    flag=1;
                }
            }
            for(int i=num2.length()-num1.length()-1;i>=0;i--){
                temp=int(num2[i])-48+flag;
                if(temp<=9){
                    result[i+4]=char(temp+48);
                    flag=0;
                    break;
                }
                else{
                    result[i+4]=char(temp-10+48);
                    flag=1;
                }
            }
        }
        else{
            result="0000"+num1;
            int temp=0;
            for(int i=num2.length()-1;i>=0;i--){
                temp=int(num1[num1.length()-num2.length()+i])-48+int(num2[i])-48+flag;
                if(temp<=9){
                    result[i+4+num1.length()-num2.length()]=char(temp+48);
                    flag=0;
                }
                else{
                    result[i+4+num1.length()-num2.length()]=char(temp-10+48);
                    flag=1;
                }
            }
            for(int i=num1.length()-num2.length()-1;i>=0;i--){
                temp=int(num1[i])-48+flag;
                if(temp<=9){
                    result[i+4]=char(temp+48);
                    flag=0;
                    break;
                }
                else{
                    result[i+4]=char(temp-10+48);
                    flag=1;
                }
            }
        }
        if(flag!=0)
            result[3]=char(flag+48);
        
        int count=0;
        for(int i=0;i<4;i++){
            if(int(result[i])==48)
                count++;
        }
        result.erase(0,count);
        
        return result;
        
       
    }
};
```
