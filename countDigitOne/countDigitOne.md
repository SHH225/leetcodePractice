# countDigitOne

#### 题目

给定一个整数 n，计算所有小于等于 n 的非负整数中数字 1 出现的个数。

示例:

输入: 13
输出: 6 
解释: 数字 1 出现在以下数字中: 1, 10, 11, 12, 13 。



### CODE
```c++
class Solution {
public:
    int countDigitOne(int n) {
        if(n <= 0)
             return 0;
        int count = 0;
        for(long i = 1; i <= n; i *= 10){
             long diviver = i * 10;
             int t1=0,t2=i;
             if (n % diviver - i + 1>0){
                t1=n % diviver - i + 1;
             }
             t2=t1<i?t1:t2;
             count += (n / diviver) * i + t2;
        }
         return count;
    }
};
```

