# PAINTER'S PARTITION
- Try : https://www.geeksforgeeks.org/problems/the-painters-partition-problem1535/1


```cpp
bool is_possible(vector<int>& arr, int mx , int k) {
        int n = arr.size();
        int i = 0 ; 
        int p = 0 ; 
        
        while (i < n) {
            int curr_work = 0 ;
            
            while (i < n && curr_work + arr[i] <= mx) {
                curr_work += arr[i] ; i++;
            }
            p++ ;
            if (p > k) return false ;
        }
        return p <= k ;
    }
    int minTime(vector<int>& arr, int k) {
        int n = arr.size();
        int total  = accumulate(arr.begin() , arr.end() , 0) ;
        int mx_val  = *max_element(arr.begin() , arr.end() ) ;
        
        int min_time = total ;
        int low = mx_val , high = total ;
        
        while (low <= high) {
            int curr = low + (high - low)/2 ;
            
            if (is_possible(arr , curr , k)) {
                min_time = curr ;
                high = curr - 1 ;
            } else {
                low = curr + 1 ;
            }
        }
        
        return min_time ;
    }
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N*log(total - mx))  | For all values of k between [mx , total_sum] we check for the validity and try to minimise the valid value|
| 🧠 SPACE |   O(1)       |    O(1)   |
