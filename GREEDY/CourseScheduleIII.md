# Course Schedule III 
- **Intuition** : Take the course with the lastEnd sorted bases , ie which even has deadline soon , but as there may be chances that we may wrong take a course with deadline nearer but long duration , but keep in mind we can UNDO our mistake as well !
- **APPROACH** : Keep the course duration in desc order so that to check which one of the courses taken has longer duration , then if while iteration ever we cross the deadline of that course make better decision which one to pick the {obviousely the one with smaller duration}

```cpp
  class Solution {
  public:
      int scheduleCourse(vector<vector<int>>& courses) {
          int n = courses.size();
          sort(courses.begin() , courses.end(), [](const vector<int>& a , const vector<int>& b) {
              return a[1] < b[1] ;
          }) ;
          priority_queue<int> pq ;
          int currTime = 0 ;
          for (int i = 0; i < n ; i++) {
              int dur = courses[i][0] ; int end = courses[i][1] ;
              currTime += dur ;
              pq.push(dur) ;

            if (currTime > end) {
                currTime -= pq.top();
                pq.pop();
            }
        }
        return pq.size();
    }
};
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(nlogn + n)   |   Sorting + MaxHeap + Traversal   |
| 🧠 SPACE |    O(n)  |   MaxHeap    |
  
