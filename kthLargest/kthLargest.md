# kthLargest


#### 题目

* Prob 54 给定一棵二叉搜索树，请找出其中第k大的节点。



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
    int kthLargest(TreeNode* root, int k) {
        if(root==nullptr)return 0;
        int res=0;
        TreeNode* node=root;
        stack<TreeNode*> st;
       
        while(node!=nullptr||!st.empty()){
            if(node){
                st.push(node);
                node=node->right;
            }else{
                 node=st.top();
                k--;
                if(k==0){
                      res=node->val;
                      break;
                  }
                st.pop();
                node=node->left;
            }
        }
            return res;
    }
};
```

