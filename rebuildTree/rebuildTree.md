# rebuild binaryTree



#### 题目

* prob 7:rebuild binaryTree  with preorder an inorder list



### CODE

```c++
//prob 7:rebuild binaryTree  with preorder an inorder list

#include <iostream>
#include <stack>
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
    cout<<root->value<<" ";
    if(node->left){
        printTree(node->left);
    }
    if(node->right){
        printTree(node->right);
    }
}
int main(){
    int pre[8]={1,2,4,7,3,5,6,8};
    int ino[8]={4,7,2,1,5,3,8,6};
    TreeNode* root=ConstructTree(pre,ino,8);
    printTree(root);
    return 0;
}



```
