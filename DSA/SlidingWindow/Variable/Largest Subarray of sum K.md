# Largest Subarray of sum K:

## Case 1: Only positive numbers:
- We simply calculate the sum by adding `a[j]`:
    - If sum>k we run a while loop to reduce sum by removing a[i]
    - If sum==k we save the window size if its greater than maxi

```cpp
int lenOfLongSubarr(int a[],  int n, int k){ 
    int i =0, j =0;
    int sum = 0, maxi = 0;
    while(j<n){
        sum+=a[j];
        if(sum>k){
            while(sum>k){
                sum -= a[i];
                i++;
            }            
        }
        else if(sum==k){
            maxi = max(maxi,j-i+1);
            sum-= a[i];
            i++;
        }
    j++;
    }
    return maxi;
} 
```

This doesn't work for -ve numbers as:

Here we assumed that once the sum of elements within the window becomes greater than 5 then increasing the window size will just add to the sum and hence we will not attain the sum 5 again. This is true when all the element are positive and hence reducing the window size by doing i++ makes sense.

## Case 2: Both positive and Negative numbers: (Prefix sum + Variable Sliding Window)
- Map to store the prefix sums and the indices.
    - We will add the current element i.e. a[i] to the prefix sum.
        - If the sum is equal to k, we should consider the length of the current subarray i.e. i+1. We will compare this length with the existing length and consider the maximum one.
        - If the sum does not exist in the map we will add that with the current index into the map.
        
    - We will calculate the prefix sum i.e. x-k, of the remaining subarray.
        - If that sum of the remaining part i.e. x-k exists in the map, we will calculate the length i.e. i-preSumMap[x-k], and consider the maximum one comparing it with the existing length we have achieved until now.
        
        
> [Edge Case] We are checking the map before insertion because we want the index to be as minimum as possible and so we will consider the earliest index where the sum x-k has occurred.

```cpp
int getLongestSubarray(vector<int>& a, int k) {
    int n = a.size(); // size of the array.

    map<int, int> preSumMap;
    int sum = 0;
    int maxLen = 0;
    for (int i = 0; i < n; i++) {
        //calculate the prefix sum till index i:
        sum += a[i];

        // if the sum = k, update the maxLen:
        if (sum == k) {
            maxLen = max(maxLen, i + 1);
        }

        // calculate the sum of remaining part i.e. x-k:
        int rem = sum - k;

        //Calculate the length and update maxLen:
        if (preSumMap.find(rem) != preSumMap.end()) {
            int len = i - preSumMap[rem];
            maxLen = max(maxLen, len);
        }

        //Finally, update the map checking the conditions:
        if (preSumMap.find(sum) == preSumMap.end()) {
            preSumMap[sum] = i;
        }
    }

    return maxLen;
}
```