# convertToreList


#### 题目

* prob 35 二叉搜索树转双向链表 （指针调整方式）



### CODE

```c++
#include<iostream>
using namespace std;
struct TreeNode {
	int val;
	TreeNode* left;
	TreeNode* right;
	TreeNode(int x):val(x),left(nullptr),right(nullptr){}
};

void connectNode(TreeNode* root, TreeNode* left, TreeNode* right) {
	if (root == nullptr)return;
	root->left = left;
	root->right = right;
}
void inorderPrintTree(TreeNode* root) {
	if (root == nullptr)return;
	if (root->left)
		inorderPrintTree(root->left);
	cout << root->val<<" ";
	if (root->right)
		inorderPrintTree(root->right);
}
void cconvert(TreeNode* root, TreeNode** plist) {
	if (root == nullptr)return;

	if (root->left)
		cconvert(root->left, plist);
	root->left = *plist;
	if (*plist != nullptr) {
		(*plist)->right = root;
	}
	*plist = root;
	if (root->right)
		cconvert(root->right, plist);
}
TreeNode* convertToreList(TreeNode* root ) {
	TreeNode* plist=nullptr;
	cconvert(root, &plist);
	while ((plist->left)!= nullptr) {
	plist = plist->left;
	}
	return plist;
}
int main() { 
	TreeNode* root = new TreeNode(10);
	TreeNode* a = new TreeNode(6);
	TreeNode* b = new TreeNode(14);
	TreeNode* c = new TreeNode(4);
	TreeNode* d = new TreeNode(8);
	TreeNode* e = new TreeNode(12);
	TreeNode* f = new TreeNode(16);
	connectNode(root,a, b);
	connectNode(a, c, d);
	connectNode(b, e, f);
	//inorderPrintTree(root);
	TreeNode* head = convertToreList(root);
	while (head) {
		cout << head->val << " ";
		if(head->left)
			cout << " left: " << head->left->val;
		if(head->right)
			cout<< " right: " << head->right->val << endl;;
		head = head->right;
	}
	return 0;
}
```

