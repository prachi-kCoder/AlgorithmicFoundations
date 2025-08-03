# MIN ELEMENTS to form RANGE [1,B]
-   ques  : Given **sorted array a** , and +ve integer **b** , element to a such that any number in range[1,b] (inclusive) can be formed by sum of sum elements in array : get min cnt of element to be added to a 


- Intution : Greedy reach upto how much we can make , utilising the continuous range made so far [1,reach]
- If a[i] <= reach+1  then all prev set of nums can get paired with a[i] and form the numbers upto reach+a[i]
- If (reach+1) can't be formed then add this number and get to the point reach + (reach+1)  {as all prev element in range will pair up with new ele{ reach +1 } and can form upto {+= reach+1)}
- Make sure to make all element upto b no matter the elements are not enough in a

```cpp
#include <bits/stdc++.h>
using namespace std;

int minAdds(vector<int>& a, int b) {
    long long reach = 0; // Use long long to avoid overflow issues
    int i = 0;
    int cnt = 0;

    // We continue as long as our reach has not covered b
    while (reach < b) {
        // Case 1: Use a number from the array if it's helpful
        if (i < a.size() && a[i] <= reach + 1) {
            reach += a[i];
            i++; // Move to the next number in the array
        } else {
            // Case 2: There's a gap, so we must add a number
            reach += (reach + 1);
            cnt++; // Increment the count of added numbers
        }
    }
    return cnt;
}

int main() {
    vector<int> a = {1, 5};
    int b = 6;
    cout << minAdds(a, b) << endl;

    vector<int> a2 = {1, 2, 4};
    int b2 = 15;
    cout << minAdds(a2, b2) << endl;

    return 0;
}
```

- TIME COMPLEXICTY : O(B) 
- SPACE COMPLEXICTY : O(1) 
