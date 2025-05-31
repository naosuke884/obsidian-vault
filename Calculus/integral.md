# 積分の公式
## 基本的な積分公式

- $\int x^n dx = \frac{x^{n+1}}{n+1} + C$ （ただし、$n \neq -1$）
- $\int \frac{1}{x} dx = \ln|x| + C$
- $\int e^x dx = e^x + C$
- $\int a^x dx = \frac{a^x}{\ln a} + C$
- $\int \sin x \, dx = -\cos x + C$
- $\int \cos x \, dx = \sin x + C$
- $\int \tan x \, dx = -\ln|\cos x| + C = \ln|\sec x| + C$
- $\int \cot x \, dx = \ln|\sin x| + C$
- $\int \sec x \, dx = \ln|\sec x + \tan x| + C$
- $\int \csc x \, dx = \ln|\csc x - \cot x| + C$

## 逆三角関数の積分

- $\int \frac{1}{\sqrt{1-x^2}} dx = \arcsin x + C$
- $\int \frac{1}{1+x^2} dx = \arctan x + C$
- $\int \frac{1}{x\sqrt{x^2-1}} dx = \arccos \frac{1}{x} + C = \text{arcsec} \, x + C$

## 部分積分の公式

$\int u(x) v'(x) dx = u(x)v(x) - \int v(x)u'(x) dx$

## 置換積分の公式

$\int f(g(x))g'(x)dx = \int f(u)du$ （ただし $u = g(x)$）

## 定積分の基本定理

$\int_{a}^{b} f(x) dx = F(b) - F(a)$ （ただし $F'(x) = f(x)$）

## 応用例

- $\int x \sin x \, dx = -x \cos x + \int \cos x \, dx = -x \cos x + \sin x + C$
- $\int \ln x \, dx = x \ln x - x + C$
- $\int x e^x \, dx = x e^x - \int e^x \, dx = x e^x - e^x + C$

積分を計算する際は、これらの公式を適用したり、部分積分や置換積分などの手法を使用したりします。複雑な積分の場合は、適切な手法を選択することが重要です。