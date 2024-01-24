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
        else if (nums[mid] < target){
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

#### Using Binary Search:
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

### Search in Rotated Array:
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

#### Duplicate Elements:
- **edge case: If arr[low] = arr[mid] = arr[high] then the answer will be wrong**
```cpp
// Just add this edge case in the previous solution

        //if mid points the target
        if (arr[mid] == k) return true;

        //Edge case:
        if (arr[low] == arr[mid] && arr[mid] == arr[high]) {
            low = low + 1;
            high = high - 1;
            continue;
        }

        //if left part is sorted:
```

### Minimum in Rotated Sorted Array:
If an array is rotated and sorted, we already know that for every index, one of the 2 halves of the array will always be sorted. Based on this observation, we adopted a straightforward two-step process to eliminate one-half of the rotated sorted array. 
- First, we identify the sorted half of the array. 
- Once found, we determine if the target is located within this sorted half.
  - If not, we eliminate that half from further consideration.
  - Conversely, if the target does exist in the sorted half, we eliminate the other half.
```cpp
int findMin(vector<int>& arr) {
    int low = 0, high = arr.size() - 1;
    int ans = INT_MAX;
    while (low <= high) {
        int mid = (low + high) / 2;
        //search space is already sorted then arr[low] will always be the minimum in that search space:
        if (arr[low] <= arr[high]) {
            ans = min(ans, arr[low]);
            break;
        }

        //if left part is sorted:
        if (arr[low] <= arr[mid]) {
            // keep the minimum:
            ans = min(ans, arr[low]);

            // Eliminate left half:
            low = mid + 1;
        }
        else { //if right part is sorted:

            // keep the minimum:
            ans = min(ans, arr[mid]);

            // Eliminate right half:
            high = mid - 1;
        }
    }
    return ans;
}
```

### How many times the array has been rotated:

**Brute force:**
- ans = INT_MAX , index = -1;
- Next, we will iterate through the array and compare each element with the variable called ‘ans’. Whenever we encounter an element ‘arr[i]’ that is smaller than ‘ans’, we will update ‘ans’ with the value of ‘arr[i]’ and also update the ‘index’ variable with the corresponding index value, ‘i’. Return index.

We will employ the same algorithm to determine the index of the minimum element. In the previous problem, we only stored the minimum element itself. However, in this updated approach, we will additionally keep track of the index. 
```cpp
int findKRotation(vector<int> &arr) {
    int low = 0, high = arr.size() - 1;
    int ans = INT_MAX;
    int index = -1;
    while (low <= high) {
        int mid = (low + high) / 2;
        //search space is already sorted then arr[low] will always be the minimum in that search space:
        if (arr[low] <= arr[high]) {
            if (arr[low] < ans) {
                index = low;
                ans = arr[low];
            }
            break;
        }

        //if left part is sorted:
        if (arr[low] <= arr[mid]) {
            // keep the minimum:
            if (arr[low] < ans) {
                index = low;
                ans = arr[low];
            }

            // Eliminate left half:
            low = mid + 1;
        }
        else { //if right part is sorted:

            // keep the minimum:
            if (arr[mid] < ans) {
                index = mid;
                ans = arr[mid];
            }

            // Eliminate right half:
            high = mid - 1;
        }
    }
    return index;
}
```

### Single Element in a Sorted Array
- If the middle element is at an even index, then the single element must be on the right side of the array, since all the elements on the left side should come in pairs.
- Similarly, if the middle element is at an odd index, then the single element must be on the left side of the array.

> Another interesting observation you might have made is that this algorithm will still work even if the array isn't fully sorted. As long as pairs are always grouped together in the array (for example, [10, 10, 4, 4, 7, 11, 11, 12, 12, 2, 2]), it doesn't matter what order they're in. Binary search worked for this problem because we knew the subarray with the single number is always odd-lengthed, not because the array was fully sorted numerically

```cpp
int singleNonDuplicate(vector<int>& nums) {
        int left = 0, right = nums.size() - 1;
        while (left < right) {
            int mid = (left + right) / 2;
            if (mid % 2 == 1) {
                mid--;
            }
            if (nums[mid] != nums[mid + 1]) {
                right = mid;
            } else {
                left = mid + 2;
            }
        }
        return nums[left];
}
```

### Find Peak Element:
- Assume only one peak
>If an index is a common point where a decreasing sequence ends and an increasing sequence begins, we can actually eliminate either the left or right half. Because both halves of such an index contain a peak.

```cpp
int findPeakElement(vector<int> &arr) {
    int n = arr.size(); 

    // Edge cases:
    if (n == 1) return 0;
    if (arr[0] > arr[1]) return 0;
    if (arr[n - 1] > arr[n - 2]) return n - 1;

    int low = 1, high = n - 2;
    while (low <= high) {
        int mid = (low + high) / 2;

        //If arr[mid] is the peak:
        if (arr[mid - 1] < arr[mid] && arr[mid] > arr[mid + 1])
            return mid;

        // If we are on the left:
        if (arr[mid] > arr[mid - 1]) low = mid + 1;

        // If we are in the right or, arr[mid] is a common point:
        else high = mid - 1;
    }
    return -1;
}
```
