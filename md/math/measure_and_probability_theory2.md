[TOC]

## 概要

> ***About this book***
>
> - Abstract 
>
>   測度論と確率について丁寧に書いてある.証明もきちんと載っているが、簡単な部分は省略してあるので自分で補足する必要あり.
>
> - Authors 
>
>   Krishna B. AthreyaSoumendra N. Lahiri
>
> - Print ISBN 
>
>   978-0-387-32903-1
>
> - Online ISBN 
>
>   978-0-387-35434-7

## 証明補足

### 1Measure

#### 1-5Problem

##### Problem1-9

k次元実ベクトル空間は任意の開集合は加算個の開区間(open interval)で表される 

> $$\mathbb{R}^k$$の任意の開集合は加算個の開区間(open interval)で表される.

Proof of (a),(b) 

任意に$$\mathbb{R}^k$$の開集合$$U$$をとる.
$$U_{\mathbb{Q}} \equiv \{ x \in U \mid \text{any elemen of } x \text{ is rational number}\}$$
$$U_{\mathbb{R}} \equiv  U \setminus U_{\mathbb{Q}}$$
と定義する.
また写像$$f: U_{\mathbb{R}} \rightarrow U_{\mathbb{Q}}$$を次のように定義する.
$$x \in U_{\mathbb{R}}$$をとると$$U$$が開集合であることから$$\epsilon_x \gt 0$$が存在し
$$(x_1 - \epsilon_x, x_1 + \epsilon_x)\times \cdots \times (x_k - \epsilon_x, x_k + \epsilon_x) \subset U$$
とできる.
また,実数の稠密性から以下を満たす有理数$$y$$がとれる.
$$
y \in (x_1 - \epsilon_x / 3, x_1 + \epsilon_x / 3) \times \cdots \times (x_k - \epsilon_x / 3, x_k + \epsilon_x / 3)
$$
これを1つ固定し,$$f(x) = y$$とする.
このとき,
$$
I_{f,x} = (y_1 - 2\epsilon_x / 3, y_1 + \epsilon_x / 3) \times \cdots \times (y_k - \epsilon_x / 3, y_k + \epsilon_x / 3)
$$
とすると,$$y \in I_{f,x} \in U$$を満たす.
また,任意の$$y \in U_{\mathbb{Q}}$$に対して$$U$$が開集合であることから以下を満たす開区間$$I_y$$がとれる.
$$
	I_y = (y_1 - \epsilon_y, y_1 + \epsilon_y) \times \cdots \times (y_k - \epsilon_y, y_k + \epsilon_y) \subset U
$$
ここで$$\epsilon_y \gt 0$$である.
このとき以下が成立(証明略)
$$
	U = \bigcup_{y \in U_{\mathbb{Q}}}
		\Big(
			\bigcup_{x \in f^{-1}(y)} I_{f,x}
		\Big)
		\cup I_y
$$
ここで,$$I_{f,x}, I_y$$は$$y$$を中心とした開区間の和集合であるので,$$\Big(\bigcup_{x \in f^{-1}(y)} I_{f,x}\Big)\cup I_y$$も$$y$$を中心とした開区間の和集合である.また,加算集合の有限個の積集合も加算集合であるので$$U_{\mathbb{Q}}$$も加算集合.ゆえに,$$U$$は開区間の加算個の和集合でかける.(特に$$\epsilon$$を有理数でとると,開区間の端点が有理数であるようにできる)



> $$\mathbb{R}$$上の開集合は高々加算個の互いに素なの開区間の和集合で表される.

Proof of (c)
有界な開集合$$U \in \mathbb{R}$$について考える.(有界でない場合も同様)
任意の$$x \in U$$に対して,$$a_x, b_x, I_x$$を以下のように定める.
$$a_x \equiv  \inf \{y \in \mathbb{R} \mid  [y,x] \subset U \}$$
$$b_x \equiv  \sup \{y \in \mathbb{R} \mid  [x,y] \subset U \}$$
定義より$$a_x \lt x \lt b_x$$であるので$$I_x \equiv (a_x, b_x)$$を定義できる.
このとき定義より$$I_x \subset U$$が成立することに注意すると,
$$
\bigcup_{x \in U} I_x = U
$$
また,
> $$I_x \ne I_y \Rightarrow I_x \cap I_y = \emptyset$$である.

