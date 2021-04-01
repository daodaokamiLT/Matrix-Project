## make same depart to useless in optimization

$$\left[\begin{matrix}
    A_a & A_b \\ 
    A^T_b & A_c
\end{matrix} \right]\left[\begin{matrix}
    \delta x_a \\ \delta x_b
\end{matrix} \right] = \left[\begin{matrix}
    g_a \\ g_b 
\end{matrix}\right]$$

change to 
$$\left[\begin{matrix}
    A_a & A_b \\ 
    0 & A_c-A^T_bA^{-1}_aA_b
\end{matrix} \right]\left[\begin{matrix}
    \delta x_a \\ \delta x_b
\end{matrix} \right] = \left[\begin{matrix}
    g_a \\ g_b-A^T_bA^{-1}_ag_a
\end{matrix} \right]$$

the second function just reference with $x_b$, we can cal the $x_b$ directly.

just for the sliding window the $H_j$ in the VINS.

so can use the Hessian matrix sparise parameters to speed up the normal euqation. 

### when use the schur comlement to mag element, the imcrement equation how it is change to piror.

$P(x,y)=P(x|y)P(y)$, $P(x|y)$ is condition, P(y) is piror

so if $(x,y)$ is gaussion, we have:

$$p(x,y) = N\left(\left[\begin{matrix}u_x \\ u_y \end{matrix}\right], \left[\begin{matrix}
    \sum_{xx} & \sum_{xy} \\ 
    \sum_{yx} & \sum_{yy}
    \end{matrix} \right]\right)$$

$$p(x,y) = p(x|y) p(y)  \\ 
p(x|y) = \frac{p(x,y)}{p(y)}$$

$$p(x|y) = N(u_x+{\sum}_{xy}{\sum}^{-1}_{yy}, {\sum}_{xx}-{\sum}_{xy}{\sum}^{-1}_{yy}{\sum}_{yx})$$

$$p(y) = N(u_y, {\sum}_{yy})$$

推导：

联合分布的方差舒尔补分解：
$$\left[\begin{matrix}
    \sum_{xx} & \sum_{xy} \\ 
    \sum_{yx} & \sum_{yy}
 \end{matrix} \right] = \left[\begin{matrix}
     1 & \sum_{xy}\sum_{yy}^{-1} \\
     0 & 1
 \end{matrix} \right]\left[\begin{matrix}
     \sum_{xx}-\sum_{xy}\sum_{yy}^{-1}\sum_{yx} & 0 \\
     0 & \sum_{yy}
 \end{matrix} \right] \left[\begin{matrix}
     1 & 0 \\
     \sum_{yy}^{-1}\sum_{yx} & 1
 \end{matrix}\right]$$

 其逆为：
 $$\left[\begin{matrix}
    \sum_{xx} & \sum_{xy} \\ 
    \sum_{yx} & \sum_{yy}
 \end{matrix} \right]^{-1} = \left[\begin{matrix}
     1 & 0 \\
     -\sum_{xy}\sum_{yy}^{-1} & 1
 \end{matrix}\right] \times \left[\begin{matrix}
     (\sum_{xx}-\sum_{xy}\sum_{yy}^{-1}\sum_{yx})^{-1} & 0 \\
     0 & \sum_{yy}^{-1}
 \end{matrix} \right] \left[\begin{matrix}
     1 & -\sum_{xy}\sum_{yy}^{-1} \\
     0 & 1
 \end{matrix}\right]$$

 密度函数的指数部分二次项为：
 $$\left(\left[\begin{matrix}
     x \\ y
 \end{matrix} \right] - \left[\begin{matrix}
     u_x \\ u_y
 \end{matrix} \right]\right)^T \left[\begin{matrix}
    \sum_{xx} & \sum_{xy} \\ 
    \sum_{yx} & \sum_{yy}
 \end{matrix} \right]^{-1} \left(\left[\begin{matrix}
     x \\ y
 \end{matrix} \right] - \left[\begin{matrix}
     u_x \\ u_y
 \end{matrix} \right]\right)$$

展开

 $$\left(\left[\begin{matrix}
     x \\ y
 \end{matrix} \right] - \left[\begin{matrix}
     u_x \\ u_y
 \end{matrix} \right]\right)^T 
 \left[\begin{matrix}
     1 & 0 \\
     -\sum_{xy}\sum_{yy}^{-1} & 1
 \end{matrix}\right] \times \left[\begin{matrix}
     (\sum_{xx}-\sum_{xy}\sum_{yy}^{-1}\sum_{yx})^{-1} & 0 \\
     0 & \sum_{yy}^{-1}
 \end{matrix} \right] \left[\begin{matrix}
     1 & -\sum_{yy}\sum_{xy}^{-1} \\
     0 & 1
 \end{matrix}\right]
 \left(\left[\begin{matrix}
     x \\ y
 \end{matrix} \right] - \left[\begin{matrix}
     u_x \\ u_y
 \end{matrix} \right]\right)$$

simplify
$$(x-u_x-{\sum}_{xy}{\sum}^{-1}_{yy}(y-u_y))^T 
\left({\sum}_{xx}-{\sum}_{xy}{\sum}_{yy}^{-1}{\sum}_{yx}\right)^{-1} \times 
(x-u_x-{\sum}_{xy}{\sum}_{yy}^{-1}(y - u_y))+(y-u_y)^T{\sum}^{-1}_{yy}(y-u_y)$$

