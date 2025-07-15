# Dice Roll Combinations for Target
# TABULATION 
```cpp
class Solution {
public:
    const int mod = 1e9 + 7 ;
    int numRollsToTarget(int n, int k, int target) {
        if ( n == 1 && k < target) return  0 ;
        vector<vector<long long>> dp(n+1 , vector<long long>(target + 1 , 0LL)) ;
        dp[0][0] = 1 ;// no dice , no target
        for (int d = 1; d <= n ; d++) {
            for (int t = 1 ; t <= target ; t++) {
                for(int face = 1 ; face <= k ; face++) {
                    if (t - face >= 0) {
                        dp[d][t] = (dp[d][t] + dp[d-1][t-face])%mod ;
                    }
                }
            }
        }
        return dp[n][target] ;
    }
};
```
## MEMOIZATION :
```cpp
class Solution {
public:
    const int mod = (int)1e9 + 7;
    long long solve(int n , int k , int target , vector<vector<long long>>& dp) {
        if (n <= 0 ) {
            if (target == 0) return  1LL;
            return 0LL ;
        }
        if (target < 0) return 0LL ;
        if (dp[n][target] != -1 ) return dp[n][target] ;
        long long c = 0LL ;
        int least = max(1 , target - (n-1)*k);
        int maxFace = min(k , target-(n-1));

        for (int face = least ; face <= maxFace  ; face++) {
            if (target - face >= 0) {
                c = (c + solve(n-1 , k , target-face , dp))%mod ;
            }else break ;
        }
        return dp[n][target] = c ;
    }
    int numRollsToTarget(int n, int k, int target) {
        if ( n== 1 && k < target) return 0 ;
        vector<vector<long long>> dp(n+1 , vector<long long>(target+1 , -1LL)) ;
        return solve(n ,  k , target , dp) ;
    }
};
```

## UNDERSTAND THE least and maxFace :-
```cpp
int least = max(1 , target - (n-1)*k);
int maxFace = min(k , target-(n-1));
```
- We can't always have least at any of our die , so that the target - face is achievable for the next (n-1) dice :
Example : _ _ _ 3 dice are to be given face & target = 14 , k= 5 , obviously we can't give 1 to any of the die , because even if we give 5+ 5 to rest to dies then also we won't form target
Here how' relation formed : Target - {Max sum that rest of dice can make =  (n-1)*k}  because k is the maxFace value for n-1 dice
So, in example we can give :14 - (2*5) = 4 (ie the min Value for the 1st dice) ,  : MinVal for dice.

- Similarly for the maxVal : Maintain at least 1 values for the rest (n-1) dice .
- That is maxVal if given to 1st dice then {1,1,1......} given to rest of the dice that is what decides the maxVal for any dice .
- Relation  =  Target - ((n-1)*1)   : MaxFace Value for currDice

## 📊 Complexity Analysis — Dice Roll Combinations
### 🧮 Tabulation (Bottom-Up DP)
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n*k*target)     |  For each n, dice, target sum , k face value looped |
| 🧠 SPACE |    O(n*target)        |     DP (2 states : n dice , target Sum )       |

## 🔍 Memoization (Top-Down DP)
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
|  🕒 Time  |  O(n*k*target) | Recursice cal for n, target , and each call process k face values in worst case |
|💾 Space	  |O(n × target) + recursion stack | Memo table + Rec Stack |


