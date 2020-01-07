# TWO_NUMBER_1

#### HashMap

使用HashMap进行查找时间复杂度为O(1)

**HashMap<K,V>  |  HashMap(int initialCapacity, float loadFactor)**

> initialCapacity为初始容量，loadFactor为加载因子（默认为0.75）


* 底层实现
* 为何线程不安全
* 为何默认为0.75
* 为何时间复杂度为O(1)
* 与HashTable区别





### CODE
```c++
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		unordered_map<int, int> record;
		for (int i = 0; i < nums.size(); i++) {
			int complement = target - nums[i];
			if (record.find(complement) != record.end()) {
				int res[] = { i, record[complement] };
				return vector<int>(res,res+2);
			}
			record[nums[i]] = i;
		}
        		return {-1,-1};
	}
};
```