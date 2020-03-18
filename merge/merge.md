# reverse


#### 题目

给你两个有序整数数组 *nums1* 和 *nums2*，请你将 *nums2* 合并到 *nums1* 中*，*使 *num1* 成为一个有序数组。

 

**说明:**

- 初始化 *nums1* 和 *nums2* 的元素数量分别为 *m* 和 *n* 。
- 你可以假设 *nums1* 有足够的空间（空间大小大于或等于 *m + n*）来保存 *nums2* 中的元素。

 

**示例:**

```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```



### CODE
```c++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
      int l1=m-1,l2=n-1;
      cout<<l1<<l2<<endl;
      for(int i=m+n-1;i>=0;i--){
            if(l1<0&&l2>=0){
                for(int k=0;k<=l2;k++)
                    nums1[k]=nums2[k];
            }
            if(l1>=0&&l2>=0){
                if(nums1[l1]>=nums2[l2]){
                    nums1[i]=nums1[l1--];
                }else{
                    nums1[i]=nums2[l2--];
                }
                cout<<nums1[i];
            }
        }
    }
};
```

思想：合并后长度为m+n 那么从m+n-1的位置倒序向前插入是一个比较好的方式，