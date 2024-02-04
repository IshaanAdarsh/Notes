# Longest Substring Without Repeating Characters:

## Naive Approach:
- Two loops one for traversing the string and another loop – nested loop for finding different substrings and after that, we will check for all substrings one by one and check for each and every element if the element is not found then we will store that element in HashSet otherwise we will break from the loop and count it.
```cpp
/*
Time Complexity: O(N^2)
Space Complexity: O(N) 
*/
int solve(string str) {

  if(str.size()==0)
      return 0;
  int maxans = INT_MIN;
  for (int i = 0; i < str.length(); i++) // outer loop for traversing the string
  {
    unordered_set < int > set;
    for (int j = i; j < str.length(); j++) // nested loop for getting different string starting with str[i]
    {
      if (set.find(str[j]) != set.end()) // if element if found so mark it as ans and break from the loop
      {
        maxans = max(maxans, j - i);
        break;
      }
      set.insert(str[j]);
    }
  }
  return maxans;
}
```

## Efficient Approach:
- We use the 2 pointer approach
- Pointer ‘left’ is used for maintaining the starting point of the substring while ‘right’ will maintain the endpoint of the substring.
- Right’ pointer will move forward and check for the duplicate occurrence of the current element if found then the ‘left’ pointer will be shifted ahead so as to delete the duplicate elements.

```cpp
/*
Time Complexity: O(2N)
Space Complexity: O(N) 
*/
int solve(string str) {

  if(str.size()==0)
      return 0;
  int maxans = INT_MIN;
  unordered_set < int > set;
  int l = 0;
  for (int r = 0; r < str.length(); r++) // outer loop for traversing the string
  {
    if (set.find(str[r]) != set.end()) //if duplicate element is found
    {
      while (l < r && set.find(str[r]) != set.end()) {
        set.erase(str[l]);
        l++;
      }
    }
    set.insert(str[r]);
    maxans = max(maxans, r - l + 1);
  }
  return maxans;
}
```

Problem with this approach is that l has to move one step at a time and if there are 2 consecutive repeating elements it has to move n time, to solve this we can just make l jump to the (last index know for the char +1)

## Optimal Approach:
- A map that will take care of counting the elements and maintaining the frequency of each and every element as a unity by taking the latest index of every element.

```cpp
/*
Time Complexity: O(N)
Space Complexity: O(N) 
*/
int lengthofLongestSubstring(string s) {
      vector < int > mpp(256, -1);

      int left = 0, right = 0;
      int n = s.size();
      int len = 0;
      while (right < n) {
        if (mpp[s[right]] != -1)
          left = max(mpp[s[right]] + 1, left);

        mpp[s[right]] = right;

        len = max(len, right - left + 1);
        right++;
      }
      return len;
    }
```