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

实值矩阵函数$F(X)=\left[f_{kl}\right]^{p,q}_{k=1,k=1}\in R^{p\times q}$，矩阵变元$X\in R^{m\times n}$。可以有多种行偏导矩阵定义。

$$\frac{\partial F(X)}{\partial X^T}=\left[ \begin{matrix}
    \frac{\partial f_{kl(X)}}{\partial X^T}   
\end{matrix}\right]^{p,q}_{k=1, l=1}=\left[ \begin{matrix}
    \frac{\partial f_{11}(X)}{\partial X^T}&&\cdots&&\frac{\partial f_{1q}(X)}{\partial X^T}\\ \vdots && \ddots && \vdots \\ \frac{\partial f_{p1}}{\partial X^T} && \cdots && \frac{\partial f_{pq}}{\partial X^T}
\end{matrix}\right] \in R^{pn \times qm}$$

或者对$X$的形式进行单个元素的求导。
$$\frac{\partial F(X)}{\partial X^T}=\left[ \begin{matrix}
    \frac{\partial f_{kl(X)}}{\partial x_{ij}^T}   
\end{matrix}\right]^{p,q}_{k=1, l=1}=\left[ \begin{matrix}
    \frac{\partial f_{11}(X)}{\partial x_{ji}}&&\cdots&&\frac{\partial f_{1q}(X)}{\partial x_{ji}}\\ \vdots && \ddots && \vdots \\ \frac{\partial f_{p1}}{\partial x_{ji}} && \cdots && \frac{\partial f_{pq}}{\partial x_{ji}}
\end{matrix}\right] \in R^{pn \times qm}$$

又或者将上面的$F$展开。但是这样定义都是不好的，不适合计算比较复杂的Jaccobi 矩阵。


可以方便的方法是：将$F(X)_{p\times q}$列向量化$F(X)_{pq\times 1}$

$$vec(F(X))=\left[ f_{11}(X), \cdots, f_{p1}(X) \right]^T \in R^{pq}$$

然后将X列向量化，对$(vec(X))^T$求偏导，给出$pq\times mn$的jaccobi矩阵

$$D_xF(X)=\frac{\partial vec(F(X))}{\partial (vecX)^T}\in R^{pq\times mn}$$

$$D_xF(X)=\left[\begin{matrix}
    \frac{\partial f_{11}}{\partial(x_{1n})} \\ \vdots \\ \frac{\partial f_{p1}}{\partial(vecX)^T} \\ \vdots \\
    \frac{\partial f_{1q}}{\partial(vecX)^T} \\ \vdots \\
    \frac{\partial f_{pq}}{\partial(vecX)^T} 
\end{matrix}\right]=\left[\begin{matrix}
    \frac{\partial f_{11}}{\partial x_{11}} && \cdots &&
    \frac{\partial f_{11}}{\partial x_{m1}} && \cdots && 
    \frac{\partial f_{11}}{\partial x_{1n}} && \cdots &&
    \frac{\partial f_{11}}{\partial x_{mn}} \\
    \vdots &&  \vdots && \vdots && \vdots && \vdots && \vdots && \vdots \\ 
    \frac{\partial f_{p1}}{\partial x_{p1}} && \cdots &&
    \frac{\partial f_{p1}}{\partial x_{m1}} && \cdots && 
    \frac{\partial f_{p1}}{\partial x_{1n}} && \cdots &&
    \frac{\partial f_{p1}}{\partial x_{mn}} \\
    \vdots &&  \vdots && \vdots && \vdots && \vdots && \vdots && \vdots \\ 
    \frac{\partial f_{1q}}{\partial x_{1q}} && \cdots &&
    \frac{\partial f_{1q}}{\partial x_{m1}} && \cdots && 
    \frac{\partial f_{1q}}{\partial x_{1n}} && \cdots &&
    \frac{\partial f_{1q}}{\partial x_{mn}} \\
    \vdots &&  \vdots && \vdots && \vdots && \vdots && \vdots && \vdots \\ 
    \frac{\partial f_{pq}}{\partial x_{pq}} && \cdots &&
    \frac{\partial f_{pq}}{\partial x_{m1}} && \cdots && 
    \frac{\partial f_{pq}}{\partial x_{1n}} && \cdots &&
    \frac{\partial f_{pq}}{\partial x_{mn}}
\end{matrix}\right]$$