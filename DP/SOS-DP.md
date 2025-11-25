# SOS-DP SUM OVER SUBSETS - DP

✔ Sum over all submasks of a mask : `g[mask] = Σ f[submask] for all (submask ⊆ mask)`
✔ Sum over all supermasks of a mask : `g[mask] = Σ f[supermask] for all (mask ⊆ supermask)`

🔎 Brute Force Approach :
 - to compute  : `g[mask] = Σ f[submask] for all (submask ⊆ mask)`
 - For each mask (there are 2^𝑛 masks if we have 𝑛 bits), we need to iterate over all its submasks.
 - A mask of size 𝑛 can have up to 2^𝑛 submasks. So brute force complexity: `O (2^n . 2^n) = O(4^n)`

 🌀 Smarter Enumeration → O(3^𝑛)
 - Instead of looping over all masks and then all submasks, you can directly enumerate pairs (mask, submask) where 𝑠𝑢𝑏𝑚𝑎𝑠𝑘⊆𝑚𝑎𝑠𝑘.
 
- Each bit has 3 choices:
- Present in mask but not in submask
- Present in both mask and submask
- Absent in mask (and thus absent in submask)
  
 So total pairs = 3^n

- ⚡ SOS DP Optimization → O(N . 2^N)
The key insight of SOS DP is to reuse results by propagating contributions bit by bit:
- Instead of recomputing sums for each mask independently, we build them incrementally.
- For each bit position, we update DP values by transferring contributions from smaller masks to larger ones (or vice versa).
- 𝑂 (𝑛⋅2^𝑛)
