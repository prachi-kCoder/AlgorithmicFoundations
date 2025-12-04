# mo's algo
```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 200005;
int freq[N], distinct_cnt;
int LEN;
vector<int> a;

void add(int i) {
    if (freq[a[i]] == 0) distinct_cnt++;
    freq[a[i]]++;
}
void remove_ele(int i) {
    freq[a[i]]--;
    if (freq[a[i]] == 0) distinct_cnt--;
}

int main() {
    a = {1,1,2,1,3,2};
    int n = a.size();

    vector<vector<int>> qu = {{0,2},{1,4},{2,3},{0,5}};
    int m = qu.size();

    LEN = sqrt(n);

    vector<vector<int>> all_q;
    for (int i = 0; i < m; i++) {
        all_q.push_back({qu[i][0], qu[i][1], i});
    }

    // ✅ Correct comparator for Mo's algorithm
    sort(all_q.begin(), all_q.end(), [&](const vector<int>& x, const vector<int>& y) {
        int block_x = x[0] / LEN;
        int block_y = y[0] / LEN;
        if (block_x != block_y) return block_x < block_y;
        return x[1] < y[1];
    });

    vector<int> res(m);
    int L = 0, R = -1; // start with empty range
    distinct_cnt = 0;

    // ✅ Process queries
    for (auto &q : all_q) {
        int l = q[0], r = q[1], idx = q[2];

        while (R < r) add(++R);
        while (R > r) remove_ele(R--);
        while (L < l) remove_ele(L++);
        while (L > l) add(--L);

        res[idx] = distinct_cnt;
    }

    // ✅ Print results
    for (int x : res) cout << x << " ";
    cout << endl;
}

```
