## Array-Binary-Search_Partitioning
- We want to find the median of two sorted arrays A and B without merging them.

- we aim to partition both arrays such that:
- The left half contains exactly ⌊(n + m + 1)/2⌋ elements.
- The right half contains the remaining elements.
- All elements in the left half ≤ all elements in the right half.
## ✂️ Partitioning Logic- 
Let’s say we binary search on array A (the smaller one). We choose a partition index i in A, and compute the corresponding partition index j in B such that:
` i + j = (n + m + 1) / 2 `
- `Aleft = A[i-1], Aright = A[i]`
- `Bleft = B[j-1], Bright = B[j]`

```cpp
  max(Aleft, Bleft) <= min(Aright, Bright)
```
This condition guarantees:
- All elements in the left half ≤ all elements in the right half.
The partition is valid.
- Because both arrays are sorted:
- Elements before i in A are ≤ elements after i.
Same for B.
- By choosing i and computing j, we’re effectively slicing both arrays so that the combined left half has the correct number of elements and is sorted.
- 
```
class Solution {
  public:
    double medianOf2(vector<int>& a, vector<int>& b) {
        int n = a.size(); 
        int m = b.size(); 
        if (n > m) return medianOf2(b,a) ;
        // to B_search
        int low = 0 ; int high = n ;
        while (low <= high) {
            int i = (low + high)/2 ;
            int j = (n + m + 1)/2 - i ;
            
            int a_left = i == 0 ? INT_MIN : a[i-1] ;
            int a_right = i == n ? INT_MAX : a[i] ;
            int b_left = j == 0 ? INT_MIN : b[j-1] ;
            int b_right = j == m ? INT_MAX : b[j] ;
            
            if (a_left <= b_right && b_left <= a_right) {
                if ((n+m)%2 == 0){
                    return (max(a_left, b_left) + min(a_right,b_right))/2.0 ;
                }else {
                    return max(a_left, b_left) ;
                }
            }else if (a_left > b_right){
                high = i-1 ;
            }else {
                low = i + 1 ;
            }
        }
        
        return 0.0 ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(log(min(n,m)))      |  Binary Search over the smaller array {a/b} |
| 🧠 SPACE |      O(1)  | Not extra space            |
