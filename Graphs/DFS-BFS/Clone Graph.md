# Clone Graph
### DFS
```cpp
class Solution {
public:
    Node* dfs(Node* node , Node* g[]) {
        if (!node) return NULL ;
        int data = node->val ;

        Node* clone = new Node(data) ;
        // mp[data] = clone ;
        g[data] = clone ;
       
        vector<Node*> neighborClone ;
        for ( Node* v : node->neighbors ) {
            if (g[v->val] == NULL ) {
                neighborClone.push_back(dfs(v,  g)) ;
            }else {
                Node* newNode = g[v->val] ;
                neighborClone.push_back(newNode);
            }
        }

        clone->neighbors = neighborClone ;
        return clone ;
    }
    Node* cloneGraph(Node* node) {
        if (!node) return NULL ;
        // map<int,Node*> mp ;
        Node* g[101] = {NULL};
        return dfs(node , g) ;
    }
};
```
### BFS :
```cpp
 Node* cloneGraph(Node* node) {
       if (!node) return NULL ;
       
       Node* g[101] = {NULL} ;
       queue<Node*> q ;
       g[node->val] = new Node(node->val);
       q.push(node) ;
       while (!q.empty()) {
            Node* currOrig = q.front() ; q.pop();

            for (Node* nbr : currOrig->neighbors) {
                if (!g[nbr->val]) {
                    g[nbr->val] = new Node(nbr->val);
                    q.push(nbr) ;
                }
                g[currOrig->val]->neighbors.push_back(g[nbr->val]);
            }
       }

       return g[node->val] ;
    }
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N)          |   Traversal  |
| 🧠 SPACE |    O(N)     | array +stack (dfs) , array + queue (bfs)       |
