# numinstr


#### 题目

实现函数判断一个字符串是否表示数值 包括整数、小数

例如+100、5e2\-123 3.14 -1E-16 true

12e 1a3.14 1.2.3 +-5 12e+5.4 false



### CODE
```c++
#include <iostream>
using namespace std;
bool isNum(string str){
    int len=str.length();
    if(len<=0)return false;
    int dotcount=0,ecount=0;
    if(len==1&&(str[0]<'0'||str[0]>'9'))return false;
    
    for(int i=0;i<len;i++){
        if(str[i]=='-'||str[i]=='+'){
            if(i==0||(i-1>=0&&(str[i-1]=='e'||str[i-1]=='E'))){
                //e+.
                if((i-1>=0&&(str[i-1]=='e'||str[i-1]=='E'))&&i+1<len&&str[i+1]=='.')return false;
                //+
                 if((i+1<len&&str[i+1]!='.'&&(str[i+1]>'9'||str[i+1]<'0')))return false;
            }else{
                return false;
            }
        }else if(str[i]=='.'){
            if(dotcount>0)return false;
            dotcount++;
            if(i-1>=0&&(str[i-1]=='+'||str[i-1]=='-')&&i==len-1)return false;
            if(i==0&&str[i]=='.')continue;
            //.
            if(i-1>=0&&str[i-1]!='+'&&str[i-1]!='-'&&(str[i-1]>'9'||str[i-1]<'0'))return false;
            if(i+1<len&&(str[i+1]>'9'||str[i+1]<'0'))return false;
        }else if(str[i]=='e'||str[i]=='E'){
            if(ecount>1)return false;
            ecount++;
            dotcount++;
            if(i==0||i==len-1)return false;
            
            if(i-1>=0&&(str[i-1]<'0'||str[i-1]>'9'))return false;
            if(i+1<len&&str[i+1]!='-'&&str[i+1]!='+'&&(str[i+1]<'0'||str[i+1]>'9'))return false;
            
        }else if(str[i]>='0'&&str[i]<='9'){
            
        }else{
            return false;
        }

    }
    return true;
}
int main()
{
    string str;
    while(cin>>str){
    bool result=isNum(str);
        cout<<result<<endl;
        
    }
    return 0;
}

```

