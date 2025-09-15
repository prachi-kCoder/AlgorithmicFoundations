# MOUNTAIN-ARRAY {BINARY-SEARCH} 


```cpp
int l = 0, r = n - 1;
while (l < r) {
    int mid = l + (r - l) / 2;
    if (arr[mid] > arr[mid + 1]) {
        r = mid;
    } else {
        l = mid + 1;
    }
}
cout << arr[l] << endl;

```
- TC : O(logN)
