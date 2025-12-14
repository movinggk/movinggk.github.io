# Ch.7: Solutions for Exercises
*Dongha Lee*

## Problem 1
*Let $\mathcal H$ be a Hilbert space of real-valued functions on $\mathcal X$ endowed with a dot product $\langle \cdot, \cdot \rangle_{\mathcal H}$, such that for any $x \in \mathcal X$, the linear form $f \mapsto f(x)$ is bounded(i.e., $\sup_{f \in \mathcal H, \|f\|_{\mathcal H} \leq 1} |f(x)|$ is finite). Using the Riesz representation theorem, show that this is an RKHS.*

**Definition (Dual Space).**

Let $\mathcal H$ be a Hilbert space over a field $\mathbb F$(either $\mathbb R$ or $\mathbb C$). Then its dual space, denoted as $\mathcal H^*$, is defined as the set of all continuous linear functionals mapping $\mathcal H$ onto $\mathbb F$.

**Definition (Dual Norm).**

Let $\mathcal H$ be a Hilbert space over a field $\mathbb F$ and $\mathcal H^*$ be its dual space. Then the dual norm is defined on $\mathcal H^*$ as
$$
\|f\|_{\mathcal H^*} = \sup_{\|x\|_{\mathcal H} \leq 1, x \in \mathcal H} |f(x)|, \quad \forall f \in \mathcal H^*.
$$

**Theorem (Riesz Representation Theorem).**

Let $\mathcal H$ be a Hilbert space over $\mathbb F$, whose inner product is linear in its first argument and antilinear in its second argument, i.e., for all $x, y, z \in \mathcal H$ and $c \in \mathbb F$,
$$
\langle cx, y \rangle = c \langle x, y \rangle,\quad \langle x, cy \rangle = \overline c \langle x, y \rangle, \quad \langle x + z, y \rangle = \langle x, y \rangle + \langle z, y \rangle, \quad \langle x, y + z \rangle = \langle x, y \rangle + \langle x, z \rangle.
$$
Then for all $\varphi \in \mathcal H^*$, there exists $f_\varphi \in \mathcal H$, called the Riesz representation of $\varphi$, such that
$$
\varphi(x) = \langle x, f_\varphi \rangle, \quad \forall x \in \mathcal H.
$$
Furthermore, $\|f_\varphi\|_{\mathcal H} = \|\varphi\|_{\mathcal H^*}$.

### Solution

Define $\psi: \mathcal X \rightarrow \mathcal H^*$ to be $\psi(x): f \mapsto f(x)$ for all $x \in \mathcal X$ and $f \in \mathcal H$. Such function exists since $\|\psi(x)\|_{\mathcal H^*} < \infty$ for all $x \in \mathcal X$. Then by the Riesz representation theorem, there exists $k_{\psi(x)} \in \mathcal H$ for all $\psi(x)$ such that
$$
\psi(x)(f) = f(x) = \langle f, k_{\psi(x)} \rangle_{\mathcal H}.
$$
Now letting $k(x, \cdot) = k_{\psi(x)}$, it can be realized that this is a reproducing kernel. Hence $\mathcal H$ is an RKHS.

---

## Problem 2
*Show that if $k: \mathcal X \times \mathcal X \rightarrow \mathbb R$ is a positive-definite kernel, so is the unction $(x, x') \mapsto e^{k(x, x')}$.*

### Solution

Symmetricity is trivial. Now with the arbitrary number of elements $\{x_1, \cdots, x_n\} \subset \mathcal X$, build the kernel matrix $K$ out of $k$ and let $r = \mathrm{rank}\, K$. Then since $K$ is real symmetric and positive semi-definite, there exists invertible $B \in \mathbb R^{r \times n}$ such that $K = B^\top B$, i.e.
$$
K_{ij} = \sum^r_{k = 1} B_{ki} B_{kj}.
$$
Hence for any $m \in \mathbb N$,
$$
K_{ij}^m = \sum^r_{k_1 = 1} \cdots \sum^r_{k_m = 1} B_{k_1 i}\cdots B_{k_m i} B_{k_1 j} \cdots B_{k_m j}.
$$
Now consider a map $\alpha$, which maps each possible $(k_1, \cdots, k_m)$ to natural number ranging from 1 to $n^m$. With that mapping, let $A \in \mathbb R^{n^m \times n}$ be
$$
A_{\alpha(k_1, \cdots, k_m), i} = B_{k_1 i}\cdots B_{k_m i},
$$
for each $k_1, \cdots, k_m$ and $i$. Then,
$$
K_{ij}^m = \sum^{n^m}_{\alpha = 1} A_{\alpha i} A_{\alpha j},
$$
and
$$
\sum_{ij} K_{ij}^m u_i u_j = \sum_{ij} \sum^{n^m}_{\alpha = 1} A_{\alpha i} u_i A_{\alpha j} u_j = \sum^{n^m}_{\alpha = 1} \left(\sum_i A_{\alpha i} u_i\right)^2 \geq 0,
$$
for all $u \in \mathbb R^n$. Hence the matrix, whose element in $i$th row and $j$th column is $K_{ij}^m$, is positive semidefinite. Now expanding $e^{k(x, x')}$,
$$
e^{k(x, x')} = \sum^\infty_{p = 0} \frac{1}{p!} k(x, x')^p
$$
And thus the kernel matrix constructed out of $e^{k(x, x')}$ has each element as a linear combination of $K_{ij}^m$s with different $m$, which are all positive semidefinite. Therefore $e^{k(x, x')}$ is a positive definite kernel.

---

## Problem 3
*Show that kernel $(x, x') = (1 + x^\top x')^s$ corresponds to the set of all monomials $x_1^{\alpha_1} \cdots x_d^{\alpha_d}$ such that $\alpha_1 + \cdots + \alpha_d \leq s$. Also, show that the dimension of the feature space is $\binom{d + s}{s}$.*
### Solution

Let $x_0 = x_0' = 1$ and construct a new vector $\mathbf x = (x_0, x_1, \cdots, x_n) \in \mathbb R^{n + 1}$. Then,
$$\begin{align*}
k(x, x') &= (\mathbf x^\top \mathbf x')^s\\
&= \sum_{\alpha_0 + \cdots + \alpha_d = s} \binom{s}{\alpha_0, \cdots, \alpha_d} (x_0 x_0')^{\alpha_0} \cdots (x_d x_d')^{\alpha_d}\\
&= \sum_{\alpha_0 + \cdots + \alpha_d = s} \binom{s}{\alpha_0, \cdots, \alpha_d} (x_1 x_1')^{\alpha_1} \cdots (x_d x_d')^{\alpha_d}.
\end{align*}
$$
Now since $\alpha_0$ ranges from 0 to $s$, the kernel is the linear combination of monomials $(x_1 x_1')^{\alpha_1} \cdots (x_d x_d')^{\alpha_d}$ such that $\alpha_1 + \cdots + \alpha_d \leq s$. Also, the feature map can be constructed as
$$
\varphi(x) = \left(\binom{s}{\alpha_0, \cdots, \alpha_d}^{1/2} x_1^{\alpha_1} \cdots x_d^{\alpha_d}\right)_{\alpha_1 + \cdots + \alpha_d = s},
$$
with dimension $\binom{d + s}{s}$, since $\mathbf x$ is in the space with one more dimension than where $x$ is.

---

## Problem 4
*Show that for $s = 2$, we have for all $x, x' \in [0, 1]$, $k(x, x') = q(x - x')$ with $q(t) = 1 - \frac{(2\pi)^4}{24}(\{t\}^4 - 2\{t\}^3 + \{t\}^2 - \frac{1}{30})$.*

### Solution

$$
\begin{align*}
q(t) &= 1 + \sum_{m \geq 1} \frac{2\cos(2\pi m t)}{m^4}, \\
\{t\} &= \frac{1}{2} - \frac{1}{2\pi} \sum_{m \geq 1} \frac{2 \sin(2\pi m t)}{m}, \\
\frac{1}{2} \{t\}^2 &= \frac{\{t\}}{2} + \frac{1}{(2\pi)^2} \sum_{m \geq 1} \frac{2(\cos(2\pi m t) - 1)}{m^2} = \frac{\{t\}}{2} - \frac{1}{12} + \frac{1}{(2\pi)^2} \sum_{m \geq 1} \frac{2\cos(2\pi m t)}{m^2}, \\
\frac{1}{6} \{t\}^3 &= \frac{\{t\}^2}{4} - \frac{\{t\}}{12} - \frac{1}{(2\pi)^3} \sum_{m \geq 1} \frac{2\sin(2\pi m t)}{m^3}, \\
\frac{1}{24} \{t\}^4 &= \frac{\{t\}^3}{12} - \frac{\{t\}^2}{24} - \frac{1}{(2\pi)^4} \sum_{m \geq 1} \frac{2(\cos(2\pi m t) - 1)}{m^4} = \frac{\{t\}^3}{12} - \frac{\{t\}^2}{24} + \frac{1}{720} + (2\pi)^4 - (2\pi)^4 q(t),\\
\end{align*}
$$
therefore,
$$
q(t) = 1 - \frac{(2\pi)^4}{24}\left(\{t\}^4 - 2\{t\}^3 + \{t\}^2 - \frac{1}{30}\right).
$$

---

## Problem 5
*Show that we have $k(x, x') = \sum_{m \in \mathbb Z} \frac{e^{2im\pi (x - x')}}{1 + \alpha^2 |m|^2} = q(x - x')$ for $q(t) = \frac{\pi}{\alpha} \frac{\cosh\left[\frac{\pi}{\alpha} (1 - 2|\{t + 1/2\} - 1/2|)\right]}{\sinh \frac{\pi}{\alpha}}$.*

### Solution

Define a linear operator
$$
L = 1 - \left(\frac{\alpha}{2\pi}\right)^2 \frac{\mathrm{d}^2 }{\mathrm{d} t^2 }.
$$
Then,
$$
L e^{2\pi i m t} = (1 + \alpha^2 m^2) e^{2\pi i m t},
$$
hence
$$
L\frac{e^{2\pi i m t}}{1 + \alpha^2 m^2} = e^{2\pi i m t},
$$
and
$$
L\sum_{m \in \mathbb Z} \frac{e^{2\pi i m t}}{1 + \alpha^2 m^2} = \sum_{m \in \mathbb Z} e^{2\pi i m t} = \sum_{n \in \mathbb Z} \delta(t - n).
$$
Therefore for $t \in (0, 1)$, we have $L q(t) = 0$. Solving, we have
$$
q(t) = A e^{2\pi t /\alpha} + B e^{-2 \pi t /\alpha},
$$
with some $A, B \in \mathbb R$. Observing the original expression, it can be realized that $q$ must be even and is 1-periodic, thus it is symmetric by $t = 1/2$, i.e. $q(1/2 + t) = q(1/2 - t)$. Therefore
$$
A \exp\left(\frac{\pi}{\alpha} + \frac{2\pi t}{\alpha}\right) + B \exp\left(-\frac{\pi}{\alpha} - \frac{2\pi t}{\alpha}\right) = A \exp\left(\frac{\pi}{\alpha} - \frac{2\pi t}{\alpha}\right) + B \exp\left(-\frac{\pi}{\alpha} + \frac{2\pi t}{\alpha}\right),
$$
and thus
$$
A = C\exp\left(-\frac{\pi}{\alpha}\right), \quad B = C\exp\left(\frac{\pi}{\alpha}\right),
$$
and
$$
q(t) = C \cosh\left(\frac{2\pi t}{\alpha} - \frac{\pi}{\alpha}\right),
$$
for some constant $C \in \mathbb R$. Now let us consider its behavior near an integer, say 0.
$$
\int^\varepsilon_{-\varepsilon} L q(t) \,\mathrm{d}  t = \int^\varepsilon_{-\varepsilon} \left[q(t) - \left(\frac{\alpha}{2\pi}\right)^2 q''(t)\right] \,\mathrm{d}  t = 1,
$$
And thus
$$
\left(\frac{\alpha}{2\pi}\right)^2 \left[q'(\varepsilon) - q'(- \varepsilon)\right] = \int^\varepsilon_{-\varepsilon} q(t) \,\mathrm{d}  t - 1.
$$
Since $q$ is even, $q'$ will be odd. Applying the oddness of derivative of $q$ and taking $\varepsilon \rightarrow 0$,
$$
\left(\frac{\alpha}{2\pi}\right)^2 q'(0) = - \frac{1}{2}.
$$
Meanwhile,
$$
q'(t) = \frac{2 \pi C}{\alpha} \sinh\left(\frac{2\pi t}{\alpha} - \frac{\pi}{\alpha}\right),
$$
thus
$$
C = \frac{\pi}{\alpha} \frac{1}{\sinh \frac{\pi}{\alpha}}.
$$
Therefore it can be concluded to be
$$
q(t) = \frac{\pi}{\alpha} \frac{1}{\sinh \frac{\pi}{\alpha}} \cosh\left(\frac{2\pi t}{\alpha} - \frac{\pi}{\alpha}\right).
$$
Now since this is valid only for $t \in [0, 1)$, it is required to make it work for all $t \in \mathbb R$. Using the periodicity and evenness of the original function, replacing $t$ to $|\{t + 1/2\} - 1/2|$(distance to the nearest integer) is enough. Hence,
$$
q(t) = \frac{\pi}{\alpha} \frac{1}{\sinh \frac{\pi}{\alpha}} \cosh\left[\frac{\pi}{\alpha}\left( 1 - 2 \left| \left\{ t + \frac{1}{2} \right\} - \frac{1}{2} \right|\right)\right].
$$

---

## Problem 6[Mercer kernels]
*Consider a probability distribution $p$ on a set $\mathcal X$, an orthonormal basis $(\varphi_i)_{i \in I}$ of the Hilbert space $L_2(p)$ of square-integrable functions(with $I$ countable), and a summable positive sequence $(\lambda_i)_{i \in I}$. Show that the function defined as $k(x, x') = \sum_{i \in I} \lambda_i \varphi_i(x) \varphi_i(x')$ is a positive-definite kernel and describe an associated feature space.*

### Solution

Consider a feature map $\psi: \mathcal X \rightarrow L_2(p)$ which is defined as
$$
\psi(x) = \sum_{i \in I} \lambda_i^{1/2} \varphi_i(x) \varphi_i
$$
for all $x \in \mathcal X$. Then,
$$
\begin{align*}
\langle \psi(x), \psi(x') \rangle_{L_2(p)} &= \sum_{i, j \in I} \lambda_i^{1/2} \lambda_j^{1/2} \varphi_i(x) \varphi_j (x') \langle \varphi_i,  \varphi_j \rangle_{L_2(p)}\\
&= \sum_{i \in I} \lambda_i \varphi_i(x) \varphi_i(x') = k(x, x').
\end{align*}
$$
Hence by the Aronszajn's theorem, $k$ is a positive-definite kernel. The RKHS(which will be denoted as $\mathcal H$) of $k$ exists again by the Aronszajn's theorem. Now letting $\mathcal H_0 = \mathrm{span}\, \{k(x, \cdot) \mid x \in \mathcal X\}$, for all $f\in \mathcal H_0$, there are $n \in \mathbb N$, $\{x_1, \cdots, x_n\}\subset \mathcal X$, $\{\alpha_1, \cdots, \alpha_n \} \subset \mathbb R$ such that
$$
f = \sum^n_{i = 1} \alpha_i k(x_i, \cdot),
$$
and since $k(x, \cdot)$ for some $x \in \mathcal X$ is a linear combination of $\{\varphi_i\}_{i \in I}$, $\mathcal H_0 \subset L_2(p)$. And because $L_2(p)$ is complete and $\mathrm{cl}\, \mathcal H_0 = \mathcal H$, $\mathcal H \subset L_2(p)$. For the inner product, it is known that the kernel in $\mathcal H$ should satisfy the reproductive property, i.e. for all $f \in \mathcal H$,
$$
f(x) = \langle f, k(x, \cdot) \rangle_{\mathcal H}, \quad \forall x \in \mathcal X.
$$
Thus for $\varphi_i \in \mathcal H$,
$$
\varphi_i(x) = \langle \varphi_i, k(x, \cdot) \rangle_{\mathcal H} = \sum_{j \in I} \lambda_j \varphi_j(x) \langle \varphi_i, \varphi_j \rangle_{\mathcal H},
$$
and
$$
\langle \varphi_i, \varphi_j \rangle_{L_2(p)} = \sum_{k \in I} \lambda_k \langle \varphi_i, \varphi_k \rangle_{L_2(p)} \langle \varphi_j, \varphi_k \rangle_{\mathcal H} = \lambda_i \langle \varphi_j, \varphi_i \rangle_{\mathcal H},
$$
hence $\langle \varphi_j, \varphi_i \rangle_{\mathcal H} = \langle \varphi_i, \varphi_j \rangle_{\mathcal H} = \delta_{ij} / \lambda_i$. Now for $f, g \in \mathcal H$, $\{\alpha_i\}_{i \in I}, \{\beta_i\}_{i \in I} \subset \mathbb R$ such that
$$
f = \sum_{i \in I} \alpha_i \varphi_i, \quad g = \sum_{i \in I} \beta_i \varphi_i,
$$
thus
$$
\langle f, g \rangle_{\mathcal H} = \sum_{ij \in I} \alpha_i \beta_j \langle \varphi_i, \varphi_j \rangle_{\mathcal H} = \sum_{i \in I} \frac{1}{\lambda_i}\alpha_i \beta_i.
$$

---

## Problem 7[Mercer decomposition]
*Consider a probability distribution $p$ in a set $\mathcal X$, a positive-definite kernel $k: \mathcal X \times \mathcal X \rightarrow \mathbb R$, and the operator $T$ defined on $L_2(p)$ as $T f(y) = \int_{\mathcal X} k(x, y) f(x) \,\mathrm{d} {p(x)}$.*
- *Show that if $\int_{\mathcal X} \int_{\mathcal X} k(x, y)^2 \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)}$ is finite, then the operator $T$ is bounded(it is an instance of Hilbert-Schmidt integral operator).*
- *Given an orthonormal basis $(\varphi_i)_{i \in I}$ of $L_2(p)$ composed of eigenvectors for $T$(which is assumed to exist), show that the corresponding eigenvalues $(\lambda_i)_{i \in I}$ are nonnegative and $k(x, x') = \sum_{i \in I} \lambda_i \varphi_i(x) \varphi_i (x')$ (convergence meant in the norm $L_2(p)$).*

