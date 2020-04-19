# findcirclein


#### 题目

寻找带环链表中环的入口



### CODE
```c++
#include <iostream>
using namespace std;
struct ListNode{
    int val;
    ListNode* next;
    ListNode(int x):val(x),next(nullptr){}
};
void printk(ListNode* head,int k){
    if(head==nullptr)return;
    ListNode* node=head;
    if(k<1){
        cout<<"invalid k"<<endl;
        return;
    }
    while(node->next){
        if(k<=1)head=head->next;
        
        node=node->next;
        k--;
    }
    if(k>1){
        cout<<"k out of range"<<endl;
    }else{
        cout<<head->val<<endl;
    }
}
void printl(ListNode* head){
    while(head){
        cout<<head->val<<" ";
        head=head->next;
    }
    cout<<endl;
}
void findcir(ListNode* root,int num){
    ListNode* node1=root;
    ListNode* node2=root;
    while(num>0){
        node1=node1->next;
        num--;
    }
    while(node1!=node2){
        node1=node1->next;
        node2=node2->next;
    }
    cout<<" circle in :"<<node2->val<<endl;
}
int judgecir(ListNode* root){
    ListNode* fast=root;
    int count=0,single=0;
    ListNode* slow=root;
    while(fast->next->next){
        fast=fast->next->next;
        slow=slow->next;
        if(single)count++;
        if(slow==fast){
            if(single)
            return count;
            single=1;
        }
    }
    return false;
}
int main()
{
 
    ListNode* head=new ListNode(0);
    ListNode* root=head;
    ListNode* cir;
    for(int i=0;i<10;i++){
        ListNode* tmp=new ListNode(i);
        head->next=tmp;
        if(i==5){
            cir=tmp;
        }
           head=head->next;
       }
    head->next=cir;
    int iscir=judgecir(root);
    if(iscir){
        cout<<"circle"<<endl;
        findcir(root,iscir);
        
    }else{
        cout<<"no cir"<<endl;
    }
    return 0;
}
```

