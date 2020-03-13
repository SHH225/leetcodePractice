# isValidBST


#### 题目

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

- 节点的左子树只包含**小于**当前节点的数。
- 节点的右子树只包含**大于**当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。

**示例 1:**

```
输入:
    2
   / \
  1   3
输出: true
```

**示例 2:**

```
输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。
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
//借助栈，中序遍历，看是否为增序
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        vector<TreeNode*> stack;
        vector<int> list;
        TreeNode* node=root;
        while(stack.size()>0||node!=NULL){
            if(node!=NULL){
                stack.push_back(node);
                node=node->left;
            }else{
                node=stack.back();
                stack.pop_back();
                list.push_back(node->val);
                node=node->right;
            }
        }  
        for(int i=0;i<list.size()-1&&list.size()>0;i++){
            if(list[i]>=list[i+1])return false;
        }
        return true;
    }
};

//递归方式
class Solution {
public:
    bool helper(TreeNode* root,int lower,int upper){
        if(root==NULL)return true;
        int val=root->val;
        if(root->right&&root->right->val<=root->val)return false;
        if(root->left&&root->left->val>=root->val)return false;
        if(upper!=NULL&&val>=upper)return false;
        if(lower!=NULL&&val<=lower)return false;
        if(!helper(root->left,lower,val))return false;
        if(!helper(root->right,val,upper))return false;
        return true;
    }
    bool isValidBST(TreeNode* root) {
        return helper(root,NULL,NULL);
    }
};
```

要注意除了对每个单独节点的左右孩子要符合要求也要符合其上级节点的界限