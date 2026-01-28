The most robust way to derive these formulas is using index notation (summation notation) combined with the definition of the partial derivative. This method avoids the confusion that often arises from trying to memorize vector/matrix rules directly.

Here is the step-by-step derivation for each formula.
********


**Important Note on Layout Conventions**
In matrix calculus, there are two common conventions. The results you provided ($\nabla_{\mathbf{x}} \mathbf{A} \mathbf{x} = \mathbf{A}^\top$) indicate you are using the **Denominator Layout**.

* **Numerator Layout (Jacobian)**: The derivative of a vector $\mathbf{y}$ w.r.t (with respect to) $\mathbf{x}$ is a matrix where rows correspond to $y$ and columns to $x$.
* **Denominator Layout (Gradient)**: The derivative is the transpose of the Jacobian. The dimensions of the gradient match the dimensions of the variable we are differentiating with respect to (i.e., if $\mathbf{x}$ is a column vector, the gradient is a column vector).
  
The derivations below utilize the **Denominator Layout** to match your requested formulas.

**********
### The Linear Forms
> Derive $\nabla_{\mathbf{x}} \mathbf{A} \mathbf{x} = \mathbf{A}^\top$

Let $\mathbf{y} = \mathbf{A}\mathbf{x}$. We want to find the derivative of the vector $\mathbf{y}$ with respect to vector $\mathbf{x}$.
1. Write in index notation: The $i$-th component of $\mathbf{y}$ is:
$$y_i = \sum_{k=1}^{n} A_{ik} x_k$$
2. Take the partial derivative: Differentiate $y_i$ with respect to a specific component $x_j$:
$$\frac{\partial y_i}{\partial x_j} = \frac{\partial}{\partial x_j} \left( \sum_{k} A_{ik} x_k \right)$$
Since $x_j$ is the only variable that varies, the term is non-zero only when $k=j$.
$$\frac{\partial y_i}{\partial x_j} = A_{ij}$$
3. Assemble the matrix: In Denominator Layout, the derivative matrix is defined such that the $(j, i)$ entry is $\frac{\partial y_i}{\partial x_j}$.
$$(\nabla_{\mathbf{x}} \mathbf{A} \mathbf{x})_{ji} = A_{ij}$$
Since the $(j,i)$ entry is $A_{ij}$, the resulting matrix is the transpose of $\mathbf{A}$.

$$\nabla_{\mathbf{x}} \mathbf{A} \mathbf{x} = \mathbf{A}^\top$$
> Derive $\nabla_{\mathbf{x}} \mathbf{x}^\top \mathbf{A} = \mathbf{A}$

Let $\mathbf{y}^\top = \mathbf{x}^\top \mathbf{A}$ (a row vector).

1. Write in index notation: The $j$-th component of the vector $\mathbf{y}^\top$ is:
$$(\mathbf{y}^\top)_j = \sum_{k=1}^{m} x_k A_{kj}$$
2. Take the partial derivative: Differentiate the $j$-th component with respect to $x_i$:
$$\frac{\partial (\mathbf{y}^\top)_j}{\partial x_i} = \frac{\partial}{\partial x_i} \left( \sum_{k} x_k A_{kj} \right)$$
The derivative is non-zero only when $k=i$:
$$\frac{\partial (\mathbf{y}^\top)_j}{\partial x_i} = A_{ij}$$
3. Assemble the matrix:Arranging these derivatives according to Denominator Layout results in the matrix $\mathbf{A}$ itself.
$$\nabla_{\mathbf{x}} \mathbf{x}^\top \mathbf{A} = \mathbf{A}$$

****

### The Quadratic Form
>Derive $\nabla_{\mathbf{x}} \mathbf{x}^\top \mathbf{A} \mathbf{x} = (\mathbf{A} + \mathbf{A}^\top)\mathbf{x}$

