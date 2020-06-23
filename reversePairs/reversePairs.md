# reversePairs


#### 题目

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。



### CODE
```c++
class Solution {
public:
int mergesort(vector<int>& nums,vector<int>& tmp,int l,int r){
    if(l>=r)return 0;
    int mid=(l+r)/2;
   int count=mergesort(nums,tmp,l,mid)+mergesort(nums,tmp,mid+1,r);
    int pos=l;
    int i=l;
    int j=mid+1;
    while(i<=mid&&j<=r){
        if(nums[i]<=nums[j]){
           count+=j-mid-1;
           tmp[pos]=nums[i];
           i++;
        }else{
            tmp[pos]=nums[j];
            j++;
        }
        pos++;
    }
    for(int k=i;k<=mid;k++){
        tmp[pos++]=nums[k];
        count+=j-mid-1;
    }
    for(int k=j;k<=r;k++){
        tmp[pos++]=nums[k];
    }
    copy(tmp.begin()+l,tmp.begin()+r+1,nums.begin()+l);
    return count;
}
    int reversePairs(vector<int>& nums) {
        int len=nums.size();
        vector<int> tmp(len);
        if(len<=1)return 0;   
        return mergesort(nums,tmp,0,len-1);
    }
};
```

