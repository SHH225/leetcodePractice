# findmininRotate


#### 题目

* prob11 find min in a rotate array 

* basic quicksort

### CODE
```c++
//prob11 find min in a rotate array
#include <iostream>
#include <stack>
#include<queue>
using namespace std;
void printV(int *a){
    for(int i=0;i<10;i++)
        cout<<" "<<a[i];
    cout<<endl;
}

int getStandard(int* a,int low,int high){
    int key=a[low];
    while(low<high){
        
        while(low<high&&a[high]>=key){
            high--;
        }
            a[low]=a[high];
        
        while(a[low]<=key&&low<high){
            low++;
        }
            a[high]=a[low];

    }
    a[low]=key;
    return low;
}

void quicksort(int* a,int low,int high){
    if(a==nullptr)return;
    if(low<high){
    int stand=getStandard(a, low, high);
    quicksort(a, low, stand-1);
    quicksort(a,stand+1,high);
    }
    
}
int findmin(int *b,int end){
    if(b==nullptr) {
        cout<<"empty array";
        return 0 ;
        
    }
    int minn=INT_MAX;
    int start=0,mid=(start+end)/2;
    if(b[start]==b[end]&&b[start]==b[mid]){
        for(int i=0;i<end;i++){
            if(b[i]<minn)minn=b[i];
        }
        
    }else{
    while(start<end){
        mid=(start+end)/2;
       
        if(b[mid]>b[start]){
            start=mid;
        }else{
            end=mid;
        }
        if(end-start==1)break;
    }
  
        minn=b[start]>b[end]?b[end]:b[start];
        
    }
    return minn;
}
int main(){
    int a[10]={0,1,2,3,4,5,6,7,8,9};
    int b[10]={5,7,7,12,9,0,1,1,3,4};
    int c[5]={1,1,1,0,1};
    int minn=findmin(b,9);
    cout<<minn;
    quicksort(a,0,9);
    printV(a);
    
    return 0;
}
/*
#include <iostream>
using namespace std;
struct ListNode{
    int val;
    ListNode* next;
    ListNode(int x):val(x),next(nullptr){}
};
int getstand(int *a,int low,int high){
    if(a==nullptr)return 0;
    int key=a[low];
    while(low<high){
        while(low<high&&a[high]>=key)
            high--;
        a[low]=a[high];
        while(low<high&&a[low]<=key)
            low++;
        a[high]=a[low];
        
    }
    a[low]=key;
    return low;
}
void quickSort(int *a,int low,int high){
    if(low<high){
        int mid=getstand(a, low,high);
        quickSort(a, low, mid-1);
        quickSort(a, mid+1, high);
    }
}
void swapNV(ListNode* a,ListNode* b){
    int tmp=a->val;
    a->val=b->val;
    b->val=tmp;
}
ListNode* getmid(ListNode* low,ListNode* high){
    if(low==high||low->next==high)return low;
    ListNode* node=low;
    ListNode* st=low;
    int key=low->val;
    while(node){
        if(node->val<key){
            st=st->next;
            swapNV(node,st);
        }
        node=node->next;
    }
    swapNV(st,low);
    return st;
}
void listQuickSort(ListNode* low,ListNode* high){
    if(low==high||low->next==high)return;
    ListNode* mid=getmid(low, high);
    listQuickSort(low, mid);
    listQuickSort(mid->next, high);
}
void printLIst(ListNode* head){
    while(head){
        cout<<head->val<<" ";
        head=head->next;
    }
    cout<<endl;
}
int main()
{
    int a[10]={2,5,2,3,7,0,9,1,5,6};
    ListNode* head=new ListNode(2);
    ListNode* high=nullptr;
    ListNode* node=head;
    for(int i=1;i<10;i++){
        
        node->next=new ListNode(a[i]);
        node=node->next;
    }
    listQuickSort(head,high);
    printLIst(head);
    quickSort(a, 0, 9);
    for(auto i:a){
        cout<<i<<" ";
    }
    return 0;
}
*/

```