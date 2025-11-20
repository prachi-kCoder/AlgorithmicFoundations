# Maximum-XOR-2-NUMS
Do it here :https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/

```cpp
struct Node {
    Node* links[2] ;
    bool containsKey( int bit ) {
        return links[bit] != NULL ;
    }
    Node* get(int bit) {
        return links[bit] ;
    }
    void put(int bit, Node* node) {
        links[bit] = node ;
    }
};
class Trie {
public :
    Node* root ;
    Trie () {
        root = new Node();
    }
    void insert(int num) {
        // msb -> lsb
        Node* curr = root ;
        for (int p = 31 ; p >= 0  ;p--) {
            int bit = (num >> p) & 1 ;
            if (!curr->containsKey(bit)) {
                curr->put(bit, new Node());
            }
            curr = curr->get(bit) ;
        }
    }
    int get_max(int num) {
        Node* curr = root ;
        int max_num = 0LL ;
        for (int p = 31 ; p >= 0 ; p--) {
            int bit = ((num >> p) & 1) ;
            if (curr->containsKey(1 - bit)) {
                max_num = (max_num | (1<<p)) ;
                curr = curr->get(1-bit) ;
            }else {
                curr = curr->get(bit) ;
            }
        }
        return max_num ;
    }
};
class Solution {
public:
    int findMaximumXOR(vector<int>& nums) {
        Trie* t = new Trie();
        int n = nums.size();
        for (int i = 0; i < n ; i++) {
            t->insert(nums[i]);
        }
        int mx = 0LL ;
        for (int i = 0; i < n ; i++) {
            mx = max(t->get_max(nums[i]) , mx );
        }

        return mx ;

    }
};
```
