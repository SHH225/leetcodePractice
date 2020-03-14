# levelOrder


#### 题目

给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> list;
        queue<TreeNode*> qu;
       
        if(root==NULL)return list;
        TreeNode* node=root;
        qu.push(node);
       int j=0;
        while(qu.size()>0){
            
            int size=qu.size();
            vector<int> temp;
            for(int i=0;i<size;i++){
                 
                TreeNode* p=qu.front();
                qu.pop();
                if(p->left){
                    qu.push(p->left);
                }
                if(p->right){
                    qu.push(p->right);
                }
                
                temp.push_back(p->val);
            }
            list.push_back(temp);
        }     
        return list;
    }
};
```
