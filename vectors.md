# Vector operations

`np` refers to the Numpy module, imported through `import numpy as np`.

## Vector creation from scratch

Vectors of character strings will be treated on a different page.

| Operation    | R | Numpy (Python) | Matlab | Mathjs (JavaScript) | Breeze (Scala)
|--------------|---|----------------|--------|---------------------|---------------
| Vector of size 0 (empty vector) | `logical()`<br>`integer()`<br>`numeric()`<br>`complex()` | `np.empty(0, "bool")`<br>`np.empty(0, "int")`<br>`np.empty(0)`<br>`np.empty(0, "complex")` | ? | ? | ?
| Vector of 0s of size $n$ | `numeric(n)`;`rep(0,n)`<br>`integer(n)`;`rep(0L, n)`<br>`complex(n)`;`rep(0+0i, n)`| `np.zeros(n)`<br>`np.zeros(n, "int")`<br>`np.zeros(n, "complex")` | ? | ? | `DenseVector.zeros[Double](n)`
| Vector of 1s of size $n$ | `rep(1,n)` | `np.ones(n)`;`np.full(n,1)` | ? | ? | ?
| Vector of `a`s of size $n$ | `rep(a,n)` | `np.ones(n)*a`;`np.full(n,a)` | ? | ? | ?
| Vector of FALSEs of size $n$ | `rep(F,n)` | `np.ones(n, "bool")`;`np.full(n,False)` | ? | ? | ?
| Vector of TRUEs of size $n$ | `logical(n)`;`rep(T,n)` | `np.zeros(n, "bool")`;`np.full(n,True)` | ? | ? | ?
| Empty vector of size $n$ | `rep(NA,n)`<br><small>Entries do contain the `NA` (missing) value.</small> | `np.empty(n)`<br><small>Entries do contain arbitrary numbers. Use with caution.</small> | ? | ? | ?
| Vector from numbers `a`, `b`, `c` | `c(a,b,c)` | `np.array([a,b,c])` | ? | ? | `DenseVector(a,b,c)`
| Vector of integers from 1 to $n$ | `1:n` ; `seq(1,n)` | ? | ? | ? | ?
| $n$ random numbers <small>following a uniform distribution on $[0,1]$</small> | `runif(n)` | ? | ? | ? | `DenseVector.rand(n)`
| Repeat sequences | ? | ? | ? | ? | ?

In R, a scalar is just a vector of size 1: `all.equal(c(1), 1)`.

## Other vector creation processes

| Operation    | R | Numpy (Python) | Matlab | Mathjs (JavaScript) | Breeze (Scala)
|--------------|---|----------------|--------|---------------------|---------------
| Sample from `numbers`<small>**without** replacement</small> | `sample(numbers)` | ? | ? | ? | ?
| Sample from `numbers`<small>**with** replacement</small> | `sample(numbers, replace=T)` | ? | ? | ? | ?
| Next useful operation | ? | ? | ? | ? | ?

## Vector indexing and assignment

`v` and `w` represent vectors ; `i`, `j`, `k` an index ; `a` a scalar.

| Operation    | R | Numpy (Python) | Matlab | Mathjs (JavaScript) | Breeze (Scala)
|--------------|---|----------------|--------|---------------------|---------------
| Index starts at...        | 1 | 0 | ? | ? | 0
| Assign one element        | `v[i] <- a` | ? | ? | ? | ?
| Assign several elements   | `v[c(i,j)] <- a` | ? | ? | ? | ?
| Assign a range of elements   | `v[i:j] <- a` | `v[(i-1):j] <- a` | ? | ? | `v((i-1) to (j-1)) := a`
| Chain two vectors, <small>return a copy</small> | `c(v, w)` | `np.concatenate([v,w])`<br>`np.concatenate((v,w))`<br>`np.append(v,w)` | ? | ? | `DenseVector.vertcat(v, w)`
| Append a scalar, <small>return a copy</small> | `c(v, a)` | `np.append(v,a)` | ? | ? | ?
| Prepend a scalar, <small>return a copy</small> | `c(a, v)` | `np.append(a,v)` | ? | ? | ?
| Can assign outside allocated size? | Yes | No | ? | ? | ?
| Can assign non-conforming types? | Converts either `a` or `v` to the most flexible type of the two. | Converts `a`'s type to `v`'s. | ? | ? | ?
| Next useful operation | ? | ? | ? | ? | ?

[^1]: On assignment `v[k]<-a`, R converts any vector to the most flexible type between `v` and `a`, following this order where Logical is the least flexible: Logical -> Integer -> Float -> Complex -> Character

## Vector element-wise operations

| Operation    | R | Numpy (Python) | Matlab | Mathjs (JavaScript) | Breeze (Scala)
|--------------|---|----------------|--------|---------------------|---------------
| Next useful operation | ? | ? | ? | ? | ?

## Vector global operations

| Operation    | R | Numpy (Python) | Matlab | Mathjs (JavaScript) | Breeze (Scala)
|--------------|---|----------------|--------|---------------------|---------------
| Length of vector | ? | `v.size`, `len(v)` | ? | ? | ?
| Next useful operation | ? | ? | ? | ? | ?