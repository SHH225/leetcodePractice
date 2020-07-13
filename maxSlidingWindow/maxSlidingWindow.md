# maxSlidingWindow


#### 题目

给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。

示例:

输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

```

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7

```

你可以假设 *k* 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。

线性时间复杂度内解决。



### CODE
```c++
class Solution {
public:
  //使用双端队列，队列的front始终保持为窗口的最大值，即便弹出了下一个front仍为当前最大。
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> res;
        deque<int> dq;
        for(int i=0;i<nums.size();i++){
          //如果窗口移出，弹出队头
            while(!dq.empty()&&dq.front()==i-k){
                dq.pop_front();
            }
          //如果当前即将入栈节点的数值大于当前队列中的back，弹出 
            while(!dq.empty()&&nums[dq.back()]<nums[i]){
                dq.pop_back();
            }
            dq.push_back(i);
          //从第三个数开始，记录接下来每个窗口的最大数
            if(i>=k-1){
                res.push_back(nums[dq.front()]);
            }
        }
        return res;
    }
};
```

