# replacespace


#### 题目

* prob:5  replace " " with "%20" in string   O(n) solution


### CODE
```c++
#include <iostream>
using namespace std;
int main(){
    char str[30]={"we a re happy."};
    int length=30;
    if(str==nullptr||length<=0)return 0;
    int orginlen=0,spacelen=0;
    for(auto i:str){
       if(i=='\0')break;
       orginlen++;
       if(i==' ')
           spacelen++;
    }
    int newlength=orginlen+2*spacelen;
    if(length<=newlength){
        
        cout<<"len not enough to expand";
        
        return 0;
    }
    for(int i=newlength-1,j=orginlen-1;i>=0&&j>=0;i--,j--){
        if(str[j]!=' '){
            
            str[i]=str[j];
        
        }else{
           
            str[i--]='0';
            str[i--]='2';
            str[i]='%';
       
        }
    }
    
    cout<<str;
    return 0;
}
```