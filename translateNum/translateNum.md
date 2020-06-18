# translateNum


#### 题目

* //46 把数字翻译成字符串



### CODE
```c++
class Solution {
public:
    int translateNum(int num) {
        int count=0;
        string str=to_string(num);
        int len=str.length();
      vector<int> dp(len,0);
      dp[0]=1;
      for(int i=1;i<len;i++){
          string tmp="";
          tmp+=str[i-1];
           tmp+=str[i];
           dp[i]=dp[i-1];
          if(tmp<="25"&&tmp>="10"){
              if(i>=2){
             dp[i]+=dp[i-2];
             }else{
                 dp[i]++;
             }
          }
      }
      count=dp[len-1];
        return count;
    }
};
```

