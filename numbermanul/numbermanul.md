# numbermanul

#### 题目

三种操作

1. 输入两个数X和Y ，讲X和Y所在的集合合并
2. 输入 sec，将X从它所在的集合分离出来
3. 输入 tird，输出 tird所在的集合的正整数个数 



T组数据，每次输入n个数，和m个操作

操作对象为1～n自然数

例：

1 //一组数据

3 7 //三个数 1 2 3  ，7个操作

1 1 2 //操作1 合并 1 2所在集合

3 1 //输出1所在集合整数个数

output：2

### CODE
```c++
#include <iostream>
#include <vector>
using namespace std;
int main()
{
    int T, m, n;
    cin >> T;

    vector<vector<int>> list;

    for (int i = 0; i < T; i++) {
        cin >> n >> m;

        vector<int> count;

        for (int i = 0; i <= n; i++) {
            count.push_back(1);
            vector<int> content;
            content.push_back(i);
            list.push_back(content);
        }

        for (int j = 0; j < m; j++) {
            int manul;
            cin >> manul;
            switch (manul) {
            case 1:
                int x, y;
                cin >> x >> y;
                if (count[x] == 1 && count[y] == 1) {
                    count[x]++;
                    count[y]++;
                    list[x].push_back(y);
                    list[y].push_back(x);
                }
                else if (count[x] > 1 && count[y] == 1) {
                    count[x]++;
                    int len = list[x].size();
                    for (int i = 0; i < len; i++) {
                        list[list[x][i]].push_back(y);
                        count[list[x][i]] = count[x];
                        if (list[x][i] != y)
                            list[y].push_back(list[x][i]);
                    }
                    count[y] = count[x];
                }
                else if (count[y] > 1 && count[x] == 1) {

                    count[y]++;
                    int len = list[y].size();
                    for (int i = 0; i < len; i++) {
                        list[list[y][i]].push_back(x);
                        count[list[y][i]] = count[y];
                        if (list[y][i] != x)
                            list[x].push_back(list[y][i]);
                    }
                    count[x] = count[y];
                }
                else {

                    for (int i = 0; i < list[x].size(); i++) {
                        if (list[x][i] == y)
                            break;
                    }
                    int tmp = count[x];
                    count[x] += count[y];
                    count[y] = count[x];

                    for (int k = 0; k < list[x].size(); k++) {
                        if (list[x][k] == x)
                            continue;
                        for (int i = 0; i < list[y].size(); i++) {
                            list[list[x][k]].push_back(list[y][i]);
                            count[list[y][i]] = count[x];
                        }
                    }

                    for (int k = 0; k < list[y].size(); k++) {
                        if (list[y][k] == y)
                            continue;
                        for (int i = 0; i < list[x].size(); i++) {
                            list[list[y][k]].push_back(list[x][i]);
                            count[list[x][i]] = count[y];
                        }
                    }
                    for (int i = 0; i < list[y].size(); i++) {
                        list[x].push_back(list[y][i]);
                    }

                    for (int i = 0; i < tmp; i++) {
                        list[y].push_back(list[x][i]);
                    }
                }
                break;
            case 2:
                int sec;
                cin >> sec;

                for (int i = 0; i < list[sec].size(); i++) {
                    if (list[sec][i] == sec)
                        continue;
                    count[list[sec][i]]--;
                    vector<int> tempd;
                    for (int j = 0; j < list[list[sec][i]].size(); j++) {

                        if (list[list[sec][i]][j] != sec) {
                            tempd.push_back(list[list[sec][i]][j]);
                        }
                    }

                    int len = tempd.size();
                    int num = list[sec][i];
                    list[list[sec][i]].clear();
                    for (int j = 0; j < len; j++) {
                        list[num].push_back(tempd[j]);
                    }
                }
                list[sec].clear();
                list[sec].push_back(sec);
                count[sec] = 1;
                break;
            case 3:
                int tird;
                cin >> tird;
                cout << count[tird] << endl;
                for (int i = 0; i < list[tird].size(); i++) {
                    cout << list[tird][i] << " ";
                }
                cout << endl;
                break;
            default:
                break;
            }
        }
    }
    return 0;
}
```

