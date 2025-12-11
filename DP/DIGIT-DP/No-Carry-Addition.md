## No-Carry-Addition

- For any number n :
- If we want to split it as addition of multiple nums following the constraits over the digitsum of n then applied:
- Such that n = a + b + c + d + ....   &  digit_sum(n) = digit_sum(a) + digit_sum(b) + digit_sum(c) + digit_sum(d) + ...
  
```
Property :
To keep the digit_sum(n) = digit_sum(a) + digit_sum(b) + digit_sum(c) + digit_sum(d) + ...
This equality holds if and only if the addition $a+b+c=n$ is performed without any carries in base 10.
, so all ones,  tens , hundreds ... all places should independently be contributing 
```

Proof :
`digit_sum(a) + digit_sum(b) + digit_sum(c) = digit_sum(n) + 9.c  , where c = carry`
Contribution to summands’ digit sum = 10𝑐+𝑑.
Contribution to result’s digit sum = 𝑑+𝑐.
Difference = (10𝑐+𝑑)−(𝑑+𝑐)=9𝑐.



Eg 9,9,9 ,8 = 35 where 
