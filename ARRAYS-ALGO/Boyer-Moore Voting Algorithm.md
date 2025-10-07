# Boyer-Moore Voting Algorithm
Try here : https://www.geeksforgeeks.org/problems/majority-element-1587115620/1

### FOR MAJORITY WITH COUNT > N/2
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

### FOR MAJORITY WITH COUNT > N/3
##### INTUITION :
- During the first pass, you're:
  - Trying to find at most two candidates (c1, c2) who could be majority.
  - Every time a new, unrelated number appears, you reduce trust in current candidates by lowering their counts—effectively making room for emerging contenders.

-In the second pass, you’re:
  - Verifying that these candidates actually appear more than n/3 times.
```cpp
class Solution {
  public:
    vector<int> findMajority(vector<int>& arr) {
        int n = arr.size();
        int c1 =  -1 , freq1 = 0;
        int c2 =  -1 , freq2 = 0;
        for (int i = 0; i < n ; i++) {
            if (c1 == arr[i]) {
                freq1++ ;
            }else if (c2 == arr[i]) {
                freq2++ ;
            }else if (freq1 == 0) {
                c1 = arr[i] ; // new element capable to secure majority
                freq1 = 1 ;
            }else if (freq2 == 0) {
                c2 = arr[i] ;
                freq2 = 1 ;
            }else {
                freq1--;
                freq2--;
            }
        }
        freq1 = freq2 = 0 ;
        for (int i = 0 ; i < n ; i++) {
            if (c1 == arr[i]) freq1++;
            else if (c2 == arr[i]) freq2++;
        }
        
        vector<int> res ;
        if (freq1 > n/3) res.push_back(c1) ;
        if (freq2 > n/3) res.push_back(c2) ;
        // increasing order
        if (res.size() > 1 && res[0] > res[1]) swap(res[0] , res[1]) ;
        
        return res ;
    }
};
```
#### TIME COMPLEXICTIY : O(N)
#### SPACE COMPLEXICTIY : O(1)
