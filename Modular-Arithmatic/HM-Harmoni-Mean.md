# hm 
- sometime mathematics constraint are put on top of dsa question to enhance a bit of trick!
- Recently saw a question that allows only to select those numbers
- HM = N / {1/x1 + 1/x2 + 1/x3 .. }
- CAN be solved using HM = N * Numer / commonDeno
- Here if sum of reciprocals is solved then ie into : N * {N1 * N2 * N3 } % {N2N3 + N1N3 + N1N2} 


```cpp
#include <iostream>
#include <vector>
#include <numeric>

// Helper function to find Greatest Common Divisor
long long gcd(long long a, long long b) {
    return b == 0 ? a : gcd(b, a % b);
}

// Helper to find Least Common Multiple
long long lcm(long long a, long long b) {
    if (a == 0 || b == 0) return 0;
    return (a / gcd(a, b)) * b;
}

bool isHarmonicMeanInteger(const std::vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return false;

    // 1. Find LCM of all numbers to use as a common denominator
    long long commonDenom = 1;
    for (int x : nums) {
        commonDenom = lcm(commonDenom, x);
    }

    // 2. Sum the numerators: (commonDenom/x1 + commonDenom/x2 + ...)
    long long sumNumerators = 0;
    for (int x : nums) {
        sumNumerators += (commonDenom / x);
    }

    // 3. Harmonic Mean = (n * commonDenom) / sumNumerators
    long long totalNumerator = (long long)n * commonDenom;

    // Check if it divides evenly
    return (totalNumerator % sumNumerators == 0);
}

int main() {
    std::vector<int> sequence = {2, 6}; // Try changing this to {3, 4} to see it fail
    
    if (isHarmonicMeanInteger(sequence)) {
        std::cout << "The Harmonic Mean is an integer!" << std::endl;
    } else {
        std::cout << "The Harmonic Mean is NOT an integer." << std::endl;
    }

    return 0;
}
```
