## Buy&Sell 1
- Try : https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/


```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        int mx_diff = 0 ;
        int mx = prices[n-1] ;
        
        for (int i = n-2 ; i >= 0 ;i--) {
            mx_diff = max(mx_diff , mx - prices[i]) ;
            mx = max(mx , prices[i]) ;
        }
        return mx_diff ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |         O(N) |      Single pass   |
| 🧠 SPACE |        O(1)    |      no extra space      |
