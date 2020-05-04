# ComplexListNode


#### 题目

* prob 35 复制复杂链表 

### CODE
```c++
#include<iostream>
using namespace std;
struct ComplexNode {
    char val;
    ComplexNode* next;
    ComplexNode* pslibling;
    ComplexNode(char x) :val(x), next(nullptr), pslibling(nullptr){}
};
ComplexNode* addNode(ComplexNode* root,char s) {
    root->next = new ComplexNode(s);
    return root->next;
}
void nodeConnect(ComplexNode* n1, ComplexNode* n2) {
    n1->pslibling = n2;
}
void copyList(ComplexNode* l1) {
    if (l1 == nullptr) return ;
    while (l1) {
        ComplexNode* tmp = new ComplexNode(l1->val);
        tmp->next = l1->next;
        l1->next = tmp;
        l1 = tmp->next;
    }
    
}
void connectCpy(ComplexNode* l1) {
    if (l1 == nullptr)return;
    while (l1) {
        if (l1->next == nullptr) {
            cout << "copy error odd list" << endl;
            break;
        }
        if(l1->pslibling!=nullptr)
            l1->next->pslibling=l1->pslibling->next;
        l1 = l1->next->next;
    }
}
ComplexNode* sepratelist(ComplexNode* root) {
    ComplexNode* l2=root->next;
    ComplexNode* l3 = root->next;
    while (l2->next) {
        root->next = l2->next;
        root = root->next;
        l2->next = root->next;
        l2 = l2->next;
    }
    return l3;
}
void printCoplexList(ComplexNode* root) {
    if (root == nullptr)return;
    while (root) {
        cout << root->val << " ";
        if (root->next)cout <<"next:"<< root->next->val;
        if (root->pslibling)cout <<" pslibing:"<< root->pslibling->val;
        cout << endl;
        root = root->next;
    }
}
int main() { 
    ComplexNode* root = new ComplexNode('a');
    ComplexNode* b = addNode(root, 'b');
    ComplexNode* c = addNode(b, 'c');
    ComplexNode* d = addNode(c, 'd');
    ComplexNode* e = addNode(d, 'e');
    nodeConnect(root, c);
    nodeConnect(b, e);
    nodeConnect(d,b);
    printCoplexList(root);
    cout << "copy start" << endl;
    copyList(root);
    printCoplexList(root);
    cout << "connect start" << endl;
    connectCpy(root);
    printCoplexList(root);
    cout << "seperate start" << endl;
    ComplexNode* cpL=sepratelist(root);
    printCoplexList(cpL);

    return 0;
}
```