### Solution

(It will be assumed that $k(x, \cdot) \in L_2(p)$.)For all $f \in L_2(p)$,
$$
\begin{align*}
\|Tf\|_{L_2(p)}^2 &= \int_{\mathcal X} \left| \int_{\mathcal X} k(x, y) f(x) \,\mathrm{d} {p(x)}\right|^2 \,\mathrm{d} {p(y)}\\
&\leq \int_{\mathcal X} \left[\int_{\mathcal X}  \left| k(x, y) \right|^2 \,\mathrm{d} {p(x)} \int_{\mathcal X} \left|f(x)\right|^2 \,\mathrm{d} {p(x)} \right]\,\mathrm{d} {p(y)} \\
&= \|f\|_{L_2(p)}^2 \int_{\mathcal X} \int_{\mathcal X}  \left| k(x, y) \right|^2 \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)},
\end{align*}
$$
by the Cauchy-Schwartz inequality. Therefore $T$ is bounded. Now for the eigenvalues,
$$
T \varphi_i(y) = \int_{\mathcal X} k(x, y) \varphi_i(x) \,\mathrm{d} {p(x)} = \lambda_i \varphi_i(y),
$$
and
$$
\lambda_i = \langle T \varphi_i, \varphi_i \rangle_{L_2(p)} = \int_{\mathcal X} \int_{\mathcal X} k(x, y) \varphi_i(x) \varphi_i(y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)}.
$$
By the Aronszajn's theorem, there exists an RKHS $\mathcal H$ of $k$ with inner product $\langle \cdot, \cdot \rangle_{\mathcal H}$, and the function $\psi: \mathcal X \rightarrow \mathcal H$ such that $k(x, x') = \langle \psi(x), \psi(x') \rangle_{\mathcal H}$. Hence,
$$
\begin{align*}
\int_{\mathcal X} \int_{\mathcal X} k(x, y) \varphi_i(x) \varphi_i(y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)} &= \int_{\mathcal X} \int_{\mathcal X} \langle \psi(x), \psi(y) \rangle_{\mathcal H} \varphi_i(x) \varphi_i(y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)}\\
&= \left\|\int_{\mathcal X} \psi(x) \varphi_i(x) \,\mathrm{d} {p(x)}\right\|_{\mathcal H}^2 \geq 0.
\end{align*}
$$
Now since for all $j \in I$,
$$
\langle k(x, \cdot), \varphi_j\rangle_{L_2(p)} = \sum_{i \in I} \lambda_i \varphi_i(x) \langle \varphi_i(x') \varphi_j(x') \rangle_{L_2(p)} = \lambda_j \varphi_j(x),
$$
thus
$$
k(x, x') = \sum_{i \in I} \lambda_i \varphi_i(x) \varphi_i(x').
$$

---

## Problem 8
*Show that column sampling corresponds to approximating optimally each $\varphi(x_j)$, $j \notin I$, by a linear combination of $\varphi(x_i)$, $i \in I$.*

### Solution

Consider a space spaned by $\{\varphi(x_i)\}_{i \in I}$. The projection of $\varphi(x_j)$ with $j \notin I$ onto this space is determined with
$$
\underset{\alpha \in \mathbb R^{I}}{\mathrm{argmin}} \, \left\|\varphi(x_j) - \sum_{i \in I} \alpha_i \varphi(x_i)\right\|_{\mathcal H}.
$$
Let the solution to be $\alpha^j$. $\alpha^j$ can be obtained by solving the root-finding of the derivative, say, observing the differentiation by $\alpha_k^j$,
$$
\sum_{i \in I} \alpha^j_i \langle \varphi(x_k), \varphi(x_i) \rangle_{\mathcal H} = \langle \varphi(x_k), \varphi(x_j) \rangle_{\mathcal H}.
$$
Now let $A \in \mathbb R^{J \times I}$ be $A_{jk} = \alpha^j_k$. Since $K_{ij} = \langle \varphi(x_i), \varphi(x_j) \rangle_{\mathcal H}$ for all $i, j$, upper equation can be rewritten as
$$
A K(I, I) = K(J, I),
$$
also, the following approximation is plausible:
$$
K(J, J) \approx A K(I, I) A^\top = A K(I, I) K(I, I)^+ K(I, I) A^\top = K(J, I) K(I, I)^+ K(I, J).
$$
This is exactly the same as the Nynstr\"om approximation.

---

## Exercise 9
*Show that the matrix $K - K(V, I) K(I, I)^+ K(I, V)$ is positive-semidefinite. If $\|M\|_*$ denotes the nuclear norm(sum of absolute values of eigenvalues of symmetric matrix $M$), show that the approximation error $\|K - K(V, I) K(I, I)^+ K(I, V)\|_*$ can be computed without the need to compute the entire matrix $K$.*

### Solution

