## Linear programming
- problem
$$

\begin{gathered}
minf(X)=CX \\
AX+B \geq 0
\end{gathered}
$$

- principle
Minumum must at cross point of constraints. Solve space of constraints is a convex polygon zone in high dimension, so start from a valid point and search along constraint and normal vector of C, we will find minimum finally.
The key is how to implement search method with a high efficiency algorithm.----simplex method.

- algorithm
Todo

## Lagrangian multiplication method
- problem
$$
\begin{gathered}
min \ f(X) \  , (\text{convex function}) 
\\
g_{i}(X) \ge 0
\\
h_{i}(X) = 0
\end{gathered}
$$
- visualize
Graph in slove zone of $h_{i}(X)$
![probelm-graph](../Imgs/nolinear-programming/contraint-programming-graph.png)
According to graph, the solve must be at edge of $f(X)$ and $g_{i}(X)$ where normal vetor of $f(X)$ and $g_{i}(X)$ in opposite direction.

- principle
According to above, we can easily get constraints of solve, but how can we define which $i$ of $g_{i}(X)$ is the actice edge? We can find that if it is not active, w don't need to constraint it, we can give it a weight 0.
$$
\begin{cases}
f'(X)-ag'(X)=0
\\
ag(X)=0
\\
g_{i}(X) \ge 0
\\
h_{i}(X) = 0
\\
a \ge 0
\end{cases}
$$
Now we can 



