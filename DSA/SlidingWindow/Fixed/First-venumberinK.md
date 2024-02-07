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
- For each window, the function finds the first negative integer within the window and stores it in a vector `v`. 

- If no negative integer is found in the current window, it stores 0 in the vector. The function iterates through the array, updating the deque to maintain the elements within the current window and efficiently find the first negative integer for each window. 

- Finally, the vector containing the first negative integers for each window is returned.
```cpp
vector<long long> printFirstNegativeInteger(long long int A[], long long int N, long long int K) {
                                                 
    deque<long long int> dq;
    for(int i=0;i<K;i++){
        // process first window and insert index in deque
        if(A[i]<0){
            dq.push_back(i);
        }
    }
    // stores answer of first window in vector
    vector<long long> v;
    if(dq.size()>0){
        v.push_back(A[dq.front()]);
    }else{
        v.push_back(0);
    }
    for(int i=K;i<N;i++){
        //pop element in deque if it is not in the current window
        if(!dq.empty() && i-dq.front()>=K){
            dq.pop_front();
        }
        //push element
        if(A[i]<0){
            dq.push_back(i);
        }
        //stores answer
        if(dq.size()>0){
        v.push_back(A[dq.front()]);
    }else{
        v.push_back(0);
    }
    }
     return v;                                            
 }
```
