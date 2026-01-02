# Reverse-SubList-LL
- Do it  : https://www.geeksforgeeks.org/problems/reverse-a-sublist-of-a-linked-list/1

- TC = O(N) 
```cpp
// Definition for singly-linked list node
struct Node {
    int data;
    Node* next;
    Node(int x) : data(x), next(nullptr) {}
};

class Solution {
  public:
    Node* reverseBetween(int a, int b, Node* head) {
        if (!head || a == b) return head;

        Node* dummy = new Node(0);   // Dummy node to simplify edge cases
        dummy->next = head;
        Node* prev = dummy;

        // Step 1: Move `prev` to the node before position `a`
        for (int i = 1; i < a; i++) {
            prev = prev->next;
        }

        // Step 2: Reverse sublist from `a` to `b`
        Node* curr = prev->next;
        Node* next = nullptr;
        Node* sublistPrev = nullptr;

        for (int i = a; i <= b; i++) {
            next = curr->next;
            curr->next = sublistPrev;
            sublistPrev = curr;
            curr = next;
        }

        // Step 3: Connect reversed sublist back
        prev->next->next = curr;   // Tail of reversed sublist points to node after `b`
        prev->next = sublistPrev;  // Node before `a` points to new head of sublist

        return dummy->next;
    }
};

```
