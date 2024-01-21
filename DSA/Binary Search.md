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
### lower_bound:
- The lower bound is -> smallest index (ind) , where arr[ind] >= x.
- But if any such index is not found, the lower bound algorithm returns n i.e. size of the given array.
```cpp
int lowerBound(vector<int> arr, int n, int x) {
    int low = 0, high = n - 1;
    int ans = n;

    while (low <= high) {
        int mid = (low + high) / 2;
        // maybe an answer
        if (arr[mid] >= x) {
            ans = mid;
            //look for smaller index on the left
            high = mid - 1;
        }
        else {
            low = mid + 1; // look on the right
        }
    }
    return ans;
}
```

#### STL:
```
lower_bound(nums.begin(), nums.end(), target) - nums.begin();
```

### upper_bound:
- The upper bound -> smallest index (ind) , where arr[ind] > x.
```cpp
int upperBound(vector<int> &arr, int x, int n) {
    int low = 0, high = n - 1;
    int ans = n;

    while (low <= high) {
        int mid = (low + high) / 2;
        // maybe an answer
        if (arr[mid] > x) {
            ans = mid;
            //look for smaller index on the left
            high = mid - 1;
        }
        else {
            low = mid + 1; // look on the right
        }
    }
    return ans;
}
```
#### STL:
```
upper_bound(nums.begin(), nums.end(), target) - nums.begin();
```

### Ceil and Floor using BS:
- **Ceil: Smallest number in array >= target** -> lower_bound of the array
- **Floor: Larget number in array <= target**

```cpp
int findFloor(int arr[], int n, int x) {
	int low = 0, high = n - 1;
	int ans = -1;

	while (low <= high) {
		int mid = (low + high) / 2;
		// maybe an answer
		if (arr[mid] <= x) {
			ans = arr[mid];
			//look for smaller index on the left
			low = mid + 1;
		}
		else {
			high = mid - 1; // look on the right
		}
	}
	return ans;
}
```

### [Search Insert Position:](https://leetcode.com/problems/search-insert-position/solutions/15101/c-o-logn-binary-search-that-handles-duplicate/)
- Can use lower bound function too:
```cpp
\\ The lower_bound() is used to return an iterator pointing to the first element in the range [first, last) which has a value >= target.

int searchInsert(vector<int>& nums, int target) {
        return lower_bound(nums.begin(), nums.end(), target) - nums.begin();
    }
```

- **Easy to understand:**
  - If the target is found well and good then we return said index.
  - But if the target is not found, the place where the low and high pointers switch over is the index to be returned.
    - We need to understand what binary search does, it closes in on the target variable, but if the target variable is not present it switches at its nearest value.
      - The low indicates the value is just greater than it
      - The high indicates the value is smaller than it
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
        // (2) From the invariant, we know that the index is between [low, high+1], so low <= high+1. Following from (1), now we know low == high+1.
        // (3) Following from (2), the index is between [low, high+1] = [low, low], which means that low is the desired index
        //     Therefore, we return low as the answer. You can also return high+1 as the result, since low == high+1
        return low;
    }
};
```

### First and Last Position:
- In a normal case we need to return [lower_bound, upper_bound-1], but this fails in the case:
  - If the number is not present -> [upper bound - 1] will not point to the number
  - If the number is greater than the greatest number and upper_bound == n -> not a real location to check its value.

#### Using lb and ub:
- Time Complexity: 2*O(log n)
- Space Complexity: O(1)
```cpp
pair<int, int> firstAndLastPosition(vector<int>& arr, int n, int k) {
    int lb = lowerBound(arr, n, k);
    if (lb == n || arr[lb] != k) return { -1, -1};
    int ub = upperBound(arr, n, k);
    return {lb, ub - 1};
}
```

#### Binary Search:
```cpp
int firstPos(vector<int>& nums, int target){
        int n = nums.size();
        int low =0, high = n-1;
        int ans = -1;
        while(low<=high){
            int mid = (low+high)/2;
            if(nums[mid]==target){
                ans = mid;
                high = mid -1;
            }
            else if(nums[mid]<target){
                low = mid+1;
            }
            else{
                high = mid - 1;
            }
        }
        return ans;
    }
    int lastPos(vector<int>& nums, int target){
        int n = nums.size();
        int low =0, high = n-1;
        int ans = -1;
        while(low<=high){
            int mid = (low+high)/2;
            if(nums[mid]==target){
                ans = mid;
                low = mid+1;
            }
            else if(nums[mid]<target){
                low = mid+1;
            }
            else{
                high = mid - 1;
            }
        }
        return ans;
    }
    vector<int> searchRange(vector<int>& nums, int target) {
        int f = firstPos(nums,target);
        if (f == -1) return { -1, -1};
        int l = lastPos(nums,target);
        return {f,l};
    }
```

### Search in Sorted Array:
#### Unique Elements:
To efficiently search for a target value using this observation, we will follow a simple two-step process. 
- First, we identify the sorted half of the array. 
- Once found, we determine if the target is located within this sorted half.
  - If not, we eliminate that half from further consideration.
  - Conversely, if the target does exist in the sorted half, we eliminate the other half.

```cpp
int search(vector<int>& arr, int n, int k) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == k) return mid;

        //left half sorted:
        if (arr[low] <= arr[mid]) {
            if (arr[low] <= k && k <= arr[mid]) {
                //element exists:
                high = mid - 1;
            }
            else {
                //element does not exist:
                low = mid + 1;
            }
        }
	//right half sorted:
        else { 
            if (arr[mid] <= k && k <= arr[high]) {
                //element exists:
                low = mid + 1;
            }
            else {
                //element does not exist:
                high = mid - 1;
            }
        }
    }
    return -1;
}
```
