# Frog Jump - 1:
If only fog can jump 1 pr 2 steps

## Recursion:
- We find the 2 cases which can happen and return them recursively
    - 1 jump 
    - 2 jump 
```cpp
int solve(int ind, vector<int>& height){
    if(ind==0) return 0;
    int jumpTwo = INT_MAX;
    // Recursive call + energy used in current jump
    int jumpOne= solve(ind-1, height)+ abs(height[ind]-height[ind-1]);
    if(ind>1)
        jumpTwo = solve(ind-2, height)+ abs(height[ind]-height[ind-2]);
    
    return min(jumpOne, jumpTwo);
}

```

## Memoization:
```cpp
int solve(int ind, vector<int>& height, vector<int>& dp){
    if(ind==0) return 0;
    if(dp[ind]!=-1) return dp[ind];
    int jumpTwo = INT_MAX;
    int jumpOne= solve(ind-1, height,dp)+ abs(height[ind]-height[ind-1]);
    if(ind>1)
        jumpTwo = solve(ind-2, height,dp)+ abs(height[ind]-height[ind-2]);
    
    return dp[ind]=min(jumpOne, jumpTwo);
}
```

## Tabulation:
- Declare a dp[] array of size n.
- Initialize the base condition values, i.e dp[0] as 0.
```cpp
vector<int> height{30,10,60,10,60,50};
  int n=height.size();
  vector<int> dp(n,-1);
  dp[0]=0;
  for(int ind=1;ind<n;ind++){
      int jumpTwo = INT_MAX;
        int jumpOne= dp[ind-1] + abs(height[ind]-height[ind-1]);
        if(ind>1)
            jumpTwo = dp[ind-2] + abs(height[ind]-height[ind-2]);
    
        dp[ind]=min(jumpOne, jumpTwo);
  }
  cout<<dp[n-1];
```

## Space Optimization:
- Values required at every iteration,
`dp[i], dp[i-1], dp[i-2]`

```cpp
int main() {
  vector<int> height{30,10,60,10,60,50};
  int n=height.size();
  int prev=0;
  int prev2=0;
  for(int i=1;i<n;i++){
      
      int jumpTwo = INT_MAX;
      int jumpOne= prev + abs(height[i]-height[i-1]);
      if(i>1)
        jumpTwo = prev2 + abs(height[i]-height[i-2]);
    
      int cur_i=min(jumpOne, jumpTwo);
      prev2=prev;
      prev=cur_i;
        
  }
  cout<<prev;
}
```

# Frog Jump - k Distances:
The frog is allowed to jump up to ‘K’ steps at a time. If K=4, the frog can jump 1,2,3, or 4 steps at every index.

## Memoization:
- We are making K calls, therefore, we can set a for loop to run from 1 to K, and in each iteration.

```cpp
/*
Time Complexity: O(N *K)
Space Complexity: O(N)
*/
int solveUtil(int ind, vector<int>& height, vector<int>& dp, int k) {
    // Base case: If we are at the beginning (index 0), no cost is needed.
    if (ind == 0) return 0;
    
    // If the result for this index has been previously calculated, return it.
    if (dp[ind] != -1) return dp[ind];
    
    int mmSteps = INT_MAX;
    
    // Loop to try all possible jumps from '1' to 'k'
    for (int j = 1; j <= k; j++) {
        // Ensure that we do not jump beyond the beginning of the array
        if (ind - j >= 0) {
            // Calculate the cost for this jump and update mmSteps with the minimum cost
            int jump = solveUtil(ind - j, height, dp, k) + abs(height[ind] - height[ind - j]);
            mmSteps = min(jump, mmSteps);
        }
    }
    
    // Store the minimum cost for this index in the dp array and return it.
    return dp[ind] = mmSteps;
}
```

## Tabulation:
```cpp
/*
Time Complexity: O(N*K)
Space Complexity: O(N)
*/

int solveUtil(int n, vector<int>& height, vector<int>& dp, int k) {
    dp[0] = 0;

    // Loop through the array to fill in the dp array
    for (int i = 1; i < n; i++) {
        int mmSteps = INT_MAX;

        // Loop to try all possible jumps from '1' to 'k'
        for (int j = 1; j <= k; j++) {
            if (i - j >= 0) {
                int jump = dp[i - j] + abs(height[i] - height[i - j]);
                mmSteps = min(jump, mmSteps);
            }
        }
        dp[i] = mmSteps;
    }
    return dp[n - 1]; // The result is stored in the last element of dp
}
```
