# zhiPrintTree


#### 题目

之字形打印二叉树，按行先从左到右再从右到左，依次来回。

在层次遍历的基础上 变换输出方向



### CODE
```c++
#include <iostream>
#include <queue>
#include <stack>
using namespace std;
struct TreeNode {
    TreeNode *left;
    TreeNode *right;
    int val;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
void levelprint(TreeNode *root)
{
    bool rev=false;
    if(root==nullptr)return;
    queue<TreeNode *> q;
    q.push(root);
    int qsize = q.size();
    stack<int> rest;
    while (!q.empty()) {
        
        TreeNode *tmp = q.front();
        if(!rev){
            cout << tmp->val << " ";
        }else{
            rest.push(tmp->val);
        }
        q.pop();
        qsize--;
        if (tmp->left)
            q.push(tmp->left);
        if (tmp->right)
            q.push(tmp->right);
        if (qsize == 0) {
            while(!rest.empty()){
                int a=rest.top();
                rest.pop();
                cout<<a<<" ";
            }
            rev=!rev;
            qsize = q.size();
            cout << endl;
        }
    }
}
void connectnode(TreeNode *root, TreeNode *l, TreeNode *r)
{
    if (root == nullptr)
        return;
    root->left = l;
    root->right = r;
}
int main()
{
    TreeNode *root = new TreeNode(0);
    TreeNode *f1 = new TreeNode(1);
    TreeNode *f2 = new TreeNode(2);
    TreeNode *s1 = new TreeNode(3);
    TreeNode *s2 = new TreeNode(4);
    TreeNode *s3 = new TreeNode(5);
    TreeNode *t1 = new TreeNode(6);
    TreeNode *t2 = new TreeNode(7);
    TreeNode *t3 = new TreeNode(8);
    connectnode(root, f1, f2);
    connectnode(f1, s1, s2);
    connectnode(f2, s3, nullptr);
    connectnode(s1, t1, nullptr);
    connectnode(s2, t2, t3);
    levelprint(root);
    return 0;
}
```

