# Binary Search:
### [Regular Binary Search:](https://leetcode.com/problems/binary-search/)
- Divide the search space into 2 halves
- Compare the middle element with the target
- Trim down the search space

```cpp
int binarySearch(vector<int>& nums, int target) {
    int n = nums.size(); 
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = low + (high-low) / 2;
        if (nums[mid] == target){
          return mid;
        } 
        else if (target > nums[mid]){
          low = mid + 1;
        }
        else{
          high = mid - 1;
        }
    }
    return -1;
}
```
### [Binary Search that handles duplicate:](https://leetcode.com/problems/search-insert-position/solutions/15101/c-o-logn-binary-search-that-handles-duplicate/)
- Can use lower boundfunction too:
```cpp
\\ The lower_bound() is used to return an iterator pointing to the first element in the range [first, last) which has a value >= target.

int searchInsert(vector<int>& nums, int target) {
        return lower_bound(nums.begin(), nums.end(), target) - nums.begin();
    }
```

```cpp
int searchInsert(vector<int>& nums, int target) {
// Invariant: the desired index is between [low, high+1]
  int low = 0, high = nums.size()-1;
  while (low <= high) {
    int mid = low + (high-low)/2;
    if (nums[mid] < target) low = mid+1;
    else high = mid-1;
  }

        // (1) At this point, low > high. That is, low >= high+1
        // (2) From the invariant, we know that the index is between [low, high+1], so low <= high+1. Follwing from (1), now we know low == high+1.
        // (3) Following from (2), the index is between [low, high+1] = [low, low], which means that low is the desired index
        //     Therefore, we return low as the answer. You can also return high+1 as the result, since low == high+1
        return low;
    }
};
```
