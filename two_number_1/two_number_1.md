# TWO_NUMBER_1

### POINTS

HashMap的使用



### CODE
```c++
#include<iostream>
#include<vector>
#include<unordered_map>
using namespace std;

class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		unordered_map<int, int> record;
		for (int i = 0; i < nums.size(); i++) {

			int complement = target - nums[i];
			if (record.find(complement) != record.end()) {
				int res[] = { i, record[complement] };
				//cout << res[1]<<res[0];

				return vector<int>(res,res+2);
			}

			record[nums[i]] = i;
		}
        return {-1,-1};
	}

};


int main() {

	Solution su;
	vector<int> nums = { 2,11,15,7};
	int target = 9;
	vector<int> a=su.twoSum(nums, target);
	for (int i = 0; i < a.size();i++) {
		cout << a[i] << " ";
	}
	system("pause");
	return 0;
}
```