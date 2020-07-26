# mergesort


#### 题目

mergesort+quicksort



### CODE
```c++
#include <iostream>
#include <vector>
using namespace std;

void merge(vector<int> &a,int l,int mid,int r,vector<int> &tmp){
    int i=l;
    int j=mid+1;
    int tempi=l;
    while(i<=mid&&j<=r){
        if(a[i]<a[j]){
            tmp[tempi++]=a[i++];
        }else{
            tmp[tempi++]=a[j++];
        }
    }
    
    while (i<=mid) {
        tmp[tempi++]=a[i++];
    }
    while(j<=r){
        tmp[tempi++]=a[j++];
    }
    while(l<=r){
        a[l]=tmp[l];
        l++;
    }
}
void mergesort(vector<int> &a,int l,int r,vector<int> &tmp){
    if(l>=r)return;
    int mid=(l+r)/2;
    mergesort(a, l, mid, tmp);
    mergesort(a, mid+1, r, tmp);
    merge(a,l,mid,r,tmp);
}




int getstand(vector<int> &nums,int l,int r){
       int tmp=nums[l];
       while(l<r){
           while(l<r&&nums[r]>=tmp){
               r--;
           }
           nums[l]=nums[r];
           while(l<r&&nums[l]<=tmp){
               l++;
           }
           nums[r]=nums[l];
       }
       nums[l]=tmp;
       return l;
   }
   void quicksort(vector<int> &nums,int l,int r){
       if(l<r){
       int mid=getstand(nums,l,r);
       quicksort(nums,l,mid-1);
       quicksort(nums,mid+1,r);
       }
   }
 
int main()
{
    int a[]={4,2,6,9,5,0,1,3,7,8};
    vector<int> src(a,a+10);
    vector<int> temp(10,0);
    mergesort(src,0,10,temp);
   // quicksort(src, 0, 9);
    for(int i=0;i<src.size();i++){
        cout<<src[i]<<" ";
    }
    return 0;
}

```

