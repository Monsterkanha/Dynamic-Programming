# Dynamic-Programming
Here, I will be posting dp problems.


# how to memoize 3d dp when range is unknown -> using map.
class Solution {
private:
    unordered_map<int, unordered_map<int, unordered_map<int, double>>>dp;
public:
    double knightProbability(int N, int K, int r, int c) {
        if(dp.count(r) && dp[r].count(c) && dp[r][c].count(K)) return dp[r][c][K];
        
        // logic.
        
        dp[r][c][K] = val;
        return val;
