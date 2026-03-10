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
