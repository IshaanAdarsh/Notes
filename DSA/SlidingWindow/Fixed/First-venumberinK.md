# First Negative Number in every Window of Size K:
Given an array A[] of size N and a positive integer K, find the first negative integer for each and every window(contiguous subarray) of size K.

## Brute Force(Nested Loops):
```cpp
/*
TC : O(N*K) {worst case , k=N}
SC : O(N-k-1) {No. of windows}
*/

// generate window of size k with the help of nested loops , store 1st negative element of every window.
for(i=0 to n-1):
     for(j=i to i+k-1):
         if(arr[j] < 0 )  : ans.push_back(arr[j]) , break;
```
- This approach is repetitive as we check if the same number is -ve multiple times.

## Optimal Approach(Sliding Window):
- 
```cpp

```