My the Mercer theorem which was shown in **Problem 7**,
$$
k(x, x') = \sum_{\alpha \in \Lambda} \lambda_\alpha \varphi_\alpha(x) \varphi_\alpha(x'),
$$
with $\lambda_i$ and $\varphi_i \in L_2(\mathcal X, p)$ are the eigenvalue and eigenfunction of the operator $T: f \mapsto \int_{\mathcal X} k(x, \cdot) f(x) \,\mathrm{d} {p(x)}$, respectively for each $i \in \Lambda$, with $\Lambda$ being the set of indices for eigenvalues and eigenvectors. Then, construction of the kernel matrix is done by
$$
K_{ij} = \sum_{\alpha \in \Lambda} \lambda_\alpha \varphi_\alpha(x_i) \varphi_\alpha(x_j),
$$
with $n$ given data. Now letting $\Phi \in \mathbb R^{\Lambda \times V}$ be $\Phi_{\alpha i} = \lambda_\alpha^{1/2} \varphi_\alpha (x_i)$, then $K = \Phi^\top \Phi$. For convenience, let $\Phi_1 = \Phi(\Lambda, I)$, $\Phi_2 = \Phi(\Lambda, J)$, $K_1 = K(I, I)$, $K_2 = K(I, J) = K(J, I)^\top$, $K_3 = K(J, J)$. Then,
$$
K_1 = \Phi_1^\top \Phi_1, \quad K_2 = \Phi_1^\top \Phi_2, \quad K_3 = \Phi_2^\top \Phi_2,
$$
$$
M = K - \begin{pmatrix}
K_1 K_1^+ K_1 & K_1 K_1^+ K_2 \\
K_2^\top K_1^+ K_1 & K_2^\top K_1^+ K_2
\end{pmatrix} = \begin{pmatrix}
0 & (I - K_1 K_1^+) K_2 \\
K_2^\top (I - K_1^+ K_1) & K_3 - K_2^\top K_1^+ K_2
\end{pmatrix}.
$$
Now consider the SVD $\Phi_1 = U \Sigma V^\top$. Then
$$
K_1 = V \Sigma^\top \Sigma V^\top, \quad K_2 = V \Sigma^\top U^\top \Phi_2.
$$
And also, since $K_1^+ = V (\Sigma^\top \Sigma)^+ V^\top = V (\Sigma^\top \Sigma)^{-1} V^\top$,
It can be realized that
$$
K_1 K_1^+ = V V^\top, \quad K_1 K_1^+ K_2 = V \Sigma^\top U^\top \Phi_2 = K_2.
$$
Hence,
$$
M = \begin{pmatrix}
0 & 0\\
0 & K_3 - K_2^\top K_1^+ K_2
\end{pmatrix}.
$$
Now for all $u \in \mathbb R^V$, let $u_1 = u(I)$, $x_2 = u(J)$. then
$$
u^\top M u = u_2^\top K_3 u_2 - u_2^\top K_2^\top K_1^+ K_2 u_2.
$$
Borrowing the notations from the **Problem 8**, and letting some feature map for $k$ be $\psi: \mathcal X \rightarrow \mathcal H$, since the Nynstr\"om approximation is equivalent to the orthogonal projection of $\psi(x_j)$ onto $\psi(x_i)$ where $j > \mathrm{rank}\, K \geq i$, there exists a orthogonal projection operator $\mathcal P: \mathcal H \rightarrow \mathrm{span}\{\psi(x_i)\}_{i \in I}$ such that
$$
\mathcal P \psi(x_j) = \sum_{i \in I} \alpha^j_i \psi(x_i),
$$
for $j \in J$. Now expressing this equation into $\varphi$-base representation, $\psi(x) = \sum_{\alpha \in \Lambda} \langle \psi(x), \varphi_\alpha \rangle_{L_2(p)} \varphi_\alpha$,
$$
\sum_{\alpha \in \Lambda}\langle\psi(x_j), \varphi_\alpha\rangle_{L_2(p)} \mathcal P \varphi_\alpha = \sum_{i \in I} \alpha^j_i \sum_{\beta \in \Lambda}\langle \psi(x_i), \varphi_\beta \rangle_{L_2(p)}\varphi_\beta,
$$
since $\mathcal P$ is linear. Let $P \in \mathbb R^{\Lambda \times \Lambda}$ be $P_{\alpha \gamma} = \langle \mathcal P \varphi_\gamma, \varphi_\alpha \rangle_{L_2(p)}$ and $\Psi \in \mathbb R^{\Lambda \times V}$ be $\Psi_{\alpha i} = \langle \psi(x_i), \varphi_\alpha \rangle_{L_2(p)}$. Then,
$$
\sum_{\alpha \in \Lambda} P_{\gamma \alpha} \Psi_{\alpha j} = \sum_{i \in I} A_{ji} \Psi_{\gamma i}
$$
Letting $\Psi_1 = \Psi(\Lambda, I)$ and $\Psi_2 = \Psi(\Lambda, J)$,
$$
P \Psi_2 = \Psi_1 A^\top.
$$
Now $G \in \mathbb R^{\Lambda \times \Lambda}$ be $G_{\alpha \beta} = \langle \varphi_\alpha, \varphi_\beta \rangle_{\mathcal H}$, then the equation $k(x, x') = \langle \psi(x), \psi(x') \rangle_{\mathcal H}$ gives a new expression for the kernel matrix,
$$
K = \Psi^\top G \Psi.
$$
Thus,
$$
K_1 = \Psi_1^\top G \Psi_1, \quad K_2 = \Psi_1^\top G \Psi_2, \quad K_3 = \Psi_2^\top G \Psi_2,
$$
and
$$
K_3 - K_2^\top K_1^+ K_2 = K_3 - A K_1 A^\top = \Psi_2^\top G \Psi_2 - A \Psi_1^\top G \Psi_1 A^\top = \Psi_2^\top (I - P)^\top G (I - P) \Psi_2,
$$
as $K_2^\top K_1^+ K_2 = A K_1 A^\top$ was shown in **Problem 8**. Hence
$$
u^\top M u = u_2^\top \Psi_2^\top (I - P)^\top G (I - P) \Psi_2 u_2 \geq 0,
$$
since $G$ is positive-semidefinite, because for an arbitrary $v \in \mathbb R^\Lambda$,
$$
v^\top G v = \left< \sum_{\alpha \in \Lambda} v_\alpha \varphi_\alpha, \sum_{\beta \in \Lambda} v_\beta \varphi_\beta \right>_{\mathcal H} = \left\|\sum_{\alpha \in \Lambda} v_\alpha \varphi_\alpha\right\|_{\mathcal H}^2 \geq 0.
$$
Thus $M$ is positive-semidefinite. Because of the positive-semidefinitiveness, the nuclear norm of $M$ is just the trace,
$$
\|M\|_* = \mathrm{Tr} \, M = \mathrm{Tr}\, K_3 - \mathrm{Tr} \left[K_2^\top K_1^+ K_2\right],
$$
hence we only need to know what $K_1$, $K_2$ and diagonal elements of $K_3$. Note that
$$
\begin{align*}
\|M\|_* &= \mathrm{Tr}[\Psi_2^\top (I - P)^\top G (I - P) \Psi_2] \\
&= \sum_{j \in J} \left\|\sum_{\alpha, \beta \in \Lambda}\varphi_\alpha (\delta_{\alpha \beta} - P_{\alpha \beta}) \Psi_{\beta j}\right\|_{\mathcal H}^2 = \sum_{j \in J} \|\psi(x_j) - \mathcal P \psi(x_j)\|_{\mathcal H}^2,
\end{align*}
$$
thus it is a squared-sum of the errors by RKHS-norm for approximation by projection.

---

## Problem 10
*In the setup of **Problem 6**, provide a random feature expansion of Mercer kernels.*
### Solution

