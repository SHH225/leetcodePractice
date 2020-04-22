# sukdo


#### 题目

解数独



### CODE
```c++
class Solution {
public:
const int sodusize=9;
bool colmask[9][9]={0};
bool rowmask[9][9]={0};
bool areamask[9][9]={0};
bool initsudo(vector<vector<char> > &board){
    for(int i=0;i<sodusize;i++){
        for(int j=0;j<sodusize;j++){
            if(board[i][j]<='9'&&board[i][j]>='1'){
                int indx=board[i][j]-'0'-1;
                colmask[i][indx]=true;
                rowmask[j][indx]=true;
                int area=(i/3)*3+j/3;
                areamask[area][indx]=true;
            }
        }
    }
    return true;
}
bool recurisesudo(vector<vector<char> > &board,int row,int col){
        if(row>=sodusize)return true;
        if(col>=sodusize){
            return recurisesudo(board,row+1,0);
        }
        if(board[row][col]!='.'){
            return recurisesudo(board,row,col+1);
        }
        for(int i=0;i<9;i++){
             int area=(row/3)*3+col/3;
            if(colmask[row][i]||rowmask[col][i]||areamask[area][i])continue;
                board[row][col]=i+'1';
               colmask[row][i]=rowmask[col][i]=areamask[area][i]=true;
                if(recurisesudo(board,row,col+1)){
                    return true;
                }
                board[row][col]='.';
                 colmask[row][i]=rowmask[col][i]=areamask[area][i]=false;
            
        }
        return false;
}
void solveSudoku(vector<vector<char> > &board) {
   if(initsudo(board)){
        recurisesudo(board,0,0);
   }
}

};
```

