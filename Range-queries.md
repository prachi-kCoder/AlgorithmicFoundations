
# SQRT Decomp:
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
