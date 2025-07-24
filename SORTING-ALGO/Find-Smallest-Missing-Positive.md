## Find-Smallest-Missing-Positive

### INTUITION : 
- Understand for a missing value in [1,n] then obviously we have nothing to do with values <= 0 or val >= n+1
- Since the array is unsorted -> Sort it using Cycle Sort [1,N]  as it help to push element at the right position
- Since the elements {Wrong set : Non-positives + Positives >= n+1} if they belong to nums , they will definitely be occupying the places of the numbers which are actully missing
- If any element in [1,n] is present in nums then definitely is will somehow takes its place nums[i]-1  , by Cycle Sort
- But those which are missing have missing , their spaces will be occupied by the values in the Wrong Set {Non-positive Or Positive of val >= n+1}

```cpp
int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        // place at right pos and if nonPositive or nums[i] >= n+1 ,then ignore 
        int i = 0; 
        while (i < n) {
            if (nums[i] <= 0 || nums[i] >= n+1 ) {
                i++ ;
                continue ;
            }
            int rightPos = nums[i]-1 ;
            if (nums[rightPos] != nums[i]) {
                swap(nums[rightPos] , nums[i]) ;
            }else {
                i++ ;
            }
        }
        for (int i = 0; i < n ; i++) {
            if (nums[i] != i+1) return i+1 ;
        }
        return n+1 ;
    }
```


# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N)    |   Linear Traversal |
| 🧠 SPACE |    O(1)       |  no extra space |

