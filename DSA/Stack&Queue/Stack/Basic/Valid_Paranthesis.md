# Valid Parenthesis:
- Opening bracket we will push it.
- Closing bracket we will check if the stack is non-empty or not.
    - If the stack is empty we will return false
    - If it is nonempty then we will check if the topmost element of the stack is the opposite pair of the closing bracket or not.
        - If it is not the opposite pair of the closing bracket then return false
        - else move ahead.

- After we move out of the string the stack has to be empty if it is non-empty then return it as invalid else it is a valid string.

```cpp
/*
Time Complexity: O(N)
Space Complexity: O(N)
*/

bool isValid(string s) {
        stack<char>st; 
        for(auto it: s) {
            if(it=='(' || it=='{' || it == '[') st.push(it); 
            else {
                if(st.size() == 0) return false; 
                char ch = st.top(); 
                st.pop(); 
                if((it == ')' and ch == '(') or  (it == ']' and ch == '[') or (it == '}' and ch == '{'))
                continue;
                else return false;
            }
        }
        return st.empty(); 
    }
```

## Longest Valid Parenthesis:

```cpp
int longestValidParentheses(string s) {
    stack<int>stk;
    stk.push(-1);
    int ans = 0;
    for(int i = 0 ; i < s.size();  i++)
    {
        if(s[i] == '(')
            stk.push(i);
        else
        {
            if(stk.size() == 1)
                stk.top() = i;
            else
            {
                stk.pop();
                ans = max(ans , i - stk.top());
            }
        }
    }
    return ans;
}
```

### Dry Run:
- `)()())`

| Index | Character | Operation | Stack         | Result |
|-------|-----------|-----------|---------------|--------|
| 0     | (         | Push      | [-1, 0]       | 0      |
| 1     | (         | Push      | [-1, 0, 1]    | 0      |
| 2     | )         | Pop       | [-1, 0]       | 2      |
| 3     | (         | Push      | [-1, 0, 3]    | 2      |
| 4     | )         | Pop       | [-1, 0]       | 4      |
| 5     | )         | Pop       | [-1]          | 6      |
| 6     | (         | Push      | [-1, 6]       | 6      |
| 7     | )         | Push      | [-1, 6, 7]    | 6      |
| 8     | )         | Pop       | [-1, 6]       | 6      |
