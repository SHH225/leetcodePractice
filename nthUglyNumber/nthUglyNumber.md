# nthUglyNumber


#### 题目

* //prob 丑数 

在层次遍历的基础上 变换输出方向



### CODE
```c++
class Solution {
public:
int minthree(int a,int b,int c){
    int tmp=min(a,min(b,c));
    return tmp;
}
    int nthUglyNumber(int n) {
        vector<int> nums;
        nums.push_back(1);
        int t=1,i=0,j=0,k=0;
        while(t<n){
            nums.push_back(minthree(nums[i]*2,nums[j]*3,nums[k]*5));
            if(nums[t]==nums[i]*2)i++;
            if(nums[t]==nums[j]*3)j++;
            if(nums[t]==nums[k]*5)k++;
            t++;
        }
        return nums[n-1];
    }
};
```