$$
k(x, x') = \sum_{i \in I} \lambda_i^{1/2} \varphi_i(x) \varphi_i(x').
$$
Let $\psi: \mathcal X \rightarrow L_2(p)$ be
$$
\psi(x) = \sum_{i \in I} \lambda_i^{1/2} \varphi_i(x) \varphi_i.
$$
Then,
$$
k(x, x') = \langle \psi(x), \psi(x') \rangle_{L_2(p)}.
$$
Now appliying the random feature method,
$$
\begin{align*}
k(x, x') &= \langle \psi(x), \psi(x') \rangle_{L_2(p)}\\
&= \sum_{i, j \in I} \lambda_i^{1/2} \lambda_j^{1/2} \varphi_i(x) \varphi_j(x') \int_{\mathcal X} \varphi_i(\xi) \varphi_j(\xi) \,\mathrm{d} {p(x)}\\
&\approx \frac{1}{m} \sum_{i, j \in I} \lambda_i^{1/2} \lambda_j^{1/2} \varphi_i(x) \varphi_j(x') \sum^m_{k = 1} \varphi_i(v_k) \varphi_j(v_k).
\end{align*}
$$
Now construct an explicit feature representation $\hat \varphi: \mathcal X \rightarrow \mathbb R^m$ as
$$
\hat \varphi_m = \frac{1}{m^{1/2}} \sum_{i \in I} \lambda_i^{1/2}\varphi_i(v_m) \varphi_i,
$$
so that
$$
k(x, x') \approx \hat \varphi(x)^\top \hat \varphi(x').
$$

---

## Problem 11
*(a) For ridge regression, compute the dual problem and compare the condition number of the primal problem and the condition number of the dual problem; (b) compare the two formulatioins to the use of normal equations as in chapter 3, and relate the two using the matrix inversion lemma $(\Phi \Phi^\top + n\lambda I)^{-1} \Phi = \Phi(\Phi^\top \Phi + n \lambda I)^{-1}$.*
### Solution

(a) For the ridge regression, the loss $l$ is given as the square function, and the dual problem is
$$
\max_{\alpha \in \mathbb R^n} \left\{\frac{1}{n} \sum^n_{i = 1} \min_{u_i \in \mathbb R} \{(y_i - u_i)^2 + n\lambda \alpha_i u_i \} - \frac{\lambda}{2} \alpha^\top K \alpha\right\}.
$$
The minimization problem inside of the summation, with respect to $u_i$, can be solved easily,
$$
\min_{u_i \in \mathbb R} \{(y_i - u_i)^2 + n\lambda \alpha_i u_i \} = n\lambda \alpha_i y_i - \frac{1}{4} (n \lambda \alpha_i)^2.
$$
Thus the problem is
$$
\max_{\alpha \in \mathbb R^n}\left\{\lambda \alpha^\top y - \frac{1}{4} n \lambda^2 \alpha^\top \alpha - \frac{\lambda}{2} \alpha^\top K \alpha \right\}
$$
Solving this problem in exact way might not be easy because it includes the inversion of large matrix $K$. Solving in iterative way, the condition number $\kappa_\mathrm{dual}$ would be
$$
\kappa_\mathrm{dual} = \frac{\sigma_\mathrm{max}(K + n\lambda I / 2)}{\sigma_\mathrm{min}(K + n\lambda I / 2)}.
$$
The primal problem refers to the original problem, and is solving the following:
$$
\min_{\alpha \in \mathbb R^n} \left\{\frac{1}{n} (K \alpha - y)^\top (K \alpha - y) + \frac{\lambda}{2} \alpha^\top K \alpha\right\}.
$$
The condition number $\kappa_\mathrm{primal}$ would be
$$
\kappa_\mathrm{primal} = \frac{\sigma_\mathrm{max}(K^\top K / n + \lambda K / 2)}{\sigma_\mathrm{min}(K^\top K / n + \lambda K / 2)} = \frac{\sigma_\mathrm{max}(K)^2 / n + \lambda \sigma_\mathrm{max}(K) / 2}{\sigma_\mathrm{min}(K)^2 / n + \lambda \sigma_\mathrm{min}(K) / 2},
$$
since $K$ is symmetric positive-semidefinite. Therefore dual problem is not ill-posed unlike the primal problem is when $n\lambda$ is large. When $n \lambda$ is small, $\kappa_\mathrm{primal} \sim \kappa_\mathrm{dual}^2$. (b) The normal equations for the primal and dual are
$$
\alpha^*_\mathrm{primal} = \left(K^2 + \frac{n\lambda}{2} K\right)^{-1} K y,\\
\alpha^*_\mathrm{dual} = \left(K + \frac{n\lambda}{2} I\right)^{-1} y,

$$
respectively($K$ assumed to be invertible). Decomposing $K$ as $K = \Phi \Phi^\top$(such $\Phi$ exists because of the positive-semidefinitiveness), and using the matrix inversion lemma,
$$
\begin{align*}
\alpha_\mathrm{primal}^* &= K^{-1} \left(\Phi\Phi^\top + \frac{n\lambda}{2} I\right)^{-1} \Phi \Phi^\top y
\\
&= K^{-1} \Phi \left(\Phi^\top \Phi + \frac{n\lambda}{2} I\right)^{-1} \Phi^\top y \\
&= K^{-1} \Phi \Phi^\top \left(\Phi\Phi^\top + \frac{n\lambda}{2} I \right)^{-1} y = \left(K + \frac{n\lambda}{2} I\right)^{-1} y.
\end{align*}
$$
Thus the primal solution is the same as the dual solution. It is because both problems are finding the best fitting $\alpha \in \mathbb R^n$ such that $\theta = \sum^n_{i = 1} \alpha_i \varphi(x_i)$.

---

## Problem 12
*Write down the dual problem in equation (7.9) for the logistic loss and for the hinge loss(compare ther results to section 4.1.2).*

### Solution

The logistic loss is defined as $l(y, y') = \log(1 + e^{-yy'})$. The dual problem is written as
$$
\max_{\alpha \in \mathbb R^n} \left\{ \frac{1}{n} \sum^n_{i = 1} \min_{u_i \in \mathbb R} \left\{\log(1 + e^{-y_iu_i}) + n\lambda \alpha_i u_i\right\} - \frac{\lambda}{2} \alpha^\top K \alpha \right\}
$$
Note that the minimization inside of the summation is convex optimization problem but it goes $-\infty$ when $1 < n\lambda \alpha_i / y_i$ or $\alpha_i y_i < 0$(i.e. having opposite sign). Thus $\alpha_i$ must satisfy $1 \geq n\lambda \alpha_i / y_i$ and $\alpha_i y_i \geq 0$ for all $i = 1, \cdots, n$. Now solving the minimization inside of the summation under thoes constraints,
$$
\min_{u_i \in \mathbb R} \left\{\log(1 + e^{-y_iu_i}) + n\lambda \alpha_i u_i\right\} = - \left(1 - \frac{n\lambda \alpha_i}{y_i}\right) \log\left(1 - \frac{n\lambda\alpha_i}{y_i} \right) - \frac{n\lambda\alpha_i}{y_i} \log\frac{n\lambda \alpha_i}{y_i},
$$
which is binary cross-entropy loss with $n\lambda \alpha_i / y_i$ as an argument. This is a concave function on $- n \lambda \alpha_i$ since it is a negative of the convex conjugate.

**Definition (Convex conjugate).**

For a function $f: \mathbb R^d \rightarrow [-\infty, \infty]$, its convex conjugate $f^*: \mathbb R^d \rightarrow [-\infty, \infty]$ is defined as
$$
f^*(y) = \sup_{x \in \mathbb R^d} \{\langle x, y \rangle - f(x) \}.
$$

**Theorem (Pointwise supremum of affine functions is convex).**

Let $H$ be a set of some affine functions on $\mathbb R^d$. Then, a function $f: \mathbb R^d \rightarrow [-\infty, \infty]$ which is defined as
$$
f(x) = \sup_{h \in H} h(x), \quad \forall x \in \mathbb R^d,
$$
is convex.

**Proof.**

For all $x, y \in \mathbb R^d$ and $\lambda \in [0, 1]$,
$$
\begin{align*}
f(\lambda x + (1 - \lambda) y) &= \sup_{h \in H} h(\lambda x + (1 - \lambda y))\\
&= \sup_{h \in H} \{ \lambda h(x) + (1 - \lambda) h(y) \}\\
&\leq \lambda \sup_{h \in H} h(x) + (1 - \lambda) \sup_{h \in H} h(y) = \lambda f(x) + (1 - \lambda) f(y),
\end{align*}
$$
hence $f$ is convex.

∎

Hence, the maximization problem can be solved by solving the root-finding problem of its gradient. For the hinge loss, $l(y, y') = \max(1 - yy', 0)$, and the dual problem is written as
$$
\max_{\alpha \in \mathbb R^n} \left\{ \frac{1}{n} \sum^n_{i = 1} \min_{u_i \in \mathbb R} \left\{\max(1 - y_i u_i, 0) + n\lambda \alpha_i u_i\right\} - \frac{\lambda}{2} \alpha^\top K \alpha \right\}.
$$
Again, the minimization problem inside of the summation is a convex optimization problem. In this case, the condition $0 \leq n \lambda \alpha_i y_i \leq 1$ sould be satisfied, otherwise it goes $-\infty$. Solving under this condition,
$$
\min_{u_i \in \mathbb R} \left\{\max(1 - y_i u_i, 0) + n\lambda \alpha_i u_i\right\} = \frac{n\lambda \alpha_i}{y_i}.
$$
Therefore the maximization is the same as
$$
\max_{\alpha \in \mathbb R^n} \left\{ \lambda \sum^n_{i = 1} \frac{\alpha_i}{y_i} - \frac{\lambda}{2} \alpha^\top K \alpha \right\}.
$$
Now convert variable: $\alpha_i \leftarrow \alpha_i/y_i$. Then,
$$
\max_{\alpha \in \mathbb R^n} \left\{\lambda \sum^n_{i = 1} \alpha_i - \frac{\lambda}{2} \sum^n_{i = 1} \sum^n_{j = 1} \alpha_i \alpha_j y_i y_j K_{ij} \right\},
$$
with conditions $0 \leq n \lambda \alpha_i \leq 1$. Therefore the dual problem with the hinge loss is similar to dual problem of the SVM with soft margin $C = 1/(n\lambda)$, but without the feasibility condition $\sum^n_{i = 1} \alpha_i y_i = 0$. In order to include the feasibility condition, the intercept term should be introduced, see the **Problem 13**.

---

## Problem 13[Unregularized constant term]
*Consider the minimization problem $\min_{\theta \in \mathcal H, c \in \mathbb R} \frac{1}{n} \sum^n_{i = 1} l(y_i, \langle \varphi(x_i), \theta\rangle + c) + \frac{\lambda}{2} \|\theta\|^2$. If the loss function is convex with respect to the second variable, show that the dual problem is the one in equation (7.9) with the additional constraint that $\sum^n_{i = 1} \alpha_i = 0$. Without any assumption on the loss function, show that we can restrict the search space for $\theta$ to all combinations $\sum^n_{i = 1} \alpha_i \varphi(x_i)$ with the same constraint that $\sum^n_{i = 1} \alpha_i = 0$.*

### Solution

The given minimization problem can be converted to a following constrained optimization problem:
$$
\min_{\theta \in \mathcal H, u \in \mathbb R^n} \frac{1}{n} \sum^n_{i = 1} l(y_i, u_i) + \frac{\lambda}{2} \|\theta \|^2 \quad \text{such that}\quad \langle \varphi(x_i), \theta \rangle + c = u_i.
$$
Then the dual problem comes out as
$$
\max_{\alpha \in \mathbb R^n} \min_{u\in \mathbb R^n, c \in \mathbb R, \theta \in \mathcal H} \left\{\frac{1}{n} \sum^n_{i = 1}  l(y_i, u_i) + \frac{\lambda}{2} \|\theta \|^2 + \lambda \sum^n_{i = 1} \alpha_i(u_i - c - \langle \varphi(x_i), \theta \rangle) \right\},
$$
which is equivalently,
$$
\max_{\alpha \in \mathbb R^n} \left\{\frac{1}{n} \sum^n_{i = 1} \min_{u_i \in \mathbb R} \{l(y_i, u_i) + n \lambda \alpha_i u_i\} + \min_{\theta \in \mathcal H} \left\{\frac{\lambda}{2} \|\theta \|^2 - \lambda \sum^n_{i = 1} \alpha_i \langle \varphi(x_i), \theta \rangle \right\} - \max_{c \in \mathbb R} \left\{c \sum^n_{i = 1} \alpha_i \right\}\right\}.
$$
The third term inside of the maximization over $\alpha \in \mathbb R^n$ gives the condition of $\sum^n_{i = 1} \alpha_i = 0$, because if not, it returns $- \infty$, which is trivially not a solution. Now define
$$
\psi(x) = \varphi(x) - \frac{1}{n} \sum^n_{i = 1} \varphi(x_i), \quad \tilde c = c + \frac{1}{n} \sum^n_{i = 1} \langle \varphi(x_i), \theta\rangle.
$$
Then the minimization problem can be rewritten as
$$
\min_{\theta \in \mathcal H, \tilde c \in \mathbb R} \left\{ \frac{1}{n} \sum^n_{i = 1} l(y_i, \langle\psi(x_i), \theta\rangle + \tilde c) + \frac{\lambda}{2} \|\theta\|^2 \right\}.
$$
By the representer theorem, $\theta \in \mathrm{span}\{\psi(x_1), \cdots, \psi(x_n)\}$. With some $\beta \in \mathbb R^n$, letting $\theta = \sum^n_{i = 1} \beta_i \psi(x_i)$,
$$
\theta = \sum^n_{i = 1} \beta_i \psi(x_i) = \sum^n_{i = 1} \beta_i \varphi(x_i) - \frac{1}{n} \sum^n_{i = 1} \beta_i \sum^n_{j = 1} \varphi(x_i) = \sum^n_{i = 1} \left(\beta_i - \frac{1}{n} \sum^n_{j = 1} \beta_j\right) \varphi(x_i),
$$
thus letting $\alpha \in \mathbb R^n$ be
$$
\alpha_i = \beta_i - \frac{1}{n} \sum^n_{j = 1} \beta_j,
$$
for each $i = 1, \cdots, n$, $\theta = \sum^n_{i = 1} \alpha_i \varphi(x_i)$ and $\sum^n_{i = 1} \alpha_i = 0$. The reason for this argument is possible is because with $c$, $\tilde c$ can be treated as the independent variable. Without $c$, $\tilde c$ should be fully determined by $\theta$ and the representer theorem with redefined variables cannot be applied.

---

## Problem 14[Limit of Gaussian kernel for infinite bandwidth]

*Consider the minimization problem $\min_{\theta \in \mathcal H, c \in \mathbb R} \frac{1}{n} \sum^n_{i = 1} l(y_i, \langle \varphi(x_i), \theta \rangle + c ) + \frac{\lambda}{2} \|\theta\|^2$ from exercise 7.13. For the Gaussian kernel $k(x, x') = \exp(- \|x - x'\|_2^2/r^2)$, show that when $r$ tends to infinity, the resulting prediction function is the same as the one obtained by the linear kernel $k(x, x') = x^\top x'$ with the regularization parameter $\lambda r^2/2$.*

### Solution

As it was shown in in **Problem 13**, the resulting $\theta$ has the form of
$$
\theta = \sum^n_{i = 1} \alpha_i \varphi(x_i),
$$
with $\alpha \in \mathbb R^n$ satisfying $\sum^n_{i = 1} \alpha_i = 0$. When $r$ tends to infinity, the exponential kernel can be approximated into the quadratic function on $x$ and $x'$, i.e.
$$
k(x, x') \approx 1 - \frac{\|x - x'\|_2^2}{r^2}.
$$
Substituting, the resulting prediction function is in the form of
$$
f(x) = \langle \varphi(x), \theta \rangle = \sum^n_{i = 1} k(x, x_i) \alpha_i \approx - \sum^n_{i = 1} \frac{\|x - x_i\|_2^2}{r^2} \alpha_i = 2\sum^n_{i = 1} \frac{x^\top x_i}{r^2} \alpha_i - \sum^n_{i = 1} \frac{\|x_i\|_2^2}{r^2} \alpha_i.
$$
When the dimension of input space is very large, $\|x\|_2^2$ is typically constant, since the volume of the high-dimensional spherical shell occupies the most part of the sphere. Thus,
$$
f(x) \approx 2\sum^n_{i = 1} \frac{x^\top x_i}{r^2} \alpha_i.
$$
and the regularization term becomes
$$
\frac{\lambda}{2} \|\theta\|^2 \approx - \frac{\lambda}{2} \sum^n_{i = 1} \sum^n_{j = 1} \alpha_i \alpha_j \frac{\|x_i - x_j\|_2^2}{r^2} = \frac{\lambda}{r^2} \sum^n_{i = 1} \sum^n_{j = 1} \alpha_i \alpha_j x_i^\top x_j.
$$
Then, approximately, the minimization problem can be written as
$$
\min_{\alpha \in A} \left\{\frac{1}{n} \sum^n_{i = 1} l\left(y_i, 2\sum^n_{j = 1} \frac{x_i^\top x_j}{r^2} \alpha_j \right) + \frac{\lambda}{r^2} \sum^n_{i = 1} \sum^n_{j = 1} \alpha_i \alpha_j x_i^\top x_j \right\},
$$
where $A = \left\{\alpha \in \mathbb R^n \mid \sum^n_{i = 1} \alpha_i \right\}$. Since $r$ is finite(it ``tends'' to infinite, but still finite), redefining $\alpha$ as $2 \alpha / r^2$ is possible. Thus upper minimization problem is eqivalent to
$$
\min_{\alpha \in A} \left\{\frac{1}{n} \sum^n_{i = 1} l\left(y_i, \sum^n_{j = 1} x_i^\top x_j \alpha_j \right) + \frac{\lambda r^2}{2} \sum^n_{i = 1} \sum^n_{j = 1} \alpha_i \alpha_j x_i^\top x_j \right\}.
$$
This is the same as the optimization problem obtained by the linear kernel with regularization parameter $\lambda r^2 / 2$.

---

## Problem 15[Optimization of the kernel]
*Show that for convex loss functions, the maximal value in equation (7.9) is a convex function of the kernel matrix $K$. For the square loss, show that it is equal to $\frac{\lambda}{2} y^\top (K + n\lambda I)^{-1} y$.*

### Solution

For convenience, let $l_i = l(y_i, \cdot)$. The problem which is considered here is
$$
\max_{\alpha \in \mathbb R^n} \left\{\frac{1}{n} \sum^n_{i = 1} \min_{u_i \in \mathbb R} \{l_i(u_i) + n \lambda \alpha_i u_i\} - \frac{\lambda}{2} \alpha^\top K \alpha \right\}.
$$
The minimization inside of the summation can be written with convex conjugate, in this case, is the same as the Legendre transformation. Letting $l_i^*$ be a convex conjugate of $l_i$, the problem can be rewritten as
$$
\max_{\alpha \in \mathbb R^n} \left\{-\frac{1}{n} \sum^n_{i = 1} l_i^*(- n\lambda \alpha_i) - \frac{\lambda}{2} \alpha^\top K \alpha \right\}.
$$
Now consider a bijective mapping $\alpha$ which maps $n^2$ pairs of natural numbers between 1 and $n$ onto natural numbers between 1 and $n^2$. Then $\alpha \alpha^\top$ and $K$ can be treated as vectors in $\mathbb R^{n^2}$ space and $\alpha^\top K \alpha = \mathrm{Tr}[\alpha\alpha^\top K]$ can be seen as the inner product between them. Hence the problem is the pointwise maximization of affine functions on $K$. Since the pointwise supremum of affine functions is convex function, the given function is convex function on $K$. For square loss $l_i(x) = (y_i - x)^2/2$,
$$
l_i^*(x) = x \left(y_i + \frac{x}{2}\right).
$$
Therefore the maximization problem is
$$
\max_{\alpha \in \mathbb R^n} \left\{- \lambda \sum^n_{i = 1} \alpha_i\left(y_i + \frac{n\lambda \alpha_i}{2}\right) - \frac{\lambda}{2} \alpha^\top K \alpha \right\} = - \lambda \min_{\alpha \in \mathbb R^n} \left\{\alpha^\top y + \frac{n\lambda}{2} \alpha^\top \alpha + \frac{1}{2} \alpha^\top K \alpha \right\}.
$$
Solving, the optimal $\alpha$ value, $\alpha^\star$ is,
$$
\alpha^\star = - (K + n\lambda I)^{-1} y.
$$
(since $n\lambda > 0$, $K + n\lambda I$ is always invertible)Substituting, the solution comes out as
$$
\frac{\lambda}{2} y^\top (K + n\lambda I)^{-1} y.
$$

---

## Problem 16
*Consider the minimization of $F(\theta) = \mathbb E[l(y, \langle \varphi(x), \theta\rangle)]$ using constant step-size SGD for a convex $G$-Lipschitz-continuous loss and features almost surely bounded by $R$. Show that after $t$ steps(initialized at $\theta_0 = 0$ and with step size $\gamma$), the averaged iterate $\bar\theta_t$ satisfies $\mathbb E[F(\bar \theta_t)] \leq \inf_{\theta \in \mathcal H} \left\{F(\theta) + \frac{\|\theta\|_{\mathcal H}^2}{2\gamma t} \right\} + \frac{\gamma G^2 R^2}{2}$.*

### Solution

At any step $t$, SGD does
$$
\theta_t = \theta_{t - 1} - \gamma g_t(\theta_{t - 1}),
$$
with
$$
g_t(\theta) = \frac{1}{m} \sum^m_{i(t) = 1} l'(y_{i(t)}, \langle \varphi(x_{i(t)}), \theta \rangle_{\mathcal H}) \varphi(x_{i(t)}),
$$
where $i(t)$ represents the index of randomly shuffled data at step $t$. Thus,
$$
\begin{align*}
\mathbb E \left[\|\theta_t - \theta\|^2\right] &= \mathbb E \left[\|\theta_{t - 1} - \gamma g_t(\theta_{t - 1}) - \theta\|^2\right]\\
&= \mathbb E \left[\|\theta_{t - 1} - \theta_*\|^2\right] + \gamma^2 \mathbb E \left[\|g_t(\theta_{t - 1})\|^2\right] - 2 \gamma \mathbb E \left[\langle g_t(\theta_{t - 1}), \theta_{t - 1} - \theta \rangle_{\mathcal H}\right],
\end{align*}
$$
with arbitrary $\theta \in \mathcal H$. Observe that by Jensen's inequality, Lipschitz continuity(bounded graident) and bounded features,
$$
\|g_t(\theta)\|^2 \leq \frac{1}{m} \sum^m_{i(t) = 1} |l'(y_{i(t)}, \langle \varphi(x_{i(t)}), \theta \rangle_{\mathcal H})|^2 \|\varphi(x_{i(t)})\|^2 \leq G^2 R^2,
$$
almost surely. Also, by the convexity,
$$
\mathbb E\left[\langle g_t(\theta_{t - 1}), \theta_{t - 1} - \theta \rangle_{\mathcal H}\right] = \mathbb E \left[\langle F'(\theta_{t - 1}), \theta_{t - 1} - \theta \rangle_{\mathcal H}\right] \geq \mathbb E[F(\theta_t)] - F(\theta).
$$
Hence,
$$
\mathbb E[F(\theta_t)] - F(\theta) \leq \frac{1}{2\gamma} \left(\mathbb E\left[\|\theta_{t - 1} - \theta\|_{\mathcal H}^2 \right] - \mathbb E\left[\|\theta_t - \theta\|_{\mathcal H}^2 \right]\right) + \frac{\gamma G^2 R^2}{2},
$$
and doing a telescopic sum,
$$
\begin{align*}
\mathbb E[F(\bar \theta_T)] - F(\theta) \leq \mathbb E\left[\frac{1}{T} \sum^T_{t = 1} F(\theta_t)\right] - F(\theta) &\leq \frac{1}{2\gamma T}\left(\|\theta_*\|_{\mathcal H}^2 - \mathbb E\left[\|\theta_T - \theta\|_{\mathcal H}^2 \right] \right) + \frac{\gamma G^2 R^2}{2}\\
& \leq \frac{1}{2\gamma T}\|\theta\|_{\mathcal H}^2 + \frac{\gamma G^2 R^2}{2},
\end{align*}
$$
thus
$$
\mathbb E[F(\bar \theta_T)] \leq F(\theta) + \frac{1}{2\gamma T}\|\theta\|_{\mathcal H}^2 + \frac{\gamma G^2 R^2}{2}.
$$
Since $\theta$ is arbitrary, taking it to make right hand side to go minimum is possible. Thus,
$$
\mathbb E[F(\bar \theta_T)] \leq \inf_{\theta \in \mathcal H} \left\{F(\theta) + \frac{1}{2\gamma T}\|\theta\|_{\mathcal H}^2\right\} + \frac{\gamma G^2 R^2}{2}.
$$

---

## Problem 17[Kernel PCA]

*We consider $n$ observations $x_1, \cdots, x_n$ in a set $\mathcal X$ equiped with a positive-definite kernel and associated feature map $\varphi$ from $\mathcal X$ to $\mathcal H$. Show that the largest eigenvector of the empirical noncentered covariance operator $\frac{1}{n} \sum^n_{i = 1} \varphi(x_i) \otimes \varphi(x_i)$ is proportional to $\sum^n_{i = 1} \alpha_i \varphi(x_i)$, where $\alpha \in \mathbb R^n$ is an eigenvector of the $n \times n$ kernel matrix associated with the largest eigenvalue. Given the RKHS $\mathcal H$ associated with kernel $k$, relate this eigenvalue problem to the maximizer of $\frac{1}{n} \sum^n_{i = 1} f(x_i)^2$ subject to $\|f\|_{\mathcal H} = 1$.*

**Definition (Tensor product).**

Let $V$ and $W$ be vector spaces. The tensor product $V \otimes W$ is a vector space, together with the bilinear map $\psi: V \times W \rightarrow V \otimes W$, which maps $(v, w)$ to $v \otimes w$, such that for every bilinear map $h: V \times W \rightarrow U$ with another vector space $U$, there is unique linear map $\tilde h: V \otimes W \rightarrow U$, which satisfies $h = \tilde h \circ \psi$, i.e. $h(v, w) = \tilde h(v \otimes w)$ for all $v \in V$ and $w \in W$.

**Definition (Tensor product of Hilbert spaces).**

For two Hilbert spaces $\mathcal H_1$ and $\mathcal H_2$ with respective inner products $\langle \cdot, \cdot \rangle_1$ and $\langle \cdot, \cdot \rangle_2$, the resulting Hilbert space $\mathcal H_1 \otimes \mathcal H_2$ is equipped and completed with the inner product
$$
\langle \varphi_1 \otimes \varphi_2, \varphi'_1 \otimes \varphi'_2 \rangle = \langle \varphi_1, \varphi'_1 \rangle_1 \langle \varphi_2, \varphi'_2 \rangle_2,
$$
for all $\varphi_1, \varphi'_1 \in \mathcal H_1$ and $\varphi_2, \varphi'_2 \in \mathcal H_2$.

**Definition (Noncentered covariance operator).**

Let $(\mathcal H,\langle\cdot,\cdot\rangle)$ be a separable Hilbert space and let $Z$ be a $\mathcal H$-valued random element with the probability measure $p$. Assume the second moment is finite: $\mathbb E\|Z\|^2<\infty$.
The covariance operator $C:\mathcal H\to\mathcal H$ is the bounded linear operator
$$
C x \;=\; \mathbb E\left[\langle x, Z\rangle Z\right]
\;=\; \int_{\mathcal H}\langle x,z\rangle z \,\mathrm{d} {p(z)},
$$
for all $x\in\mathcal H$.
The associated bilinear (covariance) form is
$$
\mathrm{Cov}(x,y)=\langle x,C y\rangle
=\mathbb E\left[\langle x,Z\rangle\langle y,Z\rangle\right].
$$
Under the finite second moment assumption, $C$ is positive, self-adjoint and Hilbert--Schmidt(hence trace-class), and
\(\operatorname{tr}C=\mathbb E\|Z\|^2\).

**Definition (Noncentered empirical covariance operator).**

Given samples $Z_1,\dots,Z_n\in\mathcal H$, the empirical covariance operator is the finite-rank operator $C_{\mathrm{emp}}:\mathcal H\to\mathcal H$ defined by
$$
C_{\mathrm{emp}}\,x
= \frac{1}{n}\sum_{i=1}^n \langle x, Z_i\rangle Z_i.
$$
Its bilinear form is
$$
\mathrm{Cov}_{\mathrm{emp}}(x,y)
= \frac{1}{n}\sum_{i=1}^n \langle x, Z_i\rangle\langle y,Z_i\rangle.
$$
Equivalently, identifying $\mathcal H\otimes\mathcal H$ with the space of Hilbert--Schmidt operators, we have
$$
C_{\mathrm{emp}} \quad\leftrightarrow\quad\frac{1}{n}\sum_{i=1}^n Z_i\otimes Z_i,
$$
and each simple tensor $Z_i\otimes Z_i$ corresponds to the rank-one operator $x\mapsto\langle x,Z_i\rangle Z_i$.

### Solution

For an eigenvector $f \in \mathcal H$ of $\hat C$ with the largest eigenvalue $\lambda_\mathrm{max}$,
$$
\hat C f = \frac{1}{n} \sum^n_{i = 1} \langle f, \varphi(x_i) \rangle \varphi(x_i) = \lambda_{\mathrm{max}} f.
$$
And,
$$
\langle \hat C f, \varphi(x_j) \rangle = \frac{1}{n} \sum^n_{i = 1} \langle f, \varphi(x_i) \rangle \langle \varphi(x_i), \varphi(x_j) \rangle = \lambda_\mathrm{max} \langle f, \varphi(x_j) \rangle.
$$
Since $K_{ij} = \langle \varphi(x_i), \varphi(x_j) \rangle$, a vector having $\langle f, \varphi(x_i)\rangle$ as an $i$th element is an eigenvector of $K$ with an eigenvalue of $n \lambda_\mathrm{max}$. Meanwhile, the eigenvalue equation $K$ with eigenvector $u \in \mathbb R^n$ and corresponding eigenvalue $\mu \in \mathbb R$ is,
$$
\sum^n_{j = 1} K_{ij} u_j = \mu u_i,
$$
for all $i = 1, \cdots, n$. In other words, this equation can be written as
$$
\sum^n_{j = 1} \left< \varphi(x_i), \sum^n_{j = 1} \varphi(x_j) u_j \right> = \mu u_i.
$$
Multiplying $\varphi(x_i)$ on both sides and summing over $i = 1, \cdots, n$,
$$
\sum^n_{i = 1} \left< \varphi(x_i), \sum^n_{j = 1} u_j \varphi(x_j) \right> \varphi(x_i) = \mu \sum^n_{i = 1} u_i \varphi(x_i).
$$
Letting $g = \sum^n_{i = 1} u_i \varphi(x_i)$,
$$
\sum^n_{i = 1} \langle \varphi(x_i), g \rangle \varphi(x_i) = \mu g.
$$
And this is equivalent to $n \hat C g = \mu g$, thus $\mu/n$ is an eigenvalue of $\hat C$ with eigenvector $g$. Thus, letting maximum eigenvalue of $K$ be $\mu_\mathrm{max}$, $\mu_\mathrm{max} = n \lambda_\mathrm{max}$. Therefore letting the eigenvector of $K$ corresponding to the largest eigenvalue be $\alpha \in \mathbb R^n$, $\alpha_i = \langle f, \varphi(x_i)\rangle$, and hence,
$$
f = \frac{1}{n} \sum^n_{i = 1} \alpha_i \varphi(x_i).
$$
Now consider an optimization problem of maximizing $(1/n) \sum^n_{i = 1} f(x_i)^2$ subject to $\|f\| = 1$. Recall that $f(x)$ could be written with the inner product, $f(x) = \langle f, k(x, \cdot) \rangle$. Let $\mathcal H_\varphi = \mathrm{cl}\, \mathrm{span} \{\varphi(x) \mid x \in \mathcal X\} \subset \mathcal H$. Let $A: \mathcal H_\varphi \to \mathcal H$ be an inner product such that $A \varphi(x) = k(x, \cdot)$ for all $x \in \mathcal X$. $A$ preserves inner product since for all $u, v \in \mathcal H_\varphi$, they can be represented in a limits of the form $\sum^{m_u}_{i = 1} \beta_i \varphi(y_i)$ and $\sum^{m_v}_{i = 1} \gamma_i \varphi(z_i)$ respectively, with $m_u, m_v \in \mathbb N$, $\beta \in \mathbb R^{m_u}$, $\gamma \in \mathbb R^{m_v}$, $y \in \mathcal X^{m_u}$ and $z \in \mathcal X^{m_v}$, thus
$$
\langle u, v\rangle = \sum^{m_u}_{i = 1} \sum^{m_v}_{i = 1} \alpha_i \gamma_j \langle \varphi(y_i), \varphi(z_j) \rangle = \sum^{m_u}_{i = 1} \sum^{m_v}_{i = 1} \beta_i \gamma_j k(y_i, z_j),
$$
and
$$
\langle Au, Av \rangle = \sum^{m_u}_{i = 1} \sum^{m_v}_{i = 1} \beta_i \gamma_j \langle A \varphi(y_i), A\varphi(z_i) \rangle = \sum^{m_u}_{i = 1} \sum^{m_v}_{i = 1} \beta_i \gamma_j \langle k(y_i, \cdot), k(z_j, \cdot) \rangle = \sum^{m_u}_{i = 1} \sum^{m_v}_{i = 1} \beta_i \gamma_j k(y_i, z_j).
$$
Such $A$ is well defined because it does not depends on the representation of vectors. Also, $A$ is surjective by definition and is injective because if $A u = 0$ for $u \in \mathcal H_\varphi$,
$$
(Au)(x) = \langle Au, k(x, \cdot)\rangle = \langle u, \varphi(x) \rangle = 0,
$$
therefore  $u \in \mathcal H_\varphi^\perp$ and $u = 0$, thus $\mathrm{ker}\, A = \{0\}$. Hence $A$ is isometric isomorphism. Let $v = A^{-1} f$. Then $\langle f, k(x, \cdot) \rangle = \langle v, \varphi(x) \rangle$ and $\|f\| = \|v\|$. Meanwhile,
$$
\langle v, \hat C v \rangle = \frac{1}{n} \sum^n_{i = 1} \langle v, \varphi(x_i) \rangle^2.
$$
Thus the original problem can be rewritten as
$$
\max_{v \in \mathcal H_\varphi, \|v\| = 1} \langle v, \hat Cv \rangle.
$$
Let $v = v_\parallel + v_\perp$, where $v_\parallel$ is in the span of eigenvectors of $\hat C$ and $v_\perp$ is in its orthogonal space. Then $\|v_\parallel\|^2 + \|v_\perp\|^2 = 1$ and $\langle v, \hat C v \rangle = \langle v_\parallel, \hat C v_\parallel \rangle$. Letting $a_i = \langle v_\parallel, u_i\rangle$, where $u_i$ is $i$th unit length eigenvector of $\hat C$, $\|v_\parallel\|^2 = \sum^n_{i = 1} a_i^2$ and $\langle v_\parallel, \hat C v_\parallel \rangle = \sum^{\mathrm{rank}\, \hat C}_{i = 1} \lambda_i a_i^2$, where $\lambda_i$ is the eigenvalue corresponding to the eigenvector $u_i$. Thus the original problem can be editted once again into the following form,
$$
\max_{a \in \mathbb R^{\mathrm{rank}\, \hat C}, \|a\|_2^2 \leq 1} \sum^{\mathrm{rank}\, \hat C}_{i = 1} \lambda_i a_i^2.
$$
Trivially, the solution of this problem is $\lambda_\mathrm{max}$ with corresponding $a_i$ having value 1, while others are zeros. Hence the given problem is equivalent to the problem of calculating the largest eigenvalue of $\hat C$. Furthermore, the resulting optimal $f$, denoting it as $f^\star$, $Af^\star$ will be a unit eigenvector of $\hat C$ corresponding to the largest eigenvalue, using the previous result,
$$
Af^\star = \frac{1}{n} \sum^n_{i = 1} \alpha_i \varphi(x_i),
$$
and thus
$$
f^\star = \frac{1}{n} \sum^n_{i = 1} \alpha_i k(x_i, \cdot).
$$

---

## Problem 18[Kernel $K$-means]
*Show that the $K$-means clustrering algorithm can be expressed only using dot products.*

**Definition ($K$-means clustering).**

Given $n$ observations $x_1, \cdots, x_n$, $K(\leq n)$-means clustering finds $K$ partitions of observations $S = \{S_1, \cdots, S_k\}$ such that
$$
\underset{S}{\mathrm{argmin}}\, \sum^k_{i = 1} \sum_{x \in S_i} \left\|x - \frac{1}{|S_i|} \sum_{y \in S_i} y \right\|^2.
$$

### Solution

$$
\begin{align*}
\sum^k_{i = 1} \sum_{x \in S_i} \left\|x - \frac{1}{|S_i|} \sum_{y \in S_i} y \right\|^2 &= \sum^k_{i = 1} \sum_{x \in S_i} \|x\|^2 - \sum^k_{i = 1} \frac{1}{|S_i|} \sum_{x, y \in S_i} \langle x, y \rangle\\
&= \sum^n_{i = 1} \|x_i\|^2 - \sum^k_{i = 1} \frac{1}{|S_i|} \sum_{x, y \in S_i} \langle x, y \rangle
\end{align*}
$$
$\sum^n_{i = 1} \|x_i\|^2$ is independent to the choice of $S$, therefore the $K$-means clustering is equivalent to solving
$$
\underset{S}{\mathrm{argmax}} \sum^k_{i = 1} \frac{1}{|S_i|} \sum_{x, y \in S_i} \langle x, y \rangle.
$$

---

## Problem 19[Kernel quadrature]
We consider a probability measure $p$ on a set $\mathcal X$ equipped with a positive-definite kernel $k$ with feature map $\varphi: \mathcal X \to \mathcal H$. For a function $f: \mathcal X \to \mathbb R$ that is linear in $\varphi$, we want to approximate $\int_{\mathcal X} f(x) \,\mathrm{d} {p(x)}$ from a linear combinatioin $\sum^n_{i = 1} \alpha_i f(x_i)$ with $\alpha \in \mathbb R^n$.
\item Show that
$$
\left| \int_{\mathcal X} f(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i f(x_i) \right| \leq \|f\| \cdot \left\| \int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i \varphi(x_i) \right\|.
$$
\item Express the square of the right side with the kernel function and show how to minimize it with respect to $\alpha \in \mathbb R^n$.
\item Show that if the points $x_1, \cdots, x_n$ are sampled i.i.d. from $p$ and $\alpha_i = 1/n$ for all $i$, then
$$
\mathbb E \left[\left\|\int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i \varphi(x_i) \right\|^2 \right] \leq \frac{1}{n} \mathbb E[k(x, x)].
$$

### Solution

(a) $f$ is linear in $\varphi$, i.e. there is $v \in \mathcal H$ such that $f(x) = \langle v, \varphi(x) \rangle$ for all $x \in \mathcal X$. Letting $\mathcal H_\varphi = \mathrm{cl}\, \mathrm{span} \{\varphi(x) \mid x \in \mathcal X\}$, $v = v_\parallel + v_\perp$ where $v_\parallel \in \mathcal H_\varphi$ and $v_\perp \in \mathcal H / \mathcal H_\varphi$ and $f(x) = \langle v_\parallel, \varphi(x) \rangle$. Hence,
$$
\left| \int_{\mathcal X} f(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i f(x_i) \right| = \left|\left< v_\parallel, \int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i \varphi(x_i) \right>\right|.
$$
Then by the Cauchy-Schwartz inequality,
$$
\left| \int_{\mathcal X} f(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i f(x_i) \right| \leq \|v_\parallel\| \left\| \int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i \varphi(x_i) \right\|.
$$
Meanwhile, since $v_\parallel$ is limit of the form $\sum^m_{i = 1} \beta_i \varphi(y_i)$ with $\beta \in \mathbb R^m$ and $y \in \mathcal X^m$,
$$
f(x) = \langle v_\parallel, \varphi(x) \rangle = \sum^m_{i = 1} \beta_i k(y_i, x),
$$
for all $x \in \mathcal X$, and thus
$$
\|f\|^2 = \sum^m_{i = 1} \sum^m_{j = 1} \beta_i \beta_j \langle k(y_i, \cdot), k(y_j, \cdot) \rangle = \sum^m_{i = 1} \sum^m_{j = 1} \beta_i \beta_j k(y_i, y_j).
$$
However,
$$
\|v_\parallel\|^2 = \sum^m_{i = 1} \sum^m_{j = 1} \beta_i \beta_j \langle \varphi(y_i), \varphi(y_j) \rangle = \sum^m_{i = 1} \sum^m_{j = 1} \beta_i \beta_j k(y_i, y_j),
$$
thus $\|v_\parallel\| = \|f\|$. Hence,
$$
\left| \int_{\mathcal X} f(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i f(x_i) \right| \leq \|f\| \left\| \int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i \varphi(x_i) \right\|.
$$
(b)
\left\| \int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i \varphi(x_i) \right\|^2 = \int_{\mathcal X} \int_{\mathcal X} k(x, y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)} \\
+ \sum^n_{i = 1} \sum^n_{j = 1} \alpha_i \alpha_j k(x_i, x_j) - 2 \sum^n_{i = 1} \alpha_i \int_{\mathcal X} k(x, x_i) \,\mathrm{d} {p(x)}

Let the right hand side be $\mathcal L(\alpha)$. Then, the Hessian of $\mathcal L$ is
$$
\frac{\partial^2 \mathcal L}{\partial \alpha_i \partial  \alpha_j } = k(x_i, x_j),
$$
for all $i, j = 1, \cdots, n$, and since the kernel $k$ is positive-definite, the Hessian is positive-semidefinite. Thus $\mathcal L$ is convex function on $\alpha$, and it can be minimized by solving the root-finding problem of its gradient, denoting the optimal $\alpha$ to be $\alpha^\star$,
$$
\frac{\partial^1 \mathcal L}{\partial \alpha_i } = 2 \sum^n_{j = 1} \alpha^\star_j k(x_i, x_j) - 2 \int_{\mathcal X} k(x, x_i) \,\mathrm{d} {p(x)} = 0,
$$
rearranging,
$$
\sum^n_{j = 1} k(x_i, x_j) \alpha^\star_j = \int_{\mathcal X} k(x, x_i) \,\mathrm{d} {p(x)}.
$$
Hence,
$$
\min_{\alpha \in \mathbb R^n} \mathcal L(\alpha) = \int_{\mathcal X} \int_{\mathcal X} k(x, y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)} - {\alpha^\star}^\top K \alpha^\star.
$$
(c)
\mathbb E\left[\left\| \int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i \varphi(x_i) \right\|^2\right] = \int_{\mathcal X} \int_{\mathcal X} k(x, y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)} + \sum^n_{i = 1} \alpha_i^2 \int_{\mathcal X} k(x, x) \,\mathrm{d} {p(x)}\\
+ \sum^n_{i = 1} \sum^n_{j = 1} \alpha_i \alpha_j (1 - \delta_{ij}) \int_{\mathcal X} \int_{\mathcal X} k(x, y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)} - 2 \sum^n_{i = 1} \alpha_i \int_{\mathcal X} \int_{\mathcal X} k(x, y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)}.

If $\alpha_i = 1/n$ for all $i = 1, \cdots, n$,
$$
\mathbb E\left[\left\| \int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i \varphi(x_i) \right\|^2\right] = \frac{1}{n} \mathbb E[k(x, x)] - \frac{1}{n} \int_{\mathcal X} \int_{\mathcal X} k(x, y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)}.
$$
And since
$$
\int_{\mathcal X} \int_{\mathcal X} k(x, y) \,\mathrm{d} {p(x)} \,\mathrm{d} {p(y)} = \left\|\int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} \right\|^2 \geq 0,
$$
it can be written that
$$
\mathbb E\left[\left\| \int_{\mathcal X} \varphi(x) \,\mathrm{d} {p(x)} - \sum^n_{i = 1} \alpha_i \varphi(x_i) \right\|^2\right] \leq \frac{1}{n} \mathbb E[k(x, x)].
$$

