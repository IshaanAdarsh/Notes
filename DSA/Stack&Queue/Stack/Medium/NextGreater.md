# Next Greater Element

## Brute Force:
- Just run 2 loops
```
/*
Time Complexity: O(N^2)
*/
for(0->n-1){
    for(i+1->n-1){
        if(a[i]<a[j]){
            nge[i]=a[i];
            break;
        }
        nge[i]=-1;
    }
}
```

## Efficient Algorithm (Stack Approach):
- We iterate from the back
    - If stack is empty we push the element
    - If not, then we compare the top with the current element
        - If top is greater we store the top into the vector and push the element into the stack
        - If not then we pop the stack until we find a greater element and then store it in the vector and push the element.

- To implement circular array we use [1%n],
as if n = 5 then 6 will point to 1.

```
vector < int > nextGreaterElements(vector < int > & nums) {
      int n = nums.size();
      vector < int > nge(n, -1);
      stack < int > st;
      for (int i = 2 * n - 1; i >= 0; i--) {
        while (!st.empty() && st.top() <= nums[i % n]) {
          st.pop();
        }

        if (i < n) {
          if (!st.empty()) nge[i] = st.top();
        }
        st.push(nums[i % n]);
      }
      return nge;
    }
```