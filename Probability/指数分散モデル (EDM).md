# 定義
$$f(y;\,\theta,\phi) = a\!\left(y,\phi\right)\, \exp\!\Bigl\{\frac{y\theta - b(\theta)}{\phi}\Bigr\}, \qquad y\in\mathcal Y$$
という形をとる確率分布族
$\theta$ : 正規化パラメータ
$\phi > 0$ : 分散パラメータ
$a(\cdot),b(\cdot)$ : 正規化定数
## 平均・分散
**平均：**　$\mu = E[Y] = b'(\theta)$
**分散：**　$Var(Y) = \phi b''(\theta) = \phi V(\mu)$
$Var(Y)$ を分散関数とよぶ
平均と分散が分離している
→平均を求めるのに，分散パラメータは使わない．分散を求めるのに分散パラメータと平均は掛け算でしか関わらない（分離している）．