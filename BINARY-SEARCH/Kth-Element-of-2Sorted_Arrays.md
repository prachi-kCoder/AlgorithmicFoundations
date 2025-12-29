# Kth-Element-of-2Sorted_Arrays

- Go do it first : https://www.geeksforgeeks.org/problems/k-th-element-of-two-sorted-array1317/1
- This to keep in mind
- Binary Search over smaller array
- {Intuition is if we know how many element out of K we take from a then the  ( k - mida ) taken from b }
  
- // {Range on smaller array a}
- So ```low = max(0 , k-m) , high = min(n , k) ```
- ```low = max(0 , k-m)``` : This min count of values that can be taken from a , since b can provide at max m values so mida min cnt = {k-m}
- ```high = min(n , k) ``` : As at max a can give n values so high will go at max to n , or k {which is the req count}
  
- Partition Boundary :
- a[0 ... mida-1] , b[0.. midb-1] => they should sum up to total K elements fullfill l1 <= r2 && l2 <= r1  {ie valid partition}

```cpp
int kthElement(vector<int> &a, vector<int> &b, int k) {
        // code here
        int n = a.size(); 
        int m = b.size() ;
        if (n > m) return kthElement(b , a , k) ;
        
        int low = max(0 , k - m) , high = min(n , k);
        
        while (low <= high) {
            int mida = (low + high)/2 ; // from a 
            int midb = k - mida ;// from b 
            
            int l1 = (mida == 0 ? INT_MIN : a[mida-1]) ;
            int r1 = (mida < n ? a[mida] : INT_MAX)  ;
            
            int l2 = (midb == 0 ? INT_MIN : b[midb-1]) ;
            int r2 = (midb < m ? b[midb] : INT_MAX)  ;
            
            if (l1 <= r2 && l2 <= r1) {
                return max(l1 , l2) ;
            }else if (l1 > r2) {
                high = mida-1 ;
            }else { // l2 > r1 
                low = mida + 1 ;
            }
        }
        
        return -1 ;
    }
```

## TC = O(log(min(n , m))) as binary search over the smaller seq  either a or b
