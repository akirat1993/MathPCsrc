[TOC]

# 教科書

グラフィカルモデル 渡辺 有祐

## 注意点

* 3章ベイジアンネットワークの証明の補足は終了 2019/2/14

ただし,定理3.5の証明が教科書だと載っていなくてネットで調べても出てこなかったので,載せていな.なお,定理3.5については[以下](https://www.slideshare.net/YukiYoshida11/probabilistic-graphical-models-3334-63870995)のスライドの定理3.4で証明の概要が載っているんですが,確率分布の具体的な構成方法もしくは存在の証明が載っていないので納得していません.



# 事前知識

* 一般的なチェーンルール
  $$P(A_1,\dots, A_n) = P(A_n \mid A_1, \dots , A_{n-1}) P(A_{n-1} \mid A_1, \dots , A_{n-2}) \cdots P(A_2 \mid A_1) P(A_1)$$



# 証明の補足



## 第3章 ベイジアンネットワーク

### 定理3.2 (ベイジアンネットワークの因子分解)



Proofの補足

$$P(X_i \mid X_{L(i)}) = \frac{P(X_i, X_{L(i)})}{P(X_{pa(i)})} \cdot \frac{P(X_{pa(i)})}{P(X_{L(i)})}=\frac{P(X_i)}{P(X_{pa(i)})} \cdot \frac{P(X_{L(i)})}{P(X_{pa(i)})} \cdot \frac{P(X_{pa(i)})}{P(X_{L(i)})} = P(X_i \mid X_{pa(i)})$$
2つ目の不等式は条件付き独立性の性質の分離律から導かれる

Proof(3.2$$\Rightarrow$$3.1)

>  まず,教科書に載っている以下を示す

$$
P(X_i,X_{\text{ndes}(i)}) = P(X_i \mid X_{\text{pa}(i)}) \cdot \prod_{j \in \text{ndes}(i)} P(X_j \mid X_{\text{pa}(j)})
$$

Proof.
$$
\begin{align*}
	P(X_i, X_{\text{ndes}(i)}) 
	&= \int P(X) dX_{\text{des}(i)} \\
	&= \int \left( \prod_{j \in V} P(X_j \mid X_{\text{pa}(j)}) \right)\\
	&= P(X_i \mid X_{\text{pa}(i)}) \cdot
		\left( \prod_{j \in \text{ndes}(i)} P(X_j \mid X_{\text{pa}(j)}) \right) \cdot \\ & \ \ \ \ 
		\int \left( \prod_{j \in \text{des}(i)} P(X_j \mid X_{\text{pa}(j)}) \right) dX_{\text{des}(i)}\\
	&= P(X_i \mid X_{\text{pa}(i)}) \cdot \left( \prod_{j \in \text{ndes}(i)} P(X_j \mid X_{\text{pa}(j)}) \right)
\end{align*}
$$
ただし, 2つ目の等式は$$j \notin \text{des}(i) \Rightarrow \text{pa}(j) \cap \text{des}(i)$$から成り立つ.また3つ目の等式は終頂点に対応する$$X$$から始頂点に向かって順に積分していくと示される. その際に一般的に条件付き確率について$$\int P (X \mid Y) dX = 1$$であることを用いる.

>  次に上記を用いて以下を示す.

$$
P(X_i,  X_{\text{ndes}(i)} \mid X_{\text{pa}(i)}) = P(X_i \mid X_{\text{pa}(i)}) \cdot P(X_{\text{ndes}(i)} \mid X_{\text{pa}(i)})
$$

Proof.
$$
\begin{align*}
	\text{(left)} 
	&= \frac{P(X_i, X_{\text{ndes}(i)}, X_{\text{pa}(i)})}{P(X_{\text{pa}(i)})}\\
	&= \frac{P(X_i, X_{\text{ndes}(i)})}{P(X_{\text{pa}(i)})}  \quad \because \text{pa}(i) \subset \text{ndes}(i)\\
	&= P(X_i \mid X_{\text{pa}(i)}) \cdot \left( \prod_{j \in \text{ndes}(i)} P(X_j \mid X_{\text{pa}(j)}) \right) \cdot \frac{1}{P(X_{\text{pa}(i)})}
\end{align*}
$$
であるので, 
$$
\prod_{j \in \text{ndes}(i)} P(X_j \mid X_{\text{pa}(j)})  = P(X_{\text{ndes}(i)},X_{\text{pa}(i)})
$$
であることを示せば十分. 
$$
\begin{align*}
	P(X_{\text{ndes}(i)},X_{\text{pa}(i)})  
	&= P(X_{\text{ndes}(i)}) \quad \because  \text{pa}(i) \subset \text{ndes}(i)\\
	&= \int P(X) dX_{\text{des}(i)} dX_i\\
	&= \prod_{j \in \text{ndes}(i)} P(X_j \mid X_{\text{pa}(j)})
\end{align*}
$$

### 補題3.3 ベイジアンネットワークの構成の証明の補足

本文中に出てくる$$q_i$$は$$q_i : X_i \times \{X_j\}_{j \in pa(i)} \rightarrow \mathbb{R}_{\ge 0}$$である  

(定理3.2の証明と同様の手法を用いる)

帰納法より

$$
\begin{align*}
	\int P(X) dX 
	&= \prod_{i \in V} q_i (X_i, X_{pa(i)}) dX\\
	&= \int \left(
			\int q_N(X_N, X_{pa(N)} dX_N \cdot \prod_{V \setminus \{N\}} q_i(X_i, X_{pa(i)}))
		\right) dX_{V \setminus \{N\}}\\
		&\quad \because N\text{ is ending vertex}\\
	&= \int \prod_{V \setminus \{N\}} q_i(X_i, X_{pa(i)}) dX_{V \setminus \{N\}}
		\quad \because \text{definition of }q_i\\
	&= \int P(X_{V \setminus \{N\}}) dX_{V \setminus \{N\}}\\
	&= 1 \quad \because \text{assumption of induction}
\end{align*}
$$
次に式(3.4)を頂点数に関する帰納法を用いて示す.
$$
\begin{align*}
	P(X) 
	= \left( \prod_{i \in V \setminus \{N\}} q_i(X_i, X_{pa(i)}) \right)
		\cdot q_N(X_N, X_{pa(N)})
\end{align*}
$$
であり,
$$
\begin{align*}
	P(X_{V \setminus \{N\}}) 
	&= \int P(X) dX_N\\
	&= \int \left(
		\prod_{i \in V} q_i(X_i, X_{pa(i)})
		\right) dX_N\\
	&= \prod_{i \in V \setminus \{N\}} q_i (X_i, X_{\text{pa}(i)}) 
		\cdot \int q_N(X_N, X_{\text{pa}(N)}) dX_N 
			\quad \because \forall i \in V, N \notin \text{pa}(i) \\
	&= \prod_{i \in V \setminus \{N\}} q_i (X_i, X_{\text{pa}(i)}) 
		\quad \because \text{definition of }q_i
\end{align*}
$$
であるので,$$U := V \setminus  ( \{ N\} \cup \text{pa }(N) )$$と定義すると,
$$
P(X) 
= P(X_{V \setminus \{N\}}) \cdot  q_N(X_N, X_{pa(N)})
= P(X_{\text{pa}(N)}, X_U) \cdot  q_N(X_N, X_{pa(N)})
$$
であり,両辺を$$X_U$$で積分すると
$$
\begin{align*}
	&P(X_N, X_{\text{pa}(N)}) 
		= q_N(X_N, X_{pa(N)}) \cdot P(X_{\text{pa}(N)})\\
	\Leftrightarrow
	& P(X_N \mid X_{\text{pa}(N)}) = q_N(X_N, X_{pa(N)})
\end{align*}
$$
また,$$P(X_{V \setminus \{N\}}) = \prod_{i \in V \setminus \{N\}} q_i (X_i, X_{\text{pa}(i)})$$であり,帰納法の仮定を用いると

$$i \in V  \setminus \{N\}$$に対しても$$P(X_i \mid X_{\text{pa}(i)}) = q_i(X_i, X_{pa(i)})$$が成立するので(3.4)は成立.

(これ以降は証明で使わなかったが,証明に挑戦する過程で示せた主張とその証明)

------

続いて以下を示す.

> トポロジカルソートに対応する全単射を$$n : V \rightarrow V$$ (つまり, $$(v_0, v_1) \in E \Rightarrow n(v_0) < n(v_1)$$)とする.
>
> また,任意の$$j \in V$$に対して$$A_j := \{ i \in V \mid n(i) < n(j) \}$$と定義する.
>
> このとき,$$\forall i \in A_j$$に対して $$j \notin { \rm pa}(i)$$

Proof. 

$$j \in \text{pa}(i)$$を満たす$$i \in A_j$$が存在したとする. $$j \in \text{pa} (i)$$より$$n(j) < n(i)$$.一方で$$i \in A_j$$ より$$n(i) < n(j)$$より矛盾

------

$$
\begin{align*}
	P(X) 
	&= \prod_{i \in V} q_i (X_i, X_{pa(i)})\\
	&= q_N (X_N, X_{pa(N)}) \prod_{i \in V \setminus \{N\}} q_i(X_i, X_{pa(i)})\\
\end{align*}
$$

Nは終頂点より任意の$$i \in V$$に対して$$pa(i) \cap \{N\} \ne mptyset$$.また, $$U$$の定義より $$U \sqcup pa(N)  = V \setminus \{N\}$$であるので,

関数$$\phi : X_U \times X_{pa(N)} \rightarrow \mathbb{R}_{\ge 0}$$が存在し
$$
\begin{align*}
	q_N (X_N, X_{pa(N)}) \prod_{i \in V \setminus \{N\}} q_i(X_i, X_{pa(i)})
	&= \phi (X_U, X_{pa(N)}) q_N (X_N, X_{pa(N)}) \\
\end{align*}
$$

------

次に$$X_N \amalg X_U \mid X_{\text{pa}(N)}$$であるときに,次式の2つ目の等号が成立することを示す.
$$
\prod_{i \in V} q_i (X_i, X_{\text{pa}(i)}) 
= P(X)
= P(X_N \mid X_{\text{pa}(N)}) \cdot P(X_{\text{pa}(N)}, X_U)
$$
Proof.
$$
\begin{align*}
	P(X) 
	&= P(X_N, X_{\text{pa}(N)}, X_U)\\
	&= P(X_N \mid  X_{\text{pa}(N)})
		\cdot P(X_{\text{pa}(N)}, X_U)
		\cdot \frac{P(X_N \mid X_{\text{pa}(N)}, X_U)}{P(X_N \mid X_{\text{pa}(N)})}
\end{align*}
$$
ゆえに, $$P(X_N \mid X_{\text{pa}(N)},X_U) = P (X_N \mid X_{\text{pa}(N)})$$であることが示せれば十分であるので,以下でそれを示す.

### 定理3.4 (d分離の導く条件付き独立性)の証明

**Step1(可能な限り周辺化したグラフに問題を落とし込む)**

> 頂点集合$$U, T, W$$に含まれないものを終頂点の方から可能な限り周辺化したグラフ$$(V', \vec{E})$$に対して定理が成立すれば元のグラフでも定理が成立する.

Proof.

グラフ構造$$(V', \vec{E})$$をもつベイジアンネットワークの確率分布関数を$$P'$$とすると,定理3.2より
$$
P'(X) 
= \prod_{i \in V'} P(i) 
= \int \prod_{i \in V } P(i) dX_{V \setminus V'}
= \int P(X) dX_{V \setminus V'}
$$
と表せる.ただし,$$P(i) := P(X_i \mid X_{pa(i)})$$とし2つ目の等号は終頂点から順に積分を行うことで得られる.

ゆえに
$$
\begin{align*}
	P'(X_U, X_T, X_W) 
	&= \int P'(X) dX_{V' \setminus (U \cup T \cup W)}\\
	&= \int \left(
			\int \prod_{i \in V } P(i) dX_{V \setminus V'}
		\right) dX_{V' \setminus (U \cup T \cup W)}\\
	&= \int P(X) dX_{V \setminus (U \cup T \cup W)}\\
	&= P(X_U, X_T, X_W)
\end{align*}
$$
以上より,グラフ構造$$(V', \vec{E'})$$をもつベイジアンネットワークで$$X_U \amalg X_T \mid X_W$$が成立するとき$$(V,E)$$上のベイジアンネットワークでも成立.  $$\Box$$



以下では$$(V', \vec{E'})$$をもつベイジアンネットワークで定理が成立することを示す

**Step2($$U$$と$$T$$を結ぶ無向路上で成立する性質)**

> $$u \in U, t \in T$$を結ぶ任意の無向路上で(ii)を満たす$$r \in W$$が存在する.
>
> (ii) $$r$$はV構造ではなく$$r \in W$$が存在

Proof.

$$U$$,$$T$$が$$W$$のもとでd分離されているので$$u,t$$を結ぶ無向路は$$W$$のもとでアクティブではない.よって,無向路上に頂点$$r$$が存在して以下の(i)または(ii)が成立する.

(i) $$r$$がV構造であり,$$\{r\} \cup \text{des}(r) \cap W = \emptyset$$

(ii) $$r$$がV構造でなく$$r \in W$$

(i)が$$r$$で成立したとすると,$$\left( \{r\} \cup  \text{des}(r) \right)  \cap (U \cup T) \ne \emptyset$$である.もしそうでないなら$$(\{r\} \cup \text{des}(r)) \cap (U \cup T \cup W) = \emptyset$$となり,最初に可能な限り周辺化を行ったことに矛盾する.仮に$$u' \in (\{r\} \cup \text{des}(r) )\cap U$$ がとれたとするとd分離より$$u'$$と$$t$$を結ぶ無向路もアクティブでないはずである.頂点$$v$$から$$u'$$まではV構造でなく$$W$$の元も存在しないことに注意すると$$r$$から$$t$$までの頂点$$r'(\ne r)$$で(i)または(ii)が成立する.

$$r$$から$$t$$までの頂点$$r'$$で(i)を満たしかつ$$t' \in ( \{r'\} \cup \text{des}(r') ) \cap T$$を満たすものが存在したとする.このとき$$u' \rightarrow r \rightarrow r' \rightarrow t'$$の無向路はアクティブではなく,$$u'$$から$$r$$,$$r'$$から$$t'$$はV構造でなく$$W$$の元も存在しないことから,$$r$$と$$r'$$の間の頂点$$r'' (\ne r, r')$$で(i)または(ii)が成立する.上記の議論を繰り返すことで$$u \in U$$と$$t \in T$$を結ぶ任意の無向路上で(ii)を満たす$$r \in W$$が存在することがわかる.



**Step3(同時確率分布の分解)**

次に証明のために$$U \subset \tilde{U}, T \subset \tilde{T}, S \subset V'$$を以下で定義する.

$$\tilde{U}$$は$$V' \setminus W$$の部分集合であって,任意の$$v \in \tilde{U}$$に対して$$u \in U$$と$$v$$を結ぶ無向路(trail)が存在し,全ての頂点上で(ii)を満たさない.

英語の方が分かりやすいのでついでに書いとく
$$\tilde{U}$$ is the set of node $$v \in V' \setminus W$$ that $$\exists u \in U$$ and a trail connecting $$u$$ and $$v$$ such that every node of the path does not satisfy (ii)

$$\tilde{T}$$は$$V' \setminus W$$の部分集合であって,任意の$$v \in \tilde{T}$$に対して$$t \in T$$と$$v$$を結ぶ無向路(trail)が存在し,全ての頂点上で(ii)を満たさない.

$$S \equiv V' \setminus (\tilde{U} \cup \tilde{T} \cup W)$$

> 任意の$$\tilde{u} \in \tilde{U}$$に対して$$ \text{pa}(\tilde{u}) \cap \tilde{T} = \emptyset$$
>
> 任意の$$\tilde{t} \in \tilde{T}$$に対して$$ \text{pa}(\tilde{t}) \cap \tilde{U} = \emptyset$$

Proof.

対称性より任意の$$\tilde{u} \in \tilde{U}$$に対して$$ \text{pa}(\tilde{u}) \cap \tilde{T} = \emptyset$$のみ示す.

$$\tilde{t} \in \text{pa}(\tilde{u}) \cap \tilde{T}$$が存在するとする.$$\tilde{T}$$の定義より$$t \in T$$が存在し,全ての頂点上で(ii)を満たさない$$t$$と$$\tilde{t}$$を結ぶ無向路が存在する.同様に.$$\tilde{U}$$の定義より$$u \in U$$が存在し,全ての頂点上で(ii)を満たさない$$u$$と$$\tilde{u}$$を結ぶ無向路が存在する.ゆえに任意の頂点において(ii)を満たさない$$u$$と$$t$$を結ぶ無向路が存在することになり矛盾.

> 任意の$$\tilde{u} \in \tilde{U}$$に対して$$ \text{pa}(\tilde{u}) \cap S = \emptyset$$
>
> 任意の$$\tilde{t} \in \tilde{T}$$に対して$$ \text{pa}(\tilde{t}) \cap S = \emptyset$$

Proof.

対称性より「任意の$$\tilde{u} \in \tilde{U}$$に対して$$ \text{pa}(\tilde{u}) \cap S = \emptyset$$」のみを示せば十分.

$$s \in  \text{pa}(\tilde{u}) \cap S$$が存在すると仮定する.$$\tilde{U}$$の定義より$$u \in U$$が存在し,全ての頂点上で(ii)を満たさない$$u$$と$$\tilde{u}$$を結ぶ無向路が存在する.よって,$$u \rightarrow \tilde{u} \rightarrow s$$の無向路を考えると$$s \notin \tilde{U}$$であることから,$$\tilde{u}, \tilde{s}$$のいずれかが(ii)を満たすことになるが$$\tilde{u}, s \notin W$$より(ii)を満たさない.ゆえに矛盾.

> 任意の$$w \in W$$に対して,

$$
\text{pa}(w) \cap \tilde{U} \neq \emptyset \Rightarrow \text{pa}(w) \cap \tilde{T} = \emptyset, \text{pa}(w) \cap S = \emptyset\\
\text{pa}(w) \cap \tilde{T} \neq \emptyset \Rightarrow \text{pa}(w) \cap \tilde{U} = \emptyset, \text{pa}(w) \cap S = \emptyset
$$

> のみ示す.

対称性より上のみ示す. $$\tilde{u} \in \text{pa}(w) \cap \tilde{U}$$とする.

Proof. $$\text{pa}(w) \cap \tilde{T} = \emptyset$$

$$\tilde{t} \in \text{pa}(w) \cap \tilde{T}$$が存在したとする.上記と同様の議論を行うことで$$u \in U$$, $$t \in T$$が存在し,全ての頂点において(ii)を満たさない$$u \rightarrow \tilde{u} \rightarrow w \rightarrow \tilde{t} \rightarrow t$$が存在するので矛盾

Proof. $$\text{pa}(w) \cap S = \emptyset$$

$$s \in \text{pa}(w) \cap S$$が存在したとする.$$\tilde{U}$$の定義より$$u \in U$$が存在し全ての頂点において(ii)を満たさない無向路$$u \rightarrow \tilde{u} \rightarrow w \rightarrow s (\notin W)$$が存在する.ゆえに$$s \in \tilde{U}$$となるがこれは$$S$$と$$\tilde{U}$$が共通部分を持たないことに矛盾.

> 任意の$$s \in S$$に対して
>
> $$\text{pa}(s) \cap \tilde{U} = \emptyset, \text{pa}(s) \cap \tilde{T} = \emptyset$$

Proof.

対称性より$$\text{pa}(s) \cap \tilde{U} = \emptyset$$のみ示す.$$\tilde{u} \in \text{pa}(s) \cap \tilde{U}$$が存在したとすると.$$\tilde{U}$$の定義より$$u \in U$$が存在し全ての頂点において(ii)を満たさない無向路$$u \rightarrow \tilde{u}  \rightarrow s (\notin W)$$が存在する.ゆえに$$s \in \tilde{U}$$となるがこれは$$S$$と$$\tilde{U}$$が共通部分を持たないことに矛盾  $$\Box$$

上記と同様の議論から$$\tilde{U} \cap \tilde{T} = \emptyset$$が示せるので$$V' = \tilde{U} \sqcup \tilde{T} \sqcup W \sqcup S$$であり,
$$
P(X_{\tilde{U}}, X_{\tilde{T}}, X_W, X_S)
= P(V')
= \prod_{i \in V'} P(X_i \mid X_{\text{pa}(i)})
= \phi_1(X_{\tilde{U}}, X_W) \phi_2(X_{\tilde{T}}, X_W) \phi_3(X_S, X_W)
$$
となる実数値関数$$\phi_i \,(i=1,2,3)$$が存在することが示される.なお最後の等式は確率の積を以下のルールに従って分解することで得られる.

任意の$$i \in V'$$に対して$$i \in \tilde{U}$$ならば$$P(X_i \mid X_{\text{pa}(i)})$$を$$\phi_1(X_{\tilde{U}}, X_W)$$の項に追加.$$i \in S$$ならば$$\phi_3(X_S, X_W)$$の項に追加, $$i \in W$$かつ$$\text{pa}(i) \cap \tilde{U} \ne \emptyset$$なら$$\phi_1(X_{\tilde{U}}, X_W)$$の項に追加.



**Step4(同時確率分布の積の分解と条件付き確率の対応)**

>  最後に以下を示す.

$$
\begin{align*}
	&P(X_{\tilde{U}}, X_{\tilde{T}}, X_W, X_S)
	= \phi_1(X_{\tilde{U}}, X_W) \phi_2(X_{\tilde{T}}, X_W) \phi_3(X_S, X_W)\\
	\Rightarrow
	& X_{\tilde{U}} \amalg X_{\tilde{T}} \mid X_W
\end{align*}
$$

Proof.

仮定の両辺を$$X_S$$で積分することで,実数値関数$$\phi_4 : X_W \rightarrow \mathbb{R}_{\ge 0}$$を用いて
$$
P(X_{\tilde{U}}, X_{\tilde{T}}, X_W)
	= \phi_1(X_{\tilde{U}}, X_W) \phi_2(X_{\tilde{T}}, X_W) \phi_4(X_W)\\
$$
と表せる.この左辺を$$X_{\tilde{T}}$$と$$X_{\tilde{U}}$$でそれぞれ積分することで
$$
P(X_{\tilde{U}}, X_W) = \phi_1(X_{\tilde{U}}, X_W) \phi_5(X_W) \phi_4(X_W)\\
P(X_{\tilde{T}}, X_W) = \phi_6(X_W) \phi_2(X_{\tilde{T}},X_W) \phi_4(X_W)\\
$$
が得られる.ゆえに
$$
\begin{align*}
	P(X_{\tilde{U}}, X_{\tilde{T}}, X_W)
		&= P(X_{\tilde{U}}, X_W) P(X_{\tilde{T}}, X_W) \cdot
		\frac{1}{
            \phi_4(X_W) \phi_5(X_W) \phi_6(X_W)
		}\\
		&= P(X_{\tilde{U}}, X_W) P(X_{\tilde{T}}, X_W) \cdot
		\frac{1}{\phi_7(X_W)}
\end{align*}
$$
ここで両辺を$$X_{\tilde{T}}$$で積分すると
$$
 P(X_{\tilde{U}}, X_W) =  P(X_{\tilde{U}}, X_W) 
 	\cdot \frac{P(X_W)}{\phi_7(X_W)}
$$
より$$\phi_7(X_W) = P(X_W)$$,ゆえに$$P(X_{\tilde{U}}, X_{\tilde{T}}, X_W)$$の両辺を$$P(X_W)$$で割ることで所望の結果が得られる.



## 4章 マルコフ確率場

### 定理4.2 (マルコフ性条件の関係 2.)

> 任意のクリーク(clique)$$C$$は $$C \subset \tilde{A} \cup S$$または $$C \subset \tilde{B} \cup S$$である.
>
> ここでのcliqueはmaximal cliqueのことを指す.

Proof.

$$^\exists \tilde{a} \in \tilde{A}, \tilde{a} \in C \Rightarrow c \notin \tilde{B}\quad (^\forall c \in C)$$

$$^\exists \tilde{b} \in \tilde{B}, \tilde{b} \in C \Rightarrow c \notin \tilde{A}\quad (^\forall c \in C)$$

を示せば十分.($$^\exists \tilde{a} \in \tilde{A}, \tilde{a} \in C$$) $$\land$$ ($$^\exists c \in C, c \in \tilde{B}$$)が成立すると仮定して矛盾を導く.

$$\tilde{A}$$の定義より$$a \in A$$が存在して$$V \setminus S$$に属する頂点のみを経由して$$\tilde{a}$$に達する路が存在する.一方$$c \in \tilde{B} = V \setminus (\tilde{A} \cup S) \subset V$$であり,クリークは完全グラフであるので$$\tilde{a}c \in E$$である.よって$$a$$から$$V \setminus S$$に属する頂点のみを経由して$$\tilde{c}$$に到達できるので$$c \in \tilde{A}$$になる.これは$$c \in \tilde{B} = V \setminus (\tilde{A} \cup S)$$に矛盾.ゆえに,$$^\exists \tilde{a} \in \tilde{A}, \tilde{a} \in C \Rightarrow c \notin \tilde{B}\quad (^\forall c \in C)$$が成立.$$^\exists \tilde{b} \in \tilde{B}, \tilde{b} \in C \Rightarrow c \notin \tilde{A}\quad (^\forall c \in C)$$も同様の議論によって示すことができる.

> $$ \def\ci{\perp\!\!\!\perp} X_{\tilde{A}} \ci X_{\tilde{B}} \mid X_S$$

Proof.

$$$P(X_V) = \frac{1}{Z} \prod_{C:\text{clique}} \phi_C(X_C) = \frac{1}{Z} \prod_{C \subset \tilde{A} \cup S} \phi_C(X_C)\prod_{C \subset \tilde{B} \cup S} \phi_C(X_C) = \phi_1(X_{\tilde{A}}, X_S)\phi_2(X_{\tilde{B}}, X_S) $$$

と表せることに注意する.

$$V = \tilde{A} \sqcup \tilde{B} \sqcup S$$であることに留意して両辺を$$\tilde{A}, \tilde{B}$$に対して周辺化すると
$$
P(X_{\tilde{B}}, X_{S}) =\phi_3(X_S) \phi_2(X_{\tilde{B}}, X_S)\\
P(X_{\tilde{A}}, X_{S}) =\phi_1(X_{\tilde{A}}, X_S) \phi_4(X_S)
$$
ゆえに,
$$
P(X_V) \phi_3(X_S) \phi_4(X_S) = P(X_{\tilde{A}}, X_{S}) P(X_{\tilde{B}}, X_{S})
$$
となり両辺を$$\tilde{A}, \tilde{B}$$に対して順に周辺化すると,
$$
P(X_S) \phi_3(X_S) \phi_4(X_S) = P(X_{S})^2
$$
ゆえに,$$P(X_S) >0$$のとき$$P(X_S) = \phi_3(X_S) \phi_4(X_S)$$が成立する.よって
$$
P(X_V) P(X_S) = P(X_{\tilde{A}}, X_{S}) P(X_{\tilde{B}}, X_{S})
$$
より証明終了.

> $$B \subset \tilde{B}$$

$$b \in \tilde{A}$$を満たす$$b \in B$$が存在したとする.この時$$\tilde{A}$$の定義より$$A$$から$$b$$への路で$$S$$に含まれない頂点のみを通るものが存在するが,これは$$S$$が$$A$$と$$B$$を分離することに矛盾する.よって$$b \in B \Rightarrow b \notin \tilde{A}$$であり,仮定より$$b \in B \Rightarrow  b \notin S$$であるので$$b \in B \Rightarrow  b \in V \setminus (S \cup \tilde{A}) = \tilde{B}$$

### 定理4.3(Hammersley-Cllifordの定理)

基本的な証明は[こちら](https://www.cs.rutgers.edu/~pa336/bwca_f15/hc.pdf)を参照

上記の補足

> Lemma 2.1 (M$$\ddot{o}$$bius Inversion Lemma)
>
> for any non empty set, there are the same number of even and odd subsets

Proof.
$$
\sum_k^{n} (-1)^k \binom{n}{k} 
= \sum_k^{n}1^{n-k} (-1)^k \binom{n}{k} 
= (1+(-1))^n
$$

> Theorem 2.2 (Hammersley and Clifford)

$$\alpha, \beta \in a, c = a \setminus \{\alpha, \beta\}, b:b \subseteq c$$であるので,$$|a \setminus b| \ge 2$$であることに注意.

確率は全て正であるので,$$f(x) = 1$$となる$$x$$は存在しない

> Theorem 2.2 (Hammersley and Clifford)
>
> (2.15) $$\Rightarrow$$ (2.16) $$f(x_\alpha \mid x_\beta, x_b, x_{d \setminus b}^*) = f(x_\alpha \mid x_b, x_{d \setminus b}^*)$$

Proof.

$$d = V \setminus \{a,b\}$$であることに注意して,

$$f(x_\alpha \mid x_\beta, x_d) = f(x_\alpha \mid  x_d)$$であることを示せば十分.

$$\def\ci{\perp\!\!\!\perp} x_\alpha \ci x_\beta \mid x_d$$であることに注意すると,
$$
f(x_\alpha \mid x_\beta, x_d) 
= \frac{f(x_\alpha, x_\beta, x_d)}{f(x_\beta, x_d)}
= \frac{f(x_\alpha, x_\beta, x_d)}{f(x_d)} \frac{f(x_d)}{f(x_\beta, x_d)}
= \frac{f(x_\alpha, x_d)}{f(x_d)} \frac{f(x_\beta, x_d)}{f(x_d)} \frac{f(x_d)}{f(x_\beta, x_d)}
=f(x_\alpha \mid  x_d)
$$

> Theorem 2.2 (Hammersley and Clifford)
>
> (2.17) $$\Rightarrow$$ (2.18) 
>
> $$f(x_\alpha^* \mid x_b, x_{d \setminus b}^*) f(x_\beta, x_b, x_{d \setminus b}^*) = f(x_b, x_\beta, x_\alpha, x_{d \setminus b}^*)$$

Proof.
$$
\begin{align*}
	f(x_\beta, x_{d \setminus b}^*, x_b,  x_\alpha^*) 
	&= f(x_\alpha^* \mid x_\beta, x_{d \setminus b}^*, x_b) f(x_b, x_\beta, x_{d \setminus b}^*)\\
	&= f(x_\alpha^* \mid x_{d \setminus b}^*, x_b) f(x_b, x_\beta, x_{d \setminus b}^*)
\end{align*}
$$

### 定理4.4(ベイジアンネットワークとマルコフ確率場) モラル化

> 確率変数族$$X = \{X_v\}_{v \in V}$$は有向非巡回グラフ$$G = (V, \vec{E})$$上のベイジアンネットワークであるとする.このとき,各頂点$$v \in V$$で$$u, u' \in \text{pa}(v)$$同士を辺で結び有向枝を無向辺にしたグラフ$$G' = (V, E)$$を考えると$$ \{X_v\}_{v \in V}$$はグラフ$$G'$$に関して因子分解する.この操作をモラル化(moralization)という.

$$E$$の構成方法により,任意の$$v \in V$$に対して$$\{v \} \cup \text{pa}(v)$$はグラフ$$G'$$上で完全グラフである.よって,任意の$$v \in V$$に対して$$\{v \} \cup \text{pa}(v) \subset C_v$$となるようなクリーク$$C_v$$を1つ定めることができる.

ここで,グラフ$$G'$$上の任意のクリーク$$C$$に対して$$\phi_C(X_c) := \prod_{v \in V, C_v = C} P(X_v \mid X_{\text{pa}(v)} )$$と定義すると,
$$
P(X) = \prod_{v \in V} P(X_v \mid X_{\text{pa}(v)} ) = \prod_{C:\text{clique}} \phi_C(X_c)
$$

### 4.5 (例) ガウス型のマルコフ確率場

[多変量正規分布について良さそうな教科書](http://www012.upp.so-net.ne.jp/doi/math/anova/m_normal.pdf)

> 確率変数ベクトル$$\boldsymbol{x}$$が$$n$$次元多変量正規分布に従っているとする.つまり確率密度関数は正定値行列は正定値行列$$\Sigma$$とベクトル$$\boldsymbol{\mu}$$を用いて以下のように表されるとする.

$$
f(\boldsymbol{x}) 
	= \frac{1}{(\sqrt{2\pi})^n \sqrt{|\Sigma|}} 
	\exp \left(
		- \frac{1}{2}(\boldsymbol{x} - \boldsymbol{\mu})^T\Sigma^{-1}(\boldsymbol{x} - \boldsymbol{\mu})
		\right)
$$



> この時,確率ベクトルの添字を以下のようにして並び替えることができる.
> 
> $$\tau$$を任意の置換とする.$$\boldsymbol{x}_{\tau} := (x_{\tau(1)}, \cdots, x_{\tau(n)})$$,$$\Sigma^{-1}_{\tau}$$を$$(\Sigma^{-1}_{\tau})_{ij} = (\Sigma^{-1})_{\tau(i) \tau(j)}$$と定義すると,

$$
f(\boldsymbol{x}) 
	= \frac{ \sqrt{|\Sigma^{-1}_{\tau}|}}{(\sqrt{2\pi})^n} 
	\exp \left(
		- \frac{1}{2}(\boldsymbol{x}_{\tau} - \boldsymbol{\mu_{\tau}})^T\Sigma^{-1}_{\tau}(\boldsymbol{x}_{\tau} - \boldsymbol{\mu}_{\tau})
		\right)
$$

(Proof.)

$$\tau$$は置換であるので$$i$$が$$1$$から$$n$$まで動く時$$\tau(i)$$も$$1$$から$$n$$まで動くことに注意すると
$$
\begin{align*}
	(\boldsymbol{x} - \boldsymbol{\mu})^T\Sigma^{-1}(\boldsymbol{x} - \boldsymbol{\mu}) 
	&= \sum_{1 \le i \le n } \left(
	\sum_{1 \le j \le n } (x_{i} - \mu_i) \Sigma^{-1}_{ij} (x_{j} - \mu_j)
	\right)\\
	&= \sum_{1 \le i \le n } \left(
		\sum_{1 \le j \le n } (x_{\tau(i)} - \mu_{\tau(i)}) \Sigma^{-1}_{\tau(i) \tau(j)} (x_{\tau(j)} - \mu_{\tau(j)})
		\right)\\
	&= (\boldsymbol{x}_{\tau} - \boldsymbol{\mu_{\tau}})^T\Sigma^{-1}_{\tau}(\boldsymbol{x}_{\tau} - \boldsymbol{\mu}_{\tau})
\end{align*}
$$
である.次に任意の正方行列$$A$$に関して$$|A_{\tau}| = |A|$$が成立することを示す.

> 一般的に(交代性)より以下が成立する.

$$
\det (\boldsymbol{a}_{\tau(1)},\cdots , \boldsymbol{a}_{\tau(n)})
= \mbox{sgn}(\tau) \det(\boldsymbol{a}_1,\cdots , \boldsymbol{a}_n)
$$

> 言い換えると, 行列$$B$$を$$b_{i j} = a_{i, \tau(j)}$$と定めると$$|B| = \mbox{sgn}(\tau)|A|$$である.

よって,行列$$B$$を$$b_{i j} = a_{j i}$$, 行列$$C$$を$$c_{ij} = b_{i \tau(j)} = a_{\tau(j) i}$$,行列$$D$$を$$d_{ij} = c_{ji} = a_{\tau(i) j}$$, 行列$$E$$を$$e_{i j} = d_{i \tau(j)} = a_{\tau(i) \tau(j)}$$と定める.この時,行列式は転置しても値が変わらないことに注意すると
$$
|E| = \mbox{sgn}(\tau)|D| =  \mbox{sgn}(\tau)|C| = \mbox{sgn}^2(\tau)|B| = |A|
$$
$$E$$の定義より$$E = A_{\tau}$$であるので証明終了.

[多変量正規分布の条件付き確率(公式のみ)](https://qiita.com/kilometer/items/34249479dc2ac3af5706)



>  多変量正規分布の分布関数の証明の補足
>
> $$\Sigma_{11}$$が正則であることの証明

(Proof)

一般に線形代数の定理で以下のようなものがある.

> $$n$$次エルミート行列$$A$$に対し,$$k$$次エルミート行列$$A_k$$を$$(i,j)$$成分が$$A$$の$$(i,j)$$成分となるように定める.この時$$A$$が正値エルミート行列であるための必要十分条件は$$k=1,\dots ,n$$に対し,$$|A_k| > 0$$であることである.

$$\Sigma$$が正定値エルミート行列であるから$$|\Sigma_{11}| >0$$であり特に正則である.



[多変量正規分布の分布関数の証明](http://www.ae.keio.ac.jp/lab/soc/takeuchi/lectures/1_Norm.pdf)

> 主張(証明されていること)
>
> 確率変数ベクトル$$\boldsymbol{x}$$が$$n$$次元多変量正規分布に従っているとする.つまり確率密度関数は正定値行列は正定値行列$$\Sigma$$とベクトル$$\boldsymbol{\mu}$$を用いて以下のように表されるとする.

$$
f(\boldsymbol{x}) 
	= \frac{1}{(\sqrt{2\pi})^n \sqrt{|\Sigma|}} 
	\exp \left(
		- \frac{1}{2}(\boldsymbol{x} - \boldsymbol{\mu})^T\Sigma^{-1}(\boldsymbol{x} - \boldsymbol{\mu})
		\right)
$$

> また$$n$$次元ベクトル$$\boldsymbol{x}$$を$$p$$次元ベクトル $$\boldsymbol{x}^{(1)}$$と$$q$$次元ベクトル $$\boldsymbol{x}^{(2)}$$に分け,$$\Sigma$$もそれに対応するように以下のように分割する.

$$
\boldsymbol{x} 
= \left(
	\begin{array}{c}
		\boldsymbol{x}^{(1)}\\
		\boldsymbol{x}^{(2)}
	\end{array}
\right),
\Sigma 
= \left(
	\begin{array}{c}
		\Sigma_{1 1} & \Sigma_{1 2}\\
		\Sigma_{2 1} & \Sigma_{2 2}
	\end{array}
\right)
$$

> このとき,$$\boldsymbol{x}^{(1)}$$の周辺分布は多変量正規分布$$\mathcal{N}_p(\boldsymbol{\mu}^{(1)} , Σ_{11})$$であり,  $$\boldsymbol{x}^{(1)}$$を与えたときの$$\boldsymbol{x}^{(2)}$$の条件付き分布は 

$$
\boldsymbol{x}^{(2)} \mid \boldsymbol{x}^{(1)} \sim
\mathcal{N}_q(
	\boldsymbol{\mu}^{(2)} + \Sigma_{21} \Sigma_{11}^{-1}(\boldsymbol{x}^{(1)} - \boldsymbol{\mu}^{(1)}) 
	, Σ_{22} - \Sigma_{21}\Sigma_{11}^{-1}\Sigma_{1 2}
)
$$

である.

> 表記間違い(証明に影響なし)

$$
\boldsymbol{\upsilon^2} 
= \boldsymbol{\mu}^{(2)} 
+ \Sigma_{2 1} \Sigma_{1 1}^{-1}(\boldsymbol{x}^{(1)} - \boldsymbol{\mu}^{(1)})
$$




## Apendix

### 定理A.1(条件付き独立性の性質 1.) 

自力で証明出来るレベルなので行き詰まったら[こちら](http://statmodeling.hatenablog.com/entry/conditional-independence-and-d-separation)を参考に

### 命題A.2 (条件付き独立性の間違いやすい性質)

> [命題 A.2(条件付き独立性の間違いやすい性質

$$
\def\ci{\perp\!\!\!\perp}

X \ci Y_1 \mid Z,\;X \ci Y_2 \nRightarrow X \ci (Y_1, Y_2) \mid Z
$$

Proof

具体的に判例を構成する.$$X,Y_1,Y_2$$を$$\pm1$$の値をとる2値の確率変数とする.十分に小さい$$\epsilon > 0$$に対して,$$P(X=x, Y_1 = y_1, Y_2 = y_2) = \frac{1}{8} + \epsilon x y_1 y_2$$と定義する.このとき,$$P(X, Y_i) = 1/4$$より, $$\def\ci{\perp\!\!\!\perp} X \ci Y_i$$が成立する.一方で$$P(X) = 1/2$$,$$P(Y_1, Y_2) = 1/4$$より$$\def\ci{\perp\!\!\!\perp} X \ci (Y_1, Y_2) \mid Z$$は成立しない.

### 定理A.3 (条件付き独立性の性質2:交差律(intersection))

> $$p(z) > 0$$なる$$z$$について,$$p(y, w \mid z) >0 $$がすべての$$y,w$$で成り立つとき,以下が成立する.

$$
\def\ci{\perp\!\!\!\perp}
X \ci W \mid (Z,Y) \land X \ci Y \mid (Z,W) \Rightarrow X \ci (Y,W) \mid Z
$$

Proof.

仮定より,
$$
P(X \mid (Z, Y)) P(W,(Z,Y)) 
= P(X, Y, Z, W)
= P(X \mid (Z, W)) P(Y,(Z,W))
$$
である.両辺に$$P(Z,Y) P(Z,W) / P((Z,W), Y)$$を掛けて$$W$$に関して足しあげると
$$
\begin{align*}
		&\int P(X,Z,Y) P(Z,W) dw = \int P(X,Z,W) P(Z,Y) dw\\
	\Leftrightarrow 
		&P(X, Y, Z) P(Z) = P(X, Z) P(Z, Y)
\end{align*}
$$
よって,
$$
\begin{align*}
	P(X,Y,Z,W) 
	&= P(X,(Z,Y)) P(W \mid (Z,Y))\\
	&= \frac{P(X,Z) P(Z,Y)}{P(Z)} \frac{P(Y,W,Z)}{P(Z,Y)}\\
	&= P(X \mid Z) P((Y,W),Z)
\end{align*}
$$
