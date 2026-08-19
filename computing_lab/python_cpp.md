---
layout: default
title: "Python & C++ Numerical Algorithms"
parent: "Computing Laboratory"
nav_order: 1
permalink: /computing_lab/python_cpp/
---

# Python & C++ Numerical Algorithms

> *High-performance implementations of the core mathematical algorithms developed in Modules A–D. Each section presents both the theoretical context and a complete, runnable implementation in Python or C++, allowing direct verification of theoretical results.*

---

## 1. Newton's Method for Root-Finding (Module D)

### Theory Review

Find $x^*$ such that $f(x^*) = 0$ using the iteration:

$$x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)}$$

This converges quadratically near a simple root.

### Python Implementation

```python
import numpy as np

def newton_method(f, df, x0, tol=1e-12, max_iter=100):
    """
    Newton's method for finding roots of f(x) = 0.

    Parameters
    ----------
    f : callable - The function whose root we seek.
    df : callable - The derivative of f.
    x0 : float - Initial guess.
    tol : float - Convergence tolerance on |f(x)|.
    max_iter : int - Maximum iterations.

    Returns
    -------
    x : float - Approximate root.
    history : list - Convergence history [(iteration, x, f(x))].
    """
    x = x0
    history = []
    for k in range(max_iter):
        fx = f(x)
        history.append((k, x, fx))
        if abs(fx) < tol:
            break
        dfx = df(x)
        if abs(dfx) < 1e-15:
            raise ValueError(f"Derivative near zero at x={x}")
        x = x - fx / dfx
    return x, history

# Example: find sqrt(2) as root of f(x) = x^2 - 2
f = lambda x: x**2 - 2
df = lambda x: 2*x
root, hist = newton_method(f, df, x0=1.0)
print(f"Root: {root:.15f}")
print(f"Exact: {np.sqrt(2):.15f}")
for k, x, fx in hist:
    print(f"  iter {k}: x = {x:.15f}, f(x) = {fx:.2e}")
```

### C++ Implementation (with Eigen)

```cpp
#include <iostream>
#include <cmath>
#include <functional>
#include <vector>
#include <tuple>

using RootHistory = std::vector<std::tuple<int, double, double>>;

std::pair<double, RootHistory> newton_method(
    std::function<double(double)> f,
    std::function<double(double)> df,
    double x0,
    double tol = 1e-12,
    int max_iter = 100)
{
    double x = x0;
    RootHistory history;
    for (int k = 0; k < max_iter; ++k) {
        double fx = f(x);
        history.emplace_back(k, x, fx);
        if (std::abs(fx) < tol) break;
        double dfx = df(x);
        if (std::abs(dfx) < 1e-15)
            throw std::runtime_error("Derivative near zero");
        x -= fx / dfx;
    }
    return {x, history};
}

int main() {
    auto f = [](double x) { return x*x - 2.0; };
    auto df = [](double x) { return 2.0*x; };
    auto [root, hist] = newton_method(f, df, 1.0);
    std::cout << "Root: " << root << std::endl;
    return 0;
}
```

---

## 2. Gradient Descent for Optimization (Module D)

### Python Implementation

```python
import numpy as np
import matplotlib.pyplot as plt

def gradient_descent(grad_f, x0, f=None, lr=0.01, tol=1e-8, max_iter=10000):
    """
    Gradient descent with fixed step size.

    Parameters
    ----------
    grad_f : callable - Gradient function.
    x0 : np.ndarray - Starting point.
    f : callable, optional - Objective (for tracking).
    lr : float - Learning rate (step size).
    """
    x = np.array(x0, dtype=float)
    history = []
    for k in range(max_iter):
        g = grad_f(x)
        if f is not None:
            history.append((k, x.copy(), f(x), np.linalg.norm(g)))
        if np.linalg.norm(g) < tol:
            break
        x = x - lr * g
    return x, history

# Rosenbrock function: f(x,y) = (1-x)^2 + 100(y-x^2)^2
def rosenbrock(x):
    return (1 - x[0])**2 + 100*(x[1] - x[0]**2)**2

def grad_rosenbrock(x):
    dx = -2*(1 - x[0]) - 400*x[0]*(x[1] - x[0]**2)
    dy = 200*(x[1] - x[0]**2)
    return np.array([dx, dy])

x_opt, hist = gradient_descent(grad_rosenbrock, [-1.0, 1.0], f=rosenbrock, lr=0.001)
print(f"Optimum: {x_opt}")  # Should be near [1, 1]
```

---

## 3. SVD via Power Iteration (Module A)

### Theory

The largest singular value $\sigma_1$ and right singular vector $v_1$ can be found by power iteration on $A^T A$:

