# deletnodedul


#### 题目

删除链表中一节点 要求时间复杂度为O（1）

删除链表中重复元素



### CODE
```c++
#include <iostream>
#include <set>
#include <vector>
using namespace std;
struct ListNode{
    ListNode* next;
    int val;
    ListNode(int x):val(x),next(nullptr){}
};
ListNode* tobedeleted;
void deleteNode(ListNode* head,ListNode* tobedeleted){
    if(head==nullptr||tobedeleted==nullptr)return;
    if(!tobedeleted->next){
        ListNode* node=head;
        while(node->next!=tobedeleted){
            node=node->next;
        }
        node->next=nullptr;
    }else{
        tobedeleted->val=tobedeleted->next->val;
        tobedeleted->next=tobedeleted->next->next;
    }
    
}
void deleteDuplicateNode(ListNode* head){
     if(head==nullptr||head->next==nullptr)return;
    if(head->val==head->next->val)head=nullptr;
    ListNode* node=head;
    ListNode* layback=head;
    int single=0;
    while(node->next){
        if(node->val==node->next->val){
            layback->next=node->next->next;
        }
        if(single)layback=layback->next;
        node=node->next;
        single=1;
    }
    
}
void addNode(ListNode* head,int val){
    ListNode* node=head;
    while(node->next){
        node=node->next;
    }
    ListNode* tmp=new ListNode(val);
    if(val==2)tobedeleted=tmp;
    node->next=tmp;
    tmp->next=nullptr;
}
void printlist(ListNode* head){
    ListNode* node=head;
    while(node){
        cout<<node->val<<" ";
        node=node->next;
    }
    cout<<endl;
    
}
int main()
{
    ListNode* head=new ListNode(0);
    for(int i=1;i<=5;i++){
        
            addNode(head,i);
        if(i==5){
            addNode(head,i);
        }
    }
    printlist(head);
    
    deleteDuplicateNode(head);
    printlist(head);
    
    
    return 0;
}

```

