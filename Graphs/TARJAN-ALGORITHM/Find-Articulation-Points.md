# FINDING ARTICULATION POINTS IN GRAPH BY TARJAN'S ALGORITHM

- Algo : Tarjan's is used to find articulation points — nodes whose removal would disconnect the graph. It's based on two key values:
- ### disc[u] : Discovery time when node u is first visited
- ### low[u] : The lowest discovery time reachable from the subtree rooted at that vertex (via tree or back edges)

- ## 🔍 Why the Root Node Needs Special Handling
  - For non-root nodes {say v}:
  - ## low[v] >= disc[u] {for a child v of u} , then u is Articulation point
  As more time to reach v than u , ie v is being reached via u .

- For Root node : {There are no parent node}
- Instead, we check: if the root has 2 or more independent DFS calls (children), it means its removal would split the graph — so it's an articulation point.

- ```cpp
  void dfs(int u, int timer, vector<int>& disc, vector<int>& low, vector<bool>& vis, vector<int>& parent, vector<int>& articulationPts) {
    vis[u] = true;
    disc[u] = low[u] = timer++;
    int children = 0;

    for (int v : adj[u]) {
        if (!vis[v]) {
            parent[v] = u;
            children++;

            dfs(v, timer, disc, low, vis, parent, articulationPts);

            low[u] = min(low[u], low[v]);

            if (parent[u] == -1 && children > 1)
                articulationPts.push_back(u);
            if (parent[u] != -1 && low[v] >= disc[u])
                articulationPts.push_back(u);
        } else if (v != parent[u]) {
            low[u] = min(low[u], disc[v]);  // Back-edge
        }
    }
}

  ``` 

