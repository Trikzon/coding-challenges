# Contains Duplicate
Easy problem from [Blind 75](../) on [LeetCode](https://leetcode.com/problems/contains-duplicate/).

## Eurekas!
- In C++, an `std::unordered_set` has about constant-time complexity while a `std::set` has logarithmic complexity.
- In C++, sorting a list in-place instead of allocating more memory improves performance significantly.

## Solutions
### C++
#### First Attempt
```cpp
bool containsDuplicate(vector<int>& nums) {
	// Create a set from the vector and compare their sizes because a set
	// only contains unique entries.
	int unique = set<int>(nums.begin(), nums.end()).size();
	return nums.size() < unique;
}
// This is slower and more memory intensive than the majority of solutions.
```

#### Second Attempt
```cpp
bool containsDuplicate(vector<int>& nums) {
	// Eureka! Using an unordered_set decreased runtime significantly.
	int unique = unordered_set<int>(nums.begin(), nums.end()).size();
	return nums.size() < unique;
}
```

#### Third Attempt
```cpp
bool containsDuplicate(vector<int>& nums) {
	// Instead of converting the entire vector to a set, I tried keeping
	// track of seen elements.
	unordered_set<int> seen;
	for (int i = 0; i < nums.size(); i++) {
		if (seen.count(nums[i]) > 0)	
			return true;
		seen.insert(nums[i]);
	}
	return false;
}
// However, this only marginally decreased memory usage.
```

#### Fourth Attempt
```cpp
// Maybe sets aren't the answer to this one 🤔
bool containsDuplicate(vector<int>& nums) {
	// Instead of allocating memory for a set, we sort the vector.
	sort(nums.begin(), nums.end());
	// Then see if any adjacent elemnts are the same.
	for (int i = 1; i < nums.size(); i++)
		if (nums[i - 1] == nums[i])
			return true;
	return false;
}
// Eureka! This solution significantly decreases runtime and memory usage.
```
