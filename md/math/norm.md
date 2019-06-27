

[TOC]

# ノルム空間

## 定義及び定理

### ノルム空間の基本的な性質

> Let $$(V, \| \cdot \|)$$ be a normed space. Then below properties are satisfied.
>
> 1. $$A \equiv \{ x \in V \mid \| x \| = r\}$$ is closed set, where $$r >0$$.
>
> Remark
>
> * Any field can be applied.

(1の証明)$$a \notin A$$を任意にとると定義より,$$\|a \| < 1$$もしくは$$\|a \| > 1$$である.$$\|a \| > 1$$の場合は$$\epsilon = | 1 - \|a\| |>0$$,とすると$$B(a, \epsilon) \subset A$$となる.



### ノルム空間には孤立点は存在しない

> Let $$(V, \| \cdot \|)$$ be a normed vector space over a field $$K (\mathbb{R} \text{ or } \mathbb{C})$$ such that $$V \ne\{0 \}$$.
>
> Then any point of $$V$$ is not an isolated point of $$V$$.

$$x \in V$$が孤立点だと仮定して矛盾を導く.[孤立点の定義より](./topology.md#Def(孤立点:isolated_point)),開集合$$U$$が存在して$$U = \{x \}$$となる.ゆえに$$r>0$$が存在して,
$$
B_r(x) \equiv \{ y \mid \| x - y \| < r \} \subset U = \{ x \}
$$
となる.ここで$$a \ne 0$$を任意に固定する.この時$$0 < | \lambda | < \frac{r}{\|a\|}$$を満たす$$\lambda \in K$$を任意にとると$$x + \lambda a \ne x$$であり,$$\| x + \lambda a - x \| = | \lambda | \| a \| < r$$より$$x + \lambda a \in B_r(x)$$であるが,$$x + \lambda a \notin \{x\}$$であるので矛盾.



### 同値なノルムは同じ位相を定める

### 同値なノルムは同じ位相を定める

> ベクトル空間$$V$$上にノルム$$\| \cdot \|_1, \| \cdot \|_2$$が定まっており,それらは同値であるとする.すなわち,$$0 < c_1, c_2 < \infty$$が存在し,$$c_1 \| x \|_2 \le \| x \|_1 \le c_2 \| x \|_2$$が成立する.この時2つのノルムは同じ位相(開集合系)を定める.

(Proof)

ノルム$$\| \cdot \|_i$$によって定まる位相を$$\tau_i$$,中心$$a$$半径$$r$$の開球を$$B_i(a,r)$$と表記することにする.

$$A_1 \in \tau_1, a \in A_1$$とする.開集合の定義より$$\epsilon > 0$$が存在し,$$B_1(a_1, \epsilon) \subset A_1$$となる.$$B_2(a, \frac{\epsilon}{c_2}) \subset B_1(a_1, \epsilon) \subset A_1$$であるので,$$A_1 \in \tau_2$$.同様の議論を行うことで$$A_2 \in \tau_2 \Rightarrow A_2 \in \tau_1$$を示せるので証明終了.



### 同値なノルムは完備性を引き継ぐ

> Let $$V$$ be a vector space and $$\| \cdot \|$$,$$\| \cdot \|'$$ are equivalent norms on $$V$$. 
>
> If $$(V, \| \cdot \|)$$ is complete, $$(V, \| \cdot \|')$$ is also complete.

証明は簡単なので略



### 連続同相写像による完備な空間の引き戻しは完備

> Let $$(X, d_X)$$ and $$(Y, d_Y)$$ be metric spaces, let $$f: X \to Y$$ be a homeomorphism which is uniformly continuous, and suppose that $$Y$$ is complete. Then $$X$$ is complete.
>
> Corollary
>
> Let $$(X, d_X)$$ and $$(Y, d_Y)$$ be metric spaces, let $$f: X \to Y$$ be a homeomorphism such that both $$f$$ and $$f^{-1}$$ are uniformly continuous. Then $$X$$ is complete if and only if $$Y$$ is complete.

(Proof)

$$X$$上のCauchy列$$\{ x_k\}$$を任意にとる.$$f$$の全単射性から$$f(x_k) = y_k$$を満たす$$y_k$$が一意に定まる.この時$$\{y_k\}$$はCauchy列である(以下証明)

任意に$$\epsilon> 0$$を固定する.$$f$$はuniformly continuousであるので$$\delta >0$$が存在して
$$
d_X (x, x') < \delta \Rightarrow d_Y (f(x), f(x')) < \epsilon
$$
が成立する.また,$$\{x_k\}$$はCauchy列であるので自然数$$N$$が存在して,
$$
n, m > N \Rightarrow d_X (x_n, x_m) < \delta
$$
が成立する.ゆえに
$$
n, m > N 
\Rightarrow d_X (x_n, x_m) < \delta
\Rightarrow d_Y (f(x_n), f(x_m)) < \epsilon
$$
となるので$$\{y_k\}$$はCauchy列.

$$Y$$は完備であるので$$\{y_k\}$$は収束する.その収束先を$$y_0$$とする.また,$$f(x_0) = y_0$$となる$$x_0$$は$$\{x_k\}$$の収束先となっている(以下証明)

$$\epsilon >0$$を固定する.$$f^{-1}$$は$$y_0$$で連続であるので$$\delta >0$$が存在して,
$$
d_Y (y_0, y) < \delta \Rightarrow d_X (x_0, f^{-1}(y)) < \epsilon
$$
となる.また,$$\{ y_k\}$$は$$y_0$$に収束するので自然数$$N$$が存在して,
$$
n > N \Rightarrow d_Y(y_0, y_n) < \delta
$$
ゆえに,
$$
n > N \Rightarrow d_Y(y_0, y_n) < \delta 
\Rightarrow
d_X (x_0, x_n ) < \epsilon
$$
よって,$$\{x_k\}$$は$$x_0$$に収束するので$$X$$は完備である.





### 完備な体上の有限次元ベクトル空間は最大値ノルムに関して完備である

> Let $$V$$ be a finite-dimensional vector space over a valued field $$(K, | \cdot |)$$. For a basis $$\{e_1, \dots ,e_n\}$$ of $$V$$ over $$K$$, set $$ \left\| \sum_{i=1}^n c_i e_i \right\|_{\infty} = \max_{1 \le i \le n} | c_i |$$ where $$c_i \in K$$. This is a norm on $$V$$, and if $$K$$ is complete with respect to $$| \cdot |$$ then $$V$$ is complete with respect to $$\| \cdot \|_{\infty}$$.

(Proof)

$$\| \cdot \|_{\infty}$$が$$V$$上のノルムになることを簡単に示せるので証明は省略する.

$$(V, \| \cdot \|_{\infty})$$上のCauchy列$$\{x^k \}$$を任意にとる.ただし,$$x^k = \sum_{i=1}^n c^k_i e_i$$とする.

この時,任意の$$j \in \{1, \dots ,n\}$$に対して$$(K, | \cdot |)$$上の点列$$\{ c^k_{j} \}_{k \in \mathbb{N}_{>0}}$$はCauchy列である.実際$$\epsilon > 0$$を任意にとると$$\{ x^k \}$$はCauchy列であるので,$$ N \in \mathbb{N}$$が存在して,
$$
k, \ell >N 
\Rightarrow |  c^k_{j} - c^{\ell}_{j} |
\le \max_{i=1,\dots ,n}
	|  c^k_{i} - c^{\ell}_{i} |
=  \| x^k - x^{\ell} \|_{\infty}
< \epsilon
$$
となるので$$\{ c^k_{j} \}_{k \in \mathbb{N}_{>0}}$$はCauchy列である.また,$$(K, | \cdot |)$$はcompleteであるので$$\{ c^k_{j} \}_{k \in \mathbb{N}_{>0}}$$は収束する.その収束先を$$c_j$$とする.この時$$\{ x^k \}$$は$$ c = \sum_{i=1}^n c_i e_i$$に収束する.実際,$$\epsilon >0$$を任意に固定すると,$$\{ c^k_{j} \}$$の収束性から$$N >0$$が存在し,任意の$$j \in \{1, \dots ,n\}$$に対して,
$$
k > N \Rightarrow |  c^k_{j} - c_j | < \epsilon
$$
が成立する.よって,$$k > N$$の時,
$$
\| x^k -  c \|_{\infty}
= \max_{i=1,\dots , n}|  c^k_{i} - c_i | < \epsilon
$$
であるので,$$\{ x^k \}$$は収束する.ゆえに$$(V, \| \cdot \|_{\infty})$$は完備である.



### 完備な体上の有限次元ベクトル空間のノルムは同値

> Any two norms on a finite-dimensional vector apce over a complete valued field are equivalent.

(Proof)

下記の証明に出てくるvalued fieldは[absolute valueが定義されている体](./group.md#Def(valued_field))のこと

[p4 Theorem3.2](https://kconrad.math.uconn.edu/blurbs/gradnumthy/equivnorms.pdf)

[保存用 p4 Theorem3.2](https://www.slideshare.net/secret/2RbAEzup5N9dif)



### 完備な体上の有限次元ベクトル空間は完備

> Let $$(K,  |\cdot|)$$ be a complete valued field and $$(E, \| \cdot \|)$$ be a finite-dimensional vector space over $$K$$. Then $$(E, \| \cdot \|)$$ is complete.



> Let $$K$$ be a complete field equipped with a absolute value $$| \cdot |:K \to [0, \infty)$$.
>
> Let $$E$$ be a $$n$$-dimensional vector space over a field $$K$$.



$$E$$の基底$$e_1, \dots ,e_n$$を1つ固定する.また,$$E$$上の関数$$\| \cdot\|_{\infty} : E \to \mathbb{R}$$を
$$
\left\| \sum_{i=1}^n \lambda_i e_i \right\|_{\infty} 
 = \max_{i=1, \dots ,n} |\lambda_i |
$$
と定義すると$$\| \cdot \|_{\infty}$$は$$E$$上のノルムになる(証明略)

同様に,$$K$$上ベクトル空間$$K^n$$上の$$\| \cdot \|_{\infty} : K^n \to [0, \infty): \boldsymbol{x} \mapsto \max_{i \in \{1, \dots ,n\}} | \boldsymbol{x}_i | $$という関数はノルムになる(証明略)

ここで,写像$$L : (K^n, \| \cdot \|_{\infty}) \to (E,  \| \cdot \|_{\infty})$$を
$$
L((\lambda_1, \dots , \lambda_n)^T) = \sum_{i=1}^n \lambda_i e_i
$$
と定義すると$$L$$はlinear isometric bijectionとなる(証明略).また[全射な等長写像の開集合の像と引き戻しは開集合](./metric#全射な等長写像の開集合の像と引き戻しは開集合)であるので,$$L$$はhomeomorphismである.また,$$L$$はisometric bijectionであるので,$$L^{-1}$$もisometricであることは容易に示せる.さらに,isometricな関数はuniformly continuousであることも容易に示せるので$$L^{-1}$$はuniformly continuous homeomorphismである.また,$$(K^n, \| \cdot \|_{\infty})$$は完備であるので(証明は最後),[連続同相写像による完備な空間の引き戻しは完備](#連続同相写像による完備な空間の引き戻しは完備)より$$(E,  \| \cdot \|_{\infty})$$は完備(complete)である.また,[完備な体上の有限次元ベクトル空間のノルムは同値](#完備な体上の有限次元ベクトル空間のノルムは同値)であり,[同値なノルムは完備性を引き継ぐ](#同値なノルムは完備性を引き継ぐ)ことから$$(E, \| \cdot \|)$$も完備である.



また,$$(K^n, \| \cdot \|_{\infty})$$のCauchy列は収束列である.つまり完備(以下証明)

$$(K^n, \| \cdot \|_{\infty})$$上のCauchy列$$\{ \boldsymbol{x}^k \}$$を任意にとる.この時,任意の$$j \in \{1, \dots ,n\}$$に対して$$(K, | \cdot |)$$上の点列$$\{ \boldsymbol{x}^k_{j} \}_{k \in \mathbb{N}_{>0}}$$はCauchy列である.実際$$\epsilon > 0$$を任意にとると$$\{ \boldsymbol{x}^k \}$$はCauchy列であるので,$$ N \in \mathbb{N}$$が存在して,
$$
k, \ell >N 
\Rightarrow |  \boldsymbol{x}^k_{j} - \boldsymbol{x}^{\ell}_{j} |
\le \max_{i=1,\dots ,n}
	|  \boldsymbol{x}^k_{i} - \boldsymbol{x}^{\ell}_{i} |
=  \| \boldsymbol{x}^k - \boldsymbol{x}^{\ell} \|_{\infty}
< \epsilon
$$
となるので$$\{ \boldsymbol{x}^k_{j} \}_{k \in \mathbb{N}_{>0}}$$はCauchy列である.また,$$(K, | \cdot |)$$はcompleteであるので$$\{ \boldsymbol{x}^k_{j} \}$$は収束する.その収束先を$$a_j$$とする.この時$$\{ \boldsymbol{x}^k \}$$は$\boldsymbol{a} = (a_1, \dots ,a_n)^T$に収束する.実際,$$\epsilon >0$$を任意に固定すると,$$\{ \boldsymbol{x}^k_{j} \}$$の収束性から$$N >0$$が存在し,任意の$$j \in \{1, \dots ,n\}$$に対して,
$$
k > N \Rightarrow |  \boldsymbol{x}^k_{j} - a_j | < \epsilon
$$
が成立する.よって,$$k > N$$の時,
$$
\| \boldsymbol{x}^k -  \boldsymbol{a} \|_{\infty}
= \max_{i=1,\dots , n}|  \boldsymbol{x}^k_{i} - a_i | < \epsilon
$$
であるので,$$\{ \boldsymbol{x}^k \}$$は収束する.ゆえに$$(K^n, \| \cdot \|_{\infty})$$は完備である.



### 完備な体上のベクトル空間の有限次元の部分空間は閉集合

> Let $$V$$ be a normed vector space over a complete valued field. 
>
> Then any linear subspace is a closed set.

(Proof)

距離空間においては集合内の収束列が集合内に収束することと閉集合であることは同値なのでこれを示す.有限次元の部分空間は1次独立な有限個のベクトルの線形結合で表されるので,$$U \equiv \langle e_1, \dots e_n \rangle$$と表すことにする.収束列$$\{x_k\} \subset U$$を任意にとる.(収束先を$$x \in V$$とする)距離空間ではCauchy列は収束列であるから$$\{ x_k\}$$は$$U$$上のCauchy列となる.また,$$U$$は有限次元ベクトル空間であるので,[完備な体上の有限次元ベクトル空間は完備](#完備な体上の有限次元ベクトル空間は完備)より$$\{x_k\}$$は$$U$$に制限した$$V$$上のノルムにおいて,点$$y \in U$$に収束する.収束先の一意性より$$x = y \in U$$となるので$$U$$は閉集合である.

### Tube_Lemma

> Let $$X_1, \dots , X_n$$ be topological spaces and $$\prod_{i=1}^n X_i $$ is product spaces. Let $$A_1, \dots , A_n$$ be compact subset of $$X_1, \dots ,X_n$$, respectively. If $$N$$ is an open set containing $$\prod_{i=1}^n A_i$$, then there exists open sets $$U_1, \dots ,U_n$$ such that $$\prod_{i=1}^n A_i \subset  \prod_{i=1}^n U_i \subset N$$.

$$k=1,\dots ,n$$に対して以下の操作を行う.

[$$k=0$$の時]

直積集合の定義より,任意の$$a_1, \dots ,a_n \;(a_i \in A_i)$$に対して開集合$$U_i^0(a_1, \dots , a_n) \subset X_i$$が存在して,$$a_i \in U_i^0(a_1, \dots , a_n)$$,$$ \prod_{i=1}^n U_i^0(a_1, \dots , a_n) \subset N$$が成立する.



また,$$k \in \{0, \dots , n\}$$の操作が終了した時点で以下が成立することに留意する.

- (条件1)任意の$$a_1, \dots ,a_{n-k}$$に対して
  $$
  \begin{align*}
  	1 \le i \le n-k 
  	&\Rightarrow
  		a_i \in U_i^k(a_1, \dots , a_{n-k})\\
  	n - (k-1) \le i \le n
    & \Rightarrow
    	A_i \subset U_i^k(a_1, \dots , a_{n-k})
  \end{align*}
  $$

- (条件2) 任意の$$i \in \{1, \dots ,n\}$$と任意の$$a_1, \dots ,a_{n-k}$$に対して
  $$
  U_i^k(a_1, \dots , a_{n-k})
  $$
  は開集合

- (条件3)任意の$$a_1, \dots ,a_{n-k}$$に対して
  $$
  \prod_{i=1}^n U_i^k(a_1, \dots , a_{n-k}) \subset N
  $$

[$$k \ge 1$$の時($$k-1$$についての操作は終了している)]

任意に$$a_1, \dots , a_{n-k}$$を固定する.この時$$k-1$$の際の(条件1)より
$$
\{ U^{k-1}_{n - (k-1)} (a_1, \dots , a_{n-(k-1)}) \mid a_{n-(k-1) \in A_{n - (k-1)}} \}
$$
は$$A_{n-(k-1)}$$の開被覆となる.$$A_{n-(k-1)}$$のコンパクト性より,有限集合$$S_{n - (k-1)} \subset A_{n - (k-1)}$$が存在し,
$$
U^{k}_{n - (k-1)} (a_1, \dots , a_{n-k})
\equiv 
\bigcup_{a_{n-(k-1)} \in S_{n - (k-1)}} 
	U^{k-1}_{n - (k-1)} (a_1, \dots , a_{n-(k-1)})
\supset A_{n - (k-1)}
$$
となる.ここで$$i \ne n - (k-1)$$に対して,
$$
U^{k}_i (a_1, \dots , a_{n-k})
\equiv
\bigcap_{a_{n-(k-1)} \in S_{n - (k-1)}} 
	U^{k-1}_i (a_1, \dots , a_{n-(k-1)})
$$
と定義すると$$k-1$$の際の(条件1)を用いると,任意の$$a_1, \dots ,a_{n-k}$$に対して
$$
\begin{align*}
	1 \le i \le n-k 
	&\Rightarrow
		a_i \in U_i^k(a_1, \dots , a_{n-k})\\
	n - (k-1) \le i \le n
  & \Rightarrow
  	A_i \subset U_i^k(a_1, \dots , a_{n-k})
\end{align*}
$$
が成立するので$$k$$の際も(条件1)が成立.また,$$S_{n - (k-1)}$$が有限集合であることと,$$k-1$$の際の(条件2)を用いると$$k$$の時にも(条件2)が成立することが分かる.

また,任意に$$b \in \prod_{i=1}^n U_i^k(a_1, \dots , a_{n-k})$$をとると,$$b_{n-(k-1)} \in U^{k}_{n - (k-1)} (a_1, \dots , a_{n-k})$$であるので,$$a_{n-(k-1)} \in S_{n - (k-1)}$$が存在して,$$b_{n-(k-1)} \in U^{k-1}_{n - (k-1)} (a_1, \dots , a_{n-(k-1)})$$が成立する.よって,

$$U_i^k$$の定義より$$b \in \prod_{i=1}^n U^{k-1}_i (a_1, \dots , a_{n-(k-1)})$$である.よって,$$k-1$$の際の(条件3)より$$b \in N$$であるので$$k$$の時も(条件3)が成立する.



$$n$$まで操作が終了した時点で,
$$
\prod_{i=1}^n A_i \subset \prod_{i=1}^n U_i^n \subset N
$$
であり$$U_i^n$$が開集合であるので証明終了.



### 完備全有界なK^nにおけるコンパクトと有界閉集合の同値性

> Let $$(K, | \cdot |)$$ be a complete valued field which satisfies that every bounded subset is totally bounded. 
>
> Let $$(K^m, \| \cdot \|)$$ be normed space. Then, any subset $$A$$ of $$K^n$$ is compact if and only if it is $$A$$ is closed and bounde.

証明のためにいくつかの補題を証明する.

------

(補題1)任意の$$r >0$$に対して$$K$$上の閉球$$\bar{B}(0,r) \equiv \{x \in K \mid | x | \le r\}$$を考えると$$\bar{B}(0,r)$$は閉集合である.

------

閉集合でないとすると,$$\bar{B}(0,r)$$のlimit pointであって$$\bar{B}(0,r)$$に含まれないものが存在するので,それを$$a \in K$$とする.この時$$|a| > r$$であるので,$$\epsilon \equiv |a| - r > 0$$と定義できる.また,limit pointの定義より,任意の自然数$$n \in \mathbb{N}_{>0}$$に対して$$a_n \in B(a, \frac{1}{n}) \cap \bar{B}(0,r), a_n \neq a$$を満たす$$a_n$$が存在する.ここで,$$\frac{1}{n} < \epsilon$$を満たす$$N$$を1つ固定すると,
$$
| a | \le | a - a_N | + |a_N| < \frac{1}{N} + | a_N| 
< \epsilon + |a_N| = |a| - r + |a_N|
$$
より$$r < | a_N|$$となる.これは$$a_N \in \bar{B}(0,r)$$に矛盾.

------

(補題2)任意の$$r >0$$に対して$$K$$上の閉球$$\bar{B}(0,r) \equiv \{x \in K \mid | x | \le r\}$$を考えると$$\bar{B}(0,r)$$はコンパクトである.

------

$$\bar{B}(0,r)$$は定義よりboundedであり,問題文の仮定よりtotally boundedとなる.[よって](#全有界と任意の点列がコーシー部分列を持つことは同値),$$\{a_n\} \subset \bar{B}(0,r)$$とすると,$$\{a_n\}$$はCauchy部分列$$\{a_{n_k}\}$$を持つ.$$K$$は完備であるので$$\{a_{n_k}\}$$は$$K$$上に収束点を持つが,補題1より$$\bar{B}(0,r)$$は閉集合であるので収束点は$$\bar{B}(0,r)$$上にある.よって$$\bar{B}(0,r)$$点列コンパクトとなるので(この[定理](#距離空間におけるコンパクトの同値条件)より),コンパクトである.

------

(補題3)$$K^n$$上の$$\| \cdot \|_{\infty} : K^n \to [0, \infty): \boldsymbol{x} \mapsto \max_{i \in \{1, \dots ,n\}} |x_i |$$という関数はノルムになる(証明略)また,$$\| \cdot \|_{\infty}$$によって誘導される位相を$$\mathcal{O}$$,直積位相を$$\mathcal{O}'$$とすると$$\mathcal{O} = \mathcal{O}'$$である.

------

$$O \in \mathcal{O}'$$と$$ \boldsymbol{x} \in O$$を任意にとると,ノルムに誘導される位相の定義より$$\epsilon >0$$が存在して,
$$
B_{\infty}(\boldsymbol{x}, \epsilon) \equiv \{ 
	\boldsymbol{y} \in K^n \mid 
		\| \boldsymbol{x} - \boldsymbol{y} \|_{\infty}
	\} 
\subset O
$$
が成立する.また,
$$
B(x_i , \epsilon) \equiv
	\{y \in K \mid | x_i - y | < \epsilon
\}
$$
と定義すると,
$$
\boldsymbol{x} 
\in \prod_{i=1}^n B(x_i, \epsilon)
\subset B_{\infty}(\boldsymbol{x}, \epsilon)
\subset O
$$
となるので,$$\mathcal{O}' \subset \mathcal{O}$$が成立.逆も容易に示せる(証明略)

------

距離空間上のコンパクト集合は有界閉集合であるので,有界閉集合ならばコンパクトであることのみを示す.$$(K^n, \| \cdot \|_{\infty})$$において有界閉集合$$A \subset K^n$$を任意にとる.$$\| \cdot \|_{\infty}$$の定義より$$M > 0$$が存在して任意の$$a = (a_1, \dots , a_m)$$に対して$$|a_i| \le M$$が成立することに注意する.

また,任意の$$j \in \{1, \dots , m\}$$に対して射影$$\pi_j:K^n \to K$$を$$\pi_j(a_1,\dots,a_n) = a_j$$を定義すると$$\pi_j(A)$$は閉集合である.

------

$$A$$は$$\| \cdot \|_{\infty}$$から誘導される位相において閉集合であるので,(補題3)より直積位相でも閉集合である.$$\pi_j(A)$$は閉集合であることの証明中では$$K^n$$には直積位相が入っていると考える.

$$a_j \notin \pi_j(A)$$とすると,
$$
\bar{B}(0, M) \times \cdots \times \{a_j\} \times \cdots \times\bar{B}(0, M) \cap A = \emptyset
$$
である.実際,空集合でないとすると$$A$$の元で$$j$$番目の要素が$$a_j$$であるものが存在するので,$$a_j \in \pi_j(A)$$となり矛盾する.上式より,
$$
\bar{B}(0, M) \times \cdots \times \{a_j\} \times \cdots \times\bar{B}(0, M)
\subset A^c
$$
が成立する.ここで,(補題2)より$$\bar{B}(0, M)$$はコンパクトであるので,[Tube_Lemma](#Tube_Lemma)より$$K$$上の開集合$$U_1, \dots ,U_m$$が存在して,
$$
\bar{B}(0, M) \times \cdots \times \{a_j\} \times \cdots \times\bar{B}(0, M)
\subset \prod_{i=1}^m U_i
\subset A^c
$$
が成立する.($$a_j \in U_j$$となっていることに注意)

この時,$$\pi_j (A) \cap U_j = \emptyset$$である.

実際,空集合でないとすると,$$A \subset \prod_{i=1}^m \bar{B}(0, M)$$であるので
$$
\prod_{i=1}^{j-1} \bar{B}(0, M) 
\times U_j 
\times \prod_{i=j+1}^{m} \bar{B}(0, M)
$$
に含まれる$$a \in A$$の元が存在することになるが,
$$
\prod_{i=1}^{j-1} \bar{B}(0, M) 
\times U_j 
\times \prod_{i=j+1}^{m} \bar{B}(0, M)
\subset \prod_{i=1}^m U_i
\subset A^c
$$
であるので矛盾.

ゆえに,$$a_j \in U_j \subset K \setminus \pi_j (A) $$となるので,$$K \setminus \pi_j (A)$$は開集合となり,$$\pi_j (A)$$は閉集合

------

ここで,$$A$$上の点列 $$\{a^n\}_n$$を任意にとる.$$a^n = (a^n_1, \dots , a^n_m)$$と表記することにする.また,収束する$$\{a^n\}$$の部分列の存在を示すために,$$1$$番目の要素から$$m$$番目の要素まで順に部分列をとって,収束させることにする.具体的には初期値を$$\{ a^{k_{n,0}}\}_n \equiv \{ a^n \}_n$$として$$j=1, \dots ,m$$まで次の操作を繰り返す.以後,$$a^{k_{n,j}} = (a^{k_{n,j}}_1, \dots ,a_m^{k_{n,j}})$$と表記することにする.

点列$$\{a_j^{k_{n,j-1}} \}_n \subset \pi_j(A) \subset \bar{B}(0, M) $$を考える.$$\pi_j(A)$$は有界であるので問題文の仮定より全有界.[よって](#全有界と任意の点列がコーシー部分列を持つことは同値),$$\{a_j^{k_{n,j-1}} \}_n$$はCauchy部分列を持つ.また,$$K$$は完備なので$$\{a_j^{k_{n,j-1}} \}_n$$の部分列$$\{a_j^{k_{n,j}} \}_n$$は$$a_j \in  \pi_j(A)$$に収束する.ここで,$$\{a^{k_{n,j-1}} \}_n$$の部分列$$\{a^{k_{n,j}} \}_n$$において,$$1 \le i \le j$$ならば$$\{a_i^{k_{n,j}} \}_n$$は$$a_i$$に収束することが分かる.

よって$$j=m$$の操作が終わった時に,$$\{a^{k_{n}} \}_n \equiv \{a^{k_{n,m}} \}_n$$,$$a = (a_1, \dots, a_m)$$と定義すると, $$\{a^n\}_n$$の部分列$$\{a^{k_{n}} \}_n$$は$$a$$に収束することが分かる.$$A$$は閉集合であるので$$a \in A$$となる.[ゆえに](#距離空間におけるコンパクトの同値条件)$$A$$は点列コンパクトであるのでコンパクト.また,この証明では$$K^n$$に$$\| \cdot \|_{\infty}$$ノルムが入っている考えて証明したが,[完備な体上の有限次元ベクトル空間のノルムは同値](#完備な体上の有限次元ベクトル空間のノルムは同値)であり,[同値なノルムは同じ位相を定める](#同値なノルムは同じ位相を定める)ので任意のノルム$$\| \cdot \|$$に関してもコンパクトである.



### 完備全有界な体におけるコンパクトと有界閉集合の同値性

> Let $$(K, | \cdot |)$$ be a complete valued field which satisfies that every bounded subset is totally bounded. 
>
> Then any subet $$A$$ of  finited-dimensional normed space $$(V, \| \cdot \|)$$ over $$K$$  is compact if and only if $$A$$ is closed and bounded.
>
> Remark
>
> - $$\mathbb{R}$$ and $$ \mathbb{C}$$  are examples satisfying that every bounded subset is totally bounded.
> - It is not true for **infinite**-dimensional normed space because of [normed space is finite if and only if the closed unit ball is compact](http://mathonline.wikidot.com/a-normed-linear-space-is-finite-dimensional-if-and-only-if-t), the proof handes the field $$\mathbb{C}$$.

$$A$$がコンパクトなら有界閉集合であることは別定理から示す事ができる(距離空間上のコンパクト集合は有界閉集合)ので逆のみを示す.

$$n$$を$$V$$の次元とすると同型写像(isomorphism)$$T:K^n \to V$$が存在する(証明略).また,$$K^n$$上の関数を$$\|x \|_V \equiv \| T(x)\|$$と定義すると$$K^n$$上のノルムとなる(証明略).

また,$$T:(K^n, \| \cdot \|_V) \to (V, \| \cdot \|)$$は等長写像isometoryとなる.また[全射な等長写像の開集合の像と引き戻しは開集合](./metric#全射な等長写像の開集合の像と引き戻しは開集合)であるので$$T$$は位相同型homeomorphism.

ここで,$$A \subset V$$がclosedかつboundedとする.$$T$$は位相同型であるので,$$T^{-1}(A)$$も($$\| \cdot \|_V$$のノルムに誘導される位相で)closedである.また$$T$$が等長写像であるので$$T^{-1}(A)$$もboundedである.[K^n上では有界閉集合とコンパクトは同値であったので(証明が一番大変)](#完備全有界なK^nにおけるコンパクトと有界閉集合の同値性),$$T^{-1}(A)$$はコンパクトである.また,全射かつ連続関数のcompact集合の像はcompactであるので$$A = T (T^{-1}(A))$$はcompact.



## Backup

### R上のノルムが定まっている有限次元ベクトル空間はR^nと位相同型

> Let $$E$$ be a $$n$$-dimensional norm space over $$\mathbb{R}$$ whose norm is represented by $$N$$.
>
> Then $$E$$ and $$(\mathbb{R}^n, \| \cdot \|)$$ be homeomorphic, where $$\| \cdot \|$$ is Eucliean norm.

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
次に$$L:(E, N) \to (\mathbb{R}^n, N')$$が同相写像(homeomorphism)であることを示す.

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

また,[有限次元ノルム空間の任意のノルムは同値(p26 A.5)](http://www.ma.noda.tus.ac.jp/u/sh/pdfdvi/13fa-s.pdf)であるので恒等写像$$\text{id}:(\mathbb{R}^n, N') \to (\mathbb{R}^n, \| \cdot \|)$$はhomeomorphism.よって,homeomorphicの推移律(transitive relation)より$$(E, N)$$と$$(\mathbb{R}^n, \| \cdot \|)$$はhomeomorphic.



### コンパクトと有界閉集合の同値性(実数体)

> Let $$(V, \| \cdot \|_V)$$ be a finite dimensional normed vector space over a field $$\mathbb{R}$$. Then a subset $$A \subset V$$ is compact if and only if $$A$$ is closed and bounded. 

(Proof)

$$A$$がコンパクトなら有界閉集合であることは別定理から示す事ができる(距離空間上のコンパクト集合は有界閉集合)ので逆のみを示す.

$$n$$を$$V$$の次元とすると同型写像(isomorphism)$$T:\mathbb{R}^n \to V$$が存在する(証明略).また,$$\mathbb{R}^n$$上のノルムを$$\|x \| \equiv \| T(x)\|_V$$と定義するとこれは$$\mathbb{R}^n$$上のノルムとなる.

また,$$T:(\mathbb{R}^n, \| \cdot \|) \to (V, \| \cdot \|_V)$$は等長写像isometoryとなる.また[全射な等長写像の開集合の像と引き戻しは開集合](#全射な等長写像の開集合の像と引き戻しは開集合)であるので$$T$$は位相同型homeomorphism.

ここで,$$A \subset V$$がclosedかつboundedとする.$$T$$は位相同型であるので,$$T^{-1}(A)$$も$$\| \cdot \|$$のノルムに誘導される位相でclosedである.また$$T$$が等長写像であるので$$T^{-1}(A)$$も$$\| \cdot \|$$に関してboundedである.また[有限次元ノルム空間の任意のノルムは同値(p26 A.5)](http://www.ma.noda.tus.ac.jp/u/sh/pdfdvi/13fa-s.pdf)であり,[同値なノルムは同じ位相を定める](#同値なノルムは同じ位相を定める)ので$$T^{-1}(A)$$は$$\mathbb{R}^n$$の標準ノルム$$\| \cdot \|_2$$上でもclosedかつbounded.ゆえに,$$T^{-1}(A)$$はcompact.また,全射かつ連続関数のcompact集合の像はcompactであるので$$A = T (T^{-1}(A))$$はcompact.



