# Count Occurrences Of Anagrams:

- In this problem the sliding window is not clear but we can see
    - `k = anagram.length()`
    - We need to find substrings in the main string

- We will store the frequency of the words and compare the values. But there is another problem there as in this approach we need to traverse the map multiple times which can be costly if the word size is high.

To avoid this we will take a integer count and it will check the number of distinct letters.

```cpp
if txt == aaba
then we take a = 3 , b = 1 and count = map.size()
while traversing if we encounter a new `a` we do a-- and remove an `a` we do a++

when a==0 -> count-- 
else -> count ++ if a goes above 0
so when count == 0 then the condition is satisfied
```

## Final Code:

```cpp
/*
Time Complexity: O(N)
Space Complexity: O(pat.size())
*/
int search(string pat, string txt) {
	int ans = 0 ;
    unordered_map<char, int> mp ;
	for(auto it : pat) {
	    mp[it]++ ;
	}
	
    int cnt = mp.size() ;
	    
	int n = txt.size(), k = pat.size(), i = 0, j = 0 ;
	while(j<n) {
	    if(mp.find(txt[j]) != mp.end()) {
	        mp[txt[j]]-- ;
	        if(mp[txt[j]] == 0) cnt-- ;
	    }
	    if(j-i+1 == k) {
	        if(cnt == 0) ans++ ;
	        if(mp.find(txt[i]) != mp.end()) {
    	        if(mp[txt[i]] == 0) cnt++ ;
    	        mp[txt[i]]++ ;
    	    }
	        i++ ;
	    }
	    j++ ;
	}
	return ans ;
}
```

