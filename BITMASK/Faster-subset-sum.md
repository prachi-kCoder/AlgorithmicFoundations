- You start form subset sum and with new elements creater new sum , rather than iterating over different bitmasks!

```cpp
vector<long long> subset_sum(const vector<int>& nums) {
        int n = nums.size();
        vector<long long> sums;
        sums.push_back(0);

        for (const long long& e : nums) { // ele from nums
            int n = sums.size();
            for (int i = 0; i < n ; i++) { // subset_sum created !
                sums.push_back(e + sums[i]);
            }
        }
        return sums ;
    }
```
