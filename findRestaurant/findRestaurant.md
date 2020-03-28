# findRestaurant

#### 题目

假设Andy和Doris想在晚餐时选择一家餐厅，并且他们都有一个表示最喜爱餐厅的列表，每个餐厅的名字用字符串表示。

你需要帮助他们用**最少的索引和**找出他们**共同喜爱的餐厅**。 如果答案不止一个，则输出所有答案并且不考虑顺序。 你可以假设总是存在一个答案。

**示例 1:**

```
输入:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
输出: ["Shogun"]
解释: 他们唯一共同喜爱的餐厅是“Shogun”。
```

**示例 2:**

```
输入:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
输出: ["Shogun"]
解释: 他们共同喜爱且具有最小索引和的餐厅是“Shogun”，它有最小的索引和1(0+1)。
```

#### CODE

```c++
class Solution {
public:
    vector<string> findRestaurant(vector<string>& list1, vector<string>& list2) {
        unordered_map<string,int> s1;
        for(int i=0;i<list1.size(); i++)
            s1[list1[i]]=i;
        vector<string> fav;
        string tmp;
        int minindex=INT_MAX;
        for(int i=0;i<list2.size() ;i++){
            if(s1.find(list2[i])!=s1.end()){
                if(s1[list2[i]]+i<minindex){
                    vector<string>().swap(fav);
                    minindex=s1[list2[i]]+i;
                    fav.push_back(list2[i]);
                }else if(s1[list2[i]]+i==minindex){
                    fav.push_back(list2[i]);
                }
            }
        }
       
        return fav;
    }
};
```
