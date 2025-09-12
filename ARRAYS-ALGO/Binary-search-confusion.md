# Binary-search-loop confusion
- this is not a problem , you can find same answer solved with these 2 while loops
  
```
int res = 0;
while (low <= high) {
    int mid = low + (high - low) / 2;
    if (is_valid(mid)) {
        res = mid;         // mid is valid, try for more
        low = mid + 1;
    } else {
        high = mid - 1;    // mid is too much, try less
    }
}
cout << res << endl;


```
- ✅ Use case: When you want to track the best answer explicitly.
- ✅ Termination: When low > high, you've exhausted the search space.
- ✅ Answer: Stored in res.

```

while (low < high) {
    int mid = low + (high - low + 1) / 2;
    if (is_valid(mid)) {
        low = mid ;// mid is valid, try for more 
    } else {
        high = mid - 1;    // mid is too much, try less
    }
}
cout << low << endl; // contains the mid which will be right at the termination condition {low > high}

```
- ✅ Use case: When you're confident the loop will converge to the correct value.
- ✅ Termination: When low == high, you've found the largest valid mid.
- ✅ Answer: Stored in low.
