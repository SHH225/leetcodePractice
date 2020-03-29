# containsNearbyDuplicate


#### 题目

给定一个整数数组和一个整数 *k*，判断数组中是否存在两个不同的索引 *i* 和 *j*，使得 **nums [i] = nums [j]**，并且 *i* 和 *j* 的差的 **绝对值** 至多为 *k*。

 

**示例 1:**

```
输入: nums = [1,2,3,1], k = 3
输出: true
```

**示例 2:**

```
输入: nums = [1,0,1,1], k = 1
输出: true
```

**示例 3:**

```
输入: nums = [1,2,3,1,2,3], k = 2
输出: false
```





### CODE
```c++
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_map<int,int> m;
        for(int i=0;i<nums.size();i++){
            if(m.find(nums[i])!=m.end()){
                if(i-m[nums[i]]>k){
                    m[nums[i]]=i;
                }else{
                    return true;
                }
            }else{
                m[nums[i]]=i;
            }
        }
        return false;
    }
};
```

