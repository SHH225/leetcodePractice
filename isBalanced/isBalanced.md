#isBalanced


#### 题目

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过1。



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
    int treedepth(TreeNode* root){
        if(root==NULL)return 0;
        int left=1,right=1;
        left+=treedepth(root->left);
        right+=treedepth(root->right);

        return left>right?left:right;

    }
    bool isBalanced(TreeNode* root) {
        if(root==NULL)return true;
        int left=treedepth(root->left);
        int right=treedepth(root->right);

        if(abs(left-right)>1)return false;

        return isBalanced(root->left)&&isBalanced(root->right);
    }
    
};
```

