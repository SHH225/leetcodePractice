# maxValue


#### 题目

* //prob 47 礼物的最大价值



### CODE
```c++
class Solution {
public:
    int maxValue(vector<vector<int>>& grid) {
        int count=0;
        vector<vector<int>> temp(grid.size(),vector<int>(grid[0].size(),0));
        temp[0][0]=grid[0][0];
        int rows=grid.size();
        int cols=grid[0].size();
        for(int i=0;i<rows;i++){
            for(int j=0;j<cols;j++){
                if(i==0&&j>0){
                    temp[i][j]+=grid[i][j]+temp[i][j-1];
                }
                if(j==0&&i>0){
                    temp[i][j]+=grid[i][j]+temp[i-1][j];
                }
                if(i>0&&j>0){
                    temp[i][j]=max(grid[i][j]+temp[i-1][j],grid[i][j]+temp[i][j-1]);
                }
            }
        }
        count=temp[rows-1][cols-1];
        return count;
    }
};
```

