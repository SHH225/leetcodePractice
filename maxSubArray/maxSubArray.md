# maxSubArray


#### 题目

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:

输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。



### CODE
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int n=nums.size();
        if(n==0)return 0;
        vector<int> sum(n);
        sum[0]=nums[0];
        int total=sum[0];   
        for(int i=1;i<n;i++){
            sum[i]=max(nums[i],nums[i]+sum[i-1]);
            total=max(total,sum[i]);
        }
        return total;
    }
};
```