Let the scalar function be $f = \mathbf{x}^\top \mathbf{A} \mathbf{x}$.
1. Write in index notation:
$$f = \sum_{i=1}^{n} \sum_{j=1}^{n} x_i A_{ij} x_j$$
2. Take the partial derivative with respect to $x_k$: We use the product rule because $x_k$ appears twice (once as $x_i$ and once as $x_j$).
$$\frac{\partial f}{\partial x_k} = \sum_{i} \sum_{j} A_{ij} \frac{\partial}{\partial x_k} (x_i x_j)$$
Using the product rule $\frac{\partial (x_i x_j)}{\partial x_k} = \frac{\partial x_i}{\partial x_k}x_j + x_i\frac{\partial x_j}{\partial x_k}$:
$\frac{\partial x_i}{\partial x_k}$ is 1 if $i=k$, else 0 (Kronecker delta $\delta_{ik}$).
$\frac{\partial x_j}{\partial x_k}$ is 1 if $j=k$, else 0 (Kronecker delta $\delta_{jk}$).
Substituting this back:$$\frac{\partial f}{\partial x_k} = \sum_{i}\sum_{j} A_{ij} (\delta_{ik} x_j + x_i \delta_{jk})$$
3. Split the sums:
$$\frac{\partial f}{\partial x_k} = \underbrace{\sum_{j} A_{kj} x_j}_{\text{Sum 1}} + \underbrace{\sum_{i} x_i A_{ik}}_{\text{Sum 2}}$$
* Sum 1 is the definition of the $k$-th element of vector $\mathbf{A}\mathbf{x}$.
* Sum 2 is the definition of the $k$-th element of vector $\mathbf{A}^\top \mathbf{x}$ (since $\sum x_i A_{ik} = \sum (A^\top)_{ki} x_i$).
4. Combine into vector form:The gradient vector $\nabla_{\mathbf{x}} f$ is composed of these partials for all $k$:
$$\nabla_{\mathbf{x}} \mathbf{x}^\top \mathbf{A} \mathbf{x} = \mathbf{A}\mathbf{x} + \mathbf{A}^\top \mathbf{x} = (\mathbf{A} + \mathbf{A}^\top)\mathbf{x}$$


>Special Case: $\|\mathbf{x}\|^2$

If $\mathbf{A} = \mathbf{I}$ (Identity matrix), then $\mathbf{x}^\top \mathbf{I} \mathbf{x} = \mathbf{x}^\top \mathbf{x} = \|\mathbf{x}\|^2$.

$$\nabla_{\mathbf{x}} \|\mathbf{x}\|^2 = (\mathbf{I} + \mathbf{I}^\top)\mathbf{x} = (2\mathbf{I})\mathbf{x} = 2\mathbf{x}$$

*****
### The Frobenius Norm
>Derive $\nabla_{\mathbf{X}} \|\mathbf{X} \|_\textrm{F}^2 = 2\mathbf{X}$

The Frobenius norm squared is the sum of the squares of all elements in the matrix.
1. Write in index notation:
$$f(\mathbf{X}) = \|\mathbf{X} \|_\textrm{F}^2 = \sum_{i=1}^{m} \sum_{j=1}^{n} X_{ij}^2$$
2. Take the partial derivative: We want the gradient with respect to the matrix $\mathbf{X}$, which means we calculate the partial derivative with respect to a specific entry $X_{kl}$.
$$\frac{\partial f}{\partial X_{kl}} = \frac{\partial}{\partial X_{kl}} \left( \sum_{i} \sum_{j} X_{ij}^2 \right)$$
All terms in the sum where $(i,j) \neq (k,l)$ are treated as constants and their derivative is 0. We are left with only the derivative of the $X_{kl}^2$ term.
$$\frac{\partial f}{\partial X_{kl}} = \frac{\partial}{\partial X_{kl}} (X_{kl}^2) = 2X_{kl}$$
3. Assemble the matrix:
The gradient is a matrix where the $(k,l)$ entry is $2X_{kl}$.
$$\nabla_{\mathbf{X}} \|\mathbf{X} \|_\textrm{F}^2 = 2\mathbf{X}$$

*******
Summary for your reference

| Expression | Derivative ∇f | Type |
|------------|----------------|------|
| $\mathbf{A}\mathbf{x}$ | $\mathbf{A}^\top$ | Linear (Vector-valued) |
| $\mathbf{x}^\top \mathbf{A}$ | $\mathbf{A}$ | Linear (Vector-valued) |
| $\mathbf{x}^\top \mathbf{A} \mathbf{x}$ | $(\mathbf{A} + \mathbf{A}^\top)\mathbf{x}$ | Quadratic (Scalar) |
| $\|\mathbf{x}\|$ | $2\mathbf{x}$ | Norm (Scalar) |
| $\|\mathbf{X}\|_F$ | $2\mathbf{X}$ | Matrix Norm (Scalar) |


