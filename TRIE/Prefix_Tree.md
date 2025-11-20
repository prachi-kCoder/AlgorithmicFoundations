# Prefix_Tree

## IMPLEMENTATION :
```cpp
struct TrieNode {
    bool eow ;
    vector<TrieNode*> children ;
    TrieNode() {
        this->children.resize(26, nullptr) ;
        this->eow = false ;
    }
};
class Trie {
public:
    TrieNode* root ;
    Trie() {
        root = new TrieNode() ;
    } 
    void insert(string word) {
        TrieNode* curr = root ;
        for (char c : word) {
            if (!curr->children[c-'a']) {
                curr->children[c-'a'] = new TrieNode();
            }
            curr = curr->children[c-'a'] ;
        }
        curr->eow = true ;
    }
    
    bool search(string word) {
        TrieNode* curr = root ;
        for (char c : word) {
            if (!curr->children[c-'a']) return false ;
            curr = curr->children[c-'a'] ;
        }
        return curr->eow  ;
    }
    bool startsWith(string prefix) {
        TrieNode* curr = root ;
        for (char c : prefix) {
            if (!curr->children[c-'a']) return false ;
            curr = curr->children[c-'a'] ;
        }
        return true ;
    }
};

```

## TC : 
- For `O(N X maxLen of the strings)`
### SC :
- `O(26 x N x maxLen of any string )` 
