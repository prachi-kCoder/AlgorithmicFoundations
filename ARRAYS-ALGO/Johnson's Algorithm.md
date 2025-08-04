# Johnson's Algorithm

- For a two-machine flow shop problem, the optimal solution can be found using Johnson's Algorithm. This algorithm provides a method to determine the optimal sequence of jobs to minimize the makespan.
- Example Ques : Two emp e1 , e2 working at a firm for n orders such that Every order needs to be worked on by both of them , e1 will work and after that e2 , time to work on each order i by e1 is in B[i] , and by e2 is in C[i], min time to complete all n orders .
1) Divide the orders into two sets:
Set 1: Orders where B[i]<C[i].
Set 2: Orders where B[i]≥C[i].

2) Sort the sets:
- Sort Set 1 in ascending order of their B[i] times.
- Sort Set 2 in descending order of their C[i] times.
3) Combine the sorted sets:
- The optimal sequence is the concatenation of the sorted Set 1 followed by the sorted Set 2.

```cpp
#include <bits/stdc++.h>
using namespace std;
int minTime(int n , vector<int>& B , vector<int>& C) {
    if (n == 0) return 0 ;
    // first order is completed by e1 then e2 joins to work
    vector<pair<int,int>> s1 ;
    vector<pair<int,int>> s2 ;
    for (int i = 0; i <  n ; i++) {
        if (B[i] < C[i]) {
            s1.push_back({B[i] , i});
        }else {
            s2.push_back({C[i] , i});
        }
    }
    // asc 
    sort(s1.begin() , s1.end()) ;
    // desc
    sort(s2.begin() , s2.end(),[](const pair<int,int>& a,const pair<int,int>& b ) {
        return a.first > b.first ;
    }) ;
    vector<int> order ;
    for (int i = 0 ; i < s1.size() ; i++) {
        order.push_back(s1[i].second) ;
    }
    for (int j = 0 ; j < s2.size() ; j++) {
        order.push_back(s2[j].second) ;
    }
    
    int t1 = 0 ; // e1 
    int t2 = 0 ;
    for (int i = 0; i < order.size() ; i++) {
        int j  = order[i] ;
        t1 += B[j] ;
        t2  = max(t2 , t1);
        t2 +=  C[j];
    }
    
    return t2 ;
}
int main() {
    int n = 4 ; // ans = 13 ?? 
    vector<int> B = {3, 2,2, 4} ;// e1 
    vector<int> C = {1 , 2, 3, 4} ;// e1 
    
    cout << minTime(n , B,C) << endl ;   
}
```


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N*logN)    | Sorting of  arrays    |
| 🧠 SPACE |  O(N)   |  O(N)       |
