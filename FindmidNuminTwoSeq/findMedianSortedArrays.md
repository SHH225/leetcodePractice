# findMedianSortedArrays


#### 题目

给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 nums1 和 nums2 不会同时为空。

示例 1:

nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
示例 2:

nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5



### CODE
```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2){
           int m=nums1.size();
        int n=nums2.size();
       
        if(m>n){
            return findMedianSortedArrays(nums2,nums1);
        }
        //cout<<m<<n;
        int imin=0,imax=m,ln=(m+n+1)/2;
        while(imin<=imax){
            int i = (imin+imax)/2;//
            int j = ln-i;
            if(i<imax&&nums1[i]<nums2[j-1]){
                imin = i+1;
            }else if(i>imin&&nums1[i-1]>nums2[j]){
                imax = i-1;
            }else{
                int maxleft=0;
                if(i==0){maxleft=nums2[j-1];}
                else if(j==0){maxleft=nums1[i-1];}
                else{maxleft=max(nums1[i-1],nums2[j-1]);}
                if((m+n)%2==1)return maxleft;
                
                int minright=0;
                if(i==m){minright=nums2[j];}
                else if(j==n){minright=nums1[i];}
                else{minright=min(nums1[i],nums2[j]);}

                return (maxleft+minright)/2.0;
            }
        }
        return 0.0;
        
    }
};

```

**注意:** 时间复杂度为log(m+n) 因此为二分的方法

* 对于有序数组 A和B，首先求长度，重新排列  短的在前
* 中位数的查找，在于每次对两个数组进行二分分割

游标更新 
ln=(m+n+1)/2
a= (imin+imax)/2; b=ln-i;
分割后的数组 每次二分通过两个游标的移动进行比较决定后续的分割
游标一 a，游标二b
通过判断 nums1[a]  num2[b]的大小与边界进行游标移动；

所以有这几种情况：

![WechatIMG1](https://tva1.sinaimg.cn/large/00831rSTly1gcfs1chx21j31430u0myv.jpg)

