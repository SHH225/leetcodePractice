# revlist

#### 题目

反转链表



### CODE
```c++
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

ListNode* reverse(ListNode* root){
  
    ListNode* node=root;
    ListNode* pre=nullptr;
    while(node){
      ListNode* tnext=node->next;
         node->next=pre;
         pre=node;
        node=tnext;
    }
    return pre;
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
    
    printl(root);
    ListNode* reroot=reverse(root);
    printl(reroot);

    return 0;
}

```

