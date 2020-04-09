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
vector<int> shhmin(vector<int> s,vector<int> under){
    vector<int> tmp;
    tmp.clear();
    int underl=under.size();
    for(int i=0;i<s.size();i++){
        if(s.size()==under.size()&&s[s.size()-1]<=under[under.size()-1])break;
        if(i<under.size()){
            if(s[i]>=under[i]){
                s[i]=s[i]-under[i];
            }else{
                s[i+1]-=1;
                s[i]=s[i]+10-under[i];
            }
        }else{
            if(s[i]<0){
                s[i+1]-=1;
                s[i]+=10;
            }
        }
        if(s[s.size()-1]==0){
            s.pop_back();
        }
    }
    
    
    return s;
}
void printv(vector<int> s){
    int len= s.size();
    for (int i = 0;i < len;i++){
     cout << s[len-i-1];
    }
}
int main()
{
    vector<int> s;
    int snum;//底数
    int num;//指数
    cin >> snum;
    cin >> num;
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
    s=fun(s, num);

    for(int i=s.size()-1;i>=0;i--){
        cout<<s[i];
    }

    return 0;
}

```

