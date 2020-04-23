# clockwiseRead


#### 题目

顺时针打印二维矩阵中的数字



### CODE
```c++
#include <iostream>
using namespace std;

void clockwiseRead(int a[5][5], int rows, int cols)
{
    if (rows <= 0 || cols <= 0)
        return;
    if (a == nullptr)
        return;
    int block = 0, i = 0, j = 0;
    bool readmask[4][5] = {0};
    while (true) {
        while (j < cols && readmask[i][j] == 0) {
            cout << a[i][j] << ",";
            readmask[i][j] = true;
            j++;
        }
        j--;
        i++;
        if (readmask[i][j])
            break;
        while (i < rows && readmask[i][j] == 0) {
            cout << a[i][j] << ",";
            readmask[i][j] = true;
            i++;
        }
        i--;
        j--;
        if (readmask[i][j])
            break;
        while (j >= 0 && readmask[i][j] == 0) {
            cout << a[i][j] << ",";
            readmask[i][j] = true;
            j--;
        }
        j++;
        i--;
        if (readmask[i][j])
            break;
        while (i >= 0 && readmask[i][j] == 0) {
            cout << a[i][j] << ",";
            readmask[i][j] = true;
            i--;
        }
        i++;
        j++;
        if (readmask[i][j])
            break;
    }
}
int main()
{
    int a[4][4] = {
        {1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}, {13, 14, 15, 16}};
    int b[4][5] = {{1, 2, 3, 4, 5},
                   {5, 6, 7, 8, 9},
                   {9, 10, 11, 12, 13},
                   {13, 14, 15, 16, 17}};
    clockwiseRead(b, 4, 5);

    return 0;
}

```

