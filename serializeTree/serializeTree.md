# zhiPrintTree


#### 题目

* prob 37 序列化/反序列化二叉树



### CODE
```c++
#include<iostream>
#include<vector>
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
void preorderprint(TreeNode* root) {
	if (root == nullptr)return;
	cout << root->val << " ";
	if (root->left)
		preorderprint(root->left);
	
	if (root->right)
		preorderprint(root->right);
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
void serializeTree(TreeNode* root,vector<int>& seq) {
	if (root == nullptr)return ;
	seq.push_back(root->val);
	if (root->left) {
		serializeTree(root->left, seq);
	}
	else {
		seq.push_back(-1);
	}
	if (root->right) {
		serializeTree(root->right, seq);
	}
	else {
		seq.push_back(-1);
	}
	
}
TreeNode* deserializeTree( vector<int>& seq,int& i) {
	TreeNode* deroot;
	if (seq[i] == -1) {
		 deroot = nullptr;
		return deroot;
	}
	deroot = new TreeNode(seq[i]); 
	deroot->left=deserializeTree( seq, ++i);
	deroot->right=deserializeTree( seq, ++i);
	return deroot;
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
	vector<int> seq;
	serializeTree(root, seq);
	for (auto i : seq) {
		cout << i << " ";
	}
	int i = 0;
	TreeNode* deroot = nullptr;
	deroot=deserializeTree(seq,i);
	inorderPrintTree(deroot);
	cout << endl;
	preorderprint(deroot);
	return 0;
}
```

