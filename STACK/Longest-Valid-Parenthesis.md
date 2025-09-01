# Longest Valid Parenthesis

# 3 Approaches
#### `STACK BASED ` :

- Stack allows to keep track of the prev index unmatched because as soon as any index match they get paired and popped out .
- Keep placeholder in stk = -1 ,initially
- As soon as you get `(` push into the stack the ith idx 
- As soon as you get `)` pop out of the stack the ith idx
- the stack keeps the unmatched index and on any `)` parenthesis , they can be merged with the `(` came far prev in string .
- This all supports matching of open-closing parenthesis 
```cpp

class Solution {
  public:
    int maxLength(string& s) {
        int n = s.length();
        
        stack<int> stk ;
        stk.push(-1) ;
        int mx_len = 0 ;
        
        for (int i = 0 ; i < n ; i++) {
            if (s[i] == '(') {
                stk.push(i) ;
            }else {
                stk.pop();
                if (stk.empty()) stk.push(i) ; // prev_end
                else {
                    mx_len = max(mx_len , i-stk.top()) ;
                }
            }
        }
        return mx_len ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N)   | single pass over the string |
| 🧠 SPACE |      O(N)      |    Stack to keep the prev index important while check for can be merged or not ? |

