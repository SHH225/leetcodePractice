# binaryTreeRead

#### 题目

二叉树遍历问题

### CODE
```c++
#include <iostream>
#include <stack>
#include<queue>
using namespace std;
struct TreeNode{
    int value;
    TreeNode* left;
    TreeNode* right;
};
TreeNode* constructCore(int* stp,int*enp,int* stin,int* enin){
    TreeNode* root=new TreeNode();
    root->value=stp[0];
    root->left=root->right=nullptr;
    if(stp==enp){
        if(stin==enin && *stp==*stin){
            return root;
        }else{
            return nullptr;
        }
    }
    int* tmpindex=stin;
    while(tmpindex<=enin){
        if(*tmpindex==root->value){
            break;
        }
        tmpindex++;
    }
   int leftlen=tmpindex-stin;
    if(leftlen>0){
    root->left=constructCore(stp+1,stp+leftlen , stin, tmpindex-1);
    }
    if(leftlen<enp-stp){
    root->right=constructCore(stp+leftlen+1, enp, tmpindex+1, enin);
    }
    return root;
}
TreeNode* ConstructTree(int* pre,int* ino,int length){
    if(pre==nullptr||ino==nullptr||length<=0){
        return nullptr;
    }
        return constructCore(pre,pre+length-1,ino,ino+length-1);
}
void printTree(TreeNode* root){
    TreeNode* node=root;
   
    if(node->left){
        printTree(node->left);
    }
    
    if(node->right){
        printTree(node->right);
    }
     cout<<root->value<<" ";
}
void preprintTree(TreeNode* root){
    stack<TreeNode*> s;
    TreeNode* node=root;
    if(node==nullptr)return;
    s.push(node);
    while(!s.empty()){
        TreeNode* tmp=s.top();
        cout<<tmp->value<<" ";
        s.pop();
        if(tmp->right){
            s.push(tmp->right);
        }
        if(tmp->left){
            s.push(tmp->left);
        }
        
    }
}

void inprintTree(TreeNode* root){
    stack<TreeNode*> s;
    TreeNode* node=root;
    if(node==nullptr)return;
    while(node!=nullptr||!s.empty()){
        if(node!=nullptr){
            s.push(node);
            node=node->left;
        }else{
            node=s.top();
            cout<<node->value<<" ";
            s.pop();
            node=node->right;
        }
    }
    
}
void bacprintTree(TreeNode* root){
    stack<TreeNode*> s;
    TreeNode* lastvist=root;
    if(root==nullptr)return;
    while(root!=nullptr||!s.empty()){
        if(root){
            s.push(root);
            root=root->left;
        }else{
            root=s.top();
            if(root->right==nullptr||lastvist==root->right){
                 cout<<root->value<<" ";
                lastvist=root;
                 s.pop();
                root=nullptr;
            }else{
            root=root->right;
            }
        }
    }
    
}
void levelprintTree(TreeNode* root){
    TreeNode* node=root;
    queue<TreeNode*> s;
    s.push(node);
    while(!s.empty()){
            TreeNode* tmp=s.front();
            cout<<tmp->value<<" ";
            s.pop();
            if(tmp->left)s.push(tmp->left);
            if(tmp->right)s.push(tmp->right);
        }
}
void findpathnum(TreeNode* root,int sum,vector<int> st,int target){
    if(root==nullptr)return;
    sum+=root->value;
        st.push_back(root->value);
    
    
    if(sum==target&&root->left==nullptr&&root->right==nullptr){
        for(int i=0;i<st.size();i++){
            cout<<st[i]<<" ";
        }
        cout<<endl;
    }
    
    if(root->left)
        findpathnum(root->left, sum,st,target);
    
    if(root->right)
        findpathnum(root->right, sum, st,target);
    
    st.pop_back();
    
}
int main(){
    int pre[8]={1,2,4,7,3,5,6,8};
    int ino[8]={4,7,2,1,5,3,8,6};
    TreeNode* root=ConstructTree(pre,ino,8);
    printTree(root);
    cout<<endl;
    bacprintTree(root);
    levelprintTree(root);
    
    return 0;
}

```

二叉树的几种遍历方式。前序遍历、中序遍历、后序遍历、层次遍历 （非递归方式）
