# Vector operations

`np` refers to the Numpy module, imported through `import numpy as np`.

## Vector properties

| Operation               | R | Python | Numpy (Python) | Matlab | JavaScript | Mathjs (JavaScript) | Breeze (Scala)
|-------------------------|---|--------|----------------|--------|------------|---------------------|--------
| Index starts at...             | 1      | 0    | 0     | 1   | 0     | 0      | 0      |
| Is a scalar a 1-element array? | Yes    | No   | No    | Yes | Yes   | No     | ?      |
| Name of 1d arrays              | Vector | List | Array | ?   | Array | Matrix | Vector |
| Can assign outside of range?   | Yes<br><small>In between values are assigned to `NA`.</small>    | No   | No   | Yes<br><small>⚠️ In between values are assigned to 0.</small>     |    Yes |  Yes<br><small>⚠️ In between values are assigned to 0.</small> | ?

## Vector creation from scratch

Vectors of character strings will be treated on a different page.

| Operation    | R | Python | Numpy (Python) | Matlab | JavaScript | mathjs (JavaScript) | Breeze (Scala)
|--------------|---|--------|----------------|--------|------------|---------------------|------------
| Vector from numbers `a`, `b`, `c` | `c(a,b,c)` | `[a,b,c]` | `np.array([a,b,c])` | `[a b c]` | `[a,b,c]` | `math.matrix([a,b,c])` | `DenseVector(a,b,c)`
| Vector of size 0 (empty vector) | `logical()`<br>`integer()`<br>`numeric()`<br>`complex()` | `[]`| `np.empty(0, "bool")`<br>`np.empty(0, "int")`<br>`np.empty(0)`<br>`np.empty(0, "complex")` | `[]` | `Array(0)`<br>`[]` | `math.matrix()` | ?
| Vector of 0s of size `n` | `integer(n)`;`rep(  0L, n)`<br>`numeric(n)`;`rep(   0, n)`<br>`complex(n)`;`rep(0+0i, n)` | `[0] * n`<br>`[0.] * n` | `np.zeros(n, "int")`<br>`np.zeros(n)`<br>`np.zeros(n, "complex")` | `zeros(1, n) % line matrix`<br>`zeros(n, 1) % column matrix` | `Array(n).fill(0)` | `math.zeros(n)` | `DenseVector.zeros[Double](n)`
| Vector of 1s of size `n` | `rep(1L,n)`<br><br><br><br>`rep(1,n)`<br><br><br><br>`rep(1+0i,n)` | `[1] * n`<br><br><br><br>`[1.] * n`<br><br><br><br>`[1+0j] * n` | `np.ones(n, 'int')`<br>`np.full(n,1,"int")`<br>`np.repeat(1,n)`<br><br>`np.ones(n)`<br>`np.full(n,1)`<br>`np.repeat(1.,n)`<br><br>`np.ones(n, "complex")`<br>`np.full(n,1,"complex")`<br>`np.repeat(1+0j,n)` | ? | `Array(n).fill(1)` | `math.ones(n)`
| Vector of `a`s of size `n` | `rep(a,n)` | `[a] * n` | `np.full(n,a)`<br>`np.ones(n) * a` | ? | `Array(n).fill(a)` | `math.multiply(math.ones(n), a)`
| Vector of FALSEs of size `n` | `rep(F,n)` | `[False] * n` | `np.ones(n, "bool")`<br>`np.full(n,False)` | ? | `Array(n).fill(false)` |? |  ? | ?
| Vector of TRUEs of size `n` | `logical(n)`;`rep(T,n)` | `[True] * n` | `np.zeros(n, "bool")`<br>`np.full(n,True)` | ? | `Array(n).fill(true)` | ?
| Empty vector of size `n` | `rep(NA,n)`<br><small>Entries do contain the `NA` (missing) value.</small> | `[None] * n` <small>Entries do contain the `None` (missing) value.</small>| `np.empty(n)`<br><small>Entries do contain arbitrary numbers. Use with caution.</small> | ? | `Array(n)` | `math.matrix(Array(n))` | ?
| Vector of integers from 1 to `n` | `1:n` ; `seq(1,n)` | `range(1, n+1)` | `np.arange(1, n+1)` | ? | <small>Nothing simple[^rangejs]</small> | `math.range(1, n+1)`<br>`math.range(1, n, true)` | ?
| `n` random numbers <small>following a uniform distribution on `[0,1]`</small> | `runif(n)` | <small>For loop with `random.random()`</small> | `np.random.rand(n)` | ? | <small>For loop with `Math.random()`</small> | `math.random(math.matrix([n]))`<br>`math.matrix(math.random([n]))`<br><small>⚠️ `math.random(n)` returns one number from `[0,n]` instead ; `math.random([n])` returns vanilla JavaScript array</small> | `DenseVector.rand(n)`
| Repeat sequence `v` `k` times | `rep(v, k)` | `v * k` | `np.tile(v, k)` | ? | `Array(k).fill(v).flat()` | ? | ?
| Repeat each element of sequence `v` `k` times | `rep(v, each=k)` | <small>`[elt for elt in v for _ in range(k)]`</small> | `np.repeat(v, k)` | ? | <small>Nothing simple[^repeatjs]</small> | ? | ?



