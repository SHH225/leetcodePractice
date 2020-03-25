# firstUniqChar

#### 题目

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**案例:**

```
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
```



### CODE
```c++
class Solution {
public:
    int firstUniqChar(string s) {
      int dist[26]={0};
      for(char i:s){
          dist[i-'a']++;
      }
      for(int i=0;i<s.length();i++){
          if(dist[s[i]-'a']==1){
              return i;
              }
      }
      return -1;
    }
};
```

构造记数数组，便于后续单次字符的出现查找