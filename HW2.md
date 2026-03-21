### Problem 5

By definition, an algorithm $\tilde{f}$ for a problem $f$ is backward stable if for every input $x$, the computed result $\tilde{f}(x)$ is exactly the correct solution to a slightly perturbed problem $f(x + \Delta x)$, where the relative perturbation in the input is small:

$$\frac{\|\Delta x\|}{\|x\|} = O(\varepsilon_{machine})$$

Mathematically, this means:

$$\tilde{f}(x) = f(x + \Delta x)$$
The relative condition number $\kappa(x)$ of a function $f$ at $x$ measures how much a small relative change in the input $x$ is magnified in the output $f(x)$. It is defined as:
$$\kappa(x) = \lim_{\delta \to 0} \sup_{\|\Delta x\| \leq \delta \|x\|} \left( \frac{\|\Delta f\| / \|f(x)\|}{\|\Delta x\| / \|x\|} \right)$$

For small perturbations $\Delta x$, this definition implies:

$$\frac{\|f(x + \Delta x) - f(x)\|}{\|f(x)\|} \leq \kappa(x) \frac{\|\Delta x\|}{\|x\|} + o(\|\Delta x\|)$$

Substituting the backward stability property $\tilde{f}(x) = f(x + \Delta x)$ into the numerator of the relative error:

$$\frac{\|\tilde{f}(x) - f(x)\|}{\|f(x)\|} = \frac{\|f(x + \Delta x) - f(x)\|}{\|f(x)\|}$$

Applying the relationship from the condition number:

$$\frac{\|f(x + \Delta x) - f(x)\|}{\|f(x)\|} \approx \kappa(x) \frac{\|\Delta x\|}{\|x\|}$$

Since we know from backward stability that $\frac{\|\Delta x\|}{\|x\|} = O(\varepsilon_{machine})$, we substitute this into the inequality:

$$\frac{\|\tilde{f}(x) - f(x)\|}{\|f(x)\|} \leq \kappa(x) \cdot O(\varepsilon_{machine})$$


Therefore, the relative error of the computed solution satisfies:

$$\frac{\|\tilde{f}(x) - f(x)\|}{\|f(x)\|} = O(\kappa(x)\varepsilon_{machine})$$

### Problem 6
By the definition:

$$\kappa(x) = \left| \frac{x f'(x)}{f(x)} \right|$$
#### 1. For  $f(x) = \frac{x}{2}$


$$f'(x) = \frac{1}{2}$$

$$\kappa(x) = \left| \frac{x \cdot \frac{1}{2}}{\frac{x}{2}} \right|$$

$$\kappa(x) = \left| \frac{x/2}{x/2} \right| = 1$$

#### 2. For $f(x) = \sqrt{x}$


$$f'(x) = \frac{1}{2\sqrt{x}}$$


$$\kappa(x) = \left| \frac{x \cdot \frac{1}{2\sqrt{x}}}{\sqrt{x}} \right|$$

$$\kappa(x) = \left| \frac{\frac{x}{2\sqrt{x}}}{\sqrt{x}} \right| = \left| \frac{x}{2\sqrt{x} \cdot \sqrt{x}} \right|$$

$$\kappa(x) = \left| \frac{x}{2x} \right| = \frac{1}{2}$$

### Problem 7

For a function $f: \mathbb{R}^n \to \mathbb{R}$, the relative condition number is defined as:

$$\kappa(x) = \frac{\|x\|_\infty \cdot \|\nabla f(x)\|_\infty}{|f(x)|}$$

The function is $f(x) = x_1 - x_2$. The gradient vector is:

$$\nabla f(x) = \begin{bmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \end{bmatrix} = \begin{bmatrix} 1 \\ -1 \end{bmatrix}$$The nput Norm ($\infty$-norm): $\|x\|_\infty = \max(|x_1|, |x_2|)$
The Gradient Norm ($1$-norm):  $\|\nabla f(x)\|_1 = |1| + |-1| = 2$

Substitute into the condition number formula:

$$\kappa(x) = \frac{\max(|x_1|, |x_2|) \cdot 2}{|x_1 - x_2|}$$

The result shows that the condition number $\kappa(x)$ depends heavily on the values of $x_1$ and $x_2$: when  $x_1 \approx x_2$, as $x_1$ and $x_2$ become very close, the denominator $|x_1 - x_2|$ approaches zero. This causes $\kappa(x) \to \infty$, which is the formal mathematical explanation for catastrophic cancellation. 

### Problem 8

For any invertible matrix $A \in \mathbb{R}^{m \times m}$, the SVD is given by:

$$A = U \Sigma V^T$$

where $U$ and $V$ are orthogonal matrices, and $\Sigma = \text{diag}(\sigma_1, \sigma_2, \dots, \sigma_m)$ with $\sigma_1 \geq \sigma_2 \geq \dots \geq \sigma_m > 0$.
#### 1. Explanation for $\|A\|_2 = \sigma_1$

The matrix 2-norm (or spectral norm) is defined as the maximum magnification of a vector:

$$\|A\|_2 = \max_{x \neq 0} \frac{\|Ax\|_2}{\|x\|_2}$$

Using the SVD:

$$\|Ax\|_2 = \|U \Sigma V^T x\|_2$$

Since $U$ is an orthogonal matrix, it preserves the $L_2$ norm ($\|Uy\|_2 = \|y\|_2$):

$$\|Ax\|_2 = \|\Sigma V^T x\|_2$$

Let $y = V^T x$. Since $V^T$ is also orthogonal, $\|y\|_2 = \|x\|_2$. The problem becomes:

$$\|A\|_2 = \max_{y \neq 0} \frac{\|\Sigma y\|_2}{\|y\|_2}$$

$$\|\Sigma y\|_2^2 = \sigma_1^2 y_1^2 + \sigma_2^2 y_2^2 + \dots + \sigma_m^2 y_m^2 \leq \sigma_1^2 (y_1^2 + \dots + y_m^2) = \sigma_1^2 \|y\|_2^2$$

Taking the square root, we see $\|Ax\|_2 \leq \sigma_1 \|x\|_2$. The maximum is achieved when $y = [1, 0, \dots, 0]^T$ (i.e., when $x$ is the first right singular vector $v_1$).

Therefore, $\|A\|_2 = \sigma_1$.

#### 2. Explanation for $\|A^{-1}\|_2 = 1/\sigma_m$

If $A = U \Sigma V^T$, then the inverse of $A$ is:

$$A^{-1} = (U \Sigma V^T)^{-1} = (V^T)^{-1} \Sigma^{-1} U^{-1} = V \Sigma^{-1} U^T$$

Where $\Sigma^{-1}$ is a diagonal matrix:

$$\Sigma^{-1} = \text{diag}\left(\frac{1}{\sigma_1}, \frac{1}{\sigma_2}, \dots, \frac{1}{\sigma_m}\right)$$

The singular values of $A^{-1}$ are the diagonal elements of $\Sigma^{-1}$, which are $\{1/\sigma_1, 1/\sigma_2, \dots, 1/\sigma_m\}$.

From the result in Part 1, we know that the 2-norm of any matrix is its **largest** singular value. Since $\sigma_1 \geq \dots \geq \sigma_m$, the largest value in the set $\{1/\sigma_i\}$ is $1/\sigma_m$.

Therefore, $\|A^{-1}\|_2 = \frac{1}{\sigma_m}$.
