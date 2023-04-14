## 题目描述
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。


## 解决思路
模拟popped的弹出过程，首先在self.pushed不为空的前提下，不断push元素，直至栈顶元素与目标弹出元素一致，弹出目标元素，继续判断下一个目标元素可否弹出。

若最终所有元素均可弹出且栈为空，则True；

若有元素未弹出（栈为空或不为空）或元素全部弹出但栈中元素不为空，则False。

## 代码
```python
def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        if not pushed:
            if not popped:
                return True
            return False
        self.pushed=[pushed[0]]
        i,j=0,1
        while True:
            while self.pushed and popped[i]!=self.pushed[-1] and j<len(pushed):
                self.pushed.append(pushed[j])
                j+=1
            if self.pushed and popped[i]==self.pushed[-1]:
                self.pushed.pop()
                if not self.pushed and j<len(pushed): 保证栈中元素不为空，才可进行判断
                    self.pushed.append(pushed[j])
                    j+=1
                i+=1
                if i==len(popped):
                    if not self.pushed:
                        return True
                    return False
            else:
                return False


```
