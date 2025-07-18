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

### IF YOU MAY WANT TO KNOW THE START NODE TO VISIT ALL NODES  :
```cpp
#include <bits/stdc++.h>
using namespace std;

int minTime(vector<vector<int>>& graph){
    int n = graph.size(); 
    int steps= 0 ;
    vector<vector<bool>> vis(n , vector<bool>(1<<n , false));
    // To know what was the starting node we can do one thing , to keep starting node in q always to all entries
    queue<vector<int>> q ;
    for (int i = 0; i <n ; i++) {
        vector<int> e = {i,i , (1<<i)};
        q.push(e) ;
        vis[i][(1<<i)] = true ;
    }
    int bestNode = -1 ;
    int mnSteps = 0 ;
    bool found = false ;
    while (!q.empty()) {
        int sz = q.size() ;
        
        while (sz--){    
            vector<int> c = q.front(); q.pop();
            int startNode = c[0] , node = c[1], mask = c[2] ;
            if (mask == ((1<<n)-1)) {
                bestNode = startNode ;
                mnSteps = steps ;
                found = true ;
                break ;
            }
            for (int nbr : graph[node]) {
                int nxtMask = mask|(1<<nbr) ;
                if (!vis[nbr][nxtMask]){
                    vis[nbr][nxtMask] = true ;
                    q.push({startNode,nbr , nxtMask}) ;
                }
            } 
        }
        if (found) break ;
        steps++;
    }
    if (found) {
        cout << "Best Node to Start :" << bestNode << " completing in steps :" << mnSteps << endl ;
    }
    return  found ? mnSteps: -1 ;
}
int main() {
	 vector<vector<int>>graph = {{1},{0,2,4},{1,3,4},{2},{1,2}};
	 int n = graph.size();
	 cout << minTime(graph) << endl;

}

```
