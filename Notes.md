### Lec 2

Maximum Denormalized number & Minimum Normalized number

Fractional part: $\times 2$ , collect as operation

L after number in R means integer

Stability (algorithm) and Conditional (problem)

$\varepsilon_{machine}=2^{-53}$ (upper bound of relative error)

mathematical problem : $f:X \to Y, x\to y$ 
computational form: $\tilde{f}:X\to Y, x\to \tilde{y}$

$fl:\mathbb{R}\to F$ real number to float number

forward error: $\Delta y =\tilde{y}-y$
backward error: the smallest $\Delta x = |\tilde{x} - x|$ such that $f(\tilde{x})=\tilde{f}(x)=\tilde{y}$

Accuracy: relative forward error (bias)
Precision:   (variance)
Stability: 
**stable** means
$$
{\|\tilde{f}(x) - f(\tilde{x}) \|\over \|f(\tilde{x})\|} = O(\varepsilon_{machine})
$$
when
$$
{\|\tilde{x} - x \|\over \|x\|} = O(\varepsilon_{machine})
$$
**backward stable** means
$$
\tilde{f}(x)=f(\tilde{x})
$$
when
$$
{\|\tilde{x} - x \|\over \|x\|} = O(\varepsilon_{machine})
$$
a correct $x$ definitely lead to a correct $y$.

Floating Point Axioms: the floating number computation remains its relative accuracy

For Cancellation: the power index would be aligned to the larger one's.
Chopping or Rounding when the digits are not enough.
Leading to loss of significance

Guard digit when the exact number is known. (One step, Benign cancellation)
Catastrophic cancellation: between **quantities**. 

### Lec 3

Stability: whether the "algorithm solution" could be regarded as "solution of some neighbor problem"
Accuracy: point property

Benign & Catastrophic Cancellation
**guard digit** :    G (Guard) 1st moved out digit
			R(round) 2nd moved out digit (round-off)
			S(Sticky) S=1 when at least 1 digit is one in the moved out digits
survives only a instant

**single step** subtraction is safe.

A **well-conditioned** problem: small perturbations to x leads to small changes in $f(x)$
A **ill-conditioned** problem: small perturbations to x leads to large changes in $f(x)$
Conditioning is intrinsic to the problem, independent of algorithm.

**Absolute & Relative Condition Number**
Let $\delta x$ denote a small perturbation of $x$, and $\delta f=f(x+\delta x)-f(x)$.
Note: $\Delta x \in \mathbb{R}$, $\delta x \to 0$

The **absolute condition number** of $f$ at $x$:
$$
\hat{\kappa}=\hat{\kappa}(x)=\lim_{\varepsilon\to 0}\sup_{\
|\delta x \|\le \varepsilon}\frac{\|\delta f\|}{\|\delta x\|}\triangleq \sup_{\delta x}\frac{\|\delta f\|}{\|\delta x\|}
$$
The Jacobian definition follows mathematical analysis.
If $f$ is differentiable, 
$$
\hat{\kappa}=\|J(x)\|
$$
The **relative condition number** is
$$
\kappa=\kappa(x)=\lim_{\varepsilon\to 0}\sup_{\
|\delta x \|\le \varepsilon}\frac{\|\delta f\|/\|f(x)\|}{\|\delta x\|/\|x\|}\triangleq \sup_{\delta x}\frac{\|\delta f\|/\|f(x)\|}{\|\delta x\|/\|x\|}
$$

If the problem is well-conditioned $\kappa(x)=O(1)\implies$ the computed solution is accurate.
$l^{0}$ norm is not a norm.

The **dual** of a norm $\|\cdot\|$:
By the **Riesz Representation Theorem** in $\mathbb{R}^{n}$, any (continuous/bounded) *linear function* $f:\mathbb{R}^{n}\to \mathbb{R}$ will take the form $f(x)=z^{T}x\triangleq f_{z}(x)$. For some $z\in \mathbb{R}^{n}$, the dual norm of $z$ is
$$
\|z\|' = \sup_{x\ne 0}\frac{|z^{T}x|}{\|x \|}
$$
$$
\|f\|' = \sup_{x\ne 0}\frac{|f(x)|}{\|x\|}
$$
For vectors, the dual norm is the linear "operator norm". The dual norms of $l^{p}$ norm is $l^{q}$ norm when and only when 
$$
\frac{1}{p}+ \frac{1}{q} = 1
$$


