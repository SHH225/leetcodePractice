# MinStack

#### 题目

设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) -- 将元素 x 推入栈中。
pop() -- 删除栈顶的元素。
top() -- 获取栈顶元素。
getMin() -- 检索栈中的最小元素。
示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.



### CODE
```c++
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {

    }
    int minnum;
    void push(int x) {
        mainst.push(x);
        if(minst.empty()){
            minst.push(x);
            minnum=x;
        }else{
            if(x<=minst.top()){
                minst.push(x);
                minnum=x;
            }
        }

    }
    
    void pop() {
        if(mainst.top()==minst.top()){
            minst.pop();
        }
         mainst.pop();
    }
    
    int top() {
        return mainst.top();
    }
    
    int getMin() {
        return minst.top();
    }
    stack<int> mainst;
    stack<int> minst;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

