# LEFT - ROTATE 

# METHOD - ONE
```cpp
void rotateArr(vector<int>& arr, int d) {
        int n = arr.size();
        d %= n ;
        if (d == 0) return ;
        reverse(arr.begin(), arr.end()) ;
        reverse(arr.begin() , arr.begin() + n-d );
        reverse(arr.begin() + n-d, arr.end()) ;
        
    }
```

## METHOD - TWO 
```cpp
void rotateArr(vector<int>& arr, int d) {
        int n = arr.size();
        d %= n ;
        if (d == 0) return ;
        
        if(d <= n/2) {
            while (d-- > 0) {
                int first = arr[0] ;
                for (int i = 0; i <n-1 ; i++) {
                    arr[i] = arr[i+1] ;
                }
                arr[n-1] = first ;
            } 
        }else {
            int rs = n-d ;
            while (rs-- > 0) {
                int last = arr[n-1] ;
                for (int i = n-1; i >0 ; i-- ) {
                    arr[i] = arr[i-1] ;
                }
                arr[0] =  last ;
            } 
        }
    }
```
## COMPLEXICITY ANALYSIS

| Method       | Time Complexity | Space Complexity | Best Use Case                          |
|--------------|------------------|------------------|-----------------------------------------|
| Reverse Trick| O(n)             | O(1)             | Fastest, in-place, ideal for all `d`    |
| Repeated Shift| O(d·n)          | O(1)             | Simple but inefficient for large `d`    |

