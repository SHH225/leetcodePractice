# groupAnagrams


#### 题目

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

**示例:**

```
输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```



### CODE
```c++
class Solution {
public:
    
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> result;
        int index=0;
        unordered_map<string,int> m;
        vector<string> tmp;
        for(auto i:strs){
            sort(i.begin(),i.end());
            tmp.push_back(i);
        }
       
        for(int i=0;i<strs.size();i++){
            if(m.find(tmp[i])!=m.end()){
                result[m[tmp[i]]].push_back(strs[i]);
            }else{
                 m[tmp[i]]=index;
                vector<string> bucket;
                result.push_back(bucket);
                result[index].push_back(strs[i]);
                 index++;
            }
        }
        return result;
    }
};


//code2
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
         vector< vector<string> > result;
         map<string,multiset<string>> m;
         for(auto i:strs){
             string word=i;
             sort(word.begin(),word.end());
             m[word].insert(i);
         }
         for(auto i:m){
             vector<string> v(i.second.begin(),i.second.end());
             result.push_back(v);
         }
        return result;
    }
};
```