### Lec 4

Why dual norm: Bridge to Condition Number (by Jacobian) & Unified Metric (sensitivity any normalized space)
Unified Metric: the choice of norm changes the exact value of condition number $\kappa$, while the well/ill-conditioned conclusion remains.

Generally, relative condition number $\kappa$ is used.

For linear system
$$
\begin{align*}
\kappa(x) =&\sup_{\delta x} \frac{\|A \delta x\|/\|Ax\|}{\|\delta x\|/\|x\|}\\
=& \frac{\|x\|}{\|Ax\|}  \sup_{\delta x} \frac{\|A \delta x\|}{\|\delta x\|}\\
=& \frac{\|x\|}{\|Ax\|} \|A\|\le \|A^{-1}\|\|A\|
\end{align*}
$$
where the trick is
$$
x = A^{-1}Ax
$$

since our problem is discuss in limited, the upper bound could be reached.
Also,
$$
\kappa(A)=\|A^{-1}\|\|A\|
$$
precision loss
$$
loss = \log_{10}\kappa(A)
$$
Singular value decomposition (SVD): $A= U\Sigma V^{T}$, then under $L_{2}$ norm
$$
\begin{align*}
\|A\|=\sigma_{1}\\
\|A^{-1}\| = 1/\sigma_{m}\\
\kappa_{A}=\frac{\sigma_{1}}{\sigma_{m}}\ge 1
\end{align*}
$$
Algorithm: 
- Count *the number of floating-point operations* (**Flops**) they perform
  Count depends on the size of the problem (the **order**)
- Memory requirement
- Accuracy

Numerical differentiation
Catastrophic Cancellation when working on differentiation. (subtraction between quantities)
Also /0 error.

**R Programming**
#TODO: Install R Studio

The **basic** data structure is **vector** (e.g. list is a (recursive) vector)
Vector: atomic vector, recursive vector/list
Everything is an object, every option is a function call

No scalar in R!

Atomic vector: each element should be with same class.
Matrix/array is not vector.
Special case for number class (default is Double):
```R
a <- 1:10
>class(a) 
[1]"integer"
c <- as.array(1:10)
```
Atomic vector v.s. array
```R
>dim(c)
[1]10
>dim(a)
NULL
```

Six classes (complex and raw are rare types)
- Vectors
- Logical
- Numeric
- Integer
- complex
- raw
Three properties
- Type, `typeof`
- Length, `length`
- Attributes, `attributes`
Type: memory property
Class: object property

Atomic vector:
created with `c` for `concatenate`.
Always flat, even if nest `c`'s
```R
c(1,c(2,c(3,4)))
# [1] 1 2 3 4
```
Missing values by `NA`.

check class by `is.` function, e.g.
```R
is.double, is.integer, is.character, is.logical
is.atomic
```
Note: `is.numeric` is a general test for the “numberliness” of a vector and returns `TRUE` for both integer and double (often called numeric) vectors
```R
>is.numeric(int_vec)
[1] TRUE
>is.numeric(dbl_vec)
[1] TRUE
```

`NA`: missing value,`" logical"`
`NaN`: impossible values, `"numeric"`
`NULL`: undefined expressions (no memory location), `"NULL"`
```R
> NA > 1
[1]NA
> NaN > 1
[2]NA
> NULL > 1
[3]logical(0)
```

### Lec 5

Different types will be coerced to the **most flexible** one.

Comparison between strings: comparing the first character of the strings 
Note: alphabeta first, numbers second

Attributes by `attr`, user defined.
`attributes` for reading attributes of teh object
`str` for knowing the structure
`structure` for constructing a new object with modified attributes.
Use by `object$attribute`. 

Advanced objects: vector + different attributes (levels, class, etc.)
Attributes is the core bone of advanced objects.

