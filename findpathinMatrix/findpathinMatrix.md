# findpathinMatrix

#### 题目

* prob12 find path in a matrix

### CODE
```c++
//prob12 find path in a matrix
#include <iostream>
#include <stack>
#include<queue>
using namespace std;

bool haspathinM(const char m[3][4],const char *str,int row,int rows,int col,int cols,bool visited[3][4],int pathlen){
    if(str[pathlen]=='\0')return true;
    bool haspath=false;
    if(str[pathlen]==m[row][col]&&visited[row][col]==0&&row<rows&&col<cols&&row>=0&&col>=0){
        visited[row][cols]=true;
        ++pathlen;
        haspath=haspathinM(m, str, row+1, rows, col, cols, visited, pathlen)||haspathinM(m, str, row-1, rows, col, cols, visited, pathlen)||haspathinM(m, str, row, rows, col+1, cols, visited, pathlen)||haspathinM(m, str, row+1, rows, col-1, cols, visited, pathlen);
        if(!haspath){
            pathlen--;
            visited[row][col]=false;
        }
    }
    
    return haspath;
}
int main(){
    char m[3][4]={{'a','b','t','g'},
                  {'c','f','d','s'},
                  {'j','d','r','h'}};
    bool visited[3][4]={0};
    char str[]={"bfdc"};
    int len=0,single=0;
    for(int i=0;i<3;i++){
        for(int j=0;j<4;j++){
            if(haspathinM(m,str,i,3,j,4,visited,len)){
                cout<<"true";
                single=1;
            }
        }
    }
    if(!single)
    cout<<"false";
    return 0;
}

```

