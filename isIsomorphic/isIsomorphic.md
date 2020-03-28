# isIsomorphic

#### 题目

给定两个字符串 ***s*** 和 ***t\***，判断它们是否是同构的。

如果 ***s*** 中的字符可以被替换得到 ***t\*** ，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。

**示例 1:**

```
输入: s = "egg", t = "add"
输出: true
```

**示例 2:**

```
输入: s = "foo", t = "bar"
输出: false
```

**示例 3:**

```
输入: s = "paper", t = "title"
输出: true
```



### CODE
```c++
class Solution {
public:
    
    bool pos(string s, string t){
        unordered_map<int,int> m;
        int l1=s.length();
        int l2=t.length();
        if(l1!=l2)return false;
        if(l1==0||l1==1)return true;
        for(int i=0;i<l1;i++){
            if(m.find(s[i])!=m.end()){
                if(t[i]-s[i]!=m[s[i]])return false;
            }else{
                m[s[i]]=t[i]-s[i];
            }
        }
         return true;
    }
    bool isIsomorphic(string s, string t) {
       return pos(s,t)&&pos(t,s);
    }
};
```
