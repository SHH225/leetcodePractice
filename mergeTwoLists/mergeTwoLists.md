# mergeTwoLists


#### 题目

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4



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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* finalList=new ListNode(0);
        ListNode* head=finalList;
        while(l1&&l2){
            if(l1->val<l2->val){
                finalList->next=l1;
                l1=l1->next;
            }else{
                finalList->next=l2;
                l2=l2->next;
            }
            finalList=finalList->next;
        }
        if(l1!=NULL){
            finalList->next=l1;
        }else{
            finalList->next=l2;
        }
        return head->next;
    }
};


//merge to l1
#include <iostream>
using namespace std;
struct ListNode{
    int val;
    ListNode* next;
    ListNode(int x):val(x),next(nullptr){}
};
void printl(ListNode* head){
    while(head){
        cout<<head->val<<" ";
        head=head->next;
    }
    cout<<endl;
}
ListNode* mergel(ListNode* root1,ListNode* root2){
    if(root1==nullptr&&root2==nullptr)return nullptr;
    if(root1==nullptr&&root2!=nullptr)return root2;
    if(root2==nullptr&&root1!=nullptr)return root1;
    
    if(root1->val>root2->val)return mergel(root2, root1);
    ListNode* node1=root1;
    ListNode* node2=root2;
    while(node1->next&&node2){
        if(node1->val<=node2->val){
            if(node1->next->val>=node2->val){
                ListNode* temp=node2->next;
                node2->next=node1->next;
                if(temp!=nullptr)
                node1->next=node2;
                node2=temp;
            }
            node1=node1->next;
        }
    }
    
    if(node2!=nullptr){
        node1->next=node2;
    }
    
    return root1;
}

int main()
{
    
    ListNode* head=new ListNode(0);
    ListNode* root1=head;
    ListNode* cir=new ListNode(0);
    ListNode* root2=cir;
    for(int i=1;i<10;i++){
        head->next=new ListNode(i);
        cir->next=new ListNode(3*i);
        head=head->next;
        cir=cir->next;
    }
    printl(root1);
    printl(root2);
    
    ListNode* mroot=mergel(root1,root2);
    printl(mroot);
    
    return 0;
}

```

