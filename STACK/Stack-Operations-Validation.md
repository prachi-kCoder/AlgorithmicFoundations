# Stack-Operations-Validation
- Using stack {Just keep popping from popped vector and push in pushed vector }
  
```cpp
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        int n = pushed.size() ;

        stack<int> stk ;
        int j = 0 ;

        for ( int i = 0 ; i < n && j < n ; i++ ) {
            stk.push(pushed[i]) ;

            while(!stk.empty() && j < n && popped[j] == stk.top()) {
                j++ ;
                stk.pop();
            }
        }

        return stk.empty();

    }
};
```
- 2 Pointers over pushed and popped
####  Most trickiest part here is that if i goes back while match with the jth characters of s then how will it come back on right indexes to continue matching ??
- for this just do :
- Even though i goes back (i.e., i--), the next iteration of the loop does pushed[i++] = val, which overwrites the popped value with the next one.
- You're writing values forward (i++), and erasing them backward (i--) when matched. It’s like a stack built on a tape—efficient and elegant.
  
```cpp
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        int n = pushed.size() ;
        int m = popped.size() ;

        int i = 0 , j = 0 ;
        for (auto val : pushed) {
            pushed[i++] = val ;
             // assigning nxt value in seq to back to match 

            while ( i-1 >= 0 && j < m  && pushed[i-1] == popped[j]) {
                i-- ; j++ ;
            }
        }
        return j == m ;

    }
};

```
