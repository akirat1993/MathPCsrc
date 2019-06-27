[TOC]

## 教科書

* [凸射影定理を図的に解説](https://maea2.github.io/convex-projection-theorem/)
* [凸射影定理の証明が載ってる](https://bit.ly/31TXyQH),[リンク切れ対策](https://www.slideshare.net/secret/MtNVjR3mrOdPYS)
* [凸体の日本語の教科書(勉強してないが詳しそう)](http://www.math.tsukuba.ac.jp/~tasaki/lecture/ln2009/2009t.pdf)



## 定義及び定理

### Def(Convex_set)

> Let $$S$$ be a vector space over the some *orderded field*. A set $$C$$ in $$S$$ is said to be **convex** if $$ (1-t)x + ty \in C \quad \forall x,y \in C, \forall t \in (0,1)$$



### Def(convex_function)

> Let $$X$$ be a *convex set* in a real vector space and let $$f:X \to \mathbb{R}$$ be a function.
>
> * $$f$$ is called **convex** if $$\forall x_1, x_2  \in X, \forall t \in [0,1]$$:
>
>   $$f(tx_1 + (1-t)x_2) \le t f(x_1) + (1-t) f(x_2)$$
>
> * $$f$$ is called **strictly convex** if $$\forall x_1 \ne x_2 \in X, \forall t \in (0,1)$$:
>
>   $$f(tx_1 + (1-t)x_2) < t f(x_1) + (1-t) f(x_2)$$
>
> * A function $$f$$ is said to be (strictly) **concave** if $$-f$$ is (strictly) convex.



### Def(エピグラフ:Epigraph)

> Let $$X \subset \mathbb{R}^n$$ be a convex set. 
>
> **Epigraph** or **supergraph** of a function $$f:X \to \mathbb{R}$$ is the set of points lying on or above its graph definied as
>
> $$\text{epi}\,f = \{ (x,t) \mid x \in \text{dom} f, f(x)\le t \} \subset \mathbb{R}^{n+1}$$
>
> ('Epi' means 'above' so  epigraph means 'above the graph')
>
> A function is convex(strictly convex) if and only if its epigraph is a (strictly) convex set.



### 凸関数の勾配の単調性

> Let $$f:\mathbb{R}^n \to \mathbb{R}$$ be class $$C^1$$. Then $$f$$ is convex if and only if $$\text{dom}\,f$$ is convex and $$\nabla f(x)$$ is a monotone operator: $$ \langle \nabla f(x) - \nabla f(y), x - y \rangle \ge 0$$

[Proof p2 Prop1.3](https://www.math.cuhk.edu.hk/course_builder/1617/math6211a/cvxop.pdf),[保存用](https://www.slideshare.net/secret/goFVDJ0ul0Vhxr)



### 凸関数の２階導関数テスト

> Let $$K \subset \mathbb{R}^n$$ be an open convex set, and let $$f:K \to \mathbb{R}$$ be continuous second partial derivatives. If the Hessian of $$f$$ is positive definite everywhere, then $$f$$ is convex on $$K$$. 

Let $$H_{(i,j)}$$ be an element of Hessian of $$f$$. Then, 
$$
H_{(i,j)} \equiv \frac{\partial^2}{\partial x_i \partial x_j} f
$$
($$x_j$$で偏微分した後で$$x_i$$で微分する)

[Proof Theorem5](http://math.ucr.edu/~res/math133/convex-functions.pdf),[保存用](https://www.slideshare.net/secret/NP7RGRYEJimsKV)



### R上の任意のノルムは凸関数である

> Let $$\| \cdot\|: V \to \mathbb{R}$$ be a norm on a vector space $$V$$ over $$\mathbb{R}$$. Then $$\| \cdot \|$$ is a convex function.

Proof.

任意の$$v, w \in V, \lambda \in [0,1]$$に対して,
$$
\| \lambda v + (1 - \lambda)w \|
\le \lambda\|v\| + (1-\lambda) \|w\|
$$



### Def(ヒルベルト空間)

> A **Hilbert space** $$(H, \langle \cdot \rangle)$$ is a real or complex inner product space that is also a complete metric space.



### 中線定理

> Let $$\mathcal{H}$$ be a Hilbert space. Then, for any $$x,y \in H$$, we have 
>
> $$\| x+ y \|^2 + \| x - y \|^2 = 2 (\|x\|^2 + \|y\|^2)$$
>
> parallelogram identity



### 凸射影定理

> Suppose $$S$$ is a nonempty closed convex subset of Hilbert space $$H$$. Then for every $$h \in H$$ there is a **unique** vector $$k \in S$$ such that
>
> $$ \| h - k \| = d (h, S) \equiv \inf_{\ell \in S}  \| h - \ell \|$$

$$d \equiv d(h, S)$$は下限であるので,任意の自然数$$n$$に対して,$$d \le \| h - k_n\| < d + \frac{1}{n}$$を満たす$$\{k_n\} \subset S$$が存在する.この時,明らかに$$\| h - k_n\| \to d (n \to \infty)$$である.[中線定理](#中線定理)より任意の自然数$$n,m$$に対して,
$$
\| (h - k_n) + (h - k_m)\|^2 + \|k_m - k_n \|^2
= 2 (\|h-k_n\|^2 + \|h-k_m\|^2)
$$
が成立する.$$(h - k_n) + (h - k_m) = 2(h - \frac{1}{2}(k_m + k_n))$$であり$$S$$が凸集合であるので$$\frac{1}{2}(k_m + k_n) \in S$$であることに注意すると,
$$
\begin{align*}
	\| k_m - k_n \|^2 
	&= 2 (\|h-k_n\|^2 + \|h-k_m\|^2)  - 4 \| h - \frac{1}{2}(k_m + k_n) \|^2\\
	&\le 2 (\|h-k_n\|^2 + \|h-k_m\|^2) - 4d^2
\end{align*}
$$
ゆえに$$n,m \to \infty$$の時,左辺$$ \to 2(d^2 + d^2) - 4d^2 = 0$$となるので$$\{k_n\}$$はコーシー列である.また,ヒルベルト空間は完備であり$$S$$は閉集合であったので$$\{k_n\}$$は$$S$$の元$$k$$に収束する.また,任意の自然数$$n$$について,
$$
| \| h - k \| - \| h - k_n \| | 
\le \| (h - k) - (h - k_n) \| = \| k - k_n \|
$$
であるので,$$\|h - k_n\| \to \|h - k \|$$である.また,$$\| h - k_n\| \to d$$であったので$$\| h - k \| = d$$である.

続いて一意性を示す.$$\| h - \ell \| = d$$が成立すると仮定する.この時,$$S$$は凸集合であるので,$$\frac{1}{2}(k+ \ell) \in S$$である.よって$$d$$の定義より$$\| h - \frac{1}{2}(k + \ell) \| \ge d$$である.一方,中線定理より,
$$
\begin{align*}
	2(d^2 + d^2) 
	&= 2 (\|h-k \|^2 + \|h - \ell\|^2) \\
	&= \| (h-k) + (h-\ell) \|^2 + \| k - \ell \|^2\\
	&= \left\| 2 \left(h - \frac{1}{2}(k + \ell) \right) \right\|^2
		+ \| k - \ell \|^2\\
	&\ge 4d^2 + \|k - \ell \|^2
\end{align*}
$$
となるので,ノルムの定義より$$k = \ell$$.



### 凸射影の幾何学的性質

> Suppose $$S$$ is a nonempty closed convex subset of Hilbert space $$(H, \langle \cdot \rangle )$$ and $$h \in H$$.
>
> Then for every $$k \in S$$,
>
> $$\| h - k \|= d(h, S) \equiv \inf_{\ell \in S} \| h - \ell \| \Leftrightarrow \text{Re}(\langle h - k, \ell - k\rangle) \le 0\quad \forall \ell \in S$$
>
> where $$\text{Re}(z)$$ is the real part of $$z$$. 

(注意)[凸射影定理](#凸射影定理)によって,$$\| h - k \|= d(h, S) $$となるような$$k \in S$$は唯一存在することは示せる.

($$\Rightarrow$$)任意に$$\ell \in S$$をとると,$$S$$は凸集合であるので任意の$$\lambda \in (0,1]$$に対して$$m \equiv \lambda \ell + (1 - \lambda)k$$は$$S$$の元である.よって,仮定より
$$
\begin{align*}
	\| h - k \| \le \|h - m\|
	&\Leftrightarrow
		\| h - k \|^2 \le \|h - m\|^2\\
	&\Leftrightarrow
		0 \le \lambda^2 \| \ell - k \|^2 
			- 2 \lambda \text{Re} (\langle h - k, \ell - k\rangle) \\
	&\Leftrightarrow
		\text{Re} (\langle h - k, \ell - k\rangle) 
			\le \frac{\lambda}{2} \| \ell - k \|^2
\end{align*}
$$
である.任意の$$\lambda \in (0,1]$$について成立しないといけないので$$\text{Re}(\langle h - k, \ell - k\rangle) \le 0$$

ただし,上記の式中の$$\|h-m\|^2$$の計算は以下を用いた.
$$
\begin{align*}
	\| h- m \|^2 
	&= \langle
				(h-k) - \lambda(\ell -k), (h - k) -\lambda(\ell - k)
			\rangle\\
	&= \| h - k\|^2 + \lambda^2\| \ell - k \|^2 
		- 2 \lambda \text{Re} (\langle h - k, \ell - k\rangle)
\end{align*}
$$
($$\Leftarrow$$)$$k \in S$$が任意の$$\ell \in S$$に対して$$\text{Re}(\langle h - k, \ell - k\rangle) \le 0$$を満たしているとする.

この時,$$\ell \in S$$を任意にとる.$$m \equiv 1 \cdot \ell + (1 - 1)k = \ell$$の定義すると,
$$
\text{Re} (\langle h - k, \ell - k\rangle) 
			\le \frac{\lambda}{2} \| \ell - k \|^2
$$
を満たす.よって上記の逆の議論をすることで,$$\| h - k \| \le \|h - m\| = \|h - \ell\|$$となる.



### 分離超平面定理(supporting_hyperplane)

> Let $$(H, \langle \cdot \rangle)$$ be a finite-deimensional Hilber space over a field $$\mathbb{R}$$ ,and $$C \subset H$$ be a *noempty convex* set.
>
>  Let $$x_0$$ be such that either $$x_0 \in bdC$$ or $$x_0 \notin C$$
>
> Then, there exists a hyperplane passing throught $$x_0$$ and containing the set $$C$$ in one of its half spaces, i.e., there is a vector $$a \in H$$, $$a \ne 0$$, such that $$\sup_{z \in C} \langle a, z \rangle \le \langle a, x_0 \rangle$$
>
> - A hyper plane with such property is reffered to as a *supporting hyperplane*.

(Proof for the case when $$C$$ is closed)

Let $$\{x_k \} \subset H \setminus C$$ sucth that $$x_k \to x_0, x_k \ne x_0$$.

------

上記の$$\{x_k\}$$の存在性の証明($$x_0 \in \text{bd}C$$の場合)

閉集合の閉包(closure)と閉集合自身は等しいので$$x_0 \in \text{bd}C = \bar{C} \setminus \text{int}C = C \setminus \text{int}C$$となる.

$$x_0 \notin \text{int}C$$より任意の$$\epsilon >0$$に対して中心$$x_0$$で変形$$\epsilon$$のball$$B_{\epsilon}(x_0) \nsubseteq C$$である.よって,任意の自然数$$k$$に対してを$$x_k \in B_{\frac{1}{k}}(x) \cap H \setminus C$$を満たすように$$\{ x_k \}_k \subset H \setminus C$$をとればよい.

上記の$$\{x_k\}$$の存在性の証明($$x_0 \notin C$$の場合)

$$C$$はclosedであったので$$H \setminus C$$はopen.よって,$$r >0$$が存在し$$B_r(x_0) \subset H \setminus C$$を満たす.また,$$H$$の任意の元は$$H$$の[孤立点ではないので](./norm.md#ノルム空間には孤立点は存在しない),$$B_r(x_0)$$から$$x_0$$に収束する点列を取れる.

------

Let $$z_k^*$$ be the projection of $$x_k$$ on the set $$C$$ for each $$k$$, i.e. 
$$
\| z_k^* - x_k \| = \text{dis}(x_k, C) \equiv  \inf_{z \in C} d(x_k, z)
$$
The exsistance and uniquness of  $$z_k^*$$ is proved [here](#凸射影定理). Consider 
$$
a_k \equiv \frac{x_k - z_k^*}{\| x_k - z_k^* \|}\quad \forall k \ge 1
$$
This sequence is bounded and, therefore there exists a subsequence of $$\{a_{\ell_k}\}$$ converging to $$a \in \mathbb{R}^n$$, where $$\| a \| = 1$$.

---

収束列$$\{a_{\ell_k}\}$$ が存在することは以下のように示すことが出来る.$$A \equiv \{ x \in H \mid \| x \| = 1 \}$$のような空間を考えると[ノルム空間の基本的な性質](./norm.md#ノルム空間の基本的な性質)より閉集合.さらに有界である.[よって](./norm.md#完備全有界な体におけるコンパクトと有界閉集合の同値性),コンパクトである.また距離空間においては[コンパクトと点列コンパクトは同値であるので](./metric.md#距離空間におけるコンパクトの同値条件), $$A$$は点列コンパクトとなるので,収束する部分列$$\{a_{\ell_k}\}$$ が存在し収束先は$$A$$の元となるのでノルムは1である.

---

Since $$z_k^*$$ is the projection of $$x_k$$, by the [Projection Theorem](#凸射影の幾何学的性質), for every $$z \in C, k \in \mathbb{N}_{>0}$$,
$$
\begin{align*}
	(z_k^* - x_k)^T (z - z_k^*) \ge 0
	&\Leftrightarrow
		a_k^T(z - z_k^*) \le 0\\
	&\Leftrightarrow
		a_k^T z\le a_k^T z_k^*
\end{align*}
$$

$$
\begin{align*}
	\langle z_k^* - x_k, z - z_k^* \rangle\ge 0
	&\Leftrightarrow
		\langle a_k, (z - z_k^*) \rangle \le 0\\
	&\Leftrightarrow
		\langle a_k, z \rangle \le \langle a_k, z_k^* \rangle
\end{align*}
$$

さらに,
$$
\langle a_k, z_k^* \rangle
= \langle a_k, z_k^* - x_k \rangle + \langle a_k, x_k \rangle
= - \langle a_k, a_k \rangle \| x_k - z_k^* \| + \langle a_k, x_k \rangle
< \langle a_k, x_k \rangle
$$
であるので,$$\langle a_k, z \rangle< \langle a_k, x_k \rangle$$であり,$$a_k$$を収束部分列に限ることによって$$\langle a_{\ell_k}, z \rangle< \langle a_{\ell_k}, x_k \rangle$$.

ここで任意の$$c \in H$$に対して,$$f:H \to \mathbb{R}; x \mapsto \langle c, x \rangle$$は連続写像であり,$$x_k \to x_0$$,$$a_{\ell_k} \to a$$であるので,$$\langle a, z \rangle \le \langle a, x_0 \rangle\quad \forall z \in C$$

---

$$f$$の連続性は$$| \langle c , x \rangle - \langle c , y \rangle|= | \langle c , x - y \rangle \| \le \|c \| \| x- y \|$$より示せる.



### イェンセンの不等式(期待値)

> $$X$$を確率変数として,$$h(x)$$を$$X$$の値域を含む区間上で凸な関数とする.$$X$$と$$h(x)$$の期待値が有限のとき,$$E[h(X)] \ge h (E[X])$$が成立する.もし,$$h(x)$$が狭義の凸関数のとき,等号が成立するのは1点分布の時に限る.

$$X$$の値域を$$\text{Im}(X)$$で表すと,仮定より区間$$I \supset \text{Im}(X)$$が存在し,$$h$$は$$I$$上で凸関数である.よって区間$$I$$に制限した$$h$$のエピグラフ
$$
\text{epi}\; \left.h\right|_{I} 
\equiv \{ (x, t) \in \mathbb{R}^2 \mid x \in I, h(x) \le t \}
$$
を考えると,$$\text{epi}\; \left.h\right|_{I}$$は凸関数である.(定義通りやれば示せる)

また,任意の$$x_0 \in I$$に対して$$(x, h(x))$$は$$\text{epi}\; \left.h\right|_{I} $$の境界(boundary)となっている.

---

実際,任意の$$\epsilon > 0$$に対して$$(x, h(x) - \frac{\epsilon}{2}) \subset B_{\epsilon}(x)$$かつ$$(x, h(x) - \frac{\epsilon}{2}) \notin \text{epi}\; \left.h\right|_{I}$$となるので,$$(x, h(x))$$は$$\text{epi}\; \left.h\right|_{I}$$の内部でないので境界

---

よって,[分離超平面定理より](#分離超平面定理(supporting_hyperplane)),$$a = (a_1, a_2)^T \ne (0,0) \in \mathbb{R}^2$$が存在し,任意の$$(x, t)$$ with $$ x \in I, t \ge h(x_0)$$に対して,
$$
\begin{align*}
	\langle a, (x, t) \rangle \le \langle a, (x_0, h(x_0)) \rangle
	\Leftrightarrow
	a_1 x + a_2 t \le \langle a, (x_0, h(x_0)) \rangle
\end{align*}
$$
が成立する.ここで右辺は定数であるので,もし$$a_2 > 0$$であるなら$$t$$を十分大きくすることで不等式が成立しなくなるので$$a_2 \le 0$$である.また,$$X$$が1点分布でないとすると不等式より$$a_2 \ne 0$$となる(1点分布の際は問題文の等号が成立),ゆえに$$a_2 < 0$$であり上式の$$t$$に$$h(x)$$を代入することで,
$$
h(x) 
\ge - \frac{a_1}{a_2}x + \frac{1}{a_2} \langle a, (x_0, h(x_0)) \rangle
= cx + d \equiv g(x)
$$
と表せる.ただし,$$c \equiv  - \frac{a_1}{a_2}$$,$$d \equiv \frac{1}{a_2} \langle a, (x_0, h(x_0)) \rangle$$である.ゆえに,$$g(x_0) = h(x_0)$$であることに注意すると,
$$
\begin{align*}
	E[h(x)] \ge E[g(x)] =E[c X + d] = cE[X] + d = cx_0 + d 
	= g(x_0) = h(x_0) = h(E[x_0])
\end{align*}
$$


また,$$h$$が狭義凸関数であるときを考える.$$X$$が2点分布の場合は定義通りに問題文の左辺と右辺を計算することで不等式(等号無し)が成立することが分かる.$$X$$が3点以上の分布の場合.上記の議論より等号成立の場合$$E[h(x)] = E[g(x)]$$の時に限るが,$$h(x) \ge g(x)$$であるので任意の$$x \in \text{Im}(X)$$に対して$$h(x) = g(x)$$が成立しなけらばならない.ここで,$$X$$は3点以上であるので$$x_1 < x_2 < x_3 \in \text{Im}(X)$$が存在する.よって,$$\lambda \in (0,1)$$が存在し$$x_2 = \lambda x_1 + (1-\lambda)x_3$$が満たされるが,$$h$$の凸性より
$$
\begin{align*}
	h(x_2) 
	&< \lambda h(x_1) + (1 - \lambda)h(x_3)\\
	&=\lambda (cx_1 +d) + (1-\lambda)(cx_3 + d)\\
	&= g(x_2)
\end{align*}
$$
より矛盾.ゆえに問題文の等号成立は1点分布の場合に限る.[参考資料](http://mcm-www.jwu.ac.jp/~konno/pdf/statg-1-8r.pdf)

## Backup

### 閉集合と点の距離

> Let $$(V, \| \cdot \|)$$ be a finite-dimensional normed space over a field $$\mathbb{R}$$, $$C$$ be a nonempty closed convex set, and $$a \in V$$. Then, $$ d(a, C) = \inf \{ \| x - a \| \mid x \in C\}$$ is reached at a **unique** point $$c \in C$$. $$c$$ is said projection of $$a$$ on the set $$C$$.i.e. 
>
> There exists unique $$c \in C$$ such that $$ \| x - c \| \le \|x - a\| (\forall x \in V)$$

$$C$$は空集合でないので,元$$c \in C$$が取れるので1つ固定する.$$S \equiv \{ x \in C \mid \|a - x \| \le \| a - c \| \}$$を定義すると,$$S$$の任意の元$$x$$に対して,$$\| x\|\le \| x - a \| + \|a\| \le \|a-c \| + \| a \|$$となるので$$S$$は有界である.また,$$f:V \to\mathbb{R}; x \mapsto \| a - x \|$$と定義すると$$f$$は連続関数であり$$D \equiv f^{-1}([0, a-c])$$と定義すると$$S = D \cap C$$となる.$$[0, a- c]$$は閉集合で$$f$$が連続写像であるので$$D$$も閉集合である.よって,$$S$$は閉集合である.また,$$S$$は有界であったので,$$S$$は有界閉集合である.よって,体$$K$$の[条件より](#完備全有界な体におけるコンパクトと有界閉集合の同値性)$$S$$はコンパクト.また定義域を$$S$$に制限した写像$$f$$を考えると,$$f$$は全射になるので$$f(S)$$はコンパクトであるので有界閉集合.$$S$$の定義より,$$d(a, C) = \inf f(S)$$であるので$$d(a, C) = \inf f(S) = \min f(S)$$.よって,$$c \in C$$で$$d(a, C) = \| a - c \|$$となるものが存在する.次に固有性を示す. $$c_1,c_2 \in C$$が$$d(a, C) = \| a - c_1 \| = \| a - c_2 \|$$を満たすとする.この時$$C$$がconvexであるので$$c = \frac{c_1 + c_2}{2} \in C$$である.よって,$$d(a, C) $$の定義より$$\|a-c_1\| \le \| a- c \|$$であるが,

