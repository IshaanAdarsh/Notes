# Sliding Window Maximum:

## Brute Force:
- We initially keep a left and right pointer to fix our window to a size of k. 
- We compute the maximum element present in this window using the GetMax function. 
- Update the left and right pointer by left++ and right++ every time to get to a new window of size k using a while loop. 

```cpp
/*
Time Complexity: O(N^2)
Space Complexity: O(K) 
*/
void GetMax(vector < int > nums, int l, int r, vector < int > & arr) {
  int i, maxi = INT_MIN;
  for (i = l; i <= r; i++)
    maxi = max(maxi, nums[i]);
  arr.push_back(maxi);
}
vector < int > maxSlidingWindow(vector < int > & nums, int k) {
  int left = 0, right = 0;
  int i, j;
  vector < int > arr;
  while (right < k - 1) {
    right++;
  }
  while (right < nums.size()) {
    GetMax(nums, left, right, arr);
    left++;
    right++;
  }
  return arr;
}
```

## Efficient Solution:
- Checking whether the incoming element is larger than the already present elements. This could be implemented with the help of a de-queue.

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