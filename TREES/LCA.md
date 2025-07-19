# FINDING LCA (LOWEST COMMON ANCESTOR ) OF BINARY TREE 

```cpp
class Solution {
  public:
    Node* lca(Node* root, int n1, int n2) {
       
        if (root == NULL) return NULL ;
        
        if (root->data == n1 || root->data == n2) return root ;
        Node* l = lca(root->left , n1 , n2) ;
        Node* r = lca(root->right , n1 , n2) ;
        
        if (l && r) return root ;
        else if (!l) return r ;
        else return l ;
    }
};
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N)  |  Visits each node once   |
| 🧠 SPACE |   O(H)   |  Recursion Stack of Height (H) |

