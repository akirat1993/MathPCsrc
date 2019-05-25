[TOC]

## 概要

重み付き並び替え(Weighted Random Sampling)のアルゴリズムを2つ紹介して,それらが同値であることを証明する



## 参考文献

基本,下記論文の要点を抜粋したものになります

> タイトル(Title)
>
> Weighted random sampling with a reservoir
>
> 著者(Author)
> Pavlos S. Efraimidis, Paul G. Spirakis
>
> 引用(Reference)
>
> Pavlos S. Efraimidis, Paul G. Spirakis, Weighted random sampling with a reservoir, Information Processing Letters, Volume 97, Issue 5, 16 March 2006, Pages 181-185, ISSN 0020-0190, 10.1016/j.ipl.2005.11.003.



## 証明

### 定義(Weighted Random Sampling)

> Def(WRS)
>
> 重み付き並び替え(Weighted Random Sampling 略してWRS)は以下のアルゴリズム(Algorithm D)によって定義される$$n$$個の重みつきアイテムから重みが大きいものを優先して,$$m$$個($$m \le n$$)を順序をつけて取り出す手法である.

**Algorithm D**

**Input**: A population $$V$$ of $$n$$ weighted items

**Output**: A set $$S$$ with a WRS of size $$m$$

1:Repeat Step 2 and 3 for $$k=1,2,\dots,m$$

2: The probability of $$v_i$$ to be selected is:
$$
p_i(k) = \frac{w_i}{\sum_{s_j \in V \setminus S} w_j}
$$
3: Randomly select an item $$v_k \in V \setminus S$$ amd insert it into $$S$$

補足:$$w_i >0$$とする

### 定義(Algorithm A High level description)

> Def(Algorithm A High level description)
>
> Algorithm Aを定義してこれがWRSと等価であることを後に示していく.

**Algorithm A**

**Input:** A population $$V$$ of $$n$$ weighted items

**Output:** A WRS of size $$m$$

1: For each $$v_i \in V$$, $$u_i = \text{random}(0,1)$$ and $$k_i \equiv u_i^{\frac{1}{w_i}}$$

2:Select the $$m$$ items with the largest keys $$k_i$$ as a WRS

補足:

$$u_i = \text{random}(0,1)$$は$$\{u_i\}_{i=1}^n$$が互いに独立に閉区間[0,1]上の一様分布に従うという意味である.

2.は$$k_i$$が大きい順に$$m$$個選ぶという意味

$$w_i >0$$とする



### 定義(記号)

$$\Pi = v_n, v_{n-1},\dots, v_1$$:$$n$$個のitemの任意の並び替え

$$P_A(\Pi)$$:Algorithm $$A$$が$$\Pi$$を出力する確率

$$P_D(\Pi)$$:Algorithm $$D$$が$$\Pi$$を出力する確率



### Remark 2.

Algorithm Dにおいて$$w_n$$が初めに選ばれる確率は$$w_n/(w_1 + w_2 + \cdots + w_n)$$. $$w_n$$が初めに選ばれたもとで$$w_{n-1}$$が2番目に選ばれる確率は$$w_{n-1}/ (w_1 + w_2 + \cdots + w_{n-1})$$であるので,
$$
P_D(\Pi) = \prod_{i=1}^n \frac{w_i}{w_1 + w_2 + \cdots + w_i}
$$


### Proposition 3 (Algorithm AとDの同値性)

> Let $$\{U_i\}_{i=1}^n$$ be i*ndependent random variables* with *uniform distribution* in $$(0,1)$$.
>
> For each positive real $$w_i$$ ($$i=1,2,\dots,n$$), let $$X_i$$ be the random variables $$X_i = U_i^{\frac{1}{w_i}}$$. Then for any $$\alpha \in [0,1]$$:

$$
P(X_1 \le \cdots \le X_n \le \alpha)
= \alpha^{w_1 + \cdots + w_n}
	\prod_{i=1}^n \frac{w_i}{w_1 + \cdots + w_i} \tag{*1}
$$

> 補足:
>
> もし(*1)が成立するなら$$\alpha=1$$とすることで,

$$
\begin{align*}
	P_A(\Pi) 
	&= P(X_1 \le \cdots \le X_n) \\
	&= P(X_1 \le \cdots \le X_n \le 1)\\
	&= \prod_{i=1}^n \frac{w_i}{w_1 + \cdots + w_i}\\
	&= P_D(\Pi)
\end{align*}
$$

> となる.