---

## Problem 20
*Consider a binary classification problems with data $(x_1, y_1), \cdots, (x_n, y_n)$ in $\mathcal X \times \{-1, 1\}$, with a positive-definite kernel $k$ defined on $\mathcal X$ with feature map $\varphi: \mathcal X \to \mathcal H$. Let $\mu_+(\mu_-)$ be the mean of all feature vectors for positive(negative) lables. We consider the classification rule that predicts $1$ if $\|\varphi(x) - \mu_+\|_{\mathcal H}^2 < \|\varphi(x) - \mu_-\|_{\mathcal H}^2$ and $-1$ otherwise. Compute the classification rule only using kernel functions and compare it to local averaging methods from chapter 6.*

### Solution

Let $\zeta^\pm_i = (1 \pm y_i) / (2N_\pm)$ for all $i = 1, \cdots, n$, where $N_\pm$ be a number of positive(``$+$'' subscript) and negative(``$-$'' subscript) labeled data, so that $\sum^n_{i = 1} \zeta^\pm_i = 1$. Then,
$$
\mu_\pm = \sum^n_{i = 1} \zeta^\pm_i \varphi(x_i),
$$
and
$$
\|\varphi(x) - \mu_\pm\|_{\mathcal H}^2 = k(x, x) + \sum^n_{i = 1} \sum^n_{j = 1} \zeta_i^\pm \zeta_j^\pm k(x_i, x_j) - 2\sum^n_{i = 1} \zeta^\pm_i k(x_i, x).
$$
Thus the classification rule is equivalent to predicting 1 when
$$
\sum^n_{i = 1} \sum^n_{j = 1} \left(\zeta^+_i \zeta^+_j - \zeta^-_i \zeta^-_j \right) k(x_i, x_j) < 2\sum^n_{i = 1} \left(\zeta^+_i - \zeta^-_i\right) k(x_i, x),
$$
and $-1$ otherwise. TBA

