# reverseprint


#### 题目

* prob 6:Listnode reverse print val of the list



### CODE
```c++
//prob 6:Listnode reverse print val of the list

#include <iostream>
#include <stack>
using namespace std;
struct ListNode{
    ListNode* next;
    int value;
    ListNode(int x):value(x),next(nullptr){}
};
void printlist(ListNode* head){
    while(head){
          cout<<head->value;
          head=head->next;
      }
}
void addtoend(ListNode* head,int value){
    ListNode* node=head;
    while(node->next){
        node=node->next;
    }
    node->next=new ListNode(value);
    node=node->next;
    node->next=nullptr;
}
ListNode* deletenode(ListNode* head,int value){
    ListNode* node;
   
    if(head->value==value){
        head=head->next;
        return head;
    }
     node=head;
    while(node->next){
        if(node->next->value==value){
            node->next=node->next->next;
              return head;
            break;
        }
        node=node->next;
    }
    return head;
}

void reverseprint(ListNode* head){
    stack<int> st;
    ListNode* node;
    node=head;
    while(node){
        st.push(node->value);
        node=node->next;
    }
    while(!st.empty()){
        cout<<st.top();
        st.pop();
    }
}
ListNode* reverseList(ListNode* head){
    ListNode* nhead=head;
    ListNode* node=head;
    while(node->next){
        ListNode* tmp=new ListNode(0);
        tmp->next=nhead;
        tmp->value=node->next->value;
        node->next=node->next->next;
        nhead=tmp;

    }
    return nhead;
}
int main(){
    ListNode *head=new ListNode(0);
    addtoend(head,5);
    addtoend(head,9);
    printlist(head);
    ListNode* node=reverseList(head);
    printlist(node);
    printlist(head);
    cout<<endl;
    reverseprint(node);
    return 0;
}
```

