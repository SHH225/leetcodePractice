# intersection

#### 题目

给定两个数组，编写一个函数来计算它们的交集。

**示例 1:**

```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2]
```

**示例 2:**

```
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [9,4]
```

**说明:**

- 输出结果中的每个元素一定是唯一的。
- 我们可以不考虑输出结果的顺序。



### CODE
```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> hashset;
        unordered_set<int> hashsettar;
        vector<int> same;
        for(int i=0;i<nums1.size();i++){
           hashset.insert(nums1[i]);
        }
        for(int i=0;i<nums2.size();i++){
            if(hashset.count(nums2[i])>0){
                hashsettar.insert(nums2[i]);
            }
        }
        for(auto it=hashsettar.begin();it!=hashsettar.end();++it){
            same.push_back(*it);
        }
        return same;
    }
};
```

