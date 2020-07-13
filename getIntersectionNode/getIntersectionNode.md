# getIntersectionNode


#### 题目

输入两个链表，找出它们的第一个公共节点。



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
class Solution {
public:
int getlen(ListNode* head){
    int count=0;
    ListNode* node=head;
    while(node){
        node=node->next;
        count++;
    }
    return count;
}
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(headA==nullptr||headB==nullptr)return nullptr;
        ListNode* re=nullptr;
        int lena=getlen(headA);
        int lenb=getlen(headB);
        if(lena<lenb)return getIntersectionNode(headB,headA);
        int cut=lena-lenb;
        while(cut>0){
            headA=headA->next;
            cut--;
        }
        while(headA!=headB){
            headA=headA->next;
            headB=headB->next;
        }
        re=headA;
        return re;
    }
};
```

