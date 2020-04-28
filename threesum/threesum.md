# threesum


#### 题目

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

 

示例：

给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]

### CODE
```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> a;
        
        int n=nums.size();
        if(n<3)return a;
       sort(nums.begin(),nums.end());
       for(int i=0;i<n-2;i++){
           if(i>0&&nums[i]==nums[i-1])continue;
           //为何是i i-1而不是i i+1，因为当i和i+1相同时 i与n-1包含的数字更多，并且可能存在多组解，若跳过可能会出现解的缺失的情况
          int f=nums[i];
           int l=i+1;
           int r=n-1;
        while(l<r){
            int b=nums[l];
            int c=nums[r];
            if(f+b+c==0){
                vector<int> tmp;
                tmp.push_back(f);
                tmp.push_back(b);
                tmp.push_back(c);
                a.push_back(tmp);
                while(r>0&&nums[r]==nums[r-1])r--;
                while(l<n-1&&nums[l]==nums[l+1])l++;
                r--;
                l++;
            }else if(f+b+c>0){
                while(r>0&&nums[r]==nums[r-1])r--;
                r--;
            }else{
                while(l<n-1&&nums[l]==nums[l+1])l++;
                l++;
            }
        }
       
       }
    
        return a;
    }
};
```

