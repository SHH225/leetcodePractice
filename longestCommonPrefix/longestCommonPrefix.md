# longestCommonPrefix


#### 题目

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1:

输入: ["flower","flow","flight"]
输出: "fl"
示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。



### CODE
```c++
//mycode
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        int len= strs.size();
        if(len==0)return "";
        string common="";

        char c;
        for(int j=0;j<strs[0].size();j++){
             c=strs[0][j];
            for(int i=0;i<len;i++){
                if(strs[i][j]==c){
                    if(i==len-1){
                        common+=c;
                    }
                }else{
                    return common;
                }
            }
        }
        return common;
    }
};
```

