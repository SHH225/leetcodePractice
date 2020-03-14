# isSymmetric


#### 题目

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 `[1,2,2,3,4,4,3]` 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 `[1,2,2,null,3,null,3]` 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```



### CODE
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool iSsame(TreeNode* root1,TreeNode* root2){
        if(root1==NULL&&root2==NULL)return true;
        if(root1==NULL||root2==NULL)return false;
        if(root1->val==root2->val){
            cout<<root1->val<<root2->val;
            return iSsame(root1->left,root2->right)&&iSsame(root1->right,root2->left);
        }else{
            return false;
        }
    }
    bool isSymmetric(TreeNode* root) {
        if(root==NULL)return true;
        TreeNode* lnode=root->left;
        TreeNode* rnode=root->right;
        bool issame=false;
        issame=iSsame(lnode,rnode);
        return issame;
    }
};
```

递归判断左右是否为镜像树