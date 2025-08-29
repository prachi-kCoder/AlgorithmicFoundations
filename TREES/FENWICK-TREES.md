## FENWICK TREE

- `USED TO GET PREFIX SUM UPTO A ith index , even with making updates O(LOGN) time form updation for the prefix sums, and updations`
# Bit set trick
- Get right most set bit of any number : by `x&(-x)`
- Remove rightmost set bit from number :`x - (x&(-x))`
- Add rightmost set bit to number : x + (x&(-x))

## BIT ARRAY[] 
- 1 based indexed & keeps the sum of a partial range of values with in array
- All ranges sum are not necessarying mutually exclusive , hence wheneven update are to be made them all ranges containing th ith index is to be udpated
- BIT :  `[0 ,   1,  2 ,  3 ,  4 ,  5,  6,  7,  8.  9.  10,  11,  12,  13]`
- Sum of range of values stored at `8`  wiil be {j+1 , i}  j is the number obtained on removing `rightmost set bit`
- `1000` remove {`0000` + 1 , 8} sum of values in the range `[1,8]` will be stored at 8th index
  
- Update similarly is to be made on all the indice have ith {updated index as in its range sum values in BIT}

- Binary Indexed Tree
  
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long

class Fenwick_tree {
public:
    int n;
    vector<ll> bit;

    Fenwick_tree(const vector<int>& a) {
        this->n = a.size();
        bit.resize(n + 1, 0LL); // BIT is 1-indexed

        for (int i = 0; i < n; ++i) {
            bit[i + 1] = a[i]; // Copy the array, adjusting for 1-based indexing
        }

        for (int i = 1; i <= n; ++i) {
            int parent_idx = i + (i & (-i));
            if (parent_idx <= n) {
                bit[parent_idx] += bit[i];
            }
        }
    }

    void update(int i, int val) { // Updates at index i with value val (1-based)
        for (; i <= n; i += (i & (-i))) {
            bit[i] += val;
        }
    }

    ll sum(int i) { // Get prefix sum up to index i (1-based)
        ll ans = 0LL;
        for (; i > 0; i -= (i & (-i))) {
            ans += bit[i];
        }
        return ans;
    }
};

int main() {
    vector<int> a = {3, 6, 1, 8, 9, 3, 2, 6, 86, 33, 23};
    int n = a.size();

    Fenwick_tree ft(a);

    // Initial sum up to index 4 (value 9 in the original array)
    // Corresponding to indices 1 to 5 in 1-based indexing
    cout << "Sum of first 5 elements: " << ft.sum(5) << endl; 

    // Update the value at index 2 (value 1 in original array) to 10
    // Corresponds to 3rd element in original array and index 3 in 1-based indexing
    int old_val = a[2];
    int new_val = 10;
    int diff = new_val - old_val;
    ft.update(3, diff);

    // Range query [l, r] is ft.sum(r) - ft.sum(l-1)
    // Sum of elements from index 2 to 5 (original array)
    cout << "Sum of elements from index 2 to 5: " << ft.sum(6) - ft.sum(2) << endl;

    return 0;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(logN) , O(logN)        |   Each update(i, val) and query(i) traverses at most log N nodes due to the binary structure using (i & -i) |
| 🧠 SPACE |    O(N+1)        |      For bit array       |
