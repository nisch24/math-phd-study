---
layout: default
title: "MATLAB Matrix & Optimization"
parent: "Computing Laboratory"
nav_order: 2
permalink: /computing_lab/matlab/
---

# MATLAB Matrix & Optimization Tutorials

> *MATLAB excels at matrix computations, numerical linear algebra, and optimization prototyping. These tutorials pair key results from Modules A and D with complete, annotated code and convergence analysis, making the theoretical guarantees visually concrete.*

---

## 1. Matrix Factorizations (Module A)

### 1.1 Eigenvalue Decomposition

```matlab
%% Spectral Decomposition of a Symmetric Matrix
A = [4, 1, 2;
     1, 3, 1;
     2, 1, 5];

% Eigendecomposition
[V, D] = eig(A);

fprintf('Eigenvalues:\n');
disp(diag(D)');

fprintf('Eigenvectors (columns of V):\n');
disp(V);

% Verify: A = V * D * V'
fprintf('Reconstruction error: %.2e\n', norm(A - V*D*V', 'fro'));

% Rayleigh quotient on the unit circle of the x1-x2 plane.
% Restricted to this plane, R(x) ranges exactly over [mu_1, mu_2], the
% eigenvalues of the leading 2x2 block A(1:2,1:2) -- NOT over
% [lambda_min(A), lambda_max(A)]. Cauchy interlacing guarantees
% lambda_1 <= mu_1 <= lambda_2 <= mu_2 <= lambda_3.
theta = linspace(0, 2*pi, 200);
R = zeros(size(theta));
for i = 1:numel(theta)
    x = [cos(theta(i)); sin(theta(i)); 0];
    R(i) = (x'*A*x) / (x'*x);
end
mu = eig(A(1:2, 1:2));
figure; hold on;
plot(theta, R, 'b-', 'LineWidth', 2);
yline(mu(1), 'k:', '\mu_1'); yline(mu(2), 'k:', '\mu_2');
yline(D(1,1), 'r--', '\lambda_{min}(A)');
yline(D(3,3), 'r--', '\lambda_{max}(A)');
xlabel('\theta'); ylabel('Rayleigh Quotient R(x)');
title('Rayleigh Quotient on a 2-D Slice: Cauchy Interlacing');
hold off;
```

### 1.2 Singular Value Decomposition

```matlab
%% SVD and Low-Rank Approximation
A = [1 2 3 4;
     5 6 7 8;
     9 10 11 12];

[U, S, V] = svd(A);

fprintf('Singular values: %.4f, %.4f, %.4f\n', diag(S));
fprintf('Rank of A: %d\n', rank(A));

% Best rank-1 approximation
A1 = S(1,1) * U(:,1) * V(:,1)';
fprintf('\nRank-1 approximation error (Frobenius): %.4f\n', norm(A - A1, 'fro'));
fprintf('Expected (sigma_2^2 + sigma_3^2)^{1/2}: %.4f\n', ...
    sqrt(S(2,2)^2 + S(3,3)^2));

% Pseudoinverse
A_pinv = V * pinv(S) * U';
fprintf('\nPseudoinverse error vs pinv(): %.2e\n', norm(A_pinv - pinv(A), 'fro'));
```

### 1.3 LU and Cholesky Factorizations

```matlab
%% LU Decomposition
A = [2 1 1; 4 3 3; 8 7 9];
[L, U, P] = lu(A);
fprintf('PA = LU reconstruction error: %.2e\n', norm(P*A - L*U, 'fro'));

%% Cholesky: A = R'*R for positive definite A
B = A'*A;  % guaranteed PD
R = chol(B);
fprintf('Cholesky reconstruction error: %.2e\n', norm(B - R'*R, 'fro'));

% Solving Bx = b efficiently
b = [1; 2; 3];
x = R \ (R' \ b);
fprintf('Solution error vs direct: %.2e\n', norm(x - B\b));
```

---

## 2. Optimization (Module D)

### 2.1 Unconstrained Optimization with `fminunc`

```matlab
%% Rosenbrock function optimization (save as a script file)
options = optimoptions('fminunc', ...
    'Algorithm', 'quasi-newton', ...
    'SpecifyObjectiveGradient', true, ...
    'Display', 'iter', ...
    'MaxIterations', 1000);

x0 = [-1; 1];
[x_opt, fval, ~, output] = fminunc(@rosenbrock_with_grad, x0, options);

fprintf('\nOptimum: [%.6f, %.6f]\n', x_opt);
fprintf('Function value: %.2e\n', fval);
fprintf('Iterations: %d\n', output.iterations);

% Local functions must come at the END of a script (R2016b+).
% Returning the gradient as a second output, guarded by nargout, is the
% documented pattern; wrapping deal() in an anonymous function errors
% whenever the solver requests only one output.
function [f, g] = rosenbrock_with_grad(x)
    f = (1 - x(1))^2 + 100*(x(2) - x(1)^2)^2;
    if nargout > 1
        g = [-2*(1 - x(1)) - 400*x(1)*(x(2) - x(1)^2);
              200*(x(2) - x(1)^2)];
    end
end
```