**Essential Attributes**: names, dim, class
To get the 3 bro:
```R
> names(y)
> dim(y)
> class(y)
```

About **names**

**Lists**
**Recursive** vectors, which could contain other lists.
Constructed by using `list` instead of `c` (for flat vector)
Flatten by `unlist`. Test with `is.list`, convert by `as.list`
- What `c` creates is an atomic vector or a list (when input contains list)

**Factors**
could only be assigned with preset levels, based on `integer`.

**Matrices and Arrays**
Adding `dim` attribute to an atomic
special case: `matrix` with 2 dimensions
**Column first**. 
`nrow, ncol`, `rownames, colnames`, `dimnames`. 
`length = nrow * ncol`
`cbind, rbind` instead of `c` (for matrices)
`abind` for array

`dim(list)<-c(m,n)`: list-matrix
arranging objects into a grid-like structure
if x is list-matrix, `ix.matrix(x)` returns `TRUE`, by observing dimensions.

**Data frame**
Most common way of storing data in R
with each column atomic vector
`class: data.frame`
A list of equal-length vectors, sharing properties of both matrix and list.
Has no `dim` attributes 
`length` is the length of the underlying list, so `==ncol()`
`nrow()`
Has `names()==colnames()`, `rownames()`
`is.vector` returns `FALSE`: `vector` could not have attributes other than `names`

Be careful of coercion !!!!!!!!!!!
`cbind`: generalized from `c`, processing as `matrix`

Useful functions
`sample`
```R
set.seed()
dat(sample(1:nrow(dat)), 100)
dat(sample(1:nrow(dat)), 100, replace = T)
```

`replicate`
```R
replicate(100, mean(rnorm(1000)))
```

If-else
```R
if (cond) statement else statement2

if (cond)
	statement # else should be used with {}
	
if (cond) (
	statement
) else (
	statement2
)
```
For, while
```R
for (var in seq) statement
for (var in seq) {
	statement
}
while (cond) statement
while (cond) {
	statement
}
```

`stopifnot`
For class checking

`...` as back door, which could process probable options for other functions in it

`return` must be at the end 
`return` is a function, so () is needed
e.g. `if (x>y) TRUE else FALSE`
could only be used in function definition

**Operation**
**IO data**
`read.table, write.table` for tabular data
`read.csv, read.delim` respectively for .csv(seperated) and .txt(tab delimited)

`a <- file.choose()` GUI file choose
`read.table(a, sep=',', header = 'T')`

In Binary Format
`load` & `save` with .RData format
`save(x, y, file="xy.RData")`
`save.image()` for saving the current workspace
`unlink("xy.Rdata") ` deletes it


### Lec 6
**Computing** & **Vectorization**

Loop in R is very slow.

**Computation**
`%*%` is the matrix multiplication
`'*'` or `"*"` is the function name of multiplication
`&&` is AND, processing vectors as scalars (first one), short circuited(may not consider the second one)
`||` the short-circuited OR

**Vector operations**
Element wise (mapping)
   e.g. 
   ```R
   (1:8)*(1:2)
   ```
   The short one would be looped over (12121212....)
   Not times of length, then truncation and warning
   Also for other operations, e.g. `^`
   
**Matrix operations**
Transpose by `t`, diagonal by `diag(v)` (both sides)
rank by `qr(M)$rank`, inverse by `solve`, `det` `eigen`
`%*%` for matrix multiplication, `+ - * / ^` for element wise (commutable)
Element wise operations should be with same dimensions for matrices, and for matrices with any vectors 
`%*%` applies auto dimension fit for applicable vectors 
what `t` processes must be a matrix, so does what returned
For $1\times 1$ matrices, `[1]` for the value.

**Subsetting** (Slicing)
`x[-4]` remove the 4th ones, return new `x` with 1 less length
`x[-(2:4)]` = `x[-2:-4]`
`x[c(1, 2, 5)]`
`x[x == 10]`
`x[x < 0]`
`x[x %in% c(1, 2, 5)]`
Or by name
`x[, "Ozone"]` where `x` is data frame, for all rows and specific column
For data frame, is equivalent to `x$Ozone`
`$` is only applicable for recursive objects, not for atomic vector
`x[, c("wind", "temp")]`
Or by `subset`
`subset(x, Temp > 80, select = c(Ozone, Temp))`

