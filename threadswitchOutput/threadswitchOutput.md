# threadswitchOutput


#### 题目

实现两个线程分别交替输出1-100

例如： 

Printer1 - 1

Printer2 - 2

Printer3 - 3

Printer4 - 4

。。。

### CODE
```c++
#include <condition_variable>
#include <iostream>
#include <mutex>
#include <thread>
#include <unistd.h>
using namespace std;
mutex mu, m1, m2;
condition_variable data_var;
bool flag = true;
int num = 1;

//first approach
void Printer1()
{
    while (num < 100) {
        usleep(10000);
        unique_lock<mutex> lck(mu) ;
        data_var.wait(lck,[]{return flag;});
        cout << "Printer1 - " << num++ << endl;
        flag = false;
        data_var.notify_one();
    }
}

void Printer2()
{
    while (num < 100) {
        usleep(10000);
        unique_lock<mutex> lck(mu) ;
        data_var.wait(lck,[]{return !flag;});
        cout << "Printer2 - " << num++ << endl;
        flag = true;
        data_var.notify_one();
    }
}
//====second approach
//void Printer1()
//{
//    while (num < 100) {
//        usleep(10000);
//        m1.lock();
//        cout << "Printer1 - " << num++ << endl;
//        m2.unlock()；
//    }
//}
//
//void Printer2()
//{
//    while (num < 100) {
//        m2.lock();
//        cout << "Printer2 - " << num++ << endl;
//        m1.unlock();
//    }
//}
int main()
{
    m2.lock();
    m1.unlock();
    thread p1(Printer1);
    thread p2(Printer2);
    p1.detach();
    p2.detach();
    pause();
    return 0;
}

```

