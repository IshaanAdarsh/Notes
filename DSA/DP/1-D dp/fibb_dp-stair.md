# Fibonacci 

## Recursion:
- `f(n)=f(n-1)+f(n-2)`
This is the principle on which fibonacci numbers work

```cpp
/*
Time complexity: O(2^n)
Space complexity: O(2^n)
*/
class Solution {
public:
    int fib(int n) {
        if(n<=1) return n;
        return fib(n-2)+fib(n-1);
    }
};
```

## Using Memoization:
- We don't need to compute values again and again so we use a map to store their values and if the values are called then we return the map values.

```cpp
/*
Time complexity: O(n)
Space complexity: O(n) + O(n)[Array]
*/

// Declare dp[n+1] as a map to store values
vector<int>dp(n+1,-1);
int fib(int n, vector<int> &dp){
    if(n<=1) return n;
    //Add a statement to check
    if(dp[n]!=-1) return dp[n];

    // Store base case in dp
    return dp[n]=fib(n-1,dp)+fib(n-2,dp);
}
```

## Using Tabulation:
- We don't need to compute separately we can do this in the dp map itself to reduce space complexity.

```cpp
/*
Time complexity: O(n)
Space complexity: O(n) as no recursion stack space
*/
int fib(int n) {
    if(n<=1) return n;
    vector<int> dp(n+1,-1);
    // We make the base case tabulated
    int dp[0]=0;
    int dp[1]=1;
    
    //Compute in the map itself
    for(int i=2;i<=n;i++){
        dp[i]=dp[i-1]+dp[i-2];
    }
    return dp[n];
}
```

## Space Optimization:
- We can remove the need for an array as we only need 3 integers
    - `prev` -> tracks (i-1)th number
    - `prev2` -> tracks (i-2)th number
    - `curri` -> the current pointer

```cpp
/*
Time complexity: O(n)
Space complexity: O(1)
*/

int fib(int n){
    int prev2 = 0;
    int prev = 1;
    for(int i =2;i<=n;i++){
        int curri = prev + prev2;
        // move them forward
        prev2 = prev;
        prev = curri
    }
    return prev;
}
```

# Counting Stairs:
- Similar to fibonacci sequence where we just replace a single line -> `when n==0 we return 1` as when we want to go to the 0th stair, then we have only one option.


```cpp
class Solution {
public:
    int climbStairs(int n) {
        vector<int>dp(n+1,-1);
        // Only difference
        dp[0]=1;
        dp[1]=1;
        for(int i =2;i<=n;i++){
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
};
```