# moveground

#### 题目

* prob13 moveground of the robot



### CODE
```c++
//prob13 moveground of the robot
#include <iostream>
#include <stack>
#include<queue>
using namespace std;
int digitsum(int m,int n){
    int sum=0;
    while(m>0){
        sum+=m%10;
        m=m/10;
    }
    while(n>0){
        sum+=n%10;
        n=n/10;
    }
    return sum;
}
bool check(int rows,int cols,int row,int col,int k,bool* visited){
    if(row<rows&&row>=0&&col<cols&&col>=0&&!visited[row*cols+col]&&digitsum(row,col)<=k){
        return true;
    }
    return false;
    
}
int pathcountCore(int rows,int cols,int row,int col,int k,bool* visited){
    int count=0;
    if(check(rows,cols,row,col,k,visited)){
        visited[row*cols+col]=true;
        count=1+pathcountCore(rows,cols,row+1,col,k,visited)
        +pathcountCore(rows,cols,row,col+1,k,visited)
        +pathcountCore(rows,cols,row-1,col,k,visited)
        +pathcountCore(rows,cols,row,col-1,k,visited);
    }
    
    return count;
}
int main(){
    int count=0;
    int m,n,k;
//    cin>>m>>n>>k;
    m=5;n=5;k=5;
    bool* visited=new bool[m*n];
    for(int i=0;i<25;i++){
        visited[i]=false;
    }
    cout<<visited[10];
    count=pathcountCore(m,n,0,0,k,visited);
    cout<<"count: "<<count;
    delete[] visited;
    return 0;
}

```

