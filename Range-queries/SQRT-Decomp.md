
# SQRT Decomp:
- GET DISTINCT COUNT 
```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
#include <cmath>
#include <bits/stdc++.h>
using namespace std ;
int block_size ;

struct Query {
  int l , r , id ;
};

int freq[1000001]; // Adjust based on max value in array
int distinct_count = 0;
void add(int ele) {
    if (freq[ele] == 0) distinct_count++ ;
    freq[ele]++ ;
}
void rem(int ele) {
    if (freq[ele] == 1) distinct_count-- ;
    freq[ele]-- ;
}
int main() {
    int n = 7;
    vector<int> a = {1, 2, 1, 3, 4, 2, 3};
    block_size = sqrt(n);
    vector<Query> queries = {{0, 2, 0}, {1, 5, 1}, {4, 6, 2}} ;
    
    sort(queries.begin(), queries.end(), [&](const Query &a, const Query &b) {
        int blockA = a.l / block_size;
        int blockB = b.l / block_size;
        if (blockA != blockB) return blockA < blockB;
        // Parity sorting optimization: zig-zag movement for the right pointer
        return (blockA % 2 == 0) ? (a.r < b.r) : (a.r > b.r);
    });
    
    int l = 0 , r = -1 ;
    int m = queries.size();
    vector<int> ans(m, 0) ;
    for (auto q : queries) {
        
        while (l > q.l) add(a[--l]); // left
        while (r < q.r) add(a[++r]) ; // right
        
        while (l < q.l) rem(a[l++]); // left
        while (r > q.r) rem(a[r--]); // right
        ans[q.id] = distinct_count ;
    }
    for (int res : ans) {
        cout << res << endl ;
    }   
    return 0;
}
```

```cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <algorithm>

using namespace std;

int main() {
    vector<int> a = {1, 2, 3, 4, 15, 16, 17};
    int n = a.size();
    
    // 1. Calculate block size and block count correctly
    int block_size = ceil(sqrt(n)); // Using ceil handles small N better
    int block_cnt = (n + block_size - 1) / block_size; // Ceiling division
    
    vector<int> b(block_cnt, 0);
    
    // 2. Pre-processing (Building the blocks)
    for (int i = 0; i < n; i++) {
        b[i / block_size] += a[i];
    }
    
    // 3. Query Range [l, r]
    int l = 1, r = 5; // Example: Sum from index 1 to 5
    int sum = 0;
    int cl = l / block_size; 
    int cr = r / block_size;
    
    if (cl == cr) {
        // Case 1: L and R are in the same block
        for (int i = l; i <= r; i++) sum += a[i];
    } else {
        // Case 2: L and R span multiple blocks
        
        // Sum the tail of the first block
        int left_end = (cl + 1) * block_size - 1;
        for (int i = l; i <= left_end; i++) sum += a[i];
        
        // Sum the full blocks in the middle
        for (int i = cl + 1; i <= cr - 1; i++) sum += b[i];
        
        // Sum the head of the last block
        for (int i = cr * block_size; i <= r; i++) sum += a[i];
    }
    
    cout << "Sum of range [" << l << ", " << r << "]: " << sum << endl;
    
    return 0;
}
```
