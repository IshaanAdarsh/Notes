# Min Stack:
> supports push, pop, top, and retrieving the minimum element in constant time.
-  The first element in the pair will store the value and the second element will store the minimum element till now.
- When the first push operation comes in we will push the value and store it as minimum itself in the pair. 
- In the second push operation, we will check if the top element’s minimum is less than the new value. If it is then we will push the value with minimum as the previous top’s minimum. 
- To get the getMin element to take the top’s second element.
```cpp
/*
Time Complexity: O(1)
Space Complexity: O(2N)
*/

class MinStack {
  stack < pair < int, int >> st;

  public:
    void push(int x) {
      int min;
      if (st.empty()) {
        min = x;
      } else {
        min = std::min(st.top().second, x);
      }
      st.push({x,min});
    }

  void pop() {
    st.pop();
  }

  int top() {
    return st.top().first;
  }

  int getMin() {
    return st.top().second;
  }
};
```