factor is integer vector with attribute `levels`
each element in `list` is a `list`, when it comes to the content, use `[[i]]`
Note: For contents in the data structures
`[i]` for vectors and factors
`[i,j]` for matrices and dataframes
`[[i]]` for lists

When it comes to `M[i,i]`, what returned is the content itself, i.e. for numeric ones, it returns a "numeric" number
For avoiding degeneration, we can use `M[i,i, drop = F]`


**Vectorization**
self-defined operation vectors:
```R
'%it%' <- function(x, y) {
	intersect(x,y)
}
a %it% b
```
Using `Reduce`
```R
a %it% b %it% c
L = list(a, b, c)
Reduce('%it%', L) # is equivalent to a %it% b %it% c
```

for data frame, `$` finds the frame as content, class not preserved
indices for lists are recursive, so `iris[[c(2,4)]] == iris[[2]][[4]]`

Using `Vectorize` for vectorization, which could receive recursive objects.

`apply` family
`sapply(vec, func)`, returns a vector
`lapply(vec, func)`, returns a list
`tapply(X, INDEX, FUNC)`, returns array, `aggregate` does similar, returning a data frame
`apply(mat, 1or2, func)`, for matrices, 1 for rows, 2 for columns

`with(df, operation)` operations in df without `$`.

### Lec 7
`mapply(func, x, times, MoreArgs)`, multivariate
operate on args by times accordingly
`MoreArgs` for usage of `func`
```R
mapply(function(x,y,z,k){(x+k)^(y+z)},
c(a=2,b=3),c(A=3,B=4),c(a=1,b=1),c(A=2,B=2))
```
???????
`outer(vec1, vec2, FUN = '*')` generate matrix
`expand.grid` generate data frame of 2 column

`ifelse(test, yes, no)`: vectorization of `if` 
can be used by **nesting**

`switch(cond, returns)`: `cond` is a integer as index, or string as names 
Vectorization: by `apply` functions. 

pre-allocation for the target vector when it comes to evident loop. 

**Recursion**
For factorial(10)
```R
Fac1 <- function(n){
	if (n=0) return(1)
	return(n*Fac1(n-1))
}
Fac1(10)
```


**Algebra**
All $A$ are invertible square matrix.
$a_{1}$ for columns, $b_{(1)}$ for rows
$a_{j}b_{(j)}$ ranks 1
Matrix multiplication is obtained by outer product summation of $a_{i}b_{(j)}$.
$A^{-1}$ change of basis (operation on coordinates)
$x = A^{-1}b$ : expanding $b$ in $R(A)$. 

Considering complex cases, **Unitary** matrix requires that 
$$
Q^{*} = Q^{-1}
$$
where $*$ is the conjugate transpose ($^H$) of $Q$.
All eigenvalues of unitary matrix should be of module $1$, and eigenvectors of different eigenvalues should be orthogonal.

inner product remains -> length and angle remains

$$
\|A\|_{F} = \sqrt{tr(A^{*}A)}
$$

$L_{k}^{-1}$ is obtained by negating its subdiagonal entries.
$L = L_{1}^{-1}L_{2}^{-1}L_{3}^{-1}$ 
$l_{jk}= {x_{jk}\over x_{kk}}$
### Lec 8
**Pivoting** 
Complete Pivoting
Semi-definite matrix could perform Cholesky decomposition by using pivoting 
**Least Squares Problems**
Projection
Overdetermined system of equations $Ax = b$
Least squares:
$$
{\rm argmin}_{x} \|b - Ax\|
$$
$m>n$, $A_{m \times n}$.
**normal equations**
$$
A^{*}Ax = A^{*}b
$$
nonsingular requires $A$ full rank
Projection is not intrinsically orthogonal
Definition: An projector is an **idempotent** matrix
$$
P = P^{2}
$$
then $P$ is a projection
$P$ has eigenvalues $0,1$, $rank(P) = trace(P)$

