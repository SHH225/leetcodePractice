# findmincutintwoseq


#### 题目

找出两个有序数组中相差最小的两个数



### CODE
```c++
#include <iostream>
using namespace std;
//输入两个排序数组，找到这两个数组中最接近的两个数字
void findCloseNum(int *a, int lena, int *b, int lenb)
{
    if (lena < 0 || lenb < 0)
        return;
    int st = 0, mincut = INT_MAX, num1, num2;
    if (b[0] > a[lena - 1]) {
        cout << b[0] << " " << a[lena - 1];
        return;
    }
    if (a[0] > b[lenb - 1]) {
        cout << a[0] << " " << b[lena - 1];
        return;
    }
    // two point move
    for (int i = 0, j = 0; i < lena, j < lenb;) {
        if (a[i] == b[j]) {
            cout << a[i] << " " << b[j];
            return;
        }
        if (a[i] > b[j]) {

            if (a[i] <= b[j + 1] && (j + 1) < lenb) {
                // change after compare
                if (b[j + 1] - a[i] < mincut) {
                    mincut = b[j + 1] - a[i];
                    num1 = a[i];
                    num2 = b[j + 1];
                }
                // change before compare
                if (a[i] - b[j] < mincut) {
                    mincut = a[i] - b[j];
                    num1 = b[j];
                    num2 = a[i];
                }
            }
            j++;
        }
        else {
            if (a[i + 1] >= b[j] && (i + 1) < lena) {
                // change after compare
                if (a[i + 1] - b[j] < mincut) {
                    mincut = a[i + 1] - b[j];
                    num1 = b[j];
                    num2 = a[i + 1];
                }
                // change before compare
                if (b[j] - a[i] < mincut) {
                    mincut = b[j] - a[i];
                    num1 = a[i];
                    num2 = b[j];
                }
            }

            i++;
        }
    }
    cout << num1 << " " << num2;
}
int main()
{
    int a[10] = {0, 2, 4, 8, 10, 12, 22, 25, 26, 34};
    int b[10] = {26, 31, 32, 33, 40, 41, 42, 43, 43, 77};
    findCloseNum(a, 10, b, 10);
    cout << endl;
    int d[10] = {0, 2, 4, 8, 10, 12, 22, 100, 101, 102};
    int c[10] = {30, 31, 32, 34, 40, 41, 42, 43, 43, 77};
    findCloseNum(c, 10, d, 10);
    cout << endl;
    int e[10] = {0, 2, 4, 8, 10, 12, 22, 25, 26, 34};
    int f[10] = {40, 41, 42, 43, 43, 77, 78, 79, 89, 87};
    findCloseNum(e, 10, f, 10);
    cout << endl;
    findCloseNum(f, 10, e, 10);
    cout << endl;

    return 0;
}

```

