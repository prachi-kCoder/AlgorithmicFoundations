# Longest Valid Parenthesis with wildcard '*'
- https://leetcode.com/problems/valid-parenthesis-string/description/

- Here `high` : the max cnt of `(` that can be considered , `low` : lowest cnt of `(` : that is just needed to match all `)`
- So if ever the high < 0 ie {total `(` + `*` together not enough for `)`}
- if `low != 0 ` ie the lowest possible `(` are to be matched rightly to the `)` + `*` ie  why low -- on getting a `*` only if possible ie if low > 0

```cpp

bool checkValidString(string s) {
        int low = 0 , high = 0 ;

        for (char c : s) {
            if (c == '(') {
                low++ ;
                high++ ;
            }else if (c == ')') {
                if (low >0) low-- ;
                high-- ;
            }else {
                if (low >0) low-- ;
                high++ ;
            }
            if (high < 0) {
                return false ;
            }
        }

        return low == 0 ;
    }
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N)   | single pass over the string |
| 🧠 SPACE |      O(N)      |    Stack to keep the prev index important while check for can be merged or not ? |

