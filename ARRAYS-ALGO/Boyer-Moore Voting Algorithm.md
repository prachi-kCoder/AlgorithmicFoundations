# Boyer-Moore Voting Algorithm
- Used to check whether the any element is in majority is freq > n/2

🧠 Intuition
- Maintain a candidate and a count.
- If the current element matches the candidate, increment count.
- If it doesn't, decrement count.
- If count reaches zero, choose a new candidate.
- After one pass, verify if the candidate is truly a majority.

```cpp
class Solution {
  public:
    int majorityElement(vector<int>& arr) {
        int candidate = -1, count = 0;
        for (int num : arr) {
            if (count == 0) candidate = num;
            count += (num == candidate) ? 1 : -1;
        }

        // Verify candidate
        count = 0;
        for (int num : arr) {
            if (num == candidate) count++;
        }

        return (count > arr.size() / 2) ? candidate : -1;
    }
};

```
- Complexicity :
  - Time Complexicity : O(N)
  - Space Complexicity : O(1)
  
