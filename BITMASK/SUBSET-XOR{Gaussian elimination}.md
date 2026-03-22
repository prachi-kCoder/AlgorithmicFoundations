# Gaussian Elimination

- This actully eliminates the need to enumerating all subsets rather , all subset [32] can be formed utilising some Gaussian Vector
- `BASIS` : Having controller's of each bit , and
- -they're all `LINEARLY INDEPENDENT` : that is `None of these can be formed by combination of others`
- - BASIS size = "No. of independent vectors"
  - and the number of distinct subset xors = `2^(BASIS SIZE)` , ie `take/skip` any vector and generate any xor

- 2 STEPS :
- `basis[i] == 0` , THIS IS THE FIRST CONTROLLER OF BIT , set it for the bit and `break` , ie reserving it !
- `basis[i] != 0` ie already a vector is assigned so reduce the current elemnet to maintain linear independence !

- Then : All non - zero basis vectors form  all possible subset xor = 2^(basis vectors)
- REf : https://cses.fi/problemset/task/3191
- and : https://cses.fi/problemset/task/3211