---

## Problem 21
*Find an upper bound of $\tilde A(\mu, f_*)$ for the same assumption on $f_*$, but with the Gaussian kernel.*

### Solution

The Gaussian kernel is the translation invariant kernel with $q: \mathbb R^d \to \mathbb R$, which is defined as
$$
q(x) = e^{-\|x\|_2^2 / r^2},
$$
with some $r \in \mathbb R$. Its Fourier dual is,
$$
\hat q(\omega) = (\pi r^2)^{d/2} e^{-r^2 \|\omega\|^2 / 4}.
$$
Since $q(x) \in W^{\infty, 2}$, there are two cases, $f_* \in \mathcal H$ and $f_* \notin \mathcal H$. If $f_* \in \mathcal H$, $\tilde A(\mu, f_*) \leq \mu \|f_*\|_{\mathcal H}^2$. When $f_* \notin \mathcal H$, recall that,
$$
\tilde A(\mu, f_*) \leq \frac{1}{(2\pi r)^d} \sup_{\omega \in \mathbb R^d} \left\{\frac{\mu r^d}{\hat q(\omega) + \mu r^d} \frac{1}{(1 + r^2 \|\omega\|_2^2)^t}\right\} \int_{\mathbb R^d} (1 + r^2 \|\omega\|_2^2)^t |\hat f_*(\omega)|^2 \,\mathrm{d} {\omega}.
$$
The supermum can be edited as
$$
\begin{align*}
\sup_{\omega \in \mathbb R^d} \left\{\frac{\mu r^d}{(\pi r^2)^{d/2} e^{-r^2 \|\omega\|^2 / 4} + \mu r^d} \frac{1}{(1 + r^2 \|\omega\|_2^2)^t}\right\} &= \sup_{w \geq 0} \left\{\frac{\mu r^d}{(\pi r^2)^{d/2} e^{-w / 4} + \mu r^d} \frac{1}{(1 + w)^t}\right\} \\
&= \sup_{w \geq 0} \left\{\frac{1}{(\pi^{d/2} / \mu) e^{-w/4} + 1} \frac{1}{(1 + w)^t}\right\}.
\end{align*}
$$
and since
$$
\frac{1}{(\pi^{d/2} / \mu) e^{-w/4} + 1} = \frac{(\mu / \pi^{d/2})e^{w/4}}{(\mu / \pi^{d/2} ) e^{w/4} + 1} < \min\left\{1, \frac{\mu}{\pi^{d/2}}e^{w/4}\right\},
$$
(if we bound it just with the exponential function, the supremum diverges)The superemum can be bounded as
$$
\begin{align*}
\sup_{w \geq 0} &\left\{\frac{1}{(\pi^{d/2} / \mu) e^{-w/4} + 1} \frac{1}{(1 + w)^t}\right\} < \sup_{w \geq 0} \left\{\min\left\{1, \frac{\mu}{\pi^{d/2}}e^{w/4}\right\} \frac{1}{(1 + w)^t}\right\}\\
&=\max\left\{\sup_{w \in [0, 4\log (\pi^{d/2}/\mu)]}\left\{\frac{\mu}{\pi^{d/2}}e^{w/4}\frac{1}{(1 + w)^t} \right\}, \sup_{w \in (4\log(\pi^{d/2}/\mu), \infty)} \left\{\frac{1}{(1 + w)^t}\right\}\right\}.
\end{align*}
$$
Now observe that
$$
\frac{\mathrm{d}^2}{\mathrm{d} w^2}\frac{e^{w/4}}{(1 + w)^t} = \frac{e^{w/4}}{(1 + w)^t}\left[\frac{t}{(1 + w)^2} + \left( \frac{t}{1 + w} - \frac{1}{4} \right)^2\right] \geq 0,
$$
thus $e^{w/4}/(1 + w)^t$ is convex function on $w$, therefore
$$
\sup_{w \in [0, 4\log (\pi^{d/2}/\mu)]}\left\{\frac{\mu}{\pi^{d/2}}e^{w/4}\frac{1}{(1 + w)^t} \right\} = \frac{\mu}{\pi^{d/2}} \max\left\{1, \frac{1}{(1 + 4\log(\pi^{d/2}/\mu))^t}\right\} = \frac{\mu}{\pi^{d/2}}.
$$
And trivailly $1/(1 + w)^t$ is convex, thus
$$
\sup_{w \in (4\log(\pi^{d/2}/\mu), \infty)} \left\{\frac{1}{(1 + w)^t}\right\} = \max\left\{ \frac{1}{(1 + 4\log(\pi^{d/2}/\mu))^t}, 0\right\} = \frac{1}{(1 + 4\log(\pi^{d/2}/\mu))^t}.
$$
Hence,
$$
\sup_{w \geq 0} \left\{\frac{1}{(\pi^{d/2} / \mu) e^{-w/4} + 1} \frac{1}{(1 + w)^t}\right\} < \max \left\{\frac{\mu}{\pi^{d/2}}, \frac{1}{(1 + 4\log(\pi^{d/2}/\mu))^t} \right\}.
$$
Also, the maximization can be bounded as the sum,
$$
\max \left\{\frac{\mu}{\pi^{d/2}}, \frac{1}{(1 + 4\log(\pi^{d/2}/\mu))^t} \right\} < \frac{\mu}{\pi^{d/2}} + \frac{1}{(1 + 4\log(\pi^{d/2}/\mu))^t}.
$$
Therefore the final result is
$$
\tilde A(\mu, f_*) < \left[\frac{\mu}{\pi^{d/2}} + \frac{1}{(1 + 4\log(\pi^{d/2}/\mu))^t}\right] \int_{\mathbb R^d} (1 + r^2 \|\omega\|_2^2)^t |\hat f_*(\omega)|^2 \,\mathrm{d} {\omega}.
$$
Note that for small enough $\mu$ the second term dominates.