### Lec 9
$$
P(I-P) =0
$$
therefore
$$
\begin{gathered}
Im(I-P) = N(P)
\\
Im(P) = N(I-P)
\\
Im(P)\cap Im(I-P) = \{0\}
\\
N(P)\cap N(I-P) = \{0\}
\end{gathered}
$$
$P$ is the projector onto $Im(P)$ along $Im(I-P)$

Projector $P$ is orthogonal if $Im(P)$ and $N(P)$ are orthogonal, **if and only if** $P = P^{*}$.
Therefore, for orthogonal projector, we have
$$
P = \hat{Q}\hat{Q}^{T}
$$
where columns of $\hat{Q}_{m\times n}$ are orthogonal. Then 
$$
P = \sum_{j=1}^{n}q_{i}q_{j}
$$
and we know 
$$
\begin{cases}
P = qq^T \\
P_{\perp} = I - qq^{T}
\end{cases}
$$
G-S orthogonalization for arbitrary column space, 
$$
\begin{gathered}
A(A^{T}A)^{-1}A^{T}\implies \sum_{i=1}^{n}QQ^{T}
\\
A = \hat{Q}\hat{R}
\end{gathered}
$$
QR is better than normal equation (Cholesky), since $\kappa$ is better (sqrt)
CGS/MGS, by the transition
$$
I - \sum_{i=1}^{n}q_{i}q_{i}^{*} = \prod_{i=1}^{n}(I - q_{i}q_{i}^{*})
$$
which could eliminate small effect of the nonorthogonality of the former steps.

### Lec 9
**Q**: What's the difference between MGS and CGS?
**A**: They are mathematically identical (sum and prod), but stability differs (nonorthogonality propagation).

GS as Triangular Orthogonlization

Householder reflector $F$. (Introducing zeros)
$F$ is diagonal component of orthogonal matrix, therefore $F$ itself is orthogonal.
$$
F = I - 2 \frac{vv^{T}}{v^{T}v}
$$
$F$ is Hermite. 
$$
v_{k} = sign(x_{1})\|x\| e_{1} + x
$$
$Q$ be obtained by operating on $e_{i}$.

Householder is More Stable than GS.
GS is triangular orthogonalization, step based on triangular; but Household is orthogonal triangularization, step based on orthogonal.
$R$ is more stable than $Q$.

LSquare by MGS
$$
x= R^{-1}z
$$
using the $R$ values, which are definitely stable.
FLOPS:

| Gaussian | $2m^{3}/3$ |
| -------- | ---------- |
|          |            |
.etc. Gaussian faster than QR(House hold)

Givens Rotation

### Lec 10
Rank is the number of non-zero Singular value but Eigenvalue.

SVD: every matrix is diagonal.

High-dimension SVD: using convolution.

All the points become equidistant from each other s.t. distance-based algorithms tend to perform poorly.

### Lec 11
$\Lambda(A)$ is the spectrum of $A$.
Geometric multiplicity, algebraic multiplicity.
Minimal polynomial $\mu_{A}$ , and Jordan Normal Form.
For all polynomial $Q$ s.t. $Q(A)=0$ $\implies \mu_{A}|Q$.
Cayley-Hamilton Thm: If $p_{A}(\lambda) = 0$, then $p_{A}(A) = 0$ $\implies \mu_{A}|p_{A}$

A matrix is positive-definite when $a_{ij}<(a_{ii}+ a_{jj})/2$
**Gershgorin circle theorem**: Every eigenvalue of $A$ lies within at least one of the Gershgorin discs $D(a_{ii},\sum_{j\ne i}|a_{ij}|)$.

Power method

Eigenvalue decomposition: $A = X \Lambda X^{-1}$, $A$ is nondefective/diagonalizable
Orthogonal decomposition: $A=Q\Lambda Q^{*}$, $A$ is normal ($A^{*}A = AA^{*}$)
Schur decomposition: $A = QTQ^{*}$ , $T$ is upper-triangular, always exists.
The eigenvalues of $A$ appear on the diagonal of $T$.

A real matrix $A$ can only be decomposed with a quasi-upper-triangular matrix $T$.

When implementing SVD, $\sigma$ is always positive