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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(headA==nullptr||headB==nullptr)return nullptr;
        if(headA==headB)return headA;
        int count=0;
        ListNode* node=nullptr;
        ListNode* n1=headA;
        ListNode* n2=headB;
        while(n1&&n2){
            n1=n1->next;
            n2=n2->next;
        }
        if(n1){
            while(n1){
            n1=n1->next;
            count++;
            }
            while(count>0){
                headA=headA->next;
                count--;
            }
            while(headA&&headB&&headA!=headB){
                headA=headA->next;
                headB=headB->next;
            }
            if(headA){node=headA;
            }

        }else if(n2){
            while(n2){
            n2=n2->next;
            count++;
            }
             while(count>0){
                headB=headB->next;
                count--;
            }
            while(headA&&headB&&headA!=headB){
                headA=headA->next;
                headB=headB->next;
            }
            if(headA){node=headA;}
        }else{
             while(headA&&headB&&headA!=headB){
                headA=headA->next;
                headB=headB->next;
            }
            if(headB){node=headB;}
        }
        return node;
    }
};
```

