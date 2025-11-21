## Binary-Lifting
- Get Kth - Ancestor :

```cpp
up[u][j] = up[up[u][j-1]][j-1];
```
- 🧠 What Does up[u][j] Represent? : It means: "Who is the 2^j-th ancestor of node u ?"
- To compute this, we break the jump into **two equal halves** :
- First jump 2^(j-1) steps from u->up[u][j-1]
- Then , jump another 2^(j-1) steps from there -> up[up[u][j-1]][j-1]
- So the total jump is:
**2^(j-1) + 2^(j-1) = 2^j**
- During the processing We compute 2^j the ancestor of all nodes By splitting in ``2^j-1 + 2^j-1`` = 2^j-1 the steps up lift


Then to compute the KTH ancestor using the dp table we use it as K can be represented in decomposition of powers of 2 only
- For all set bit positions tells use how much to lift you curr u then we keep on lifting until reached the Kth ancestor !

```
Loop j,   Check Condition,    Action,            			Distance Covered
j=0,      Is b0​ set in K?   (k & (1 << 0)),u←up[u][0]    	(Jump 20=1 step),1
j=1,	  Is b1​ set in K?  (k & (1 << 1)),u←up[u][1] 		(Jump 21=2 steps),1+2=3
j,		  Is bj​ set in K?  (k & (1 << j)),u←up[u][j]         (Jump 2j steps), ..... Sum of all steps ≤K
```
- TC = O(logK)  
```cpp
#include <bits/stdc++.h>
using namespace std;
const int MAXN = 2e5 + 5, LOG = 18;
vector<int> adj[MAXN];
int up[MAXN][LOG]; // Binary lifting table
int depth[MAXN];

void dfs(int u , int par) {
    up[u][0] = par;  // Direct parent
    depth[u] = (par != -1) ? depth[par] + 1 : 0;
 
    for (int v : adj[u]) {
        if (v != par) dfs(v, u);
    }
}
void preprocess(int n) {
    for (int j = 1; j < LOG; j++) {
        for (int i = 0; i < n; i++) {
            if (up[i][j - 1] != -1)
                up[i][j] = up[up[i][j - 1]][j - 1];
        }
    }
}
int get_Kth_Parent(int u, int k) {
    for (int j = 0; j < LOG; j++) {
        if (k & (1 << j)) { // Check if `j-th` bit is set
            u = up[u][j];
            if (u == -1) return -1 ; // beyond root 
        }
    }
    return u;
}
int main() {
	memset(up, -1 , sizeof(up));
	memset(depth, -1 , sizeof(depth));
	int n , q;
	cin >> n >> q;
	for (int i = 1 ; i < n ;i++) {
        int p ;
        cin >> p;
        p-- ;
        adj[i].push_back(p) ;
        adj[p].push_back(i) ;
    }
    dfs(0 , -1) ;
    preprocess(n) ;
    for (int j = 1 ; j <= q ; j++) {
        int x , k ;
        cin >> x >> k ;
        x-- ;
        int ans = get_Kth_Parent(x , k) ;
        if (ans == -1) {
            cout << -1 << endl ;
        }else {
            cout << ans + 1 << endl ;
        }
    }

    
    return 0 ;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N*LOGN)  | Worst case for skewed tree, Tree height will be logN |
| 🧠 SPACE |  O(N*LOGN)       |   Up table , Depth for all nodes    |
