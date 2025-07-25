# ALIEN DICTIONARY 
## INTUITION : 
- Order is determined by finding the character where the 2 words actually differ and determine which character should come at before as per the lexo order of alien dictionary .

- ```cpp
    class Solution {
    public:
      string findOrder(vector<string> &words) {
          int n = words.size(); 
          
          map<char , vector<bool>> adj ;
          vector<int> deg(26 , -1) ;
          for (string w : words) {
              for (char c : w) {
                  deg[c-'a'] = 0;
                  adj[c].resize(26, false);
              }
          }
          int cnt = 0 ;
          for (int i = 0 ; i<26 ; i++) {
              if (deg[i] == 0) cnt++ ;
          }
          for (int i = 0; i < n - 1; ++i) {
              string s = words[i], t = words[i + 1];
              int len = min(s.length() , t.length()) ;
              int k = 0 ;    
              while (k < len && s[k] == t[k]) k++ ;
              if (k < len) {
                  if (!adj[s[k]][t[k]-'a']) {
                      adj[s[k]][t[k]-'a'] = true ;
                      deg[t[k]-'a']++ ;
                      
                  }else if (adj[t[k]].size() > 0 && adj[t[k]][s[k]-'a']) return "";// direct rev edge
              }else {
                  if (s.length() > t.length()) return "" ;
              }
          }
          queue<int> q ;
          for (int i = 0; i < 26 ; i++) {
              if (deg[i] ==  0) {
                  q.push(i); // have no deg is at the end in order
              }
          }
          string res = "" ;
          while (!q.empty()) {
              int c = q.front(); q.pop();
              char ch = (char)(c + 'a') ;
              res += ch ;// smaller degree -> smaller in lexo
              for (int i = 0 ; i < 26 ; i++){
                  if (!adj[ch][i]) continue ;
                  int nbr = i ;
                  deg[nbr]-- ;
                  if (deg[nbr] == 0) {
                      q.push(nbr) ;
                  }
              }
          }
          if (res.length() < cnt) return "";
          
          
          return res ;
      }
  };
  ```

### MOSTLY IMPORTANT FAILING POINTS OR CONFUSION IS :
#### we take the order comparing only the adjacent pair of words , not all possible pair of words of the given dictionary .
1) 🤯 Why Only Adjacent Pairs Can Give Trustworthy Info
Imagine the sorted list is:["abc", "acd", "adf"] :
- Looking at "abc" and "adf" directly seems tempting—but that’s dangerous. The reliable precedence comes only from step-by-step transitions between adjacent entries.
-  Only comparing the adjacents pairs are enough and reduces the contradictions to inferences
2) Keep in mind to check cycles do check whether all the characters that came in any of the words as a part of order
 - We checked for cycle by 2 conditions
   - adj[t[k]].find(s[k])  is it true ?? because if a direct cycle already exist then immediately says a cycle , ie a->b , b->a  {both can't be true for order so cycle}
   - But for longer cycles like a->b ->c->a  here we need to check whether we have take all characters in order or not because if cycle exist the deg != 0 for the nodes in cycle ever & hence the order never completes for all characters


  
# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N*M) + O(N*M) + O(26)  | To get all character counted in all n words , of max word len = M , + Check all pairs of words  and character differences + Topo Sort for 26 characters at max|
| 🧠 SPACE |  O(26*26) + O(26)   |   Adj List + Deg Array         |
   
