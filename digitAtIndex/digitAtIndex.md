# digitAtIndex


#### 题目

* Prob//44



### CODE
```c++
#include <iostream>
#include<math.h>
using namespace std;
int printn(string str,int n,int len){
    int res=0;
    if(n>len)return -1;
    if(len==1)return 0;
    int cutlen=n;
    int times=1,i=1;
    cutlen--;
    while(cutlen>0){
        cutlen-=9*times*i;
        times*=10;
        i++;
    }
    i--;
    cutlen+=(times/10)*9*i;
    res+=pow(10,i-1)-1;
    res+=cutlen/i;
    int pos=cutlen%i;
    if(pos==0){return res%10;
        
    }else {
        while(pos>0){
            res/=10;
            pos--;
        }
        return res%10;
    }
}
int main(){
    string str;
    int n;
    cin>>str;
     int len=str.length();
    while(cin>>n){
    int res=printn(str,n+1,len);
    if(res==-1)cout<<"wrong n"<<endl;
    else cout<<res<<endl;
    
    }
    return 0;
}

```

