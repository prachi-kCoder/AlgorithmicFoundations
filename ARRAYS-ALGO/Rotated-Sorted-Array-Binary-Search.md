# BINARY SEARCH IN ROTATED SORTED ARRAY

- Intuition is there could be 2 scenarios you may need ot handle {as Array has 2 sorted parts : Left / Right}
- If your mid is in left_sorted part
- Eg `arr = {9,20,1,2,3,4,5,6,7,8}`  here mid  in right sorted part
- Eg `arr = {4,5,6,7,8,9,20,1,2,3}`  here mid  in left sorted part

- as per the target value take the right decision for searching
- If mid in left sorted part and target also in left sorted part so eliminate the whole right part
- If mid in left sorted part and target is not in left sorted part `ie arr[l] > target` so eliminate the left sorted part itself

- Similarly for right sorted part compare target if it lies in right sorted part so eliminate left by `l = mid + 1` else  eliminate right `r = mid-1`
```
long long l = 0 , r = N-1 ;
        long long res = -1 ; 

        while (l <= r) {
            int mid = l + (r-l)/2 ;
            long long mid_val = ask(mid) ;
            if (mid_val == X) {
                res = mid ; break ;
            }
            int left_val = ask(l) ;
            int right_val = ask(r) ;
            if (left_val <= mid_val ){ // left sorted part of arr 
                if (X >= left_val && X < mid_val) {
                    r = mid - 1 ;
                }else { // ie not in left_sorted part so skip this part
                    l = mid + 1 ;
                }
            } else {// right Sorted part 
                if (X <= right_val && X > mid_val) {
                    l = mid + 1 ;
                }else {
                    r = mid - 1 ;
                }
            }
        }
```

- TIME COMPLEXICITY : O(logN)
- SC : O(1) 
