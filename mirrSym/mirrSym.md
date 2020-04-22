# mirrSym


#### 题目

输出一个树的镜像树

判断一个树是否为对称树



### CODE
```c++
#include <iostream>
#include <vector>
using namespace std;
struct TreeNode {
    TreeNode *left;
    TreeNode *right;
    double val;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void printpre(TreeNode *root)
{
    if (root == nullptr)
        return;
    cout << root->val << " ";
    if (root->left)
        printpre(root->left);
    if (root->right)
        printpre(root->right);
}

void connectNode(TreeNode *root, TreeNode *left, TreeNode *right)
{
    if (root) {
        root->left = left;
        root->right = right;
    }
}
bool numCompare(double a, double b)
{
    if (b - a < 0.0000001 && b - a > -0.0000001)
        return true;

    return false;
}
bool compareTree(TreeNode *r1, TreeNode *r2)
{
    bool isco = false;
    if (r2 == nullptr)
        return true;
    if (r1 == nullptr && r2 != nullptr)
        return false;
    if (numCompare(r1->val, r2->val)) {
        isco = true;
    }
    return isco && compareTree(r1->left, r2->left) &&
           compareTree(r1->right, r2->right);
}

bool issubTree(TreeNode *root1, TreeNode *root2)
{

    bool hassub = false;
    if (root1 != nullptr && root2 != nullptr) {
        if (numCompare(root1->val, root2->val)) {
            if (compareTree(root1, root2))
                hassub = true;
        }
        if (!hassub)
            hassub = issubTree(root1->left, root2);
        if (!hassub)
            hassub = issubTree(root1->right, root2);
    }
    return hassub;
}
void MirroTree(TreeNode *root)
{
    if (root == nullptr)
        return;
    if (root->left == nullptr && root->right == nullptr)
        return;

    TreeNode *tmp = root->left;
    root->left = root->right;
    root->right = tmp;
    if (root->left)
        MirroTree(root->left);
    if (root->right)
        MirroTree(root->right);
}

vector<int> Readpre(TreeNode *root, vector<int> &a)
{
    if (root != nullptr) {
        a.push_back(root->val);
        if (root->left == nullptr && root->right != nullptr)
            a.push_back(-1);
        if (root->left) {
            Readpre(root->left, a);
        }
        if (root->right == nullptr && root->left != nullptr)
            a.push_back(-1);
        if (root->right) {
            Readpre(root->right, a);
        }
    }

    return a;
}
vector<int> Readinpre(TreeNode *root, vector<int> &a)
{
    if (root != nullptr) {
        a.push_back(root->val);
        if (root->right == nullptr && root->left != nullptr)
            a.push_back(-1);
        if (root->right) {
            Readinpre(root->right, a);
        }
        if (root->left == nullptr && root->right != nullptr)
            a.push_back(-1);
        if (root->left) {
            Readinpre(root->left, a);
        }
    }

    return a;
}
void printvec(vector<int> a)
{
    for (int i = 0; i < a.size(); i++) {
        cout << a[i] << " ";
    }
    cout << endl;
}
bool isSymmetrical(TreeNode *root)
{

    vector<int> a, b;
    a = Readpre(root, a);
    b = Readinpre(root, b);
    printvec(a);
    printvec(b);
    for (int i = 0; i < a.size(); i++) {
        if (a[i] != b[i])
            return false;
    }
    return true;
}
bool isformalsym(TreeNode *root1, TreeNode *root2)
{
    if (root1 == nullptr && root2 == nullptr)
        return true;
    if (root1 == nullptr || root2 == nullptr)
        return false;
    if (root1->val != root2->val)
        return false;

    return isformalsym(root1->left, root2->right) &&
           isformalsym(root1->right, root2->left);
}
bool formalSym(TreeNode *root) { return isformalsym(root, root); }
int main()
{
    TreeNode *aroot = new TreeNode(8);
    TreeNode *a1 = new TreeNode(7);
    TreeNode *a2 = new TreeNode(7);
    TreeNode *a3 = new TreeNode(4);
    TreeNode *a4 = new TreeNode(5);
    TreeNode *a5 = new TreeNode(7);
    TreeNode *a6 = new TreeNode(7);
    connectNode(aroot, a1, a6);
    connectNode(a1, a2, a3);
    connectNode(a6, a4, a5);
    printpre(aroot);
    cout << endl;
    //    MirroTree(aroot);
    //    printpre(aroot);
    //    cout << endl;
    if (formalSym(aroot)) {
        cout << "a is Symmetrical" << endl;
    }
    else {
        cout << "a is not Symmetrical" << endl;
    }

    return 0;
}


```

