# Maximum of all subarrays of size k:

## Brute Force:
Use 2 loops to calculate the maximum.


## Optimal Solution:
-  When shifting our window, we push the new element in from the rear of our de-queue.
- Every time before entering a new element, we first need to check whether the element present at the front is out of bounds of our present window size. If so, we need to pop that out. 
- We need to check from the rear that the element present is smaller than the incoming element. 
    - If yes, there’s no point storing them and hence we pop them out. (No need to store smaller elements on the left of `j`)
    - The element present at the front would be our largest element.

```cpp
/*
Time Complexity: O(N)
Space Complexity: O(K)
*/
vector < int > maxSlidingWindow(vector < int > & nums, int k) {
  deque < int > dq;
  vector < int > ans;
  for (int i = 0; i < nums.size(); i++) {
    if (!dq.empty() && dq.front() == i - k) dq.pop_front();

    while (!dq.empty() && nums[dq.back()] < nums[i])
      dq.pop_back();

    dq.push_back(i);
    if (i >= k - 1) ans.push_back(nums[dq.front()]);
  }
  return ans;
}
```