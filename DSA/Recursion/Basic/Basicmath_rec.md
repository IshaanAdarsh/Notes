# Fibonacci:
- Use the formula `Fibonacci(N) = Fibonacci(N-1) + Fibonacci(N-2)`  
```cpp
int fib(int n) {
        if(n==0){
            return 0;
        }
        else if(n==1||n==2){
            return 1;
        }
        else{
            return fib(n-2)+fib(n-1);
        }
    }
```

# Palindrome:

### Iterative:
- Check if the first and last elements of the string are equal. And then move both pointers first pointer forward and last pointer backward.
```cpp
bool isPalindrome(string s) {

        int left = 0, right = s.length()-1;
        while(left<right)
        {
            if(!isalnum(s[left])) 
                left++;
            else if(!isalnum(s[right])) 
                right--;
            else if(tolower(s[left])!=tolower(s[right])) 
                return false;
            else {
                left++; 
                right--;
            }
        }
        return true;

}
```

### Recursive:
- In this approach, we check the string using functional recursion where firstly, the letters on the two ends of the string (start, end) are compared to see if they’re the same or not.

- If they’re the same then we simply call recursion for the next elements (start+1, end-1) and so on until the start becomes greater than or equal to the end. 
```cpp
bool palindrome(int i, string& s){
    
    // Base Condition
    if(i>=s.length()/2) return true;
    
    if(s[i]!=s[s.length()-i-1]) return false;

    return palindrome(i+1,s);
}
```

# Permutation and Combination:
```cpp
// Combination
int nCr(int N, int r)
{
    int res = 0;
    if (r == 0) {
        return 1;
    }
    else {
        res = nCr(N, r - 1)
              * (N - r + 1) / r;
    }
    return res;
}

// Permutation:
int fact(int n)
{
    if (n <= 1)
        return 1;
    return n * fact(n - 1);
}
 
int nPr(int n, int r)
{
    return fact(n) / fact(n - r);
}
```