# minispoporder


#### 题目

实现最小栈

弹栈顺序正误判断



### CODE
```c++
#include <iostream>
#include <stack>
using namespace std;
class minStack {
  public:
    minStack() {}
    void push(int x)
    {
        mainst.push(x);
        if (minst.empty()) {
            minst.push(x);
        }
        else {
            if (x < minst.top()) {
                minst.push(x);
            }
        }
    }
    void pop()
    {
        if (!mainst.empty()) {

            if (!minst.empty() && mainst.top() == minst.top())
                minst.pop();
            mainst.pop();
        }
    }
    int min()
    {
        if (!minst.empty())
            return minst.top();

        return -1;
    }
    stack<int> mainst;
    stack<int> minst;
};
bool ispoporder(int a[5], int b[5])
{
    if (a == nullptr || b == nullptr)
        return false;

    stack<int> s1;
    for (int i = 0, j = 0; i < 5&&j < 5;) {

        if (!s1.empty() && s1.top() == b[j]) {
            s1.pop();
            j++;
        }
        else {
            s1.push(a[i++]);
        }
    }
    if (s1.empty())
        return true;
    return false;
}
int main()
{

    // prob 30
    //    minStack ms;
    //    ms.push(5);
    //    ms.push(9);
    //    ms.push(3);
    //    ms.push(2);
    //    int mins = ms.min();
    //    cout << mins;
    //    ms.pop();
    //    mins = ms.min();
    //    cout << mins;

    // prob 31
    int a[5] = {1, 2, 3, 4, 5};
    int b[5] = {4, 5, 3, 2, 1};
    int c[5] = {4, 3, 5, 1, 2};

    bool result = ispoporder(a, c);
    if(result){
        cout<<" is pop order"<<endl;
    }else{
        cout<<"nooooooo"<<endl;
    }

    return 0;
}

```

