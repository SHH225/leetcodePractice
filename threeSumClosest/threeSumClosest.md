# threeSumClosest


#### 题目

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).



### CODE
```c++
class Solution {
public:
    int close(int a, int b){
        int res=a-b;
        if(res<0)res=-res;

        return res;
    }
    int threeSumClosest(vector<int>& nums, int target) {
        int len=nums.size();
        int result=0;
      
        int min=INT_MAX;
        sort(nums.begin(),nums.end());
       for(int i=0;i<len-2;i++){
            int l=i+1;
            int r=len-1;
            int a=nums[i];
           while(l<r){
               int b=nums[l];
               int c=nums[r];
               if(a+b+c-target==0){
                   return target;
                }else if(a+b+c-target>0){
                       int tmp=close(target,a+b+c);
                        if(tmp<min){
                         min=tmp;
                        result=a+b+c;
                        }
                        r--;
               }else{
                   int tmp=close(target,a+b+c);
                        if(tmp<min){
                         min=tmp;
                        result=a+b+c;
                        }
                        l++;

               }   
               
           }
       }
       return result;
    }
}
```

先排序，再选择能减少时间复杂度