### 2.2 Constrained Optimization with `fmincon`

```matlab
%% min f(x) = x1^2 + x2^2  subject to  x1 + x2 >= 1
objective = @(x) x(1)^2 + x(2)^2;
A_ineq = [-1, -1];   % -x1 - x2 <= -1  (i.e., x1+x2 >= 1)
b_ineq = -1;

options = optimoptions('fmincon', 'Display', 'iter', 'Algorithm', 'interior-point');
[x_opt, fval] = fmincon(objective, [0; 0], A_ineq, b_ineq, [], [], [], [], [], options);

fprintf('Optimum: [%.4f, %.4f]\n', x_opt);
fprintf('f(x*) = %.4f (expected 0.5)\n', fval);
fprintf('Constraint: x1 + x2 = %.4f (expected 1.0)\n', sum(x_opt));
```

### 2.3 Convergence Visualization

```matlab
%% Steepest descent with exact line search on a quadratic, vs. the theoretical rate
A = [10, 1; 1, 1];   % eigenvalues ~0.890 and ~10.110, so cond(A) ~ 11.4
b = [1; 1];
grad_f = @(x) A*x - b;
x_exact = A \ b;
kappa = cond(A);
rate  = (kappa - 1) / (kappa + 1);   % per-step contraction in the A-norm

A_norm = @(e) sqrt(e' * A * e);
x = [5; 5];
err = A_norm(x - x_exact);
for k = 1:200
    g = grad_f(x);
    if norm(g) < 1e-14, break; end   % avoid 0/0 in alpha once converged
    alpha = (g'*g) / (g'*A*g);       % exact line search for a quadratic
    x = x - alpha*g;
    err(end+1) = A_norm(x - x_exact); %#ok<AGROW>
end

iters = 0:numel(err)-1;
figure;
semilogy(iters, err, 'b-', 'LineWidth', 2); hold on;
semilogy(iters, err(1) * rate.^iters, 'r--', 'LineWidth', 1.5);
xlabel('Iteration k'); ylabel('||x_k - x^*||_A');
legend('steepest descent', '((\kappa-1)/(\kappa+1))^k bound');
title('Steepest Descent: Linear Convergence Governed by \kappa(A)');
grid on; hold off;
```

The A-norm error satisfies $\|x_k - x^*\|_A \leq \left(\frac{\kappa-1}{\kappa+1}\right)^k \|x_0 - x^*\|_A$, which is the square root of the function-value bound in Nonlinear Optimization I. Try `A = [100, 1; 1, 1]` to watch the rate degrade.

---

## 3. Simulation and Visualization (Module B)

### Monte Carlo and Random Walks

```matlab
%% Simulate Brownian Motion paths
n_paths = 5;
n_steps = 1000;
dt = 1/n_steps;
t = (0:n_steps)*dt;

figure; hold on;
for i = 1:n_paths
    dW = sqrt(dt) * randn(1, n_steps);
    W = [0, cumsum(dW)];
    plot(t, W, 'LineWidth', 1.5);
end
xlabel('t'); ylabel('B(t)');
title('Sample Paths of Standard Brownian Motion');
grid on; hold off;

%% Verify E[B_t] = 0 and Var(B_t) = t
n_sim = 10000;
t_test = 0.5;
n_steps_sim = round(t_test / dt);
samples = zeros(n_sim, 1);
for i = 1:n_sim
    dW = sqrt(dt) * randn(1, n_steps_sim);
    samples(i) = sum(dW);
end
fprintf('E[B(%.1f)] = %.4f (expected 0)\n', t_test, mean(samples));
fprintf('Var(B(%.1f)) = %.4f (expected %.1f)\n', t_test, var(samples), t_test);
```

---

## Exercises

1. **Eigenvalue sensitivity**: Perturb a symmetric matrix by $\varepsilon E$ (random symmetric $E$) and plot eigenvalue shifts vs $\varepsilon$. Compare with Weyl's inequality bounds.
2. **Image compression via SVD**: Load an image as a matrix, compute the SVD, and reconstruct using rank-$k$ approximations for $k = 1, 5, 20, 50$. Plot the reconstruction error vs. $k$.
3. **Implement steepest descent from scratch**: Compare convergence on $f(x) = x^T A x / 2$ for well-conditioned ($\kappa = 2$) and ill-conditioned ($\kappa = 100$) matrices.
4. **Interior-point method**: Implement a basic log-barrier method for a small LP with 3 variables and 5 constraints. Plot the central path.
5. **Random walk simulation**: Simulate many independent simple symmetric random walks ($\pm 1$ steps) and verify the CLT: plot the histogram of $S_n / \sqrt{n}$ for large $n$ and overlay the $N(0,1)$ density. Extension: for the 2-D lattice walk (each step one of the four unit vectors), show that $S_n/\sqrt{n}$ is approximately $N(0, \tfrac{1}{2} I_2)$ and plot the joint histogram.