这就是条件概率和边缘概率。

### still lost same math basic

$$X \sim N(u_x, {\sum}_{xx}) \\ p_x(x) = \frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{1}{2}(\frac{x-u}{\sigma})^2}， \sigma = {\sum}_{xx}$$

$$Y \sim N(u_y, {\sum}_{yy})$$

$$p(x,y) = p(x|y) p(y)$$

<!-- important gaussion process -->
$$p(x|y) \sim N(ux+{\sum}_{xy}{\sum}^{-1}_{yy}(Y-uy), {\sum}_{xx}-{\sum}_{xy}{\sum}^{-1}_{yy}{\sum}_{yx})$$
also has 
$$p(y|x) \sim N(uy+{\sum}_{yx}{\sum}^{-1}_{xx}(X-ux),{\sum}_{yx}{\sum}^{-1}_{xx}{\sum}_{xy})$$


当联合分布(x,y)是相互独立的并且，并且满足标准正太分布，则可以得到联合概率分布函数如下：
$$z_i = \frac{x_i-u_i}{\sigma_i}$$
$$p_x(z_i) = \frac{1}{\sigma \sqrt{2\pi}}e^{-\frac{1}{2}z^2}$$

$$1 = \int^{\infin}_{-\infin}p_x(z)dx \\ 
    = \int^{\infin}_{-\infin}\frac{1}{\sigma \sqrt{2\pi}}e^{-\frac{1}{2}z^2}dx \\ 
    = \int^{\infin}_{-\infin}\frac{1}{\sqrt{2\pi}}e^{-\frac{1}{2}z^2}d\frac{(x-u)}{\sigma} \\
    = \int^{\infin}_{-\infin}\frac{1}{\sqrt{2\pi}}e^{-\frac{1}{2}z^2}dz$$

有条件如下$X \sim N(0,I), Y \sim N(0,I)$:
$$p(x, y) = \frac{1}{\sqrt{2\pi}}e^{-\frac{1}{2}(x)^2}\frac{1}{\sqrt{2\pi}}e^{-\frac{1}{2}(y)^2} \\
= \frac{1}{(2\pi)^\frac{2}{2}}e^{-\frac{1}{2}(X^TY)}$$
$$1 = \int^{\infin}_{-\infin}\int^{\infin}_{-\infin}p(x,y)dxdy$$

有联合分布,(x,y 不是相互独立的) ,将$(x, y)$成为向量$X$， $X$是线性相关的，通过变换将$X$线性变换后彼此独立。
$$Z = B^{-1}(X-u), Z \sim N(0, I)$$
$z_1, z_2$对应了原始的非标准正态分布$x, y$

$$p(z_1, z_2) = \frac{1}{(2\pi)^\frac{n}{2}}e^{-\frac{1}{2}(Z^TZ)} \\ 
p(z_1(x,y), z_2(x,y)) = \frac{1}{(2\pi)^{\frac{n}{2}}}e^{[-\frac{1}{2}(B^{-1}(X-u))^T(B^{-1}(X-u))]} \\
\frac{1}{(2\pi)^{\frac{n}{2}}}e^{[-\frac{1}{2}(X-u)^T(BB^T)^{-1}(X-u)]}$$


$$1 = \int^\infin_{-\infin}\int^\infin_{-\infin}p(z_1(x, y), z_2(x, y))dz_1dz_2 \\
= \int^\infin_{-\infin}\int^\infin_{-\infin}\frac{1}{(2\pi)^{\frac{n}{2}}}e^{-\frac{1}{2}[(X-u)^T(BB^T)^{-1}(X-u)]}dz_1dz_2$$
J means Jacobi
$$J(Z\rightarrow X) = |B^{-1}| = |B^{-1}| = |B|^{-\frac{1}{2}}|B^T|^{-\frac{1}{2}} = |BB^T|^{\frac{1}{2}}$$

so the last equation can be simplify to 
$$1 = \int^\infin_{-\infin}\frac{1}{(2\pi)^{\frac{n}{2}}|BB^T|^{\frac{1}{2}}}e^{-\frac{1}{2}[(X-u)^T(BB^T)^{-1}(X-u)]}dxdy$$

so we can has the p(x,y) is follow the bellow equation
$$p(x,y) \sim N(u, \sum)$$
$$u = u$$

$$\sum= E[(X-u)(X-u^T)] \\ =E[(BZ - 0)(BZ-0)^T] \\
= Conv(BZ, BZ) \\ =BConv(Z, Z)B^T \\ 
= BB^T$$

这个$BB^T$就是线性变化钱随机吸纳改良 $X(x,y)$的协防差矩阵。我们可以得到联合概率密度函数的最终形式：
$$p(x_1, x_2, \cdots, x_n) = \frac{1}{(2\pi)^{\frac{n}{2}}|\sum|^{\frac{1}{2}}}e^{-\frac{1}{2}(X-u)^T){\sum}^{-1}(X-u)}$$

## Extend KF




## sliding window 