---

## Problem 22
*Consider the optimization problem $\min_{\theta, \eta} \left\{\frac{1}{2n} \|y - \Phi \theta - \eta 1_n\|_2^2 + \frac{\lambda}{2} \|\theta\|_2^2\right\}$ in the variables $\theta \in \mathbb R^d$ and $\eta \in \mathbb R$, where $\Phi \in \mathbb R^{n \times d}$ is the design matrix obtained from feature map $\varphi$ and data points $x_1, \cdots, x_n$, $y \in \mathbb R^n$, and $1_n \in \mathbb R^n$ is the vector of all $1$s. Show that the optimal values of $\theta$ and $\eta$ are $\theta = \Phi^\top \alpha$ and $\eta= \frac{1}{n} 1_n^\top (y - \Phi \theta)$, with $\alpha = \Pi_n (\Pi_n K \Pi_n + n \lambda I)^{-1} \Pi_n y$, and $\Pi_n = I - \frac{1}{n} 1_n 1_n^\top$. Show that the prediction function $f(x) = \varphi(x)^\top \theta + \eta$ takes the form $\sum^n_{i = 1} \hat w_i(x) y_i$ with weights that sum to $1$.*

### Solution

Since the objective function is convex as a function of $\theta$ or $\eta$, the minimization problem can be solved by solving the root-finding problem of the gradient. i.e. the optimal $\theta$ and $\eta$, which will be denoted as $\theta^\star$ and $\eta^\star$ respectively, should satisfy
$$
\frac{1}{n} \Phi^\top (\Phi \theta^\star + \eta^\star 1_n - y) + \lambda \theta^\star = 0, \\
\frac{1}{n} 1_n^\top (\Phi \theta^\star + \eta^\star 1_n - y) = 0.

