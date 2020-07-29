# 题目描述
给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

示例 1:

输入: 1->2->3->4->5->NULL, k = 2

输出: 4->5->1->2->3->NULL

解释:

向右旋转 1 步: 5->1->2->3->4->NULL

向右旋转 2 步: 4->5->1->2->3->NULL

示例 2:

输入: 0->1->2->NULL, k = 4

输出: 2->0->1->NULL

解释:

向右旋转 1 步: 2->0->1->NULL

向右旋转 2 步: 1->2->0->NULL

向右旋转 3 步: 0->1->2->NULL

向右旋转 4 步: 2->0->1->NULL

# 解决思路
根据题目描述，最简单的思路是执行k轮旋转，每轮旋转1步，旋转通过修改head指针的指向，以及末尾元素的指向实现；

每轮旋转，将链表最末元素指向head，使链表成环；

然后拆环，head指向链表最末元素，原链表倒数第二末尾元素next指针指向NULL；

**需要注意的是开始不为空的判断以及k的处理（不处理会遇到超时错误）；**

# 提交代码
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if(head==NULL||head->next==NULL){
            return head;
        }
        ListNode *u;
        int length=1;
        u=head;
        while(u->next!=NULL){
                length++;
                u=u->next;
        }
        k=k%length;
        for(int i=0;i<k;i++){
            u=head;
            while(u->next->next!=NULL){
                u=u->next;
            }
            u->next->next=head;
            head=u->next;
            u->next=NULL;
        }
        return head;
    }
};
```