対偶を示す.
$$I_x \cap I_y \ne \emptyset$$とする.
任意の$$z \in I_x \cap I_y$$に対して$$I$$の定義より$$I_x = I_z$$となる.
実際,$$a_x \lt a_z$$とすると,$$a_x \lt a \lt a_z$$を満たす$$a$$に対して,$$a_x$$の定義より,$$[a,x] \subset U$$であり, $$\min\{x,z\} \gt b \gt b_x$$を満たす$$b$$に対して,$$b_x$$の定義より,$$[x,b] \subset U$$であるので$$[a,z) \subset [a,b] \subset U$$.これは$$a_z$$の定義に矛盾.ゆえに.$$a_x = a_z$$.同様に$$b_x = b_z$$も示せるので$$I_x=I_z$$が成立.
同様の議論技$$I_y$$にも成立するので$$I_y = I_z = I_x$$
よって対偶が示された.
また$$U$$上に以下の同値類を定める.
$$x, y \in U$$に対して$$x \sim y \Leftrightarrow I_x = I_y$$
このとき,
$$
	\bigcup_{x \in U / \sim} I_x = U
$$
である.
また,$$x, y \in U / \sim (x \ne y)$$に対して$$I_x \cap I_y = \emptyset$$であるので,
を$$x \in U / \sim$$に対して$$f(x)$$を区間$$I_x$$に含まれる有理数と定めた写像$$f: U / \sim \rightarrow \mathbb{Q}$$は単射である.ゆえに,$$U / \sim$$は高々加算個であり,また$$I_x$$は互いに素な開区間である.



##### Problem1-18

> Let $$\Omega \equiv \mathbb{N}, \mathcal{F} = \mathcal{P}(\Omega)$$, and $$A_n = \{j : j \in \mathbb{N}, j \ge n\}, n \in \mathbb{N}$$. Let $$\mu$$ be the counting measure on $$(\Omega, \mathcal{F})$$. Verify that $$\lim_{n \to \infty} \mu(A_n) \ne \mu \left( \bigcap_{n \ge 1} A_n \right)$$ 

(Proof)

