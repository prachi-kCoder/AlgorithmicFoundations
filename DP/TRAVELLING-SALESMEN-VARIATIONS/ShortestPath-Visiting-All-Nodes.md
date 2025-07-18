# SHORTEST PATH VISITING ALL NODES 

```cpp
class Solution {
public:
    int shortestPathLength(vector<vector<int>>& graph) {

        int n = graph.size();
        vector<vector<bool>> vis(n , vector<bool>(1<<n , false)) ;
        queue<pair<int,int>> q ;
        for (int i  = 0 ;i < n ; i++) {
            vis[i][1<<i] = true ;
            q.push({i , 1<<i}) ;
        }
        int steps = 0 ;
        while (!q.empty()) {
            int sz = q.size();
            for (int i = 0; i <sz ; i++) {
                auto [node , msk] = q.front() ; q.pop();
                if (msk == ((1<<n)-1)) return steps ;

                for (int nbr : graph[node]) {
                    int nextMask = (msk|(1<<nbr));
                    if (!vis[nbr][nextMask]) {
                        vis[nbr][nextMask] = true ;
                        q.push({nbr , nextMask});
                    }
                }
            }
            steps++ ;
        }
        return steps ;
    }
};
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N*2^N)     | Each state is defined by (node, mask), For N nodes -> 2^N possible masks,  BFS explores all states until the final state fo all visited is not reached ! |
| 🧠 SPACE |  O(N*2^N)      |  visited DP + Queue (N,2^N) states :{Keep in mind :at a single level, the queue may hold up to N entries for N nodes } |
