# 指数分散モデル (EDM)
[[自然指数族]]を拡張したもの．
$\phi$ を固定すれば，自然指数族になる．

## 定義
$$f(y;\theta,\phi) = a(y,\phi)\exp\Bigl(\frac{y\theta - b(\theta)}{\phi}\Bigr), \quad y\in\mathcal{Y}$$

- $\theta$: 正規化パラメータ
- $\phi>0$: 分散パラメータ
- $a(\cdot), b(\cdot)$: 正規化定数

## 平均・分散
- **平均**: $\mu = E[Y] = b'(\theta)$
- **分散**: $\mathrm{Var}(Y) = \phi\,b''(\theta) = \phi\,V(\mu)$