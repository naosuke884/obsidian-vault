# Tweedie分布

Tweedie分布は多種の分布を包含する指数分散モデル([[指数分散モデル (EDM)]])の一種．

$$
f_{Y}(y;\mu,\phi,p)=a(y;\phi,p)\,
\exp\!\left\{
  \frac{1}{\phi}
  \left[
    \frac{y\,\mu^{1-p}}{1-p}
    -\frac{\mu^{2-p}}{2-p}
  \right]
\right\},
\qquad
\phi>0,\; p\neq 1
$$

$$
\theta=\frac{\mu^{1-p}}{1-p},
\qquad
\kappa(\theta)=\frac{\mu^{2-p}}{2-p},
\qquad
f_{Y}(y;\mu,\phi,p)=a(y;\phi,p)\,
\exp\!\left\{\frac{y\theta-\kappa(\theta)}{\phi}\right\}.
$$

$$
\operatorname{Var}[Y\mid\mu]=\phi\,\mu^{p},
\qquad
p=0:\ \text{Normal},\;
p=1:\ \text{Poisson},\;
p=2:\ \text{Gamma},\;
p=3:\ \text{Inverse Gaussian}.
$$
