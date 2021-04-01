<!-- KF.md -->
## KF

if we has 
$$x_k = A x_{k-1}+B u_k + w_{k-1}$$
$$z_k = Hx_k+v_k$$

$v_k, w_k$ is noise follow as $N(0, Q), N(0, R)$



对于时刻$k-1$有一个估计状态（通过融合各市局状态）$\tilde{x}_{k-1|k-1}$, 预测下一次的状态$\hat{x}_{k|k-1}$, 该估计的协防差为 $\tilde{P}_{k-1|k-1}$

$\tilde{*}$ 估计， $\tilde{*}$ 最优估计， $*$ ground truth

$$\tilde{x}_{k|k-1} = A\tilde{x}_{k-1|k-1}+Bu_{k-1}$$

$$error(x_k - \tilde{x}_{k|k-1})= x_k - \tilde{x}_{k|k-1}$$


$x_k, z_k$ follow the probility $p_k = \left[\begin{matrix}
    \sum_{xx} & \sum_{xz} \\
    \sum_{zx} & \sum_{zz}
\end{matrix} \right]$ ， so the next status can be estimate like follow:

we cal the $p(x_k|x_{k|k-1}, z_k)$ the most big one is what?

we have a status change equation:

$$\tilde{x}_k = \hat{x}_k + K_k(z_k-\hat{z}_k)\\
              = \hat{x}_k + K_k(z_k-H\hat{x}_k)$$

求解本次预测情况下的误差：
$$M_k = E[(x_k-\tilde{x}_k)(x_k-\tilde{x}_k)^T]$$

将上式子带入

$$M_k = E[(x_k - \hat{x}_k - K_k(z_k-H\hat{x}_k))(x_k - \hat{x}_k - K_k(z_k-H\hat{x}_k))^T] \\ 
 = E[(x_k-(I+K_kH)\hat{x}_k-K_kz_k)(same)^T] \\
 = E[(x_k-(I-K_kH)\hat{x}_k-K_k(Hx_k+v_k))(same)^T]\\
 = E[(x_k-(I-K_kH)\hat{x}_k-K_kHx_k-K_kv_k)(same)^T] \\
 = E[((I-K_kH)(x_k-\hat{x})-K_kv_k)(same)^T]$$
又有公式如下
 $$E[(Av+bw)(Av+bw)^T] = AE[vvT]A+bE[ww^T]b^T$$

so we also has 
$$M_k = (I-K_kH)E[(x_k-\hat{x})(x-\hat{x})^T](I-K_kH)^T+K_kE[v_kv_k^T]K^T_k$$
设置
$$\hat{M}_k = E[(x_k - \hat{x}_k)(x_k-\hat{x}_k)^T]$$
$$R = E[v_k v_k^T]$$

展开为：
$$M_k = \hat{M}_k-(K_kH\hat{M}_k+\hat{M}_kH^TK^T_k)+K_k(H\hat{M}_kH^T+R)K^T_k$$

均方误差矩阵是对称的，求迹

$$tr(M_k) = tr(\hat{M}_k)+2tr(K_kH\hat{M}_k)+tr(K_k(H\hat{M}_kH^T+R)K^T_k)$$

最小化真实值与估计值的均方误差，令$\frac{\partial M_k}{\partial K_k}$ 最小， 即应该为 0.

$$-2(H\hat{M}_k)^T+2K_k(H\hat{M}_kH^T+R) = 0$$

可以解得：
$$K_k = \hat{M}_kH^T(H\hat{M}H^T+R)^{-1}$$

因此还可以得到$M_k$的表示。

