# linear regression
## principle
$$
\begin{gathered}
f(x) = c_n x^n +c_{n-1}x^{n-1}+... +c_0x^0 = y \\
given \  x_i,y_i \\
X=[x_i^{n},x_i^{n-1},...,x_i^0; ...] \\
Y=[y_i;...] \\
A = [c_n; c_{n-1}; ...;c_0] \\
\min_{A,B}{\sum{(Y-X \cdot A)^2}}
\end{gathered}
$$
## derivation
$$
\begin{gathered}
\begin{aligned}
&\min_{A,B} \sum{(Y-X \cdot A)^2} \\
=& \min_{A,B} (Y-X \cdot A)^T \cdot (Y-X \cdot A) \\
=& \min_{A,B} g(A) \\
\end{aligned} \\
\text{it's a convex problem.} \\
\begin{aligned}
&\frac{\partial g(A)}{\partial A} \\ 
=& (-X)^T \cdot (Y-X \cdot A) + ((Y-X \cdot A)^T  \cdot (-X))^T \\
=& -2 X^T \cdot (Y-X \cdot A) = 0 \\
\end{aligned} \\
A = (X^T \cdot X)^{-1} \cdot X^T \cdot Y
\end{gathered}
$$
## Note
