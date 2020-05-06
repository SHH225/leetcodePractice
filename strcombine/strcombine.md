# strcombine


#### 题目

* prob 38 字符串排列



### CODE

```c++
#include <iostream>
#include <set>
using namespace std;
void printAllCombine(string &str, set<string> &res, int begin)
{
    res.insert(str);
    for (int i = begin; i < str.length(); i++) {
        swap(str[i], str[begin]);
        printAllCombine(str, res, begin + 1);
        swap(str[i], str[begin]);
    }
}
int main()
{
    string str;
    cin >> str;
    int len = str.length();
    set<string> res;
    printAllCombine(str, res, 0);
    for(auto i:res){
        cout<<i<<endl;
    }
    return 0;
}

```

