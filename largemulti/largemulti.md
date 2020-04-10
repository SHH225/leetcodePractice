# largemulti


#### 题目

* 给定N L 求N的L次幂。（计算结果超过常规整形表示范围）



### CODE
```c++
#include<iostream>
#include<vector>
#include<string>
using namespace std;
const int under=1000000007;
int dns=0;
vector<int> plu(vector<int>a, vector<int>b)
{
    vector<int>c;
    c.clear();
    for (int i = 0, t = 0; i < a.size() || i < b.size() || t; i++)
    {
        if (i < a.size()) t += a[i];
        if (i < b.size()) t += b[i];
        c.push_back(t % 10);
        t = t / 10;
    }
    return c;//还是倒着的
}
vector<int>  simplemul(vector<int>a, int b)//数组乘以常熟
{
    vector<int> c;
    if (b == 0)
    {
        c.push_back(0);
        return c;
    }
    c.clear();
    for (int i = 0, t = 0; i < a.size() || t; i++)
    {
        if (i < a.size()) t += b * a[i];
        c.push_back(t % 10);
        t = t / 10;
    }
    return c;
}

vector<int> simpleminus(vector<int>a ,vector<int> b){
    vector<int> c;
    if(b.size()==1&&b[0]==0)return a;
    string bs;
    for(int i=b.size()-1;i>=0;i--){
        bs+=to_string(b[i]);
    }
    //    string bs=to_string(b);
    string as;
    for(int i=a.size()-1;i>=0;i--){
        as+=to_string(a[i]);
    }
    int lena=as.length();
    int lenb=bs.length();
    if(as>=bs||lena>=lenb){
        
        int dif=lena-lenb;
        for(int i=lena-1;i>=0;i--){
            int a=as[i]-'0'+dns;
            int b=bs[i-dif]-'0';
            if(lena-i>lenb){
                b=0;
            }
            int p=a-b;
            dns=0;
            if(p<0){
                p+=10;
                dns=-1;
            }
            c.push_back(p);
        }
    }else{
        return a;
    }
    
    
    while(c.back()==0){
        if(c.size()==1)break;
        c.pop_back();
    }
    return c;
}

vector<int> mul(vector<int>a, vector<int> b)//数组乘法
{
    vector<int>c;
    c.clear();
    vector<int>d;
    for (int i = 0; i < a.size() || d.size(); i++)
    {
        if (i < a.size())
        {
            d = plu(d, simplemul(b, a[i]));
        }
        c.push_back(d[0]);
        d.erase(d.begin(), d.begin() + 1);
    }
    return c;
}
vector<int> fun(vector<int>s,int n)//幂次方+二分法
{
    if (n == 1) { return s; }
    if (n == 2) { return mul(s,s); }
    if (n % 2 == 0)
    {
        vector<int>c;
        c.clear();
        c = fun(s, n / 2);
        return(mul(c,c));
    }
    else
    {
        vector<int>c;
        c.clear();
        c = fun(s, n / 2);
        vector<int>d;
        d.clear();
        d = mul(c, c);
        return(mul(d,s));
    }
}

void printv(vector<int> s){
    int len= s.size();
    for (int i = 0;i < len;i++){
        cout << s[len-i-1];
    }
    cout<<endl;
}
bool compare(vector<int> a,vector<int> b){
    if(a.size()<b.size())return false;
    if(a.size()>b.size())return true;
    for(int i=a.size()-1;i>=0;i--){
        if(a[i]>b[i])return true;
        if(a[i]<b[i])return false;
    }
    return true;
}
int main()
{
    vector<int> s;
    int snum;//底数
    int num;//指数
    while(cin>>snum>>num){
        
        if(snum==0&&num==0)break;
        
        int N=snum;
        
        while (snum != 0)
        {
            s.push_back(snum % 10);//得到s为倒序数组
            snum = snum / 10;
        }
        vector<int> underv;
        int tmp=under;
        while(tmp!=0){
            underv.push_back(tmp%10);
            tmp/=10;
        }
        vector<int> result;
        vector<int> rone;
        rone.push_back(0);
        result.push_back(0);
        //        求和
        for(int i=1;i<=num;i++){
            rone=fun(s, i);
            result=plu(rone,result);
        }
//        取余。还没写好。。。
//        while(result.size()>underv.size()){
//            vector<int> temp(underv.begin(),underv.end());
//            int time=result.size()-underv.size();
//            for(int i=0;i<time-1;i++){
//                temp=simplemul(temp, 10);
//            }
//            result=simpleminus(result, mul(underv, temp));
//        }
//        result=simpleminus(result,underv);
//        result=simpleminus(result,underv);
        printv(result);
        result.clear();
        s.clear();
    }
    
    return 0;
}

```

