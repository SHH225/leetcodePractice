# nextNode

#### 题目

* prob 8:find next point of binaryTree  with  in order

### CODE
```c++


#include <iostream>
#include <stack>
using namespace std;
struct TreeNode{
    int value;
    TreeNode* left;
    TreeNode* right;
    TreeNode* father;
};
TreeNode* tmpnode;
int single=0;
TreeNode* constructCore(char* stp,char*enp,char* stin,char* enin){
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
    char* tmpindex=stin;
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
TreeNode* ConstructTree(char* pre,char* ino,int length){
    if(pre==nullptr||ino==nullptr||length<=0){
        return nullptr;
    }
        return constructCore(pre,pre+length-1,ino,ino+length-1);
}
void printTree(TreeNode* root){
    TreeNode* node=root;
    cout<<(char)root->value<<" ";
     if(root->value=='i')tmpnode=root;
    if(node->left){
        TreeNode* left;
        left=node->left;
        left->father=node;
        printTree(node->left);
    }
    if(node->right){
        TreeNode* right;
        right=node->right;
        right->father=node;
        printTree(node->right);
    }
}
TreeNode* getNext(TreeNode* node){
    TreeNode* nextnode=nullptr;
    if(node==nullptr)return nullptr;
    if(node->right!=nullptr){
        TreeNode* rightnode=node->right;
        while(rightnode->left!=nullptr){
            rightnode=rightnode->left;
        }
        nextnode=rightnode;
    }else if(node->father!=nullptr){
        
        TreeNode* nfather=node->father;
        while(nfather!=nullptr&&node==nfather->right){
            
            node=nfather;
            nfather=nfather->father;
        }
        nextnode=nfather;
    }
    return nextnode;
}
int main(){
    char pre[9]={'a','b','d','e','h','i','c','f','g'};
    char ino[9]={'d','b','h','e','i','a','f','c','g'};
    TreeNode* root=ConstructTree(pre,ino,9);
    printTree(root);
    cout<<endl;
    cout<<(char)tmpnode->value<<" next is ";
    TreeNode* nexnode=getNext(tmpnode);
    cout<<(char)nexnode->value<<endl;
    return 0;
}

```

