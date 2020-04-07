# numof1


#### 题目

* Prob15 num of 1 in binarynum

### CODE

```c++
//prob14 num of 1 in binarynum

using namespace std;

int main(){
    int n,count=0;
    while(cin>>n){
       
//    while(n!=0){
//        if(n%2==1)count++;
//        n/=2;
//    }
        while(n){
            ++count;
            n=(n-1)&n;
        }
        cout<<count<<endl;
        count=0;
    }
    return 0;
}
ck>
#include<queue>
using namespace std;
int maxmtlti(const int n){
    if(n<2)return 0;
    if(n==2)return 1;
    if(n==3)return 2;
    int result[n+1];
    
    //这部分的初始化为经过分割后第一段能达到最大的值，前面为整段的分割后返回
    result[3]=3;
    result[2]=2;
    result[1]=1;
    result[0]=0;
    for(int i=4;i<=n;i++){
        int max=0;
        for(int j=1;j<=i/2;j++){
            int product=result[j]*result[i-j];
            if(product>max)
                max=product;
            result[i]=max;
        }
    }
    return result[n];
}
int main(){
    int ropelen;
    cin>>ropelen;
    int result=maxmtlti(ropelen);
    cout<<result<<endl;
    return 0;
}

```

