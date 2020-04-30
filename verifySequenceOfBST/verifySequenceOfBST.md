# verifySequenceOfBST


#### 题目

验证序列是否为二叉搜索树的后续遍历序列



### CODE
```c++
#include <iostream>
using namespace std;
bool isbinarySearchTreeBack(int a[7],int root,int st,int end){
    if(st>=end)return true;
    int mid;
    for(mid=end-1;mid>=st;mid--){
        if(root>a[mid])break;
    }
    for(int j=st;j<mid;j++){
        if(root<a[j])return false;
    }
    return isbinarySearchTreeBack(a, a[mid], st, mid)&&isbinarySearchTreeBack(a, a[end], mid+1, end-1);
}
int main()
{

    int backlist[7]= {4, 6, 12, 8, 16, 14, 10};
    int len=7;
    bool result=isbinarySearchTreeBack(backlist,backlist[len-1],0,len-1);
    if(result){
        cout<<"is true back"<<endl;
    }else{
        cout<<"is false backlist"<<endl;
    }
    return 0;
}

```

