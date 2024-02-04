# Maximum Sum Subarray of size K :
Given an array of integers Arr of size N and a number K. Return the maximum sum of a subarray of size K.

## Brute Force:
```cpp
/*
TC : O(N*K) {worst case , k=N}
SC : O(1)
*/
for (i =0 to n-1):
     sum=0;
     for(j=i to i+k-1):
         sum+=arr[j]
         if (j-i+1 == k):      //got window of size k
            update maxi
```

## Optimal Approach(Sliding Window):
- We set the sliding window length == k and then apply the maximum sum condition.
```cpp
/*
TC : O(N)
SC : O(1)
*/

//Simple Approach
long maximumSumSubarray(int k, vector<int> &arr, int n) {
        long i = 0, j = 0;
        long maxi = 0;
        long sum = 0;
        
        while (j < n) {
            sum += arr[j];
            if (j - i + 1 == k) {
                maxi = max(maxi, sum);
                sum -= arr[i];
                i++;
            }
            j++;
        }

        return maxi;
    }

// Another approach
long maximumSumSubarray(int k, vector<int> &arr , int n){
        // code here 
        long sum=0;
        for(int i=0;i<k;i++){
            sum+=arr[i];
        }
        long max_sum=sum;
        
        for(int i=0;i<n-k;i++){
            sum+=arr[i+k]-arr[i];
            if(max_sum<sum) max_sum=sum;
        }
        return max_sum;
    }
```