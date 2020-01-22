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
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
     int freq[256] = {0};
        int l = 0, r = -1; //滑动窗口为s[l...r]
        int res = 0;
        // 整个循环从 l == 0; r == -1 这个空窗口开始
        // 到l == s.size(); r == s.size()-1 这个空窗口截止
        // 在每次循环里逐渐改变窗口, 维护freq, 并记录当前窗口中是否找到了一个新的最优值
        while(l < s.size()){
            if(r + 1 < s.size() && freq[s[r+1]] == 0){
                r++;
                freq[s[r]]++;
            }else {   //r已经到头 || freq[s[r+1]] == 1
                freq[s[l]]--;
                l++;
            }
            res = max(res, r-l+1);
        }
        return res;
    }
};

```
