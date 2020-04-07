# powernum


#### 题目

* prob16 power

### CODE
```c++
//prob16 power
#include <iostream>
using namespace std;

double powernum(double base,int exponent){
    double result=1.0;
    for(int i=0;i<exponent;i++){
        result*=base;
    }
    return result;
}
int main(){
    double base,result;
    int exponent;
    cin>>base>>exponent;
    if(base==0.0&&exponent<0){
        cout<<"math error /0 "<<endl;
        return 0;
    }
    if(base==0.0){cout<<0;return 0;}
    if(exponent>0){
       result=powernum(base, exponent);
    }else{
        result=powernum(base, -exponent);
        result=1.0/result;
    }
    cout<<result;
    return 0;
}

```

考虑 base 取值情况  exponent 取值情况

正、负、零

