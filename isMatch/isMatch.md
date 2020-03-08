# isMatch


#### 题目

给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配。

'.' 匹配任意单个字符
'*' 匹配零个或多个前面的那一个元素
所谓匹配，是要涵盖 整个 字符串 s的，而不是部分字符串。

说明:

s 可能为空，且只包含从 a-z 的小写字母。
p 可能为空，且只包含从 a-z 的小写字母，以及字符 . 和 *。
示例 1:

输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
示例 2:

输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
示例 3:

输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
示例 4:

输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
示例 5:

输入:
s = "mississippi"
p = "mis*is*p*."
输出: false

### CODE
```c++
class Solution {
public:
    bool isMatch(string s, string p) {
     if (s==p) {
        return true;
    }

    bool isFirstMatch = false;
    if (s.length()>0 && p.length()>0 && (s[0] == p[0] || p[0] == '.')) {
        isFirstMatch = true;
    }

    if (p.length() >= 2 && p[1] == '*') {
        // 看 s[i,...n] 和 p[j+2,...m] 或者是 s[i+1,...n] 和 p[j,...m]
        return isMatch(s, p.substr(2))
                 || (isFirstMatch && isMatch(s.substr(1), p));
    }

    // 看 s[i+1,...n] 和 p[j+1,...m]
    return isFirstMatch && isMatch(s.substr(1), p.substr(1));
    }
};
```

对于此类问题 递归的使用相对于其他方法较容易理解，*的情况是本题重点

第一种情况：完全匹配

每次 对字符串首字符进行比较，

对于此次比较pattern中第二位是否为*，

如果为*，将分为两种情况：

1. 去掉 *及它之前的字符。即 a * 相当于 不存在。那么  return 中将p的这两位截取掉，继续进行正常比较即：isMatch(s, p.substr(2))

2. 去掉s的第一项后面继续与p进行常规比较，即把*当作其前一字符的多个。

   <img src="https://tva1.sinaimg.cn/large/00831rSTly1gcmfgr5jiuj31440u0e83.jpg" alt="WechatIMG2" style="zoom: 25%;" />

后面就是正常情况每次吧此次的firstmacth &&上，最后即为整个字符串的匹配结果。