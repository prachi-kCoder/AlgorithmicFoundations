# Bucket-Sort

### THIS IS NOT FOR SORING ELEMENTS AS PER THEIR  VALUES RATHER SORTING BASED ON FREQ  

- ques like TOPK FREQ ELEMENTS to get the mostfreq K element of array !
  
```cpp
vector<int> topKFrequent(vector<int>& nums, int k) {
        int n = nums.size();

        unordered_map<int,int> mp ;
        for (int e : nums) mp[e]++ ;

        vector<vector<int>> buckets( n+1 ) ;
        for (auto [e,f] : mp) {
            buckets[f].push_back(e) ;
        }
        vector<int> ans ;
        for (int i = n ; i >= 1 ; i--) {
            for (int e : buckets[i]) {
                if (ans.size() == k) break ;
                ans.push_back(e) ;
            }
            if (ans.size() == k) break ;
        }

        return ans ;
    }
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N)       |    Freq calc , Bucket filling based on freq       |
| 🧠 SPACE |      O(N)      |    Map and Buckets        |
