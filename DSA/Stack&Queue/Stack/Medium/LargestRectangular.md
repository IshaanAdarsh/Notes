# Area of largest rectangle in Histogram:

## Brute Force:
Try out every histogram block as a particular rectangle 

```cpp
/*
Time Complexity: O(N*N ) 
Space Complexity: O(1)
*/
int largestarea(int arr[], int n) {
  int maxArea = 0;
  for (int i = 0; i < n; i++) {
    int minHeight = INT_MAX;
    for (int j = i; j < n; j++) {
      minHeight = min(minHeight, arr[j]);
      maxArea = max(maxArea, minHeight * (j - i + 1));
    }
  }
  return maxArea;
}
```

## Efficient Approach:
- We take a particular block and find the block on its right and left which is smaller than it.
    - Width = |left smaller - right smaller|
    - Area = Width * ht. of block

```cpp
/*
Time Complexity: O(N) 
Space Complexity: O(3N)
*/
int largestRectangleArea(vector < int > & heights) {
      int n = heights.size();
      stack < int > st;
      int leftsmall[n], rightsmall[n];

      //find left smaller index  
      for (int i = 0; i < n; i++) {
        while (!st.empty() && heights[st.top()] >= heights[i]) {
          st.pop();
        }
        if (st.empty())
          leftsmall[i] = 0;
        else
          leftsmall[i] = st.top() + 1;
        st.push(i);
      }
      // clear the stack to be re-used
      while (!st.empty())
        st.pop();

      //find right smaller index  
      for (int i = n - 1; i >= 0; i--) {
        while (!st.empty() && heights[st.top()] >= heights[i])
          st.pop();

        if (st.empty())
          rightsmall[i] = n - 1;
        else
          rightsmall[i] = st.top() - 1;

        st.push(i);
      }

      // Compute area
      int maxA = 0;
      for (int i = 0; i < n; i++) {
        maxA = max(maxA, heights[i] * (rightsmall[i] - leftsmall[i] + 1));
      }
      return maxA;
    }
};
```

## Best Approach:
> It uses only one pass of the vector
- In this we compute the area in the single traversal itself
```
int largestRectangleArea(vector < int > & histo) {
      stack < int > st;
      int maxA = 0;
      int n = histo.size();
      for (int i = 0; i <= n; i++) {
        while (!st.empty() && (i == n || histo[st.top()] >= histo[i])) {
          int height = histo[st.top()];
          st.pop();
          int width;
          if (st.empty())
            width = i;
          else
            width = i - st.top() - 1;
          maxA = max(maxA, width * height);
        }
        st.push(i);
      }
      return maxA;
    }
```