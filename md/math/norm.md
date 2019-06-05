[TOC]

## 定理

### ノルムが定まっている有限次元ベクトル空間はR^nと位相同型

> Let $$E$$ be a $$n$$-dimensional norm space over $$\mathbb{R}$$ whose norm is represented by $$N$$.
>
> Then $$E$$ and $$\mathbb{R}^n$$ be homeomorphic.

Proof.

$$E$$の基底(basis)を$$u_1,\dots ,u_n$$とおき$$L: E \to \mathbb{R}^n$$を
$$
L (\sum_{i=1}^n \lambda_i u_i) = \sum_{i=1}^n \lambda_i e_i
$$
とおく.ただし$$e_1,\dots ,e_n$$は$$\mathbb{R}^n$$の標準基底(standard basis)とする.この時$$L$$は全単射な線形写像(linear map)である(証明略).また,$$N': \mathbb{R}^n \to [0, \infty):x \mapsto N(L^{-1}(x))$$と定義する.この時$$N'$$はnormとなる.以下では劣加法性(subadditive)のみ示してその他は略する.
$$
\begin{align*}
N'(x + y) 
&= N\left(
		\sum_{i=1}^n (x_i + y_i) u_i
	\right)\\
&= N\left(
		\sum_{i=1}^n x_i u_i + \sum_{i=1}^n y_i u_i
	\right)\\
&\le 
	N\left( \sum_{i=1}^n x_i u_i \right)
	+ N\left( \sum_{i=1}^n y_i u_i \right)\\
&= N'(x) + N'(y)
\end{align*}
$$
次に$$L$$が同相写像(homeomorphism)であることを示す.

証明のために中心$$v$$,半径(radius)$$r$$である$$E$$上の開球(open ball) $$B_{r}(v)$$を以下で定める.
$$
B_{r}(v) \equiv \{ w \in E \mid N(w - v) < \epsilon \}
$$
同様に$$\mathbb{R}^n$$上のopen ballは$$B'_{r}(x_0)$$で表すことにする.

まず$$V \subset E$$がopenならば$$L(V)$$がopenであることを示す.

任意に$$x_0 \in L(V)$$をとると$$L^{-1}(x_0) \in V$$であり$$V$$はopenであることから$$\epsilon > 0$$が存在し,$$B_{\epsilon} (L^{-1}(x_0)) \subset V$$を満たす.この時,任意の$$x \in \mathbb{R}^n$$に対して
$$
\begin{align*}
L^{-1}(x) \in B_{\epsilon}(L^{-1}(x_0))
&\Leftrightarrow N \left( L^{-1}(x) - L^{-1}(x_0) \right) < \epsilon\\
&\Leftrightarrow N (L^{-1}(x - x_0)) < \epsilon\\
&\Leftrightarrow N'(x - x_0) < \epsilon
\end{align*}
$$
であることに注意すると,
$$
\begin{align*}
B'_{\epsilon}(x_0) 
&= \{ x \in \mathbb{R}^n \mid N'(x - x_0) < \epsilon \}\\
&= \{ x \in \mathbb{R}^n \mid L^{-1}(x) \in B_{\epsilon}(L^{-1}(x_0)) \}\\
&= L \left( B_{\epsilon} (L^{-1}(x_0)) \right) \subset V
\end{align*}
$$
次に$$U \subset \mathbb{R}^n$$がopenならば$$L^{-1}(U)$$がopenであることも同様に示せる.よって$$L$$はhomeomorphism.

