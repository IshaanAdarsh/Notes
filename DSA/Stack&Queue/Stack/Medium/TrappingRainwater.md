# Trapping Rainwater:
- We find the maximum prefix and maximum suffix for each block
- If at a particular block the min(maxpre,maxsuf) is greater than the hight then only water can be stored.
```
int trap(vector<int>& height) {
        int n = height.size();
        int maxipre = height[0];
        int maxisuf = height[n-1];
        vector<int>pre;
        vector<int>suf;
        for(int i =0;i<n;i++){
            if(maxipre<height[i]){
                maxipre = max (maxipre,height[i]);
            }
            
            if(maxisuf<height[n-i-1]){
                maxisuf = max(maxisuf,height[n-i-1]);
            }
            pre.push_back(maxipre);
            suf.push_back(maxisuf);
        }
        reverse(suf.begin(),suf.end());
        int sum =0;
        int res = 0;

        for(int i =1;i<n;i++){
            sum = min(pre[i],suf[i])-height[i];
            if(sum>0){
                res+=sum;
            }
        }

        for(int i =0;i<n;i++){
            cout<<pre[i]<<" ";
        }
        for(int i =0;i<n;i++){
            cout<<suf[i]<<" ";
        }
        
        return res;
    }
```