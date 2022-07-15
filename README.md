# Dynamic-Programming
Here, I will be posting dp problems.


#### Memoize 3d dp-> using map.
```cpp
class Solution {
private:
    unordered_map<int, unordered_map<int, unordered_map<int, double>>>dp;
public:
    double knightProbability(int N, int K, int r, int c) {
        if(dp.count(r) && dp[r].count(c) && dp[r][c].count(K)) return dp[r][c][K];
        
        // logic.
        
        dp[r][c][K] = val;
        return val;
```

### Coin change problem, 
##### 1st. No of ways to get ordered way of count. eg. 
N = 4 coins = [1,2,3] 
ans = 1,1,1,1   2,2  1,1,2   1,3 
you can take repeatation of coin.

Now here, dp[i][j] will tell using first i coins number of ways to get jth sum. 
Here, two cases arises one 1. Can't take one coin twice then 
                                dp[i][j] = dp[i-1][j] if you do not take this coin
                                dp[i][j] += dp[i][j-A[i]] if you can take this one.
                            
                            Now, we want to conver it to 1D dp so here we can have more than one time take. 
                            So we need dp[i-A[i]] for current coin as well so increasing loop.
  
  ```cpp
  int Solution::coinchange2(vector<int> &A, int B) {
    int n = A.size(), mod = 1000007;
    vector<int> dp(B+1, 0);
    dp[0] = 1;                      // Don't forget to initialise with 1. 
    for(int i = 0; i < n; i++){    // interpret of this using first i coins total ways to get jth sum. 
        for(int j = A[i]; j <= B; j++){
            (dp[j] += dp[j-A[i]])%=mod;
        }
    }
    return dp[B];
}
```

            2. Case when one coin only once.
                then we need dp[j-A[i]] value stored by previous ith iteration so reverse loop.
   
   ```cpp
   int Solution::coinchange2(vector<int> &A, int B) {
    int n = A.size(), mod = 1000007;
    vector<int> dp(B+1, 0);
    dp[0] = 1;
    for(int i = 0; i < n; i++){
        for(int j = B; j >= A[i]; j++){
            (dp[j] += dp[j-A[i]])%=mod;
        }
    }
    return dp[B];
}
```

##### 2nd where unordered way.
Here we need to make sum using all coins avaiable so just invert the loop and you are done.
No. of ways to create sum j using all the coins. 

```cpp
int Solution::coinchange2(vector<int> &A, int B) {
    int n = A.size(), mod = 1000007;
    vector<int> dp(B+1, 0);
    dp[0] = 1;
    for(int j = 0; j <= B; j++){
        for(int i = 0; i < n; i++){
            if(j >= A[i])
            (dp[j] += dp[j-A[i]])%=mod;
        }
    }
    return dp[B];
}

```

### int8_t -> its a signed char.
can assign true ,false but use this variable to return . so to avoid type cast.
```cpp
int Solution::isMatch(const string A, const string B) {
    int n = A.size(), m = B.size();
    vector<vector<int8_t>> dp(n+1, vector<int8_t>(m+1, -1));
    
    function<int8_t(int i, int j)> solve = [&](int i, int j){
        if(i == 0){
            while(j > 0 && B[j-1] == '*') j--;
            if(j == 0) return dp[i][j] = true;
            return dp[i][j] = false;
        }   
        if(j == 0) return dp[i][j] = false;
        
        if(dp[i][j] != -1) return dp[i][j];
        
        dp[i][j] = false;
        if(A[i-1] == B[j-1] || B[j-1] == '?'){
            return dp[i][j] = solve(i-1, j-1);
        }
        else if(B[j-1] == '*'){
            return dp[i][j] = solve(i-1, j) || solve(i, j-1);
        }
        return dp[i][j];
    }; 
    
    return solve(n, m);
}
```

                                
                    
