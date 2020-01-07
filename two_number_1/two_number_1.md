# TWO_NUMBER_1

#### HashMap

使用HashMap进行查找时间复杂度为O(1)

**HashMap<K,V>  |  HashMap(int initialCapacity, float loadFactor)**

> initialCapacity为初始容量，loadFactor为加载因子（默认为0.75）


* [底层实现](######底层实现)
* [为何线程不安全](######为何线程不安全)
* 为何默认为0.75
* 为何时间复杂度为O(1)
* 与HashTable区别

###### 底层实现

###### 为何线程不安全
HashMap在put的时候，插入的元素超过了容量（由负载因子决定）的范围就会触发扩容操作，就是rehash，这个会重新将原数组的内容重新hash到新的扩容数组中，在多线程的环境下，存在同时其他的元素也在进行put操作，如果hash值相同，可能出现同时在同一数组下用链表表示，造成闭环，导致在get时会出现死循环，所以HashMap是线程不安全的




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