$$
Solving the second equation with respect to $\eta^\star$,
$$
\eta^\star = \frac{1}{n} 1_n^\top (y - \Phi \theta^\star).
$$
Substituting this into the original problem, it reduces to the following form:
$$
\min_{\theta \in \mathbb R^d} \left\{\frac{1}{2n} \|\Pi_n(y - \Phi \theta) \|_2^2 + \frac{\lambda}{2} \|\theta\|_2^2\right\}.
$$
Now let $V = \mathrm{span}\{\varphi(x_1), \cdots, \varphi(x_n)\}$ and further simpify the problem by applying the representer-type argument. Then it can be concluded that $\theta^\star$ lies on $V$. Thus now restrict the search space for $\theta$ to $V$. Let $\alpha \in \mathbb R^n$ a vector satisfying $\theta = \sum^n_{i = 1} \alpha_i \varphi(x_i) = \Phi^\top \alpha \in V$. Then the minimization problem again reduces to
$$
\min_{\alpha \in \mathbb R^n} \left\{\frac{1}{2n} \|\Pi_n (y - K \alpha)\|_2^2 + \frac{\lambda}{2} \alpha^\top K \alpha\right\}.
$$
The optimal $\alpha$, denoted as $\alpha^\star$, can be found by solving the root-finding problem of the gradient,
$$
\frac{1}{n} K \Pi_n (K \alpha^\star - y) + \lambda K \alpha^\star = 0,
$$
Note that $\Pi_n^\top = \Pi_n$ and $\Pi_n^2 = \Pi_n$. Rearranging,
$$
K (\Pi_n K + n\lambda I) \alpha^\star = K \Pi_n y.
$$
Assume that $K$ is invertible. Then,
$$
(\Pi_n K + n\lambda I) \alpha^\star = \Pi_n y,
$$
or
$$
n \lambda \alpha^\star = \Pi_n(y - K \alpha^\star).
$$
Since right hand side is in $\mathrm{Range}\, \Pi_n$, $\alpha^\star \in \mathrm{Range}\, \Pi_n$. Then it can be easily seen that $\Pi_n \alpha^\star = \alpha^\star$. Therefore,
$$
(\Pi_n K \Pi_n + n\lambda I) \alpha^\star = \Pi_n y,
$$
and
$$
\alpha^\star = \Pi_n \alpha^\star = \Pi_n (\Pi_n K \Pi_n + n \lambda I)^{-1} \Pi_n y.
$$
Note that
$$
\alpha^\star = \Pi_n \alpha^\star = \alpha^\star - \frac{1}{n} 1_n \sum^n_{i = 1} \alpha_i,
$$
thus it is ``centered'', i.e. the sum of all elements is zero. Now let $A = \Pi_n (\Pi_n K \Pi_n + n \lambda I)^{-1} \Pi_n$ for convenience and substituting $\theta^\star = \Phi^\top \alpha^\star$ and $\eta^\star = \frac{1}{n} 1_n^\top (y - \Phi \theta)$ in $f(x) = \varphi(x)^\top \theta^\star + \eta^\star$,
$$
\begin{align*}
f(x) &= \varphi(x)^\top \Phi^\top Ay + \frac{1}{n} 1_n^\top (y - \Phi \Phi^\top Ay)\\
&= \left[ \left(\varphi(x)^\top - \frac{1}{n} 1_n^\top \Phi \right) \Phi^\top A + \frac{1}{n} 1_n^\top \right] y.
\end{align*}
$$
Letting the coefficent be $\hat w(x)^\top$,
$$
\sum^n_{i = 1} \hat w_i(x) = \hat w(x)^\top 1_n = 1,
$$
since $\Pi_n 1_n = 0$ and thus $A 1_n = 0$.

---

## Problem 23
*For $x_1, \cdots, x_n$ equally spaced in $[0, 1]$ with $x_1 = 0$ and $x_n = 1 - 1/n$ and for a translation-invariant kernel from section 7.3.2, compute the eigenvalues of the kernel matrix and the smoothing matrix.*

### Solution

$$
k(x, x') = \sum_{m \in \mathbb Z} \hat q_m e^{2\pi im (x - x')},
$$
with $\hat q_m$ being the Fourier transform of 1-periodic function $q$ such that $k(x, x') = q(x - x')$. Then,
$$
K_{jk} = \sum_{m \in \mathbb Z} \hat q_m e^{2\pi i m (x_j - x_k)} = \sum_{m \in \mathbb Z} \hat q_m e^{2\pi im (j - k)/n}.
$$
Now define the shift operator matrix $\Pi \in \mathbb R^{n \times n}$ as
$$
(\Pi v)_i = \begin{cases}
v_{i + 1} & i = 1, \cdots, n - 1\\
v_1 & i = n
\end{cases},
$$
for any $v \in \mathbb R^n$. Consider an eigenvector $u \in \mathbb R^n$ of $\Pi$, corresponding to the nonzero eigenvalue $\mu \in \mathbb R$. Then
$$
(\Pi u)_i = \begin{cases}
u_{i + 1} & i = 1, \cdots, n - 1\\
u_1 & i = n
\end{cases} = \mu u_i,
$$
which means
$$
u_i = \mu^{i - 1} u_1, \quad u_1 = \mu u_n = \mu^n u_1.
$$
There are two possibilities: $u_1 = 0$ or $\mu^n = 1$. Former one generates the zero vector and later one shows there are $n$ distinctive eigenvalues, $\mu_j = e^{2\pi i j/n}$, $j = 1, \cdots, n$. Meanwhile, $\Pi$ commutes with $K$, since
$$
(\Pi K v)_j = \sum^n_{k = 1} \sum_{m \in \mathbb Z} \hat q_m e^{2\pi im (j - k + 1) / n} v_k,\\
(K \Pi v)_j = \sum^{n - 1}_{k = 1} \sum_{m \in \mathbb Z} \hat q_m e^{2\pi im (j - k) / n} v_{k + 1} + \hat q_m e^{2\pi i m j / n} v_1 = \sum^n_{k = 1} \sum_{m \in \mathbb Z} \hat q_m e^{2im\pi (j - k + 1) / n} v_k,

$$
hence $\Pi K v = K \Pi v$ for any $v \in \mathbb R^n$. Therefore it can be concluded that $K$ shares eigenvectors with $\Pi$. The eigenvector $u^{(l)}$ of $\Pi$ corresponding to the eigenvalue $\mu_l = e^{2\pi i l/n}$ has $k$th element of
$$
u_k^{(l)} = e^{2\pi i k l /n} u_1.
$$
Therefore,
$$
\begin{align*}
(K u^{(l)})_j &= u^{(l)}_1 \sum^n_{k = 1} \sum_{m \in \mathbb Z} \hat q_m e^{2 \pi im (j - k)/n} e^{2\pi i k l / n} \\
&= u^{(l)}_1 \sum_{m \in \mathbb Z} \hat q_m e^{2 \pi im  j/n}\sum^n_{k = 1} e^{2\pi i(l - m) k / n} \\
&= n u^{(l)}_1  \sum_{m \in \mathbb Z} \hat q_m e^{2 \pi im j / n} \sum_{r \in \mathbb Z}\delta_{(l+rn)m}\\
&=n u^{(l)}_1 \sum_{r \in \mathbb Z} \hat q_{l + rn} e^{2\pi i (l + rn) j / n} = n \sum_{r \in \mathbb Z} \hat q_{l + rn} u^{(l)}_j,
\end{align*}
$$
and $K$ has eigenvalues of $n \sum_{r \in \mathbb Z} \hat q_{l + rn}$, with $l = 1, \cdots, n$. Note that if $q$ has small high-frequency components, the eigenvalues can be effectively approximated as $n \hat q_l$. The smoothing matrix is $H = K(K + n \lambda I)^{-1}$ with regularization parameter $\lambda > 0$. Since $(K + n \lambda I)^{-1}$ commutes with $K$ and $K$ has $n$ distictive eigenvalues, $H$ has the same eigenvector as $K$, and letting the $i$th eigenvalue of $K$ be $\eta_i$, the eigenvalue of $H$ with the same eigenvector comes out as
$$
\frac{\eta_i}{\eta_i + n \lambda} = \frac{\sum_{r \in \mathbb Z} \hat q_{i + rn}}{\sum_{r \in \mathbb Z} \hat q_{i + rn} + \lambda},
$$
and of course, for $i = 1, \cdots, n$.
