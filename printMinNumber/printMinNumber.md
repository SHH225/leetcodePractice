# printMinNumber


#### 题目

* Prob//45



### CODE
```c++
#include <iostream>
#include <vector>
using namespace std;
int comparetwostr(string a,string b){
    string l1=a,l2=b;
    l2+=a;
    l1+=b;
    return l1<l2;
}
int main()
{
    vector<string> nums;
    int n;
    cin>>n;
    string str;
    for(int i=0;i<n;i++){
        cin>>str;
        nums.push_back(str);
    }
    sort(nums.begin(), nums.end(), comparetwostr);
    for(auto i:nums){
        cout<<i<<" ";
    }
    return 0;
}

```

