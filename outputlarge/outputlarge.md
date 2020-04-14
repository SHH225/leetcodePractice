# outputlarge


#### 题目

输入n

输出从1，2，3，4 ，，，直到n位的最大数

例：

3

1，2，3，4，，，，999

4

1，2，3，4，，，，9999



### CODE
```c++
#include <iostream>
#include <set>
#include <vector>
using namespace std;
void printresult(vector<int> a)
{
    for (int i = a.size()-1; i >=0; i--) {
        cout << a[i];
    }
    cout<<endl;
}
int main()
{
    int n;
    cin >> n;
    vector<int> result;
    result.push_back(1);
    while (result.size() < n + 1) {
        printresult(result);
        result[0] += 1;
        for (int i = 0; i < result.size(); i++) {
            if (result[i] >= 10 && i + 1 < result.size()) {
                result[i] -= 10;
                result[i + 1] += 1;
            }
        }
        if (result[result.size() - 1] >= 10) {
            result[result.size() - 1] -= 10;
            result.push_back(1);
        }
        
    }
    
    
    return 0;
}
```

