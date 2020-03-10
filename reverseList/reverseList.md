# reverseList


#### 题目

反转一个单链表。

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
进阶:
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

### CODE
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
//迭代法
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pre=NULL;
         ListNode* l=head;
        while(l){
            ListNode* tmp=l->next;
            l->next=pre;
            pre=l;
            l=tmp;
        }
        return pre;
    }
};
```

重点在于进行反转指向的时候pre的保存