[$$\mu$$がmeasureになる証明>濃度を表す関数は測度である](./set.md#濃度を表す関数は測度である)

任意の自然数$$n$$に対して,$$A_n$$は無限集合$$\mathbb{N}$$から有限集合($$n$$より小さい自然数)を除いたものなので,無限集合である.ゆえに任意の$$n$$に対して$$\mu(A_n) = \infty$$であるので,(左辺)$$= \infty$$.

一方,$$\bigcap_{n \ge 1} A_n = \emptyset$$であるので右辺$$=0$$.

このことから,Prop1.2.3(i)の仮定である自然数$$n_0$$に対して$$\mu(A_{n_0}) < \infty$$ を満たさないと,$$\lim_{n \to \infty} \mu(A_n) \ne \mu \left( \bigcap_{n \ge 1} A_n \right)$$ となる場合がある.(Prop1.2.3(i)の結果を満たさない)



##### Problem1-19

> Let $$\Omega$$ be a nonempty set and let $$\mathcal{C} \subset \mathcal{P}(\Omega)$$ be a semialgebra. Let
$$
\mathcal{A}( \mathcal{C}) \equiv \{ A : A = \bigcup_{i=1}^K B_i: B_i \in \mathcal{C}, i= 1,2,\dots,k, k \in \mathbb{N}\}
$$
(a) Show that $$\mathcal{A}(\mathcal{C})$$ is the smallest algebra containing $$\mathcal{C}$$
(b) Show $$\sigma \langle \mathcal{C} \rangle = \sigma \langle \mathcal{A}(\mathcal{C}) \rangle$$
(c)追加 For any $$A \in \mathcal{A(\mathcal{C})}$$, there exist disjoint $$\{B_i\}_{i=1}^K \subset \mathcal{C} \quad (K \in \mathbb{N})$$ such that $$A = \bigcup_{i=1}^K B_i$$

Proof
$$\mathcal{C} \ne \emptyset$$と仮定する.(これは必要)
このとき, $$\emptyset \in \mathcal{C}$$であることは容易に示せる(証明略)

(a) algebraであることを示す.
(a1) $$\Omega \in \mathcal{A}(\mathcal{C})$$
(c1) $$A, B \in \mathcal{A}(\mathcal{C}) \Rightarrow A \cap B \in \mathcal{A}(\mathcal{C})$$
は容易に示せる. (証明略)
(b1) $$A \in \mathcal{A}(\mathcal{C}) \Rightarrow A^c$$
を示す.
任意に$$A \in \mathcal{A}(\mathcal{C})$$ととると仮定より,$$A = \bigcup_{i=1}^K B_i \quad (B_i \in \mathcal{C})$$と表せる.
また,$$\mathcal{C}$$がsemialgebraであることから,
$$
B_i^c = \bigcup_{j=1}^{N_i} C_j^i 
	\quad (C_j^i \in \mathcal{C}, C_j^i \cap C_{j'}^i = \emptyset \text{   for  } j \ne j')
$$
と表せる.ゆえに,$$C_j^i \cap C_{j'}^i = \emptyset \text{   for  } j \ne j'$$であることを注意すると,
$$
\begin{align*}
	A^c &= \Big( \bigcup_{i=1}^K B_i  \Big)^c\\
		&= \bigcap_{i=1}^K B^c_i\\
		&= \bigcap_{i=1}^K \big( \bigcup_{j=1}^{N_i} C_j^i \big)\\
		&= (C^1_1 \cap C^1_2 \cap \cdots \cap C^1_{N_1}) \cap 
			\Bigg( 
				\bigcap_{i=2}^K \Big(
					\bigcup_{j=1}^{N_i} C^i_j
				\Big) 
			\Bigg)\\
		&= \bigcup_{l_1 = 1}^{N_1} \Bigg(
			C_l^1 \cap \Big(
				\bigcap_{i=2}^K \bigcup_{j=1}^{N_i} C_j^i
				\Big)
			\Bigg)\\
		&= \bigcup_{l_1=1}^{N_1} \bigcap_{i=2}^{K} \bigcup_{j=1}^{N_i} 
			C_{l_1}^1 \cap C_j^i
\end{align*}
$$
上の式において,
$$\bigcap_{i=2}^{K} \bigcup_{j=1}^{N_i}  C_{l_1}^1 \cap C_j^i$$に対して同様の処理を再帰的に繰り返すことによって以下が得られる.
$$
\begin{align*}
	A^c &=  \bigcup_{l_1=1}^{N_1} \bigcup_{l_2=1}^{N_2} \Bigg(
					\bigcap_{i=3}^K \bigcup_{j=1}^{N_i} C_{l_1}^1 \cap C_{l_2}^2 \cap C_j^i
			\Bigg)\\
		&= \bigcup_{l_1=1}^{N_1} \bigcup_{l_2=1}^{N_2} \cdots \bigcup_{l_K=1}^{N_K}
		C_{l_1}^1 \cap C_{l_2}^2 \cap \cdots C_{l_K}^K \in \mathcal{A}(\mathcal{C})
\end{align*}
$$
ゆえに$$\mathcal{A}(\mathcal{C})$$はalgebraである.

(a) 最小性を示す.
$$\mathcal{F}$$を$$\mathcal{C}$$を含むalgebraだとする.
もし$$B_1, B_2, \dots, B_K \in \mathcal{C} \quad (K \in \mathbb{N})$$が存在して,$$\bigcup_{i=1}^K B_i \notin \mathcal{F}$$だとする.
仮定より$$\mathcal{F}$$は$$\mathcal{C}$$を含むので,$$B_i \in \mathcal{F}$$である.
また,$$ \mathcal{F}$$はalgebraであり有限和に閉じているので,
$$\bigcup_{i=1}^K B_i \in \mathcal{F}$$が成立する.ゆえに矛盾.
よって,
$$
\begin{align*}
	\mathcal{A}( \mathcal{C}) 
		\equiv \{ A : A = \bigcup_{i=1}^K B_i: B_i\in \mathcal{C}, i= 1,2,\dots,k, k \in \mathbb{N}\}
		\subset \mathcal{F}
\end{align*}
$$
であるので,$$\mathcal{A}( \mathcal{C}) $$は$$\mathcal{C}$$を含む最小のalgebraである.

Proof.(b)
$$\mathcal{C} \subset \mathcal{A} (\mathcal{C})$$より,$$\sigma\langle \mathcal{C} \rangle \subset \sigma \langle \mathcal{A} (\mathcal{C}) \rangle$$は自明.逆を示す.
$$ \mathcal{A} (\mathcal{C}) \subset \sigma \langle \mathcal{C} \rangle$$が示されれば,$$\sigma \langle \mathcal{A} (\mathcal{C}) \rangle$$は$$\mathcal{A} (\mathcal{C})$$を含む最小の$$\sigma$$-algebraであるので,$$\sigma \langle \mathcal{A} (\mathcal{C}) \rangle \subset \sigma\langle \mathcal{C} \rangle$$が示される.よって以下では,
$$ \mathcal{A} (\mathcal{C}) \subset \sigma \langle \mathcal{C} \rangle$$を示す.
任意に$$\bigcup_{i=1}^k B_i\in \mathcal{A}(\mathcal{C}), B_i \in \mathcal{C}$$をとる.
定義より$$\mathcal{C} \subset \sigma \langle \mathcal{C} \rangle$$であり,$$\sigma \langle \mathcal{C} \rangle$$有限和に閉じているので$$\bigcup_{i=1}^k B_i \in \sigma \langle \mathcal{C} \rangle$$である.よって題意は示せた.

Proof.(c)
For any $$A \in \mathcal{A}$$,  there exist $$\{A_n\}_{n=1}^N \subset \mathcal{C} \quad N \in \mathbb{N}$$ such that $$A = \bigcup_{n=1}^N A_n$$.
We define $${B_n}$$ as $$B_n = A_n \setminus \bigcup_{k=1}^{n-1} A_k \quad (1 \le n \le N, A_0 = \emptyset)$$.
Then $$A = \bigcup_{n=1}^N A_n = \bigcup_{n=1}^N B_n$$ and $$\{B_n\}_{n = 1}^N$$ is disjoint.

Moreover,
$$
\begin{align*}
	B_n &=  A_n \setminus \bigcup_{k=1}^{n-1} A_k\\
		&= A_n \cap \Big(
				\bigcup_{k=1}^{n-1} A_k
			\Big)^c\\
		&= A_n \cap \Big(
				\bigcap_{k=1}^{n-1} A_k^c
			\Big)\\
\end{align*}
$$
For any $$1 \le k \le N$$, since $$A_k \in \mathcal{C}$$, there exist disjoint subsets $$\{A_{kl}\}_{l=1}^{N_k} \subset \mathcal{C} \quad (N_k \in \mathbb{N})$$ such that $$A_k^c = \bigcup_{l=1}^{N_k} A_{kl}$$.
Therefore
$$
\begin{align*}
	\bigcap_{k=1}^{n-1} A_k^c &= \bigcap_{k=1}^{n-1} \bigg(
			\bigcup_{l=1}^{N_k} A_{kl}
		\bigg)\\
	&= \bigg(
			\bigcup_{l=1_1}^{N_1} A_{1l_1}
		\bigg) \cap 
		\Bigg(
				\bigcap_{k=2}^{n-1} \bigg(
					\bigcup_{l=1}^{N_k} A_{kl}
				\bigg)
		\Bigg)\\
	&= \bigcup_{l=1_1}^{N_1} \bigcap_{k=2}^{n-1} \bigcup_{l=1}^{N_k} 
		(A_{1l_1} \cap A_{kl})\\
	&= \cdots\\
	&= \bigcup_{l=1_1}^{N_1}  \bigcup_{l_2=1}^{N_2} \cdots \bigcup_{l_{n-1}=1}^{N_{n-1}} 
		(A_{1l_1} \cap A_{1l_2} \dots \cap A_{1l_{n-1}} )\\
\end{align*}
$$
Therefore 
$$
\begin{align*}
	B_n &= A_n \cap \Big(
				\bigcap_{k=1}^{n-1} A_k^c
			\Big)\\
	&= A_n \cap \Bigg(
			\bigcup_{l=1_1}^{N_1}  \bigcup_{l_2=1}^{N_2} \cdots \bigcup_{l_{n-1}=1}^{N_{n-1}} 
				(A_{1l_1} \cap A_{1l_2} \dots \cap A_{1l_{n-1}} )
		\Bigg)\\
	&= \bigcup_{l=1_1}^{N_1}  \bigcup_{l_2=1}^{N_2} \cdots \bigcup_{l_{n-1}=1}^{N_{n-1}} 
				(A_n \cap A_{1l_1} \cap A_{1l_2} \dots \cap A_{1l_{n-1}} )
\end{align*}
$$
Therefore, $$B_n \quad (1 \le n \le N)$$ is represented as disjoint finite union of $$\mathcal{C}$$. Since $$A = \bigcup_{n=1}^N B_n$$ and $$\{B_n\}_{n=1}^N$$ is disjoint, A is represented as finite disjoint union of $$\mathcal{C}$$.



##### Problem1-20

> Given a measure $$\mu$$ on a *semialgebra* $$\mathcal{C}$$, let the *outer measure* induced by $$\mu$$ be $$\mu^*$$
>
> Then, the following statements satisfy 

$$
\begin{align}
	\mu^* (\emptyset) &= 0 \tag{*1} \\
	A \subset B &\Rightarrow \mu^*(A) \le \mu^*(B) \tag{*2}\\
	\mu^*\left(
			\bigcup_{n \ge 1} A_n 
		\right) 
	&\le \sum_{i=1}^{\infty} \mu^*(A_n) 
		\quad \forall\{A_n\}_{n \ge 1} \subset \mathcal{P}(\Omega)
		\tag{*3}
\end{align}
$$

任意の$$A \in \mathcal{P}(\Omega)$$ ($$A \subset \mathbb{R}$$)に対して
$$
\mathcal{G}_A 
\equiv \left\{
	\sum_{n=1}^{\infty} \mu(A_n) 
		\mid \{A_n\}_{n \ge 1} \subset \mathcal{C}, 
			A \subset \bigcup_{n \ge 1} A_n
\right\}
$$
と定義すると$$\mu^*(A)  = \inf \mathcal{G}_A$$と表せる.

Proof (*1)

$$\mathcal{G}_A$$の定義より任意の$$x \in \mathcal{G} \subset \mathbb{R} \cup \{\infty\}$$に対して$$0 \le x$$.よって,下限の定義より$$0 \le \inf \mathcal{G}_A$$.また$$\emptyset \subset \emptyset \in \mathcal{C}, \mu(\emptyset) =0$$であるのでinfの定義より$$\inf \mathcal{G}_A \le \mu(\emptyset) = 0$$

Proof (*2)

$$A \subset B$$とすると$$\mathcal{G}_A \subset \mathcal{G}_B \subset \mathbb{R} \cup \{\infty\}$$.よって,$$\inf \mathcal{G}_A \le \inf \mathcal{G}_B \Leftrightarrow \mu^*(A) \le \mu^*(B)$$

Proof(*3)

Case1:任意の自然数$$n$$に対して$$\mu^*(A_n) < \infty$$が成立している場合

$$\epsilon > 0$$を任意に固定する.下限の定義より任意の自然数$$n$$に対して
$$
\sum_{j=1}^{\infty} \mu(A_{nj}) < \mu^*(A_n) + \frac{\epsilon}{2^n}
$$
を満たす$$\{A_{nj}\}_{j\ge1} \subset \mathcal{C}, A_n \subset \bigcup_{j \ge 1} A_{nj}$$が存在する.

(Case1-1) $$\sum_{n \ge 1} \mu^*(A_n) < \infty$$の場合

M-testより$$\sum_{n \ge 1} \sum_{j \ge 1} \mu(A_{nj})$$は収束する.よって
$$
\sum_{n \ge 1} \sum_{j \ge 1} \mu(A_{nj}) 
\le \sum_{n \ge 1} \mu^*(A_n) + \epsilon
$$
が成立する.$$\bigcup_{n \ge 1} A_n \subset \bigcup_{n \ge 1} \bigcup_{j \ge 1} A_{nj}$$であることに注意すると,
$$
\begin{align}
	\mu^* \left( 
			\bigcup_{n \ge 1} A_n
		\right)
	&\le \mu^* \left(
			\bigcup_{n \ge 1} \bigcup_{j \ge1} A_{nj}
  	\right) \quad \because (\text{*2})\\
  &\le \sum_{n \ge 1} \sum_{j \ge 1} \mu(A_{nj}) \\
  	&\quad \because \text{definition of }\mu^*,\\
  	&\quad \text{cartesian product of countable set is also countable}\\
  &\le \sum_{n \ge 1} \mu^*(A_n) + \epsilon
\end{align}
$$
$$\epsilon > 0$$は任意にとったので,(*3)が成立.

(Case1-2)$$\sum_{n \ge 1} \mu^*(A_n) = \infty$$の場合

(*3)の右辺が$$\infty$$なので常に成立

(Case2)ある自然数$$n$$に対して$$\mu^*(A_n) = \infty$$が成立している場合

(*3)の右辺が$$\infty$$なので常に成立

##### Problem1-22

> Let $$F:\mathbb{R} \rightarrow \mathbb{R}$$ be nondecreasing.Then, $$F$$ has right(left)side limit. 

Proof. (right-side limit)
Fix $$x \in \mathbb{R}$$.
We define sequence $$\{a_n\}_{n \ge 1},a_n \equiv F(x+1/n)$$.
Since $$F(x)$$ is nondecreasing, $$\{a_n\}_{n \ge 1}$$ is nonincreasing. Moreover $$F(x) \le a_n$$. Therefore $$\{a_n\}_{n \ge 1}$$ is convergent, and we can define $$a \equiv \lim_{n \rightarrow \infty} a_n$$. We show that
$$
lim_{y \downarrow x} F(y) = a
$$
Fix $$\epsilon \gt 0$$.
Since $$a_n$$ is  convergent, there exist $$N \in \mathbb{N}$$ such that
$$
 n \gt N \Rightarrow 0 \lt a_n - a \lt \epsilon \Leftrightarrow 0 \lt F(x+1/n) -a \lt \epsilon
$$
We take $$\delta$$ with $$\delta \in (0, \frac{1}{N+1})$$, and if we consider $$F$$ is nonincreasing,
$$
0 \lt y - x \lt \delta \Rightarrow 
	0 \lt F(y) -a \le F(x+\delta) - a \lt F(x+\frac{1}{N+1}) -a \lt \epsilon
$$

---
Proof. (left-side limit)
It is also proved in the same way, so ignore if you don't care.

Fix $$x \in \mathbb{R}$$.
We define sequence $$\{a_n\}_{n \ge 1},a_n \equiv F(x-1/n)$$.
Since $$F(x)$$ is nondecreasing, $$\{a_n\}_{n \ge 1}$$ is also nondecreasing. Moreover $$F(x) \ge a_n$$. Therefore $$\{a_n\}_{n \ge 1}$$ is convergent, and we can define $$a \equiv \lim_{n \rightarrow \infty} a_n$$. We show that
$$
lim_{y \uparrow x} F(y) = a
$$
Fix $$\epsilon \gt 0$$.
Since $$a_n$$ is  convergent, there exist $$N \in \mathbb{N}$$ such that
$$
 n \gt N \Rightarrow 0 \lt a -a_n \lt \epsilon \Leftrightarrow 0 \lt a - F(x-1/n) \lt \epsilon
$$
We take $$\delta$$ with $$\delta \in (0, \frac{1}{N+1})$$, and if we consider $$F$$ is nonincreasing,
$$
0 \lt x - y \lt \delta \Rightarrow 
	0 \lt a- F(y)  \le a- F(x-\delta) \lt  a - F(x-\frac{1}{N+1}) \lt \epsilon
$$
$$G(\infty+) \equiv G(\infty) $$
と定義する.

Proof.(a)(i) $$G(\cdot)$$ is nondecreasing
x = yのときは明らか.
x < yのとき成立しない、すなわち$$G(x) \gt G(y) \Leftrightarrow F(x+) \gt F(y+)$$が成立すると仮定する.
このとき$$\epsilon = \frac{F(x+) - F(y+)}{2} $$とすると$$F(x+)$$の定義より$$0 \lt \delta$$が存在し,以下を満たす.
$$
0 \lt z - x \lt \delta \Leftrightarrow
| F(x+) - F(z) | \lt \frac{\epsilon}{2}
$$
同様に$$F(y+)$$の定義より,$$0 \lt \delta'$$が存在し,以下を満たす.
$$
0 \lt v - y \lt \delta' \Leftrightarrow
| F(y+) - F(v) | \lt \frac{\epsilon}{2}
$$

ゆえに$$z = x + \min\{\delta / 2, \frac{y-x}{2}\}$$とすると,上記より$$| F(x+) - F(z) | \lt \frac{\epsilon}{2}$$.
また$$0 \lt v - y \lt \delta'$$を満たす$$v$$を1つとると,$$z \lt y \lt v$$なので
$$
\begin{align*}
	F(x+) \lt \frac{\epsilon}{2} + F(z) 
			\le \frac{\epsilon}{2}+ F(v) 
			\lt \epsilon + F(y+)
			= \frac{F(x+)+F(y+)}{2}
\end{align*} 
$$
より,$$F(x+) \lt F(y+)$$なので矛盾.

Proof. $$\lim_{y \downarrow x} G(y) = G(x)$$
任意に$$\epsilon \gt 0$$をとる.$$F(x+)$$の定義より$$\delta_1$$が存在して,
$$
\begin{align*}
	0 \lt z - x \lt \delta_1 \Rightarrow
	|F(z) - F(x+)| \lt \epsilon /2
\end{align*}
$$
ここで,$$\delta = \delta_1 / 2$$とすると,
$$
\begin{align*}
	0 \lt y - x \lt \delta \Rightarrow
	|G(y) - G(x)| \lt \epsilon
\end{align*}
$$
である.
実際上記を満たす$$y$$を任意にとると$$F(y+)$$の定義より$$\delta_2 \gt 0$$が存在して,
$$
\begin{align*}
	0 \lt z-y \lt \delta_2 \Rightarrow 
	|F(z) - F(y+)| \lt \epsilon /2
\end{align*}
$$
ここで,$$v$$を$$y \lt v \lt y+ \min\{\delta_1/2, \delta_2\}$$を満たすようにとると,
$$0 \lt v - x \lt \delta_1, 0 \lt v - y \lt \delta_2$$が成立するので,
$$|F(v) - F(x+)| \lt \epsilon /2 \land |F(v) - F(y+)| \lt \epsilon /2$$である.
ゆえに,$$|F(y+) - F(x+)| \lt \epsilon$$つまり,$$|G(y) - G(x)| \lt \epsilon$$

Proof.$$\mu_F(A) = \mu_G(A) \quad (A \in \mathcal{C})$$
> 始めに$$G((-\infty)+) = \lim_{x \downarrow - \infty} G(x) = F(-\infty)$$を示す.

任意に$$\epsilon  \gt 0$$をとると,$$F(-\infty)$$の定義より,$$C \lt 0$$が存在して,
$$
x \lt C \Rightarrow |F(x) - F(-\infty)| \lt \epsilon / 2
$$
が成立.このような$$x$$を任意にとると,$$G(x)$$の定義より$$\delta \gt 0$$が存在して,
$$
0 \lt y - x \lt \delta  \Rightarrow
|F(y) - G(x)| \lt \epsilon / 2
$$
である.ここで$$z = x+ \min\{\frac{c-x}{2}, \delta /2\}$$とすると,
$$
(z \lt C) \land (0 \lt z -x \lt \delta)
$$
であるので,
$$
\big(
	|F(z) - F(-\infty)| \lt \epsilon /2
\big) \land
\big(
	|F(z) - G(x)| \lt \epsilon / 2
\big)
$$
が成立.ゆえに,$$|G(x)- F(-\infty)| \lt \epsilon$$

次に本題の証明に入る.
定義より$$F((-\infty)+) = F(-\infty)$$とright continuousであることに注意すると,$$\mu_F(A) = \mu_G(A) \quad (A \in \mathcal{C})$$は明らか.

Proof.(b)
$$(a_k, b_k]$$を$$b_{i+1} \le a_i$$となるように並び替えても一般性を失わない.
$$
\begin{align*}
	F(b) - F(a) =& F(b) - F(b_1) \\
			&+ F(b_1) - F(a_1) + F(a_1) -F(b_2)\\
			&+F(b_2) - F(a_2) + F(a_2) - F(b_3)\\
			&\dots\\
			&+F(b_{k-1}) - F(a_{k-1}) + F(a_{k-1}) - F(b_k)\\
			&+F(b_{k}) - F(a_{k-1}) + F(a_{k-1}) - F(a_k)\\
			&+F(a_k) - F(a)\\
	=&F(b) - F(b_1) + F(a_k) - F(a) + \sum_{i=1}^{k-1} F(a_i) - F(b_{i+1}) + \sum_{i=1}^k F(b_i) - F(a_i)\\
	\ge& \sum_{i=1}^k F(b_i) - F(a_i)
\end{align*}
$$
ここで,両辺の極限をとると以下が成立.
$$
F(b) - F(a) \ge \sum_{i=1}^{\infty} F(b_i) - F(a_i)
$$
Proof(c)
> 始めに以下を示す.

$$
\begin{align*}
&[c,b] \subset \bigcup_{i=1}^K (a_i, d_i)
	\quad (-\infty \lt c \le b \lt \infty, a_i \lt d_i) \\
\Leftrightarrow
&F(b) - F(c) \le \sum_{i=1}^k F(a_i) - F(d_i)
\end{align*}
$$

$$(a_i, d_i)$$を以下のように並び替える.
$$a_0 = b$$
for i=1 ++:
$$\quad$$if $$a_{i-i} < c$$:
$$\quad$$$\quad$break
$$\quad$$else:
$$\quad$$$\quad$$$(a_i,d_i)$$は $$a_{i-1} < d_n$$を満たす$$(a_n, d_n)$$の組のなかで$$a_n$$が最小のもの.
上で選ばれたものを$$\{(a_i,d_i)\}_{i=1}^{K'}$$とする.つまり,
$$
	\bigcup_{i=1}^K (a_i, d_i) 
		= \bigcup_{i=1}^{K'} (a_i, d_i) \cup 
			\bigcup_{i=K'+1}^{K} (a_i, d_i) 
$$
と表すことにする.このとき,$$[c,b] \subset \bigcup_{i=1}^{K'} (a_i, d_i)$$と$$a_{i-1} \lt d_i$$であることに注意すると,
$$
\begin{align*}
	F(b) - F(c ) &= F(b) - F(a_1) + 
			\sum_{i=1}^{K'-1} \big\{F(a_i) - F(a_{i+1})\big\} + 
			F(a_{K'}) - F(c)\\
		&\le F(d_1) - F(a_1) + 
			\sum_{i=1}^{K'-1} \big\{F(d_{i+1}) - F(a_{i+1})\big\} +
			F(a_{K'}) - F(c)\\
		&\le \sum_{i=1}^{K'} \big\{F(d_{i+1}) - F(a_{i+1})\big\}\\
		& \le \sum_{i=1}^K F(a_i) - F(d_i)
\end{align*}
$$
本題の証明に入る.
任意に$$\eta \gt 0$$をとる.
$$
F(c) - F(a) \lt \eta, F(d_n) - F(b_n) \lt \frac{\eta}{2^n} \quad (n \ge 1)
$$
を満たすように$$c (\gt a)$$と$$d_n (\gt b_n)$$をとる.このとき,
$$
[c,b] \subset (a,b] = \bigcup_{n \ge 1} (a_n, b_n] \subset \bigcup_{n \ge 1} (a_n, d_n)
$$
であることに注意すると[Heine-Borel theorem](https://www.math.utah.edu/~bobby/3210/heine-borel.pdf)よって$$K \in \mathbb{N}$$が存在して,
$$
[c,b] \subset \bigcup_{i=1}^K (a_i, d_i)
$$
とできる.
ここで,$$(a_i,b_i)$$の1番目からK番目までは上記に対応するものに並び替えておく.このとき,$$[c,b] \subset \bigcup_{i=1}^K (a_i, d_i)$$であるので,
$$
\begin{align*}
	F(b) - F(c) &\le \sum_{i=1}^K F(d_i) - F(a_i)\\
		&= \sum_{i=1}^K F(d_i) - F(b_i) + F(b_i) - F(a_i)\\
		&\lt \eta(1 - (1/2)^K) + \sum_{i=1}^K F(b_i) - F(a_i)\\
		&\lt \eta + \sum_{i=1}^K F(b_i) - F(a_i)
\end{align*}
$$
ゆえに,
$$
\begin{align*}
	F(b) - F(a) &= F(b) - F(c) + F(c) - F(a)\\
		&\lt \Big( \sum_{i=1}^K F(b_i) - F(a_i)\Big) + 2 \eta\\
		& \le \Big( \sum_{i=1}^{\infty} F(b_i) - F(a_i)\Big) + 2 \eta
\end{align*}
$$
