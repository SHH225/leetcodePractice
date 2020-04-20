# issubtree

#### 题目

* Prob26 输入两棵树a、b，判断b是不是a的子结构 



### CODE
```c++
#include <iostream>
using namespace std;
struct TreeNode{
    TreeNode* left;
    TreeNode* right;
    double val;
    TreeNode(int x):val(x),left(nullptr),right(nullptr){}
};


void printpre(TreeNode* root){
    if(root==nullptr)return;
    cout<<root->val<<" ";
    if(root->left)
        printpre(root->left);
    if(root->right)
        printpre(root->right);
}

void connectNode(TreeNode* root,TreeNode* left,TreeNode* right){
    if(root){
        root->left=left;
        root->right=right;
    }
}
bool numCompare(double a,double b){
    if(b-a<0.0000001&&b-a>-0.0000001)return true;
    
    return false;
}
bool compareTree(TreeNode* r1,TreeNode* r2){
    bool isco=false;
    if(r2==nullptr)return true;
    if(r1==nullptr&&r2!=nullptr)return false;
    if(numCompare(r1->val, r2->val)){
        isco=true;
    }
    return isco&&compareTree(r1->left, r2->left)&&compareTree(r1->right, r2->right);
}

bool issubTree(TreeNode* root1,TreeNode* root2){

    bool hassub=false;
    if(root1!=nullptr&&root2!=nullptr){
    if(numCompare(root1->val, root2->val)){
        if(compareTree(root1, root2))
            hassub=true;
    }
    if(!hassub)
        hassub=issubTree(root1->left, root2);
    if(!hassub)
        hassub=issubTree(root1->right, root2);
        
    }
    return hassub;
}
int main()
{
    TreeNode* aroot=new TreeNode(8);
    TreeNode* a1=new TreeNode(8);
    TreeNode* a2=new TreeNode(9);
    TreeNode* a3=new TreeNode(3);
    TreeNode* a4=new TreeNode(4);
    TreeNode* a5=new TreeNode(7);
    TreeNode* a6=new TreeNode(7);
    connectNode(aroot, a1, a6);
    connectNode(a1, a2,  a3);
    connectNode(a3, a4, a5);
    printpre(aroot);
    cout<<endl;
    
    TreeNode* broot=new TreeNode(3);
    TreeNode* b2=new TreeNode(4);
    TreeNode* b3=new TreeNode(7);
    connectNode(broot, b2, b3);
    printpre(broot);
    cout<<endl;
    
    
    if(issubTree(aroot, broot)){
        cout<<"b is subTree of a"<<endl;
        
    }else{
        cout<<"b is not subtree of a"<<endl;
    }
    
    return 0;
}

```

