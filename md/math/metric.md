[TOC]

# 距離空間

## 参考資料

* 距離空間上のコンパクト集合の同値条件の証明が詳しい(重要な定理及び証明はこのページに記載)[pdf](http://pioneer.netserv.chula.ac.th/~lwicharn/2301631/Compact1.pdf),[リンク切れ用](https://www.slideshare.net/secret/DAW5Aq88EQ0o2n)



## 定義及び定理

### Def(全有界)

> A subset $$A$$ of a metric space $$(X,d)$$ is said to be **totally bounded** or **precompact** if for any $$\epsilon > 0$$, there is a finite cover of $$A$$ by sets of diameter less thant $$\epsilon$$.
>
>
> A subset $$A$$ of a metric space $$(X,d)$$ is totally bounded if and only if for each $$\epsilon>0$$, $$A$$ can be covered by finitely many $$\epsilon$$-balls.(容易に示せるため証明略)



### Def(Balzano-Weierstrass-property)

> A subset $$A$$ of  topological space $$X$$ is said to satisfy the **Balzano-Weierstrass property** if every infinite subset of $$A$$ has a limit point in $$A$$.



### Def(点列コンパクト)

> A subset of $$A$$ in metric space $$(X,d)$$ is said to be **sequentially compact** if every sequence in $$A$$ has convergent subsequence in whose limit point is in $$A$$. 



### Def(ルベーグ数)

> Let $$\mathcal{C}$$ be a cover of a subset $$A$$ of a metric space $$X$$. A **Lebesgue number** for $$\mathcal{C}$$ is a positive number $$\lambda$$ such that any subset of $$A$$ of diameter less than or equal to $$\lambda$$ is contained in some member of $$\mathcal{C}$$.
>
> * From the definition, if $$\lambda$$ is a Lebesgue number, then so is any $$\lambda' > 0$$ such that $$\lambda' \le \lambda$$.



### 点列コンパクト集合の開被覆にはルベーグ数が存在する

> Let $$A$$ be a sequentially compace subset of a metric space $$(X,d)$$. Then every open cover of $$A$$ has a Lebesgue number.

(Proof)

$$\mathcal{C}$$を$$A \subset X$$の開被覆とする.$$\mathcal{C}$$がルベーグ数を持たないと仮定して矛盾を導く.仮定より任意の自然数$$n$$に対して
$$
\text{diam}\, (B_n) \le \frac{1}{n}, B_n \nsubseteq G \; (\forall G \in \mathcal{C})
$$
を満たす$$B_n \subset A$$が存在するので$$x_n \in B_n \subset A$$が取れる.$$A$$は点列コンパクトであるので$$\{x_n\}$$の収束部分列$$\{x_{n_k}\}$$と収束先$$x \in A$$が存在する.$$\mathcal{C}$$は$$A$$の開被覆であるので$$x \in G_0$$を満たす$$G_0 \in \mathcal{C}$$が存在する.$$G_0$$は開集合であるので,$$\epsilon >0$$が存在して$$B_d(x, \epsilon) \subset G_0$$が成立する.また,$$\{x_{n_k}\}$$の収束性より,自然数$$N$$が存在して,
$$
k > N \Rightarrow d(x_{n_k}, x) < \frac{\epsilon}{2}
$$
が成立する.ここで,$$\frac{1}{M} < \frac{\epsilon}{2}$$を満たす自然数$$M$$の1つ固定して,$$K \equiv \max \{ M+1,N+1\}$$と定義する.この時$$n_K \ge K \ge N+1$$が成立するので,
$$
d(x_{n_K}, x) < \frac{\epsilon}{2}, x_{n_K} \in B_{n_K}
$$
となる.さらに
$$
\text{diam}\;(B_{n_K}) \le \frac{1}{n_K} < \frac{\epsilon}{2}
$$
が成立する.よって任意の$$y \in B_{n_K}$$に対して,
$$
d(x,y) \le d(x, x_{n_K}) + d(x_{n_K}, y) 
< \frac{\epsilon}{2} + \frac{\epsilon}{2} = \epsilon
$$
が成立するので$$y \in B_d(x, \epsilon)$$.ゆえに $$B_{n_K} \subset B_d(x, \epsilon) \subset G_0$$となるが,これは$$B_{n_K}$$の定義に矛盾.



### 全有界と任意の点列がコーシー部分列を持つことは同値

> A subset $$A$$ of a metric space $$(X,d)$$ is totally bounded if and only if every sequence in $$A$$ has a Cauchy subsequence.

(Proof)

($$\Leftarrow$$)$$A$$上の任意の点列がCauchy subsequenceを持つと仮定する.この時,$$A$$がtotally boundedでないとすると矛盾が生じることを示す.$$A$$がtotally boundedでないのだから,ある$$\epsilon > 0$$が存在して$$A$$が有限個の半径$$\epsilon$$のballで被覆できない.つまり,任意の自然数$$n \in \mathbb{N}_{\ge 0}$$に対して,$$x_{n+1} \in A \setminus \bigcup_{i=1}^n B_d (x_i, \epsilon)$$を満たす点列$$\{x_n\}$$がとれる.($$A$$から任意に元をとって$$x_0$$とする)この時,$$m > n$$ならば$$x_m \notin B_d(x_n, \epsilon)$$であるので$$d(x_m, x_n) \ge \epsilon$$.よって$$\{x_n\}$$はCauchy subsequenceを持たないので矛盾

($$\Rightarrow$$)$$A$$がtotally boundedだと仮定する.$$\{x_n\} \subset A$$を任意にとる.$$A$$がtotally boundedであるのだから,任意の自然数$$k \in \mathbb{N}_{> 0}$$に対して,以下の手順によって点列$$\{x_{kn}\}_n$$を$$k=1$$から順に構成する.

初期値として$$\{x_{0n}\}_n \equiv \{x_n\}$$, $$B_0 = A$$とする.

$$B_{k-1}$$はtotally boundedであるので,直径が$$1 / k$$より小さい$$A_{k1}, A_{k2}, \dots , A_{kn_{k}}$$が存在して,$$B_{k-1} = \bigcup_{i=1}^{n_k} A_{ki}$$となる.$$A_{k1}, \dots , A_{kn_{k}}$$のうち少なくとも1つは$$\{x_{(k-1)n}\}_n$$の点列を無限個含んでいるので,それを$$B_k \subset B_{k-1}$$とする.また$$B_k$$に含まれる$$\{x_{(k-1)n}\}_n$$の部分列を$$\{x_{kn} \}_n$$とする.この時以下が成立しているので,$$\{x_{(k+1)n} \}_n$$を同様の操作によって構成することができる.

* $$B_k \subset B_{k-1}$$であり$$B_{k-1}$$がtotally boundedであるので$$B_k$$もtotally bounded
* $$\text{diam} \,B_k  < \frac{1}{k}$$
* $$\{x_{kn} \}_n \subset B_k$$は$$\{x_{(k-1)n}\}_n$$の部分列

この時,点列$$\{ x_{11}, x_{22}, \dots , x_{nn} \}$$は$$\{x_n\}$$の部分列であり(単調する添字が$$\{x_n\}$$上で単調増加になっていることに注意),任意の$$\epsilon>0$$に対して,$$\frac{1}{N} < \epsilon$$を満たす$$N$$をとると,$$m,n > N$$ならば,$$x_{mm} \in B_m \subset B_N$$,$$x_{nn} \in B_n \subset B_N$$であるので
$$
d(x_{mm}, x_{nn}) \le \text{diam}\,B_N < \frac{1}{N} < \epsilon
$$
よって,$$\{x_{nn}\}_n$$はCauchy subsequence of $$\{x_{n}\}$$.



### 距離空間におけるコンパクトの同値条件

> In a metric space $$(X,d)$$, the following statements are equivalent:
>
> 1. $$A \subset X$$ is compact;
> 2. $$A \subset X$$ has the Bolzano-Weierstrass property:
> 3. $$A \subset X$$ is sequentially compact;
> 4. $$A \subset X$$ is complete and totally bounded.

$$(3) \Rightarrow (4)$$complete性は自力で示せると思うので証明略.また,距離空間上では収束列はCauchy列であるので,[全有界と任意の点列がコーシー部分列を持つことは同値](#全有界と任意の点列がコーシー部分列を持つことは同値)よりtotally boundedであることも容易に示せる.

$$(4) \Rightarrow (3)$$は[全有界と任意の点列がコーシー部分列を持つことは同値](#全有界と任意の点列がコーシー部分列を持つことは同値)を使えば容易に示せる.

$$(1) \Rightarrow (2)$$ $$S \subset A$$をininite subsetとする.$$S$$が$$A$$上でlimit pointを持たないと仮定する.任意の$$x \in A$$に対して,$$V_x \cap S \setminus \{x\} = \emptyset$$を満たすような$$x$$のopen neighborhoodが存在する.この時$$C \equiv \{ V_x \mid x \in A \}$$はopen cover of $$A$$.$$A$$はcompactであるので finite subcover $$\{ V_{x_1}, \dots , V_{x_n} \}$$が存在する.また,$$V_{x_{i}}$$は最大でも$$S$$の元を1つしか持たないため,$$ \bigcup_{i=1}^n V_{x_i} ( \supset A \supset S)$$は有限個の$$S$$の元を含む.従って,$$S$$は有限集合となるので矛盾.

$$(2) \Rightarrow (3)$$$$\{x_n\} \subset A$$を任意にとり$$S \equiv \{ x_n \mid n \in \mathbb{N}_{>0} \}$$と定義すると,Case1, Case2のどちらかが成立するので場合分けして考える.

Case1($$S$$ がfinite)無限個の自然数$$n$$に対して$$a = x_n$$を満たす$$a \in A$$が存在する.自然数の任意の部分集合には最小元が存在するので,$$n_1 \equiv \min\{ n \in \mathbb{N} \mid x_n = a\}$$が存在する.同様に$$k \ge 2$$ に対しても,$$n_k \equiv \min(\{ n \in \mathbb{N} \mid x_n = 1 \} \setminus \{n_1,\dots ,n_{k-1} \})$$を定めることができる.この時,点列$$\{x_{n_k}\}$$はconstant subsequence of $$\{x_n\}$$であり$$a \in A$$に収束する.

Case2($$S$$がinfinite)$$A$$はBolzano-Weierstrass propertyであるので,$$S$$のlimit point $$x \in A$$が存在する.limit pointの定義より,任意の自然数$$n$$に対して,$$B_d(x, \frac{1}{n}) \cap (S \setminus \{x \}) \ne \emptyset$$である.(空集合でないというだけでなく,infinite setである)よって,任意の$$k \ge2$$に対して,
$$
n_1 \equiv \min \{ 
	n \in \mathbb{N}_{>0} \mid x_n \in B_d(x, 1) \cap (S \setminus \{x\})
	\}
$$

$$
n_k \equiv \min \left\{ 
	n \in \mathbb{N}_{>0} \mid x_n \in B_d\left(x, \frac{1}{k}\right) \cap (S \setminus \{x\})
	\right\}
$$

を定めることができる.この時,$$\{x_{n_k} \}$$は $$\{x_n\}$$のsubsequcenceであり,任意の自然$$k$$に対して$$d(x_{n_k}, x) < \frac{1}{k}$$であるので$$\{ x_{n_k} \}$$は$$x$$に収束する.

$$(3) \Rightarrow (1)$$$$\mathcal{C}$$を点列コンパクトである$$A$$の開被覆とする.[点列コンパクト集合の開被覆にはルベーグ数が存在する](#点列コンパクト集合の開被覆にはルベーグ数が存在する)ので$$\mathcal{C}$$のルベーグ数$$\lambda > 0$$が存在する.また$$(3) \Rightarrow (4)$$より$$A$$は全有界であるので,$$A \subset \bigcup_{i=1}^n A_i, \text{diam} \; (A_i) \le \lambda$$を満たす$$A_1, \dots , A_n \subset A$$が存在する.またルベーグ数の定義より,任意の$$i \in \{1, \dots n\}$$に対して$$A_i \subset G_i$$を満たす$$G_i \in \mathcal{C}$$が存在する.ゆえに,$$A \subset \bigcup_{i=1}^n G_i$$となるので,$$A$$はコンパクトである.



### Def(等長写像isometry)

> Let $$(X, d_X)$$ and $$(Y, d_Y)$$ are metric spaces. Then A map $$f:X \to Y$$ is called an **等長写像(isometry)** or **distance preserving** if for any $$a,b \in X$$ one has $$d_Y(f(a), f(b)) = d_X(a,b)$$. 
>
> * 等長写像(isometry)は一様連続(uniformly continuous)



### 等長写像は単射

> $$f:(X, d_X) \to (Y, d_Y)$$ を等長写像とする.この時$$f$$は単射

(Proof)

$$f$$が単射でないとすると$$a \neq b$$かつ$$f(a) = f(b)$$が存在する.一方で距離の定義から,$$d_X(a,b) > 0$$, $$d_Y(f(a), f(b)) = d_Y(f(a), f(a)) = 0$$となるので,$$f$$が等長写像であることに矛盾.



###全射な等長写像の開集合の像と引き戻しは開集合

> $$f:(X, d_X) \to (Y, d_Y)$$ を全射である等長写像とする.この時,任意の開集合$$A \subset X$$の像$$f(A)$$は開集合,任意の開集合$$B \subset Y$$の引き戻し$$f^{-1}(B)$$は開集合

(Proof)

$$A \subset X$$を開集合とする.任意に$$y \in f(A)$$を固定する.$$f$$は全射であるので$$x \in A$$が存在して$$f(x) = y$$を満たす.$$A$$は開集合であるので$$\epsilon > 0$$が存在して$$B_X(a,\epsilon) \subset A$$となる.また,$$f$$は等長写像(isometry)で全射なので$$f(B_X(x, \epsilon)) = B_Y(f(x), \epsilon)$$.よって,$$B_Y(f(x), \epsilon) = f(B_X(x, \epsilon)) \subset f(A)$$より$$f(A)$$は開集合.同様の議論を行うことで任意の開集合$$B \subset Y$$の引き戻し$$f^{-1}(B)$$は開集合である事が示せる(証明略)



