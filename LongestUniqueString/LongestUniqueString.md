# LongestUniqueString


#### 题目

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。



### CODE
```c++
//myCode
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
       int len=s.length();
       unordered_map<int,int> record;
       int max=0;
       for(int j=0;j<len;j++){
            for(int i=j;i<len;i++){
                if(record.find(s[i])!=record.end())break;
                record[s[i]]=i;
            if(max<=record.size())
                max=record.size();
            }
            record.clear();
        }
        return max;
    }
};

//GoodCode


```
