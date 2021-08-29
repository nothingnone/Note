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

## Laga
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
According to graph, the solve must be at position where normal vetor of $f(X)$ and $g_{i}(X)$ in 