In R, a scalar is just a vector of size 1: `all.equal(c(1), 1)`.

[^rangejs]: https://stackoverflow.com/questions/3746725/how-to-create-an-array-containing-1-n
[^repeatjs]: https://stackoverflow.com/questions/50672126/repeat-an-array-with-multiple-elements-multiple-times-in-javascript

## Other vector creation processes

| Operation    | R | Numpy (Python) | Matlab | Mathjs (JavaScript) | Breeze (Scala)
|--------------|---|----------------|--------|---------------------|---------------
| Sample from `numbers`<small>**without** replacement</small> | `sample(numbers)` | ? | ? | ? | ?
| Sample from `numbers`<small>**with** replacement</small> | `sample(numbers, replace=T)` | ? | ? | ? | ?
| Next useful operation | ? | ? | ? | ? | ?

## Vector indexing and assignment

`v` and `w` represent vectors ; `i`, `j`, `k` an index ; `a` and `b` scalars.

| Operation    | R | Python | Numpy (Python) | Matlab | JavaScript | Mathjs (JavaScript) | Breeze (Scala)
|--------------|---|--------|----------------|--------|------------|---------------------|---------------
| Get the `i`th element of `v` |  `v[i]` | ? | ? | `v.subset(math.index(i+1))`<br>`math.subset(v, math.index(i+1))` | ?
| Get the several elements of `v` |  `v[c(i,j)]` | ? | ? | `v.subset(math.index([i+1, j+1]))`<br>`math.subset(v, math.index([i+1,j+1]))` | ?
| Assign one element        | `v[i] <- a` | ? | ? | In place:<br>`v.subset(math.index(i+1), a)`<br>Returns a copy:<br>`math.subset(v, math.index(i+1), a)` | ?
| Assign several elements   | `v[c(i,j)] <- a`<br>`v[c(i,j)] <- c(a,b)` | ? | ? | In place:<br>`v.subset(math.index([i+1,j+1]), [a,a])`<br>`v.subset(math.index([i+1,j+1]), [a,b])`<br>Returns a copy:<br>`math.subset(v, math.index([i+1,j+1]), [a,a])`<br>`math.subset(v, math.index([i+1,j+1]), [a,b])`| ?
| Assign a range of elements   | `v[i:j] <- a` | `v[(i-1):j] <- a` | ? | ? | `v((i-1) to (j-1)) := a`
| Chain two vectors, <small>return a copy</small> | `c(v, w)` | `np.concatenate([v,w])`<br>`np.concatenate((v,w))`<br>`np.append(v,w)` | ? | `v.concat(w)`<br>`[...v, ...w]`<br>`math.concat(v, w)` | `DenseVector.vertcat(v, w)`
| Append a scalar, <small>return a copy</small> | `c(v, a)` | `np.append(v,a)` | ? | `v.concat(a)`<br>`[...v, a]`<br>`math.concat(v, [a])` ⚠️ | ?
| Prepend a scalar, <small>return a copy</small> | `c(a, v)` | `np.append(a,v)` | ? | ? | ?
| What happens type-wise when assigning `a` into `v`? | <small>`a` is coerced to `v`'s type<br>OR `v` is coerced to `a`'s type<br>OR fails</small> | <small>`a` is coerced to `v`'s type<br>OR fails </small> | ? | Nothing | ?
| Next useful operation | ? | ? | ? | ? | ?

[^1]: On assignment `v[k]<-a`, R converts any vector to the most flexible type between `v` and `a`, following this order where Logical is the least flexible: Logical -> Integer -> Float -> Complex -> Character

## Vector element-wise operations

| Operation         | R           | Python | Numpy (Python) | Matlab | JavaScript | Mathjs (JavaScript) | Breeze (Scala)
|-------------------|-------------|--------|----------------|--------|------------|---------------------|---------------
| `v` and `w`       | `v & w`     | <small>for loop with `&`</small> | `v & w` | ? | <small>for loop with `&&`</small> | `math.and(v, w)` |
| `v` or `w`        | `v | w`     | <small>for loop with `|`</small> | `v | w` | ? | <small>for loop with `||`</small> | `math.or(v, w)` |
| not `v`           | `!v`        | <small>for loop with `not`</small> | `~v`<br><small>⚠️ `~` stands for bit-wise inversion[^bitwiseinv]</small> | ? | <small>for loop with `!`</small> | `math.not(v)` |

[^bitwiseinv]: See here: https://numpy.org/doc/stable/reference/generated/numpy.invert.html

## Vector global operations

| Operation         | R           | Python | Numpy (Python) | Matlab | JavaScript | Mathjs (JavaScript) | Breeze (Scala)
|-------------------|-------------|--------|----------------|--------|------------|---------------------|---------------
| Length of vector | `length(v)` | `len(v)` | `len(v)`<br>`v.size` | `length(v)` | `v.length` | `// with v a vanilla JS array and w = math.matrix(v)`<br> `w.size()`<br>`math.count(v)`;`math.count(w)`<br><br>`math.size(v) // returns an array`<br>`math.size(w) // returns a mathjs 1d matrix` | ?
| Next useful operation | ? | ? | ? | ? | ?

## Vector properties

Is a vector different from a 1d array ?