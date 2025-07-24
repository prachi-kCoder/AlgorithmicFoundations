# Floyd’s Tortoise and Hare 
- To detect a single duplicate element in the array of size n+1 having elements[1,n] + 1 duplicated
 
## 💡 Intuition Behind the Trick :
- Mapping values to indices creates a cycle, and the duplicate is the cycle entry point.

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int sz = nums.size() ;
        if (sz == 2) {// single ele ie itself repeated
            return nums[0] ;
        }
        // sz = n+1
        int slow =  nums[0] ;
        int fast =  nums[0] ;
        do {
            slow = nums[slow] ;// move the ele's index
            fast = nums[nums[fast]] ; // move to ele's to ele's idx
        }while (slow != fast) ;
        // reset 
        fast = nums[0] ;
        while (slow != fast) {
            slow = nums[slow] ;
            fast = nums[fast] ;
        }
        return slow ;
    }
};
```
### COMPLEXICITY ANALYSIS 
SPACE : O(1)
TIME : O(N)
