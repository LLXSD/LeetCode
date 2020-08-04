# 题目描述
你这个学期必须选修 numCourse 门课程，记为 0 到 numCourse-1 。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们：[0,1]

给定课程总量以及它们的先决条件，请你判断是否可能完成所有课程的学习？

示例 1:
```
输入: 2, [[1,0]] 
输出: true
解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。
```
示例 2:
```
输入: 2, [[1,0],[0,1]]
输出: false
解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。
```
提示：

输入的先决条件是由 边缘列表 表示的图形，而不是 邻接矩阵 。详情请参见图的表示法。

你可以假定输入的先决条件中没有重复的边。

1 <= numCourses <= 10^5

# 解决思路
第一想法是拓扑排序，但是拓扑排序需要先DFS，比较麻烦；

进一步分析问题，本质上是判断是否形成回路，因此利用Bellman算法，每条边权重看作-1,判断形成的图中是否有负权回路即可；

# 提交代码
```cpp
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        if(prerequisites.size()==0){
            return true;
        }
        int inf=99999999;
        int dis_list[numCourses];
        for(int i=0;i<numCourses;i++){
            dis_list[i]=inf;
        }
        dis_list[0]=0;
        for(int i=0;i<numCourses-1;i++){
            for(int j=0;j<prerequisites.size();j++){
                if(dis_list[prerequisites[j][1]]>dis_list[prerequisites[j][0]]-1)
                    dis_list[prerequisites[j][1]]=dis_list[prerequisites[j][0]]-1;
            }
        }
        for(int i=0;i<prerequisites.size();i++){
            if(dis_list[prerequisites[i][1]]>dis_list[prerequisites[i][0]]-1)
                return false;
        }
        return true;
    }
};
```
