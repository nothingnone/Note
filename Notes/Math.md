# linear regression
## principle
$$
\begin{gathered}
f(x) = c_n x^n +c_{n-1}x^{n-1}+... +c_0x^0 = y \\
given \  x_i,y_i \\
X=[x_i^{n},x_i^{n-1},...,x_i^0; ...] \\
Y=[y_i;...] \\
A = [c_n, c_{n-1}, ...,c_0] \\
\min_{A,B}{\sum{(Y-AX)^2}}
\end{gathered}
$$
## derivation
$$
\begin{gathered}
\begin{aligned}
&\min_{A,B} \sum{(Y-AX)^2} \\
=& \min_{A,B} (Y-AX)^T \cdot (Y-AX) \\
=& \min_{A,B} g(A) \\
\end{aligned}
\begin{gathered}
\frac{\partial g(A)}{\partial A}
\end{gathered}
\end{gathered}
$$