(Proof)

$$n$$に関する帰納法で示す.

任意の$$\alpha \in [0,1]$$と$$i \in \{1,\dots,n\}$$に対して$$w_i >0$$より$$0 \le \alpha^{w_i} \le 1$$であることに注意して$$F_{X_i}(\alpha)$$を以下のように定義する.
$$
F_{X_i}(\alpha) \equiv P[X_i \le \alpha] 
= P[U_i^{\frac{1}{w_i}} \le \alpha]
= P[U_i \le \alpha^{w_i}]
= \alpha^{w_i}
$$
また,$$F_{X_i}$$の確率密度関数を$$f_{X_i}$$とすると$$f_{X_i}$$は分布関数$$F_{X_i}$$の微分であるので,
$$
f_{X_i}(\alpha) \equiv P(X_i = \alpha)
= w_i \alpha^{w_i - 1}
$$
となる.

[1]$$n=1$$のとき
$$
P(X_1 \le \alpha) = F_{X_1}(\alpha) = \alpha^{w_i}
$$
より(*1)は成立.

[2]$$n = k$$ ($$k \ge 1$$)のとき(*1)が成立していると仮定する.
$$
\begin{align*}
	P(X_1 \le \cdots \le X_{k+1} \le \alpha)
	&= \int_0^{\alpha}
		P(X_1 \le \cdots \le X_k \le t, X_{k+1} = t) dt\\
	&= \int_0^{\alpha}
		P(X_1 \le \cdots \le X_k \le t) \cdot P(X_{k+1} = t) dt\\
	&= \prod_{i=1}^k \frac{w_i}{w_1 + \cdots + w_i}
		\int_0^{\alpha} t^{w_1 + \cdots + w_k} \cdot w_{k+1} t^{w_{k+1} -1} dt\\
	&= \left(
			\prod_{i=1}^k \frac{w_i}{w_1 + \cdots + w_i}
		\right) \cdot w_{k+1}
		\cdot \left[
			\frac{t^{w_1+\cdot +w_{k+1}}}{w_1 + \cdots + w_{k+1}}
		\right]_0^{\alpha}\\
	&= \left(
			\prod_{i=1}^{k+1} \frac{w_i}{w_1 + \cdots + w_i}
		\right) 
		\cdot \alpha^{w_1 + \cdots + w_{k+1}}
\end{align*}
$$
であるので,(*1)は$$n=k+1$$の時でも成立.

### Lemma 3.1

> Let $$U_1$$ and $$U_2$$ be *independent random variables* with *uniform distributions* in $$[0,1]$$. 
>
> Let $$X_1$$ and $$X_2$$ be the random variables, $$X_1 = U_1^{1/w_1}$$ and $$X_2 = U_2^{1/w_2}$$ where $$w_1$$ and $$w_2$$ are positive reals. Then $$P[X_1 > X_2] = \frac{w_1}{w_2 + w_1} = \frac{w_1}{w_2} P[X_1 < X_2]$$
>
> これはWRSが備えるべき性質が実際に成立することを示している.

(Proof)

$$u_1, u_2 \in [0,1]$$のとき,
$$
u_1^{\frac{1}{w_1}} \ge u_2^{\frac{1}{w_2}}
\Leftrightarrow
u_1 \ge u_2^{\frac{w_1}{w_2}}
$$
である.また,$$ 0 \le u_2^{\frac{w_1}{w_2}} \le 1$$である.$$U_1, U_2$$は独立に$$[0,1]$$の一様分布に従うので,
$$
P(U_1 = u_1, U_2 = u_2) = P(U_1 = u_1) P(U_2 = u_2) = 1
$$
であることに注意すると
$$
\begin{align*}
	P[X_1 > X_2] 
	&= P[X_1 \ge X_2]\\
	&= \int_0^1 \int_{u_2^{\frac{w_1}{w_2}}}^1 
		P(U_1 = u_1, U_2 = u_2) 
		d_{u_1} d_{u_2}\\
	&= \int_0^1 \int_{u_2^{\frac{w_1}{w_2}}}^1 1 \,ed_{u_1} d_{u_2}\\
	&= \int_0^1 1 - u_2^{\frac{w_1}{w_2}} d_{u_1}\\
	&= 1 
	- \left[
			\frac{u_2^{\frac{w_1}{w_2}}}
				{\frac{w_1}{w_2} + 1}
  	\right]_0^1\\
  &= \frac{w_1}{w_1 + w_2}
\end{align*}
$$
