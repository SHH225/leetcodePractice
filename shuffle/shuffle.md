# shuffle

#### 题目

打乱一个没有重复元素的数组。

示例:

// 以数字集合 1, 2 和 3 初始化数组。
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// 打乱数组 [1,2,3] 并返回结果。任何 [1,2,3]的排列返回的概率应该相同。
solution.shuffle();

// 重设数组到它的初始状态[1,2,3]。
solution.reset();

// 随机返回数组[1,2,3]打乱后的结果。
solution.shuffle();



### CODE
```c++
class Solution {
public:
    Solution(vector<int>& nums): _nums(nums), _solution(nums) {
            srand(time(NULL));//以机器时间作为随机种子，是的随机不重复
    }
    
    /** Resets the array to its original configuration and return it. */
    vector<int> reset() {
        return _solution=_nums;
    }
    
    /** Returns a random shuffling of the array. */
    vector<int> shuffle() {
        int n=_solution.size();
        while(--n>0){
            int j=rand()%(n+1);
            swap(_solution[n],_solution[j]);
        }
        return _solution;
    }
private:
     vector<int> _nums,_solution;
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(nums);
 * vector<int> param_1 = obj->reset();
 * vector<int> param_2 = obj->shuffle();
 */
```

这道题注意 c++的类的使用 以及随机数的使用 ，随即种子的设定 

要取得 [a,b) 的随机整数，使用 (rand() % (b-a))+ a;

要取得 [a,b] 的随机整数，使用 (rand() % (b-a+1))+ a;

要取得 (a,b] 的随机整数，使用 (rand() % (b-a))+ a + 1;