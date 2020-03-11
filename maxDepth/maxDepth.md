# maxDepth


#### 题目

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
给定二叉树 [3,9,20,null,null,15,7]，

   3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。



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
//dfs解法
class Solution {
public:
    int maxDepth(TreeNode* root) {
       if(root==NULL)return 0;
       return max(maxDepth(root->left),maxDepth(root->right))+1; 
    }
};



//bfs解法
class Solution {
public:
    int maxDepth(TreeNode* root) {
       if(root==NULL)return 0;
       int num=0;
       queue<TreeNode*> que;
       que.push(root);
       while(!que.empty()){
           int n=que.size();
           for(int i=0;i<n;i++){
                TreeNode* cur=que.front();
                if(cur->left!=NULL){
                    que.push(cur->left);
                }
                if(cur->right!=NULL){
                    que.push(cur->right);
                 }
                que.pop();
           }
           num++;
       }      
       return num; 
    }
};
```

