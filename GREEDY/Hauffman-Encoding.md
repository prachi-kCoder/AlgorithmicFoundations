# Hauffman-Encoding
- Haufman encode is like to reach from top to btm what direction will you be taking L-`0` , R->`1`

Now do it on :https://www.geeksforgeeks.org/problems/huffman-encoding3345/1

```cpp
class Node {
public :
    int val ;
    Node* left; Node* right;
    char c ;
    Node(int v, char c) : c(c) , val(v) ,left(nullptr) , right(nullptr) {}
};
struct comp {
    bool operator()( Node* a , Node* b) {
        return a->val > b->val ;
    }
};
void pre_order( Node* root , string& p, vector<string>& res) {
    if (!root) return ;
    
    if ( root->c != '*' ) {
        res.push_back(p) ;
    }
    
    if (root->left) {
        p.push_back('0') ;   
        pre_order(root->left , p , res);
        
        p.pop_back();   
    }
    if (root->right) {
        p.push_back('1') ;
        pre_order(root->right, p , res);
        
        p.pop_back();
    }
}
class Solution {
    
  public:
    
    vector<string> huffmanCodes(string S, vector<int> f, int N) {
        vector<string> res;
        
        priority_queue<Node*,vector<Node*>,comp>  pq ; 
        int n = S.length();
        
        for (int i = 0; i < n ; i++) {
            pq.push(new Node(f[i] , S[i] ));
            
        }
        
        while (pq.size() >= 2) {
            Node* n1 = pq.top(); pq.pop();
            Node* n2 = pq.top(); pq.pop();
            
            Node* new_node = new Node( n1->val + n2->val , '*' ) ;
            if (n1->val <= n2->val) {
                new_node->left = n1 ;
                new_node->right = n2 ;
            }else {
                new_node->left = n2 ;
                new_node->right = n1 ;
            }
           
            pq.push(new_node);
        }
        Node* root = pq.top(); pq.pop();
        
        string pat = "" ;
        pre_order(root , pat , res) ;
        
        return res ;
    }
};
```
