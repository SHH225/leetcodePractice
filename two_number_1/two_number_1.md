# TWO_NUMBER_1


#### 题目

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]



#### HashMap

使用HashMap进行查找时间复杂度为O(1)

**HashMap<K,V>  |  HashMap(int initialCapacity, float loadFactor)**

> initialCapacity为初始容量，loadFactor为加载因子（默认为0.75）


* [底层实现](#底层实现)
* [为何线程不安全](#为何线程不安全)
* [为何默认为0.75](#为何默认为0.75)
* [为何时间复杂度为O(1)](#为何时间复杂度为O(1))
* [与HashTable区别](#与HashTable区别)






### CODE
```c++
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		unordered_map<int, int> record;
		for (int i = 0; i < nums.size(); i++) {
			int complement = target - nums[i];
			//查找符合条件数字，若找到即未到结尾，赋值 i 及对应的value的位置
			if (record.find(complement) != record.end()) {
				int res[] = { i, record[complement] };
				return vector<int>(res,res+2);//返回res[0],res[1]也行，这个位置是地址才+2
			}
			record[nums[i]] = i;//记到map上 key-value
		}
        		return {-1,-1};//没找到的返回 
	}
};
```

顺序容器（vector）
关联容器 （map）支持高效的关键字查找访问 （即：<key,value>）![截屏2020-03-01上午10.34.27](https://tva1.sinaimg.cn/large/00831rSTly1gce83t3p34j310q0g2qc4.jpg)




##### 底层实现

底层数据结构是由数组+链表组成链表散列。HashMap先得到key的散列值，在通过扰动函数（减少碰撞次数）得到Hash值，接着通过hash & （n -1 ），n位table的长度，运算后得到数组的索引值。如果当前节点存在元素，则通过比较hash值和key值是否相等，相等则替换，不相等则通过拉链法查找元素，直到找到相等或者下个节点为null

##### 为何线程不安全

HashMap在put的时候，插入的元素超过了容量（由负载因子决定）的范围就会触发扩容操作，就是rehash，这个会重新将原数组的内容重新hash到新的扩容数组中，在多线程的环境下，存在同时其他的元素也在进行put操作，如果hash值相同，可能出现同时在同一数组下用链表表示，造成闭环，导致在get时会出现死循环，所以HashMap是线程不安全的

##### 为何默认为0.75

**Hashtable** 初始容量是11 ，扩容 方式为**2N+1**, **HashMap** 初始容量是16,扩容方式为**2N**　
当哈希表中的条目数超出了加载因子与当前容量的乘积时，则要对该哈希表进行扩容、rehash操作提高空间利用率和 减少查询成本的折中，主要是泊松分布，0.75的话碰撞最小

* 加载因子过高，虽然减少了空间开销，提高了空间利用率，但同时也增加了查询时间成本；
* 加载因子过低，虽然可以减少查询时间成本，但是空间利用率很低，同时提高了rehash操作的次数
* 时间和空间成本上寻求的一种折衷选择

##### 为何时间复杂度为O(1)

在进行查找的过程中需要经过以下过程：
1.判断key，根据key算出索引。
2.根据索引获得索引位置所对应的键值对链表。
3.遍历键值对链表，根据key找到对应的Entry键值对。
4.拿到value

若要使查找的时间复杂度为O(1)，那么需要保证每一步的时间的复杂度都为O(1)，则需要及逆行key值计算，再查找到对应链表时该位置的查找尽可能少，也就是说是查找的时间复杂度为单位数量级是可以的

##### 与HashTable区别

Hashtable既不支持Null key也不支持Null value
Hashtable是线程安全的，它的每个方法中都加入了Synchronize方法。在多线程并发的环境下，可以直接使用Hashtable，不需要自己为它的方法实现同步
Hashtable直接使用对象的hashCode。hashCode是JDK根据对象的地址或者字符串或者数字算出来的int类型的数值。然后再使用除留余数发来获得最终的位置。 然而除法运算是非常耗费时间的。效率很低
HashMap为了提高计算效率，将哈希表的大小固定为了2的幂，这样在取模预算时，不需要做除法，只需要做位运算。位运算比除法的效率要高很多。
