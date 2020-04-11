# knife

#### 题目

输入T组数据

M为格子宽高 L为🔪长，且M*M范围内格子内部分区域不为0

X，Y为人的位置

人物旋转他的刀，刀所覆盖的范围内有不为0的点刀变长+area[i][j]

输出最后刀能到多长





### CODE
```c++
#include <iostream>
using namespace std;
bool isgot(int a,int b,int x,int y,int len){
    int sum1=(a-x)*(a-x)+(b-y)*(b-y);
    int sum2=len*len;
    if(sum1>sum2)return false;

    return true;
}
int main() {
    int T,tmpl;

    int M,L,X,Y;
    cin>>T;
    for(int k=0;k<T;k++){
        cin>>M>>L;
        int area[500][500]={0};
        bool areavisited[500][500]={0};
        for(int i=0;i<M;i++){
            for(int j=0;j<M;j++){
                cin>>area[i][j];
            }
        }
        cin>>X>>Y;

        while(true){
            tmpl=L;
            int len=L,x=X,y=Y,m=M;
            int startx,starty,endx,endy;
               int templen=len;
               if(x-len>=0){
                   startx=x-len;
               }else{
                   startx=0;
               }
               if(y-len>=0){
                   starty=y-len;
               }else{
                   starty=0;
               }
               if(x+len>=m){
                   endx=m;
               }else{
                   endx=x+len;
               }
               if(y+len>=m){
                   endy=m;
               }else{
                   endy=y+len;
               }
               for(int i=startx;i<=endx;i++){
                   for(int j=starty;j<=endy;j++){
                       if(isgot(i, j, x, y, len)&&!areavisited[i][j]&&area[i][j]!=0){
                           templen+=area[i][j];
                           areavisited[i][j]=true;
                       }
                   }
               }
            L=templen;
            if(tmpl==L){
                cout<<L;
                break;

            }
        }

    }
    return 0;
}
//0 0 0 0 0 0 0 0 0 0
//0 0 0 0 0 0 0 0 0 0
//0 0 0 0 0 0 0 0 0 0
//0 0 0 0 0 0 0 0 0 0
//0 0 2 0 0 1 0 0 0 0
//0 0 0 1 2 0 2 0 0 0
//0 0 0 0 2 1 2 0 2 0
//0 0 2 0 0 0 0 0 2 0
//0 0 0 0 0 0 0 2 0 0
//0 0 0 1 0 0 0 0 0 0

//0 0 0 0 0 0 0 0 0 0
//0 0 0 0 0 0 0 0 0 0
//0 0 0 0 0 0 0 0 0 0
//0 0 0 0 0 0 0 0 0 0
//0 0 0 0 2 0 0 0 0 0
//0 0 0 0 0 0 0 0 0 0
//0 0 0 0 1 0 2 0 0 0
//0 0 0 0 0 0 0 0 0 2
//0 0 0 1 0 0 0 0 0 1
//0 0 0 1 0 0 2 0 2 0

```
