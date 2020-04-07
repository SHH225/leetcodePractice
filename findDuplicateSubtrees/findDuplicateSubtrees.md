# findDuplicateSubtrees


#### 题目

给定一棵二叉树，返回所有重复的子树。对于同一类的重复子树，你只需要返回其中任意一棵的根结点即可。

两棵树重复是指它们具有相同的结构以及相同的结点值。

示例 1：

        1
       / \
      2   3
     /   / \
    4   2   4
       /
      4
下面是两个重复的子树：

      2
     /
    4
和

    4
因此，你需要以列表的形式返回上述重复子树的根结点。



### CODE
```c++
class Solution {
public:

    string helper(TreeNode* root,unordered_map<string,int> &m,vector<TreeNode*> &res){
        if(root==NULL)return "";
        string str=to_string(root->val)+','+helper(root->left,m,res)+','+helper(root->right,m,res);
        if(m[str]==1){
            res.push_back(root);
        }
        m[str]++;
        return str;
    }

    vector<TreeNode*> findDuplicateSubtrees(TreeNode* root) {
       unordered_map<string,int> m;
       vector<TreeNode*> result;
       helper(root,m,result);
       return result;
    }
};
```

