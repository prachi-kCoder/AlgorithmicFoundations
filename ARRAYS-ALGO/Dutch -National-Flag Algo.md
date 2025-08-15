# DUTCH NATIONAL FLAG ALGORITHM 

## To sort the Arrays with only 3 distinct values typically 0,1,2
# 3 pointer approach :
- low: marks the boundary for 0s
- mid: current index being evaluated 
- high: marks the boundary for 2s

  Eg : For values 0 , 1, 2
```cpp
void sort012(vector<int>& arr) {
    int low = 0, mid = 0, high = arr.size() - 1;

    while (mid <= high) {
        if (arr[mid] == 0) {
            swap(arr[low++], arr[mid++]);
        } else if (arr[mid] == 1) {
            mid++;
        } else { // arr[mid] == 2
            swap(arr[mid], arr[high--]);
        }
    }
```
#### Important points to keep in mind :
   - Mid is not increment if swapping happens with arr[high] because if arr[high] = 2 then even after swapping arr[mid] = 2 , so high decrements by 1 then then for high-1 , the same mid is evaluated
   - If mid = 1 then mid increments while and if any smaller value lets say 0 comes than it is resolved by swapping with arr[low]
  
- Time Comlexicity : `O(N)`
- Space Comlexicity : `O(1)`



