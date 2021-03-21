## Jacobian Matrix Default
$1\times M$行向量偏导算子：
$$D_x=\frac{\partial}{\partial x^T}=\left[\begin{matrix}
   \frac{\partial}{\partial{x_1}},...,\frac{\partial}{\partial{x_m}}
\end{matrix}\right]$$

关于实值标量函数$f(x)$在x的偏导向量由$1\times m$行向量
$$D_xf(x)=\left[\begin{matrix}
 \frac{f(x)}{\partial{x_1}},....,\frac{f(x)}{\partial{x_m}}
 \end{matrix}\right]$$

当实值标量函数$f(X)$的变元为实值矩阵$X\in{R^{m\times n}}$,定义成两种可能，但是实际上有用的定义为第二种：

$$D_{vecX}f(X)=\left[\begin{matrix}
    \frac{\partial f(x)}{\partial x_{11}} && \cdots && \frac{\partial f(x)}{\partial x_{m1}} \\ \vdots && \ddots && \vdots \\ \frac{\partial{f(X)}}{\partial x_{{1n}}} && \cdots && \frac{\partial f(X)}{\partial x_{mn}}
\end{matrix}\right] \in R^{n\times m}$$

