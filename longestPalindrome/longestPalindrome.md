# longestPalindrome


#### 题目
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
示例 2：

输入: "cbbd"
输出: "bb"



### CODE

```c++

class Solution {
public:

    void findsolu(string s,int n,int left,int right,int &start,int &maxwidth){
       
        while(left>=0&&right<=n&&s[left]==s[right]){
            left--;
            right++;
        }
        if(right-left-1>maxwidth){
            maxwidth=right-left-1;
            start=left+1;

        }
    }
    string longestPalindrome(string s) {
        int len=s.length();
        if(len<=1)return s;
        int maxwidth=0;
        int sratr=0;int left=0,right=0,start=0;
        for(int i=0;i<len-1;i++){

          findsolu(s,len,i,i,start,maxwidth);
          findsolu(s,len,i,i+1,start,maxwidth);
        }
       return s.substr(start,maxwidth);
    }
};
```

镜像展开，从头开始，注意奇数偶数的不同，对比的方式不同 使用left，right能够很好的把两种游标区分开，

一个是从同一起点开始向左右，一个是从对称位置出发。注意substr（start，len）使用