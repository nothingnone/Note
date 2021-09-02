# Linear programming
## problem
$$

\begin{gathered}
minf(X)=CX \\
AX+B \geq 0
\end{gathered}
$$

## principle
Minumum must at cross point of constraints. Solve space of constraints is a convex polygon zone in high dimension, so start from a valid point and search along constraint and normal vector of C, we will find minimum finally.
The key is how to implement search method with a high efficiency algorithm.----simplex method.

- algorithm
Todo

# Lagrangian multiplication method
## problem
$$
\begin{gathered}
min \ f(X) \  , (\text{convex function}) 
\\
h_{i}(X) = 0
\\
g_{i}(X) \ge 0
\end{gathered}
$$

## visualize
![probelm-graph](../Imgs/nolinear-programming/contraint-programming-graph.png)
According to graph, the solve must be at edge of $f(X)$ and $g_{i}(X)$ or $h_i(X)$ where normal vetor of $f(X)$ and $g_{i}(X)$ or $h_i(X)$ in opposite direction. Considering 
$$  h_i(X) = 0 \  \text{equal to} \   h_i(X) \ge 0 \ and \ -h_i(X) \ge 0 $$
So we can treat $h_i(X)$ as $g_i(X)$. Here we comes a problem, if the constraints are combination of two constraints, how to decide the **"normal vector"**. Here only address conclusion: 
$$ 
\begin{gathered}
V_{combine} = \sum{a_i \cdot V_i}, \\
a \ge 0 \ and \ V_i \ \text{is normal vector of }g_i(X), \\
X \in \cap{\{g_i(X) = 0 \}}
\end{gathered}
$$
Because $X$ in solve zone is not differentiable, so all vector meet above can be considered as "normal vector". The origin now expand to following.
$$
\begin{gathered}
f'(X) = \sum{a_i \cdot g'_i(X)},\ a_i \ge 0
\end{gathered}
$$




## principle
According to above, we can easily get constraints of solve, but how can we define which $i$ of $g_{i}(X)$ is the actice edge? We can find that if it is not active, we don't need to constraint it, we can give it a weight 0.
Now, the optimize solve must meet following constraints.
We can solve them to get potential solution.
$$\begin{cases}
f'(X)-a_i \cdot h'(X)-b_i \cdot g'(X)=0
\\
b_i \cdot g(X)=0
\\
b_i \ge 0
\\
g_{i}(X) \ge 0
\\
h_{i}(X) = 0
\end{cases}$$

## strong dual problem
According to above, we can transform origin problem to following when $f(X)$ is convex, and $g''_i(X),h''_i(X)$ is 0.
$$\begin{gathered}
min \mathcal{L}(X)=   f(X)-ag_i(X)-b_ih(X), \text{ for all } a \ge 0,b
\end{gathered}$$
The above is convex, so the local minimum is global minimum. QP(Quadratic Programming) problem, SVM are 
classic strong dual problem. Have following equation.
$$
\min_{x}\max_{a,b} \mathcal{L}(X) = \max_{a,b}\min_{x} \mathcal{L}(X)
$$
This can reduce computation. It can be derived easily.
sufficient but not necessary condition of strong dual problem--slater condition.
Exist $X$, makes all $g_i(X)>0$.

# Interior Point Method
## principle
### obstacle function method
Key idea is very simple, turn strict constraints into soft. 
$$
\begin{gathered}
g(X) \ge 0 \implies -\tau \cdot ln(g(X)), \tau \to 0 \\
h(X)=0 \implies (|h(X)|)^{\frac{1}{\tau}} \  or \ \frac{1}{\tau}(h(X))^4,\tau \to 0
\end{gathered}
$$
Besides, two punishment functions are convex.
On the one hand, we can simply use decent method to find method.
We can alse use Analytic Method to find solve, if $f(X),g(X),h(X)$ is easily to analyze.
$$
\begin{gathered}
min f(X) \implies min\ f(X)-\tau ln(g_i(X)) \\
h_i(X) = 0 \\
\text{now KKT condition is easier to solve without }
\end{gathered}
$$
