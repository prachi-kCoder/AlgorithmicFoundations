## Eventual Safe States 
- Check on : https://leetcode.com/problems/find-eventual-safe-states/
## DFS
```cpp
class Solution {
public:
    bool dfs(int node , vector<vector<int>>& graph , vector<bool>& vis , vector<bool>& recStk) {
    
        vis[node] = true ;
        recStk[node] = true ;
        for (int nbr : graph[node]) {
            if (recStk[nbr]) return true ;
            if (!vis[nbr] && dfs(nbr , graph , vis , recStk)) return true ;
        }
        recStk[node] = false;
        return false ;
    }
    vector<int> eventualSafeNodes(vector<vector<int>>& graph) {
        int n = graph.size() ;
        vector<bool> vis(n) , recStk(n);

        for (int i = 0; i < n ; i++) {
            dfs(i , graph , vis , recStk) ;
        }
        vector<int> res ;
        for (int i = 0; i < n ; i++) {
            if (!recStk[i]) {
                res.push_back(i) ;
            }
        }
        return res ;
    }
};
```
- Here don't get confused that how all cycles are detected , as people usually do that even if 1 cycle is detected the dfs is called for all nodes so all cycle are to be detected

 ### BFS  + TOPOLOGICAL SORT 
 
```cpp
class Solution {
public:
    vector<int> eventualSafeNodes(vector<vector<int>>& graph) {
        int n = graph.size();
        vector<vector<int>> revGraph(n);
        vector<int> inDegree(n, 0);

        // Build reverse graph and in-degree count
        for (int u = 0; u < n; ++u) {
            for (int v : graph[u]) {
                revGraph[v].push_back(u);
                inDegree[u]++;
            }
        }

        queue<int> q;
        vector<bool> safe(n, false);

        // Start with terminal nodes (in-degree 0)
        for (int i = 0; i < n; ++i) {
            if (inDegree[i] == 0) {
                q.push(i);
                safe[i] = true;
            }
        }

        while (!q.empty()) {
            int node = q.front(); q.pop();
            for (int nbr : revGraph[node]) {
                inDegree[nbr]--;
                if (inDegree[nbr] == 0) {
                    q.push(nbr);
                    safe[nbr] = true;
                }
            }
        }

        vector<int> res;
        for (int i = 0; i < n; ++i) {
            if (safe[i]) res.push_back(i);
        }
        sort(res.begin(), res.end());
        return res;
    }
};
```

# 🔍 Complexity Analysis
## BFS
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(V+E) + O(V)     |   Adj List + InDeg + Safe Node     |
| 🧠 SPACE |  O(V+E)      |    Adj List        |

## DFS
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(V+E) + O(V)     |   Adj List + Safe Node    |
| 🧠 SPACE |  O(V+E)     |    Adj List + Recursion Stack         |
