# maxArea


#### 题目

给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器，且 n 的值至少为 2。

<img src="https://tva1.sinaimg.cn/large/00831rSTly1gcmh0128rej30m90anwep.jpg" alt="question_11" style="zoom:50%;" />

图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

示例：

输入：[1,8,6,2,5,4,8,3,7]
输出：49

### CODE
```c++
class Solution {
public:
    int min(int a,int b){
        return a<b?a:b;
    }
    int maxArea(vector<int>& height) {
        int totalmax=0;
        int len=height.size();
       int i=0,j=len-1;
       while(i<j){
           int v=(j-i)*min(height[i],height[j]);
           if(v>totalmax)totalmax=v;
           if(height[i]>=height[j]){
               j--;
            }else{
                i++;
            }
       }
          return totalmax;
    }
};
```

