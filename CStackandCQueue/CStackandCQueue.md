# CStackandCQueue

#### 题目

* prob 9: apply a queue with two stack /apply a stack with two queue



### CODE
```c++
//prob 9: apply a queue with two stack

#include <iostream>
#include <stack>
#include<queue>
using namespace std;
template <typename T> class CQueue
{
public:
    CQueue(void);
    ~CQueue(void);

    void appendTail(const T& node);
    T deleteHead();
private:
    stack<T> stack1;
    stack<T> stack2;
};
template <typename T> CQueue<T>::CQueue(void)
{
}

template <typename T> CQueue<T>::~CQueue(void)
{
}
template<typename T> void CQueue<T> :: appendTail(const T& element){

    stack1.push(element);
    }
template<typename T> T CQueue<T> ::deleteHead(){
    T head;
    if(stack2.empty()){
        while(!stack1.empty()){
            auto tmp=stack1.top();
            stack1.pop();
            stack2.push(tmp);
        }
        head= stack2.top();
        stack2.pop();
    }else{
         head=stack2.top();
        stack2.pop();
    }
    return head;
    }

template <typename T> class CStack
{
public:
    CStack(void);
    ~CStack(void);
    void pushCStack(const T& element);
    T deleteCStackTop();
private:
    queue<T> q1;
    queue<T> q2;
};
template <typename T>CStack <T>::CStack(void){}
template <typename T>CStack <T>::~CStack(void){
    
}
template <typename T> void CStack<T>::pushCStack(const T& element){
    q1.push(element);
}
template<typename T> T CStack<T>::deleteCStackTop(){
    T node;
    if(!q1.empty()){
    while(q1.size()>1){
        T& tmp= q1.front();
        q1.pop();
        q2.push(tmp);
    }
       node=q1.front();
        q1.pop();
        
    }else{
         while(q2.size()>1){
             T& tmp=q2.front();
             q1.push(tmp);
             q2.pop();
         }
        node=q2.front();
        q2.pop();
    }
    if(q1.empty()){
        while(q2.empty()){
            T& tmp=q2.front();
            q1.push(tmp);
            q2.pop();
        }
    }
    return node;
}

int main(){
    CQueue<char> q;
    q.appendTail('a');
    q.appendTail('b');
    q.appendTail('c');
    char a=q.deleteHead();
    cout<<a;
    a=q.deleteHead();
    cout<<a;
    cout<<endl;
    CStack<char> s;
    s.pushCStack('a');
    s.pushCStack('b');
    s.pushCStack('c');
    char r=s.deleteCStackTop();
    cout<<r;
    s.pushCStack('o');
    r=s.deleteCStackTop();
    cout<<r;
    return 0;
}

```

模版类的使用可以使类适用于各种类型的输入

在所有的函数类前加上。templete <typename T>

函数的参数精良使用const 的引用 其中T即为类型名称