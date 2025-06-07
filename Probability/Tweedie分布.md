---
tags:
  - probability
  - distribution
  - tweedie
---

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

## 平均と分散
- **平均**: $E[Y]=\mu$
- **分散**: $\operatorname{Var}[Y\mid\mu]=\phi\,\mu^{p}$

## ポイント
- 分散関数が $\operatorname{Var}[Y\mid\mu]=\phi\,\mu^{p}$ となる．
- $p$ の値によって特定の分布をとる．
	- $p=0$: [[正規分布]]
	- $p=1$: [[ポアソン分布]]
	- $1 < p < 2$: [[混合ポアソン・ガンマ分布]]
	- $p=2$: [[ガンマ分布]]
	- $p=3$: [[逆正規分布]]

$p = 1,2$ の時は，そのまま代入すると0で割ることになって計算できないが，$p \rightarrow 1$ の極限をとるとポアソン分布になるそう．