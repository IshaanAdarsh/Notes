# Longest Substring With K Unique Characters:
Given a string you need to print the size of the longest possible substring that has exactly K unique characters. If there is no possible substring then print -1.


## Sliding Window:
- We just maintain a map to count the number of unique elements in the string using map size and adjust the size of the window accordingly:
    - If `k<map.size()` we will remove the elements from the `i` index until `k==mapsize()`

```cpp
int longestKSubstr(string s, int k) {
        int n = s.size();
        int i =0,j=0;
        int maxi = -1;
        map<int,int>mp;
        while(j<n){
            mp[s[j]]++;
            if(mp.size()==k){
                maxi = max(maxi,j-i+1);
            }
            else if(mp.size()>k){
                while(mp.size()>k){
                    mp[s[i]]--;
                    if(mp[s[i]]==0){
                        mp.erase(s[i]);
                    }
                    i++;
                }
            }
            j++;
        }
        
        return maxi;
    }
```