$$v^{(k+1)} = \frac{A^T A v^{(k)}}{\|A^T A v^{(k)}\|}$$

### Python Implementation

```python
import numpy as np

def power_iteration_svd(A, num_components=1, max_iter=1000, tol=1e-10):
    """
    Compute the top singular values/vectors of A via power iteration.
    """
    m, n = A.shape
    ATA = A.T @ A
    singular_values = []
    right_vectors = []
    left_vectors = []
    A_residual = A.copy()

    for _ in range(num_components):
        # Power iteration on A_residual^T A_residual
        v = np.random.randn(n)
        v = v / np.linalg.norm(v)
        for _ in range(max_iter):
            v_new = A_residual.T @ (A_residual @ v)
            v_new = v_new / np.linalg.norm(v_new)
            if np.abs(np.abs(v_new @ v) - 1) < tol:
                break
            v = v_new
        v = v_new
        sigma = np.linalg.norm(A_residual @ v)
        u = (A_residual @ v) / sigma

        singular_values.append(sigma)
        right_vectors.append(v)
        left_vectors.append(u)

        # Deflate
        A_residual = A_residual - sigma * np.outer(u, v)

    return np.array(singular_values), np.array(left_vectors).T, np.array(right_vectors).T

# Verify against numpy
A = np.random.randn(5, 3)
sigmas, U, V = power_iteration_svd(A, num_components=3)
sigmas_np = np.linalg.svd(A, compute_uv=False)
print("Power iteration:", np.sort(sigmas)[::-1])
print("NumPy SVD:      ", sigmas_np)
```

---

## 4. Monte Carlo Integration (Module B)

### Theory

Estimate $I = \int_a^b g(x)\,dx$ using:

$$\hat{I}_n = \frac{b-a}{n}\sum_{i=1}^n g(X_i), \quad X_i \sim \text{Uniform}(a, b)$$

By the Strong Law: $\hat{I}_n \xrightarrow{\text{a.s.}} I$. By the CLT: $\sqrt{n}(\hat{I}_n - I) \xrightarrow{d} N(0, (b-a)^2 \text{Var}(g(X)))$.

### Python Implementation

```python
import numpy as np

def monte_carlo_integrate(g, a, b, n=100000):
    """
    Estimate the integral of g from a to b using Monte Carlo.
    Returns estimate\u00b1 95% CI.
    """
    X = np.random.uniform(a, b, size=n)
    gX = g(X)
    estimate = (b - a) * np.mean(gX)
    std_err = (b - a) * np.std(gX) / np.sqrt(n)
    return estimate, 1.96 * std_err

# Example: integral of exp(-x^2) from 0 to 1
# Exact value: sqrt(pi)/2 * erf(1) ≈ 0.7468
est, ci = monte_carlo_integrate(lambda x: np.exp(-x**2), 0, 1)
print(f"Estimate: {est:.6f} ± {ci:.6f}")
print(f"Exact:    {0.5 * np.sqrt(np.pi) * 0.8427:.6f}")  # erf(1) ≈ 0.8427
```

---

## 5. BFGS Optimization (Module D)

### Python (using SciPy)

```python
from scipy.optimize import minimize
import numpy as np

def rosenbrock(x):
    return (1 - x[0])**2 + 100*(x[1] - x[0]**2)**2

def grad_rosenbrock(x):
    dx = -2*(1 - x[0]) - 400*x[0]*(x[1] - x[0]**2)
    dy = 200*(x[1] - x[0]**2)
    return np.array([dx, dy])

result = minimize(rosenbrock, x0=[-1.0, 1.0], jac=grad_rosenbrock, method='BFGS',
                  options={'disp': True, 'maxiter': 1000})
print(f"Solution: {result.x}")
print(f"Function value: {result.fun}")
print(f"Iterations: {result.nit}")
print(f"Gradient evaluations: {result.njev}")
```

---

## Exercises

1. **Modify Newton's method** to handle systems of equations: $F: \mathbb{R}^n \to \mathbb{R}^n$, solving $J(x_k) d_k = -F(x_k)$. Test on the system $x^2 + y^2 = 1$, $x - y = 0$.
2. **Implement backtracking line search** (Armijo condition) and integrate it with gradient descent. Compare convergence with fixed step size on the Rosenbrock function.
3. **Implement the power method** for the largest eigenvalue of a symmetric matrix. Verify against `np.linalg.eigh`.
4. **Implement importance sampling** to estimate $P(X > 4)$ where $X \sim N(0,1)$. Compare with naive Monte Carlo.
5. **Implement L-BFGS** (limited-memory BFGS) from scratch using the two-loop recursion algorithm from Nocedal & Wright Chapter 7.
