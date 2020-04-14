# cutwood


#### 题目

输入n，接下来输入n个整数为木棍长度，

输入的数字应该保持近递增关系，若中间有不符合长度的木棍，需要对木棍进行折断操作。

问对于输入序列最少需要折几次能满足题目要求的近递增关系。

例：

5 

2 3 5 13 9      // 13位不符合条件的长度需要进行折断

1    //只需折断一次



### CODE

```c++
#include<iostream>
#include<vector>
 using  namespace std;
 int cutWood(vector<int> &list){
    int result=0;
    for(int i=list.size()-2;i>=0;i--){
        if(list[i]>list[i+1]){
            int tmp=(list[i]-1)/list[i+1];
            result+=tmp;
            list[i]=list[i]/(tmp+1);
        }
    }
    return result;
}
 int main(){
    int n;
    cin>>n;
    int a;
    int result=0;
    vector<int> list;
    for(int i=0;i<n;i++){
        cin>>a;
        list.push_back(a);
    }
    result=cutWood(list);

    cout<<result<<endl;

    return 0;
}
```

本题关键点在于需要折断几次，对于折断后各部分长度为多少没有要求。