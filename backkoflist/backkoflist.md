# backkoflist


#### 题目

找到链表的倒数第k个节点



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
int main()
{
    int k;
    ListNode* head=new ListNode(0);
    ListNode* root=head;
    for(int i=0;i<10;i++){
           ListNode* tmp=new ListNode(i);
           head->next=tmp;
           head=head->next;
       }
    while(cin>>k){
   
    printl(root);
    printk(root, k);
    }
    return 0;
}
```

注意几点  k的输入合法性、链表长度与k的比较 链表是否为空