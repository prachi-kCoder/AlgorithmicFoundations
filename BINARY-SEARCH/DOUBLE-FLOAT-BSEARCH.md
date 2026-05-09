### BINARY SEARCH ON FLOAT/DOUBLE IS different from integers
- NEVEN use while (low <= high) as double can be precise compared
- USE fixed iterations for (int i = 0; i < 100 ; i++) {} , always move to MID only !
```
- ASK : CAN MID be accepted ?
- For  maxi :
low , high 
  for (int i = 0; i < 100 ; i++) {
      if (valid( ..)) {
          res = mid ;
          low = mid ;
      }else {
         high = mid ;
      }
}
FOR MIN :
  for (int i = 0; i < 100 ; i++) {
     if (valid(..)) {
         res = mid ;
         high = mid ;
       }else {
         low = mid ;
      }
   }
```
