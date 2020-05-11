# letterCombinations


#### 题目

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

示例:

输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
说明:
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。



### CODE
```c++
class Solution {
public:
    vector<string> collectallCombine(string digits,vector<string>& dic){
        vector<string> result;
        for(int i=0;i<digits.length();i++){
             int d=digits[i]-'0';
            if(result.size()<=0){
                for(int j=0;j<dic[d].size();j++){
                    string s="";
                    s+=dic[d][j];
                    result.push_back(s);
                }
                continue;
            }
            vector<string> r;
              for(int l=0;l<result.size();l++){
                 for(int j=0;j<dic[d].size();j++){
                    string tmp="";
                    tmp+=result[l]+dic[d][j];
                 
                    r.push_back(tmp);
                }
            }
            result=r;
        }
        return result;
    }

    vector<string> letterCombinations(string digits) {
        vector<string> dic;
        dic.push_back("00");
        dic.push_back("11");
        dic.push_back("abc");
        dic.push_back("def");
        dic.push_back("ghi");
        dic.push_back("jkl");
        dic.push_back("mno");
        dic.push_back("pqrs");
        dic.push_back("tuv");
        dic.push_back("wxyz");
        vector<string> list;
        if(digits.length()<=0)
            return list;
        list=collectallCombine(digits,dic);
        return list;
        
    }
};
```

