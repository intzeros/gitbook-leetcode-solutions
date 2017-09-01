# 47. Permutations II

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example,
`[1,1,2]` have the following unique permutations:

```
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```



有重复元素的全排列。

<pre>

[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]

</pre>





仅加该条件是无法完全去重的: if(i != from && nums[i] == nums[from]) continue;

解法1: 用 set.
最后 vector<vector<int>>(set.begin(), set.end());

```cpp
class Solution {
public:
    vector<vector<int>> rst;
    
    void solve(int from, vector<int>& nums){
        int n = nums.size();
        if(from == n){
            rst.push_back(nums);
            return;
        }
        for(int i = from; i < n; i++){
            if(i != from && nums[from] == nums[i]) continue;
            if(i > from && nums[i] == nums[i-1]) continue;
            swap(nums[from], nums[i]);
            solve(from+1, nums);
            swap(nums[from], nums[i]);
        }
    }
    
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        solve(0, nums);
        return rst;
    }
};
```

