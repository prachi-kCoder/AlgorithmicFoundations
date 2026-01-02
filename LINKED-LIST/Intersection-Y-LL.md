## Intersection-Y-LL
- Do it : https://www.geeksforgeeks.org/problems/intersection-point-in-y-shapped-linked-lists/1

- Approach 1 : Using auxiliary space of set /unordered_set as {set , unordered_set , map , unordered_map => Do loopup by reference}
- Approach 2 : Get len of both LL then make the temp pointers such that from thereon the same length of LL1 , LL2 exist that , and get the first intersection point . byt TC = O{m+n}
## OPTIMAL APPROACH : Pointer Switching
- Intuition is : if 2 pointer 1 starting from H1 , other from H2 travels same length , then they will definitely meet
- For pointers t1 , of LL1 , t2 of LL2 
- So if x is the intersection node of LL1 of length = m , LL2 of lem n , and let c be the comm
- a = Length of LL1 upto node x 
- b = Length of LL2 upto node x  , c => Common length in both after intersection
- `T1 -> travels a + c + b ` as if it reached the end then direct it to the start of LL2
- `T2 -> travels b + c + a ` as if it reached the end then direct it to the start of LL1
- So they meet at exactly the intersection point of the 2 LL


## TC = O(a + b + c)
```cpp
 Node* intersectPoint(Node* head1, Node* head2) {
        Node* t1 = head1 ;
        Node* t2 = head2 ;
        
        while (t1 != t2) {
            t1 = (t1 == nullptr ? head2 : t1->next) ;
            t2 = (t2 == nullptr ? head1 : t2->next) ;
        }
        
        return t1 ;
        
    }
```
