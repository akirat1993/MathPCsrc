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

#### 1-1Classes_of_sets

##### Example1-1-6

> $$\sigma \langle \mathcal{O}_2 \rangle = \langle \mathcal{O}_4 \rangle = \mathcal{B}(\mathbb{R})^k$$

$$\mathcal{G}$$を$$\mathcal{O}_4$$を含む$$\sigma$$-algebraだとする.
このとき$$\mathbb{R}^k$$の任意の開集合$$A \subset \mathbb{R}^k$$をとると,Problem1.9より$$\{B_n\}_{n \ge 1} \subset \mathcal{O}_3$$が存在して,$$A = \bigcup_{n \ge 1} B_n$$とできる.
ここで,
$$B_n = (a_1^n, b_1^n) \times \cdots \times (a_k^n, b_k^n)$$
とおくと,
$$
\begin{align*}
	B_n &= (a_1^n, b_1^n) \times \cdots \times (a_k^n, b_k^n)\\
		&= \bigcup_{i \ge 1} (-\infty, b_1^n) \times \cdots \times (-\infty, b_k^n) \setminus
			(-\infty, a_1^n + \frac{1}{i}) \times \cdots \times (-\infty, a_k^n + \frac{1}{i})\\
		&= \bigcup_{i \ge 1} C_n \setminus C_n^i
\end{align*}
$$
ゆえに,$$A = \bigcup_{n \ge 1} \bigcup_{i \ge 1} C_n \cap (C_n^i)^c$$.
$$C_n, C_n^i \in \mathcal{O}_4$$であり,$$\mathcal{G}$$は$$\mathcal{O}_4$$を含む$$\sigma$$-algebraなので$$A \in \mathcal{G}$$.
ゆえに,$$\mathcal{G}$$は$$\mathbb{R}^k$$の任意の開集合を含む$$\sigma$$-algebraであるので以下が成立
$$
\mathcal{B}(\mathbb{R}^k) \supset 
	\sigma \langle \mathcal{O}_2 \rangle \supset 
	\sigma \langle \mathcal{O}_4 \rangle =
	\bigcap_{\mathcal{G}: \mathcal{O}_4 \subset \mathcal{G}, \sigma \text{-field}}
		\mathcal{G} \supset
	\mathcal{B}(\mathbb{R}^k)
$$

##### Theorem1-1-2
>$$\lambda_1(\mathcal{C})$$ is $$\lambda$$-system

Proof.
(i)$$\Omega \in \lambda_1(C)$$は明らか.
(ii) $$A, A' \in \lambda_1(\mathcal{C}), A \subset A' \Rightarrow A' \setminus A \in \lambda_1(\mathcal{C})$$を示す.
$$A, A' \in \lambda_1(C)$$より$$A, A' \in \lambda \langle \mathcal{C} \rangle$$であり, $$ A \subset A' $$であることを踏まえると,$$A' \setminus A \in \lambda\langle \mathcal{C} \rangle$$.
また,任意の$$B \in \mathcal{C}$$をとったとき,$$(A' \setminus A) \cap B = (A' \cap B) \setminus (A \cap B) \in \lambda\langle \mathcal{C} \rangle$$
(iii)$$A_n \in \lambda_1(\mathcal{C}), A_n \subset A_{n+1} \Rightarrow \bigcup_n A_n \in \lambda_1(\mathcal{C})$$
任意の$$B \in \mathcal{C}$$をとったとき,$$(\bigcup_n A_n) \cap B = \bigcup_n (A_n \cap B) \in \lambda \langle \mathcal{C} \rangle$$($$A_n \cap B \subset A_{n+1} \cap B$$)

>by the previous step $$\mathcal{C} \subset \lambda_1(\mathcal{C})$$

Proof.
任意に$$A \in \mathcal{C}$$をとる.また任意に$$A' \in \lambda \langle \mathcal{C} \rangle = \lambda_1(\mathcal{C})$$をとると,$$\lambda_1(C)$$の定義より,$$A' \cap A \in \lambda \langle \mathcal{C} \rangle$$.また$$A \in \mathcal{C}$$より,$$A \in \lambda \langle \mathcal{C} \rangle$$は明らか.



#### 1-2Measures

##### Example1-2-1

[濃度を表す関数は測度であるを参照](./set.md#濃度を表す関数は測度である)

##### Example1-2-2(Discrete Probability Measure)

> Let $$w_1, w_2,\dots \in \Omega$$ and $$p_1, p_2,\dots \in [0,1]$$ be such that $$\sum_{i=1}^{\infty} p_i = 1$$. Define for any $$A \subset \Omega$$
> 
> $$P(A) = \sum_{i=1}^{\infty} p_i I_A (w_i)$$
> 
> Then $$P(\cdot)$$ is a measure and finite.

Proof.

まず,$$P(A)$$が定義できることを示す.任意の自然数$$n \ge 1$$について,$$0 \le  \sum_{i=1}^n p_i I_A (w_i) \le \sum_{i=1}^n p_i \le \sum_{i=1}^{\infty} p_i = 1$$であるので$$ \sum_{i=1}^n p_i I_A (w_i)$$は単調増加で上に有界なので上限に収束する.よって,$$P(A)$$はwell-definedでfiniteつまり$$P(\Omega) < \infty$$である.

次に$$P(\cdot)$$がmeasureであることを示す.(i)先の議論より任意の$$A \subset \Omega$$に対して,$$P(A) \in [0,1] \subset [0, \infty]$$.(ii)$$P(\emptyset) = 0$$は定義より明らか.(iii)互いに素な集合$$A_1, A_2,\dots \in \Omega$$に対して,
$$
\begin{align*}
	P\left(
		\bigcup_{n \ge 1} A_n
		\right)
	&= \sum_{i=1}^{\infty} p_i I_{\left( \cup_{n \ge1} A_i\right)} (w_i)\\
  &= \sum_{i=1}^{\infty} p_i
  	\left(
  		\sum_{n=1}^{\infty} I_{A_n} (w_i) 
  	\right) \quad \because A_n \text{ is disjoint}\\
  &= \sum_{i=1}^{\infty} \sum_{n=1}^{\infty} 
  	\left(
  		p_i I_{A_n} (w_i)
  	\right) \\
  	&\quad \because \text{const multiply of convergent sequence is also converge}\\
  &= \sum_{n=1}^{\infty} \sum_{i=1}^{\infty} 
  	\left(
  		p_i I_{A_n} (w_i)
  	\right) \\
  	& \quad \because \text{interchanging the order of summation}\\
  &= \lim_{n \to \infty} \sum_{i=1}^{n} P(A_n)\\
  &= \lim_{n \to \infty} P 
  	\left(
  		\bigcup_{i = 1}^n A_i
  	\right) \quad \because \text{below}
\end{align*}
$$
[収束列の定数倍は収束列](./calculus_compl.md#収束列の定数倍は収束列)

無限和の交換について.上式の式変形から,任意の$$i \in \mathbb{N}_{\ge 1}$$に対して $$\sum_{n=1}^{\infty} | p_i I_{A_n} (w_i) | = \sum_{n=1}^{\infty}  p_i I_{A_n} (w_i) $$は$$p_i$$か0に収束するので,
$$
\sum_{i=1}^{k} \sum_{n=1}^{\infty} | p_i I_{A_n} (w_i) | 
\le \sum_{i=1}^{k} p_i 
\le \sum_{i=1}^{\infty} p_i 
\le 1
$$
が任意の自然数$$k$$に対して成立.ゆえに,左辺の極限も1以下.よって, [無限和の交換(interchanging the order of summation)](./calculus_compl.md#無限和の交換)を用いることができる.

最後の式変形を示すためには,互いに素な集合$$A, B \in \Omega$$に対して
$$
P(A) + P(B) = P(A \cup B)
$$
を示せば十分.$$A, B$$が互いに素であることに注意すると,
$$
\begin{align*}
	P(A \cup B) 
	&= \sum_{i=1}^{\infty} p_i I_{A \cup B} (w_i)\\
	&= \sum_{i=1}^{\infty} p_i (I_A(w_i) + I_B(w_i))\\
	&= \sum_{i=1}^{\infty} p_i I_A (w_i) + \sum_{i=1}^{\infty} p_i I_B (w_i)\\
		&\quad \because \text{infinite sum of convergent series is also converge}\\
	&= P(A) + P(B)
\end{align*}
$$


##### Prop1-2-2(iii)

> Let $$\mu$$ be a measure on an algebra $$\mathcal{F}$$, and let $$A,B, A_1, \dots ,A_k \in \mathcal{F}$$, $$1 \le k < \infty$$. Then,
>
> (iii) (Inclusion-exclusion formula) If $$\mu (A_i) < \infty$$ for all $$i = 1, \dots ,k$$, then

$$
\begin{align*}
\mu (A_1 \cup \dots \cup A_k)
&= \sum_{i=1}^k \mu (A_i) 
	- \sum_{1 \le i < j \le k} \mu(A_i \cap A_j) + \cdots
  + (-1)^{k-1} \mu (A_1 \cap \cdots \cap A_k)\\
&= \sum_{j=1}^k 
	(-1)^{j-1} \sum_{1 \le i_1 < i_2 < \cdots< i_j \le k}
		\mu(A_{i_1} \cap A_{i_2} \cdots \cap A_{i_j})
\end{align*}
$$

(Proof.)

Prop 1.2.2 (ii)の証明より,$$\mu(A) < \infty$$と$$\mu(B) < \infty$$のどちらかが成立しているならば,
$$
\mu(A \cup B) = \mu(A) + \mu(B) - \mu(A \cap B)
$$
が成立することが示された.

ここで(iii)が$$k=n$$の時,成立していると仮定して$$k=n+1$$の時も成立することを示す.仮定より$$\mu(A_{n+1}) < \infty$$であることに注意すると
$$
\begin{align*}
	\mu\left( \bigcup_{i=1}^{n+1} A_i \right)
	=& \mu \left( \bigcup_{i=1}^{n} A_i \right)
		+ \mu(A_{n+1})
		- \mu \left( \bigcup_{i=1}^{n} A_i \cap A_{n+1} \right)\\
  =& \sum_{j=1}^n
    (-1)^{j-1} \sum_{1 \le i_1 < i_2 < \cdots< i_j \le n}
      \mu(A_{i_1} \cap A_{i_2} \cdots \cap A_{i_j})
      + \mu (A_{n+1})\\
   &(-1) \sum_{j=2}^{n+1}
    (-1)^{j-2} \sum_{1 \le i_1 < i_2 < \cdots< i_{j-1} \le n}
      \mu(A_{i_1} \cap \cdots \cap A_{i_{j-1}} \cap A_{n+1})\\
  =& \sum_{j=1}^{n+1}
    (-1)^{j-1} \sum_{1 \le i_1 < i_2 < \cdots< i_j \le n+1}
      \mu(A_{i_1} \cap A_{i_2} \cdots \cap A_{i_j})
\end{align*}
$$



##### Prop1-2-3 

> Let $$\mu$$ be a *measure* on an *algebra* $$\mathcal{F}$$
>
> (i) (Monotone continuity from above)
>
> Let $$\{A_n\}_{n \ge 1}$$ be a sequence of sets in $$\mathcal{F}$$ such that $$A_{n+1} \subset A_n$$ for all $$n \ge 1$$ and $$A \equiv \bigcap_{n \ge 1} A_n \in \mathcal{F}$$. Also, let $$\mu(A_{n_0}) < \infty$$ for some $$n_0 \in \mathbb{N}$$. Then, 
> 
> $$\lim_{n \to \infty} \mu(A_n) = \mu(A)$$

Proof(i)

$$C_n \equiv A_{n_0} \setminus A_n$$と定義すると,$$\{C_n\}_{n \ge 1}$$は単調増加であり,
$$
\bigcup_{n \ge 1} C_n 
=  A_{n_0} \setminus \bigcap_{n \ge 1} A_n
= A_{n_0} \setminus A \in  \mathcal{F}
$$
であるので,Prop1.2.1$$(iii)'_b$$より,$$\mu(A_{n_0} \setminus A) = \lim_{n \to \infty} \mu(A_{n_0} \setminus A_n) $$

$$A \subset A_{n_0}$$であるので,$$\mu(A_{n_0} \setminus A) = \mu(A_{n_0}) - \mu(A)$$.また,十分大きな$$n$$に対して$$A_n \subset A_{n_0}$$であるので,
$$
\lim_{n \to \infty} \mu(A_{n_0} \setminus A_n)
= \lim_{n \to \infty} \left(
		 \mu(A_{n_0}) - \mu(A_n)
	\right)
= \mu(A_{n_0}) -  \lim_{n \to \infty} \mu(A_n)
$$


##### Prop1-2-3

> Let $$\mu$$ be a measure on an algebra $$\tilde{\mathcal{F}}$$
> (Monotone continuity from below)
> Let $$\{A_n\}_{n \ge 1} \subset \tilde{\mathcal{F}}$$ satisfies $$A_n \subset A_{n+1}, A \equiv \bigcup_{n \ge1} A_n \in \tilde{\mathcal{F}}, \mu(A_n) \lt \infty \quad(n \in \mathbb{N})$$ . Then,
> $$$\lim_{n \rightarrow \infty} \mu(A_n) = A$$$

Proof.
Let $$\{B_n\}_{n \ge 1}$$ be $$B_n = A_n \setminus A_{n-1} (n \in \mathbb{N}, A_0 = \emptyset)$$.Then, $$\{B_n\}_{n \ge 1} \subset \tilde{\mathcal{F}}$$ are disjoint and $$\bigcup_{n \ge 1} = A$$.Therefore,
$$
\begin{align*}
	\mu(A) &= \mu \big(
				\bigcup_{n \ge 1} B_n
			\big)\\
		&= \sum_{n \ge 1} \mu(B_n)\\
		&= \sum_{n \ge 1} \mu(A_{n} \setminus A_{n-1})\\
		&= \sum_{n \ge 1} \mu(A_{n}) - \mu(A_{n-1})\\
		&= \lim_{n \rightarrow \infty} \mu(A_n)
\end{align*}
$$



#### 1-3The_extension_theorems_and_Lebesgue-Stieltjes_measures

##### Definition1-3-1(*semialgebra*)

>  Let $$\Omega$$ be a noempty set and let $$\mathcal{P} (\Omega)$$ be the power set of $$\Omega$$. A class $$\mathcal{C} \subset \mathcal{P} (\Omega)$$ is called a *semialgebra* if (i) $$A, B \in \mathcal{C} \Rightarrow A \cap B \in \mathcal{C}$$ and (ii) for any $$A \in \mathcal{C}$$, there exists $$\{B_i\}_{i=1}^k \subset \mathcal{C}$$, for some $$1 \le k < \infty$$, such that $$B_i \cap B_j = \emptyset$$ for $$i \ne j$$, and $$A^c = \bigcup_{i=1}^k B_i$$



##### Example1-3-2(区間はsemialgebra)

> $$\Omega = \mathbb{R}, \mathcal{C} \equiv \{I : I \text{ is an interval}\}$$. An interval $$I$$ in $$\mathbb{R}$$ is a set in $$\mathbb{R}$$ such that $$a, b \in I, a < b \Rightarrow (a,b) \subset I$$.
>
> Then, $$\mathcal{C}$$ is semialgebra, that is if (i) $$A,B \in \mathcal{C} \Rightarrow A \cap B \in \mathcal{C}$$ and (ii) for any $$A \in \mathcal{C}$$, there exist sets $$B_1, B_2, \dots , B_k \in \mathcal{C}$$, for some $$1 \le k < \infty$$, such that $$B_i \cap B_j = \emptyset$$ for $$i \ne j$$, and $$A^c = \bigcup_{i=1}^k B_i$$



(Proof)

(i) $$A,B \in \mathcal{C} \Rightarrow A \cap B \in \mathcal{C}$$は定義通りに示せるので略.

(ii) for any $$A \in \mathcal{C}$$, there exis sets $$B_1, B_2, \dots , B_k \in \mathcal{C}$$, for some $$1 \le k < \infty$$, such that $$B_i \cap B_j = \emptyset$$ for $$i \ne j$$, and $$A^c = \bigcup_{i=1}^k B_i$$.

を示す.

$$I$$をintervalとする.$$I = \emptyset$$と時は$$I^c = \mathbb{R}$$となり$$\mathbb{R}$$はIntervalであるのでOK.

$$I$$が単集合の時も自明であるので,以後$$I$$は空集合でも単集合でもないとする

$$A \equiv \{x \in \mathbb{R} \mid (-\infty, x] \subset I^c\}$$と定義する.

Intervalである$$C$$を以下のように定める.(​後に$$D$$を定めて,$$I^c = C \cup D$$であることを示す)

(1)$$A = \emptyset$$の場合

$$I$$は下に有界でない.この時は$$C = \emptyset$$と定める.

(2)$$A$$が上に有界でない場合

$$A$$の定義より$$A = \mathbb{R}$$となるので$$I^c = \mathbb{R}$$.これは$$I = \emptyset$$となり矛盾するので,(2)は起こり得ない

(3)$$A$$が上に有界である場合

上限が存在するので$$c$$とおく. 

(3-1) $$c \in I$$ならば$$C = (-\infty,  c)$$と定義する.

(3-2)$$c \notin I$$ならば$$C = (-\infty,  c]$$と定義する

(1)~(3)のいずれの場合でも$$A$$の定義から

- 「$$C$$と$$I$$は互いに素」である.

- また$$I$$が上に有界ならば$$b = \sup I$$,有界でない場合は$$b = \infty$$と定めると$$(-\infty, b) \subset C \sqcup I$$である(*1)

(*1)の証明

(1)すなわち$$A = \emptyset$$の場合は$$I$$は下に有界でないことを考慮すると簡単に示せる.

(3)の場合

$$x \in (-\infty, b)$$を任意にとる.$$x$$より小さい実数で$$I$$に含まれるものが存在するなら,$$b$$とIntervalの定義より$$x \in I$$であることがわかる.そうでない場合, すなわち$$(-\infty, x] \subset I^c$$の時を考える.

$$c$$の定義より$$x \le c$$である.この時(3-1),(3-2)のいずれの場合でも$$x \in C$$であることが示せるのでOK.



同様にして$$ \{x \in \mathbb{R} \mid [x, \infty) \subset I^c\}$$についても考えると以下のようなInterval  $$D$$を作成することが出来る.

- $$D$$と$$I$$は互いに素
- $$I$$が下に有界ならば$$a = \inf I$$,有界でない場合は$$a = -\infty$$と定めると$(a, \infty) \subset 
  D \sqcup I$



$$I$$が単集合でないことを考慮すると$$(-\infty, b) \cup  (a, \infty) = \mathbb{R}$$であるので,
$$
\mathbb{R}
= (-\infty, b) \cup  (a, \infty)
\subset C \cup D \cup I
$$
最後に$$C$$と$$D$$が互いに素であることを背理法を用いて示す.

$$C$$と$$D$$が互いに素でない場合は$$A \equiv \{x \in \mathbb{R} \mid (-\infty, x] \subset I^c\}$$が上に有界(上限を$$c$$とおく)かつ$$\{ x \in \mathbb{R} \mid [x, \infty) \subset I^c \}$$が下に有界(下限を$$d$$とおく)で,
$$
(-\infty, c] \cap [d,\infty) \ne \emptyset
$$
である時に限る.

一方で$$x \in (-\infty, c] \land d < x$$を満たす$$x$$が存在するならば$$c,d$$の定義より$$I^c = \mathbb{R}$$となり$$I$$が空集合となってしまうので矛盾.$$x < c \land d = x$$を満たす$$x$$が存在する場合も同様の理由で矛盾.よって,$$(-\infty, c] \cap [d,\infty) \ne \emptyset$$を満たすならば$$c =d$$の時に限るがその場合$$I$$が単集合になり矛盾



##### Example1-3-3

> $$\Omega = \mathbb{R}^k, \mathcal{C} \equiv \{I_1 \times I_2 \times \, \times I_k:I_j \text{ is an interval in } \mathbb{R}  \text{ for } 1 \le j \le k \}$$
>
> Then, $$\mathcal{C}$$ is a $$semialgebra$$

(Proof)

(i) Example 1.3.2で$$\mathbb{R}$$上の区間は*semialgebra​*であることが分かったので,*semialgebraの*定義(i)を用いれば,$$C_1, C_2 \in \mathcal{C} \Rightarrow C_1 \cap C_2 \in \mathcal{C}$$は容易に示せる.

(ii)任意に$$\prod_{j=1}^k I_j \in \mathcal{C}$$をとり,$$I_j^0 \equiv I_j, I_j^1 \equiv I_j^c$$と定義する.この時
$$
\left( \prod_{j=1}^k I_j \right)^c 
= \bigsqcup_{x \in \{0,1\}^k, x \ne {\bf 0}} \prod_{j=1}^k I_j^{x_j}
$$
が成立する(証明略)

また$$\mathbb{R}$$上の区間は*semialgebra*であるので,任意の区間$$I_j$$に対して$$I_j^c = \bigsqcup_{i=1}^{m_j} B_j^i$$となるような区間$$B_j^i$$が存在する.よって,$$B_j^0 \equiv = I_j^0 = I_j$$,任意の自然数$$n$$に対して$$[n] = \{0,1,\dots,n\}$$と定義すると
$$
I_j^{x_j} 
= \bigsqcup_{
		y_j \in [m_j]\\
		y_j = 0 (\text{if } x_j = 0)\\
		y_j \ne 0 (\text{if } x_j = 1)
	} B_j^{y_j}
$$
が成立.よって,


$$
\prod_{j=1}^k I_j^{x_j}
 = \bigsqcup_{
 		y \in \prod_{j=1}^k [m_j]\\
 		y_j = 0 (\forall j: x_j = 0)\\
 		y_j \ne 0 (\forall j: x_j = 1)
 	}
 	\prod_{j=1}^k B_j^{y_j}
$$
であるので,(ii)が示せた.



##### Proposition1-3-1

 > Let $$\mu$$ be a *measure* on a *semialgebra* $$\mathcal{C}$$. Let $$\mathcal{A(\mathcal{C})}$$ be the smallest algebra generated by $$\mathcal{C}$$. For each $$A \in \mathcal{A}$$, set
 > 
 > $$\bar{\mu} (A) = \sum_{i=1}^k \mu (B_i)$$.
 > 
 > if the set $$A$$ has teh representation $$A = \bigcup_{i=1}^k B_i$$, for some $$B_1, \dots , B_k \in \mathcal{C}, k < \infty$$ with $$B_i \cap B_j = \emptyset$$ for $$i \ne j$$. Then
 >
 > (i) $$\overline{\mu}$$ is independent of the representation of $$A$$ as $$A = \bigcup_{i=1}^k B_i$$
 > Note:
 > For any $$A \in \mathcal{A}$$, there exist disjoint $$\{B_i\}_{i=1}^K \subset \mathcal{C} \quad (K \in \mathbb{N})$$ such that $$A = \bigcup_{i=1}^K B_i$$
 >
 > (iii) $$\bar{\mu}$$ is *countably additive* on $$\mathcal{A}$$, *i.e.*, if $$A_n \in \mathcal{A}$$ for all $$n \ge 1$$, $$A_i \cap A_j = \emptyset$$ for all $$i=j$$, and $$\bigcup_{n \ge 1} A_n \in \mathcal{A}$$, then
 > 
 > $$\bar{\mu} \left(  \bigcup_{n \ge 1} A_n  \right) = \sum_{n=1}^{\infty} \bar{\mu} (A_n)$$

(Proof)

始めに$$\mathcal{C}$$に誘導される最小の*algebra*を具体的に構成する.

> Let $$\mathcal{C}$$ be a *semialgebra* on no-empty set $$\Omega$$. Then, we define
> 
> $$\mathcal{A} \equiv  \left\{   \bigsqcup_{i=1}^k A_i \mid A_i \in \mathcal{C}, 0 \le k < \infty \right\}$$
> 
> Then, $$\mathcal{A}$$ is algebra 

(c')$$\bigsqcup_{i=1}^k A_i, \bigsqcup_{j=1}^{\ell} B_j \in \mathcal{A}$$とすると
$$
\left( \bigsqcup_{i=1}^k A_i \right) \cap \left( \bigsqcup_{j=1}^{\ell} B_j \right)
=  \bigsqcup_{
    \substack{i= \{1,2,\dots,k\}\\
      j= \{1,2,\dots,\ell\}
    }
  } \big( A_i \cap B_j \big)
\in \mathcal{A}
$$
(b)
$$
\left( \bigsqcup_{i=1}^k A_i \right)^c
= \bigcap_{i=1}^k A_i^c
$$
であり,*semialgebra*の定義より$$A_i^c \in \mathcal{A}$$であるので(c')より(右辺)$$\in \mathcal{A}$$

(c)$$\emptyset \in \mathcal{A}$$であるので,(b)より$$\Omega = \emptyset^c \in \mathcal{A}$$

次に以下を示す.

> Let $$\mathcal{A} (\mathcal{C})$$ be the smallest algebra generated by $$\mathcal{C}$$. Then $$\mathcal{A} (\mathcal{C}) = \mathcal{A}$$

 $$\mathcal{A}$$は$$\mathcal{C}$$を含む*algebra*であることから,$$\mathcal{A} \subset \mathcal{A} (\mathcal{C})$$を示せば十分だが,これは$$ \mathcal{A} (\mathcal{C})$$が*algebra*であることから自明



Proof.(i)
$$A$$が$$A = \bigcup_{i=1}^K A_i, \bigcup_{j=1}^L B_j \quad (A_i \in \mathcal{C}, A_i \cap A_{i'} = \emptyset \text{    for  } i \ne i', B_j \text{  に対しても同様}) $$と2通りで表せられたとすると,
$$
\begin{align*}
	\overline{\mu}\Big(
		\bigcup_{i=1}^K A_i
	\Big) 
	&= \overline{\mu}\Bigg(
		\Big( \bigcup_{i=1}^K A_i \Big) \cap A
		\Bigg)\\
	&= \overline{\mu}\Bigg(
			\Big( \bigcup_{i=1}^K A_i \Big) \cap 
			\Big( \bigcup_{j=1}^L B_j \Big)
		\Bigg)\\
	&= \overline{\mu}\Big(
		\bigcup_{
			\substack{i= \{1,2,\dots,K\}\\
				j= \{1,2,\dots,L\}
			}
		} \big( A_i \cap B_j \big)
	\Big) \\
	&= \bigcup_{
			\substack{i= \{1,2,\dots,K\}\\
				j= \{1,2,\dots,L\}
			}
		} \mu(A_i \cap B_j)\\
\end{align*}
$$
である.同様に
$$
\begin{align*}
	\overline{\mu}\Big(
		\bigcup_{j=1}^L B_j
	\Big) 
	&= \bigcup_{
			\substack{i= \{1,2,\dots,K\}\\
				j= \{1,2,\dots,L\}
			}
		} \mu(A_i \cap B_j)\\
\end{align*}
$$
であるので,題意は示せた.

Proof (iii)

$$A_n$$の定義より,任意の$$n \ge 1$$に対して,$$A_n = \bigcup_{j=1}^{k_n} B_{nj}$$, $$B_{nj} \in \mathcal{C}$$, $$\{B_{nj}\}_{j=1}^{k_n}$$が互いに素になるような$$\{B_{nj}\}_{j=1}^{k_n}$$が存在する.また,$$\bigcup_{n \ge 1} A_n \in \mathcal{A}$$であるので,互いに素な$$\{B_i\}_{i=1}^k \subset \mathcal{C}$$で$$\bigcup_{n \ge 1} A_n = \bigcup_{i=1}^k B_i$$を満たす$$B_i$$が存在する.
$$
B_i 
= B_i \cap \bigcup_{n \ge 1} A_n
= \bigcup_{n \ge 1} B_i \cap A_n
= \bigcup_{n \ge 1} \bigcup_{j=1}^{k_n} B_i \cap B_{nj}
$$
であり,$$\mu$$はは*semi-algebra*$$\mathcal{C}$$上の*measure*であるので,
$$
\mu(B_i) = \sum_{n \ge 1} \sum_{j=1}^{k_n} \mu(B_i \cap B_{nj})
$$
よって,
$$
A_n 
= A_n \cap \bigcup_{i=1}^k B_i 
= \bigcup_{i=1}^k \bigcup_{j=1}^{k_n} B_i \cap B_{nj}
$$


であるので,
$$
\begin{align*}
	\bar{\mu}\left(
		\bigcup_{n \ge 1} A_n
	\right)
	&= \sum_{i=1}^k \mu (B_i)\\
  &= \sum_{i=1}^k \sum_{n \ge 1}
  	\left(
  		\sum_{j=1}^{k_n} \mu (B_i \cap B_j)
  	\right)\\
   &= \sum_{n \ge 1} 
  	\left(
  		\sum_{i = 1}^k \sum_{j=1}^{k_n} 
  			\mu (B_i \cap B_j)
  	\right)\\
  &= \sum_{n \ge 1} \bar{\mu}(A_n)

\end{align*}
$$


3つ目の等号が成立することを示す.

(case1) 任意の$$i \in \{1, \dots ,k \}$$について$$\mu(B_i) < \infty$$の場合.

[有限和と無限和の交換](calculus_compl.md#有限和と無限和の交換)より成立

(case2)$$i_0 \in \{1, \dots ,k \}$$が存在して$$\mu(B_{i_0}) = \infty$$を満たす場合
$$
\bar{\mu} \left(
	\bigcup_{n \ge 1} A_n
\right) 
= \sum_{n = 1}^{\infty} \bar{\mu}(A_n) 
= \infty
$$
であることを示す.

(ii)で示した*finitely additive*性より
$$
A, B \in \mathcal{A}, A \subset B 
\Rightarrow
\bar{\mu}(B) = \bar{\mu}(A) + \bar{\mu}(B \setminus A) \ge \bar{\mu}(A)
$$
が成立することに注意すると,
$$
\bar{\mu} \left(
	\bigcup_{n \ge 1} A_n
\right)
= \bar{\mu} \left(
	\bigcup_{i = 1}^k B_i
\right) 
\ge \bar{\mu}(B_{i_0}) = \infty
$$
また,$$\bigcup_{n \ge 1} A_n = \bigcup_{i=1}^k B_i$$であるので,$$\bigcup_{\ell = 1}^m A_{\ell}  \supset B_{i_0}$$を満たす$$m$$が存在する.

$$\mathcal{A}$$は*algebra*であるので,$$\bigcup_{\ell = 1}^m A_{\ell} \in \mathcal{A}$$であり(ii)で示した*finitely additive*性を用いると,
$$
\sum_{\ell = 1}^m \bar{\mu}(A_\ell)
=\bar{\mu} \left(
	\bigcup_{\ell = 1}^m A_{\ell}
\right) 
\ge \bar{\mu}(B_{i_0})
= \infty
$$
であるので,
$$
\sum_{n = 1}^{\infty} \bar{\mu}(A_n) 
= \infty
$$

##### Definition1-3-3

> $$\mu^* = \overline{\mu} \text{ on } \mathcal{A}$$
>
> $$\mu^* = \mu \text{ on } \mathcal{C}$$

Prrof.$$\mu^* = \overline{\mu} \text{ on } \mathcal{A}$$

Fix $$A \in \mathcal{A}$$.
任意に$$\{A_n\}_{n \ge 1} \subset \mathcal{C}$$ with $$A \subset \bigcup_{n \ge 1} A_n$$をとる.
We define $$\{B_n\}_{n \ge 1}$$ as
$$
\begin{align*}
	B_n \equiv \Bigg(
			A_n \setminus \bigcup_{k=1}^{n-1}  A_k
		\Bigg) \cap A
		\quad (
			B_1 \equiv A_1, n \ge 1
		)
\end{align*}
$$
Then, $$\{B_n\}_{n \ge 1}$$ is disjoint,  $$B_n \subset A_n$$.
Since algebra is closed under complementation and finite intersection, $$\{B_n\}_{n \ge 1} \subset \mathcal{A}$$.
It also satisfies $$A = A \cap \bigcup_{n \ge 1} A_n = \bigcup_{n \ge 1} B_n$$.
Therefore
$$
\begin{align*}
	\overline{\mu}(A) &= \overline{\mu}\Big(
				\bigcup_{n \ge 1} B_n
			\Big)\\
		&= \sum_{n \ge 1} \overline{\mu}(B_n) 
			\quad(\because \overline{\mu} \text{ is a measure on an algebra } \mathcal{A})\\
		&\le \sum_{n \ge 1} \overline{\mu}(A_n)
			\quad (\because B_n \subset A_n) \\
		&= \sum_{n \ge 1} \mu (A_n)
\end{align*}
$$
右辺の下限をとると$$\overline{\mu}(A) \le \mu^{*}(A)$$が示せる.
Next we show $$\overline{\mu}(A) \ge \mu^{*}(A)$$.
Since, $$A \in \mathcal{A}$$, 
$$
A = \bigsqcup_{i=1}^N C_n 
	\quad (N \in \mathbb{N}, \{C_n\}_{i=1}^N \subset \mathcal{C})
$$
Since $$A \subset \bigsqcup_{i=1}^N C_n $$, 
$$
\begin{align*}
	\mu^*(A) &\le \sum_{i=1}^N \mu(C_n)\\
		&= \overline{\mu}(A)
\end{align*}
$$
Proof.$$\mu^* = \mu \text{ on } \mathcal{C}$$
Since $$\mathcal{C} \subset \mathcal{A}$$, $$\mu^* = \overline{\mu} \text{ on } \mathcal{A}$$, and $$\overline{\mu} = \mu \text{ on } \mathcal{C}$$.
Therefore,$$\mu^* = \mu \text{ on } \mathcal{C}$$

##### 1-3-2Lebesgue-Stieltjes_measures_on...

(a)$$\mu_F(\emptyset) = \mu_F([a,a]) = F(a+) - F(a+) = 0$$は明らか.
(b)$$\mu_F(\cdot) \in [0, \infty]$$を示す.
(1) 
$$
-\infty \le a \lt b \lt \infty \Rightarrow F(b+) - F(a+) \ge 0
$$
を示す.

(1-1)$$-\infty \lt a$$のとき.
背理法で示す.

$$F(b+) \lt F(a+)$$であるとする.
$$\epsilon = \frac{F(b+) - F(a+)}{2} (\gt 0)$$とおく.
このとき$$F(a+)$$の定義より$$\delta_1 \gt 0$$が存在して,
$$
0 \lt x - a \lt \delta_1 \Rightarrow |F(a+) - F(x)| \lt \epsilon /2
$$
である.ここで,$$x = a + \min\{ \delta_1/2, b-a\}$$とすると$$0 \lt x - a \lt \delta_1$$であり,$$x \le b$$である.
また$$F(b+)$$の定義より$$\delta_2 \gt 0$$が存在して
$$
0 \lt y - b \lt \delta_1 \Rightarrow |F(b+) - F(y)| \lt \epsilon /2
$$
が成立.ここで$$0 \lt y - b \lt \delta_1$$を満たす.$$y$$を任意にとると,
$$
\begin{align*}
	F(a+) \lt F(x) + \epsilon /2
	\le F(y) + \epsilon /2
	\le F(b+) + \epsilon
	= \frac{F(a+)+F(b+)}{2}
\end{align*}
$$
ゆえに矛盾.同様に(1-2)$$a = -\infty$$
(2)
$$
-\infty \le a \lt \infty \Rightarrow
F(\infty) - F(a+) \ge 0
$$
も示せるので(b)は示せる.

(c)

$$\{C_n\}_{n \ge 1} \subset \mathcal{C}$$がdisjointで$$\bigcup_{n\ge1} C_n \in \mathcal{C}$$だとすると,$$\bigsqcup_{n \ge 1} C_n$$は次のいずれかで表される.
$$
\bigsqcup_{n \ge 1} (a_n, b_n] \cup (b, \infty)\\
\bigsqcup_{n \ge 1} (a_n, b_n]
$$
ただし,$$\bigsqcup_{n \ge 1} (a_n, b_n] = (a,b]$$と表される.

[Problem1-22](./measure_and_probability_theory2.md#Problem1-22)(b),(c)において$$F(\cdot)$$を$$G(\cdot)$$に置き換えても成立するので,
の証明は下記.
$$
\begin{align*}
	G(b) - G(a) = \sum_{n \ge 1} G(b_i) - G(a_i)
\end{align*}
$$
が成立.
ゆえに,
$$
\begin{align*}
	\mu_F((a,b]) &= \mu_G((a,b])\\
		&= G(b+) - G(a+)\\
		&= G(b) - G(a)\\
		&= \sum_{n \ge 1} G(b_i) - G(a_i)\\
		&= \sum_{n \ge 1} G(b_i+) - G(a_i+)\\
		&= \sum_{n \ge 1} \mu_G((a_i, b_i])\\
		&= \sum_{n \ge 1} \mu_F((a_i, b_i])\\
\end{align*}
$$

$$
\begin{align*}
	\mu_F((a,\infty)) &= \mu_G((a,\infty))\\
		&= G(\infty) - G(a+)\\
		&= G(\infty) - G(b+) + G(b) - G(a)\\
		&= \mu_G((b, \infty)) + G(b) - G(a)\\
		&= \mu_F((b, \infty)) + \sum_{n \ge 1} \mu_F((a_i, b_i])\\
\end{align*}
$$

##### Definition1-3-7

>  $$\sigma \langle \mathcal{C} \rangle = \mathcal{B}(\mathbb{R})$$

Proof.
$$(a,b] = (a, \infty) \cap (b, \infty)^c$$であり,$$(a, \infty), (b, \infty)$$は$$\mathbb{R}$$の開集合なので$$(a, \infty), (b, \infty) \in \mathcal{B}(\mathbb{R})$$.また,$$\mathcal{B}(\mathbb{R})$$は$$\sigma$$-fieldより,$$[a,b] \in \mathcal{B}(\mathbb{R})$$.また,$$(a,\infty) \in \mathcal{B}(\mathbb{R})$$は明らかなので,$$\mathcal{C} \subset \mathcal{B}(\mathbb{R})$$.よって,$$\sigma \langle \mathcal{C} \rangle$$の定義より$$\sigma \langle \mathcal{C} \rangle \subset \mathcal{B}(\mathbb{R})$$.
$$
\begin{align*}
	 \mathcal{C} 
		 &\equiv  \{(a,b] : -\infty \le a \le b \lt \infty\} \cup \{(a,\infty) : -\infty \le a  \lt \infty\}\\
	 &= \mathcal{O}_1 \cup \mathcal{O}_2
\end{align*}
$$
とすると,P12 Example 1.1.6より
$$
\sigma \langle \mathcal{C} \rangle 
	=\sigma \langle \mathcal{\mathcal{O}_1 \cup \mathcal{O}_2} \rangle 
	\supset \sigma \langle \mathcal{\mathcal{O}_2} \rangle
	= \mathcal{B}(\mathbb{R})
$$

>  $$\mu_F^*$$ is also a measure on $$(\mathbb{R}, \mathcal{B}((\mathbb{R}))$$

Proof.
From Th1.3.3, $$\mathcal{C} \subset \mathcal{M}$$, and Th1.3.2 says $$\mathcal{M}$$ is $$\sigma$$-algebra. Therefore, $$\sigma \langle \mathcal{C} \rangle \subset \mathcal{M}$$. Moreover, Th1.3.2 says $$\mu^*$$ restricted to $$\mathcal{M}$$ is measure, so $$\mu^*$$ is a measure on $$\sigma \langle \mathcal{C} \rangle = \mathcal{B}((\mathbb{R}))$$

>  $$\mu_F= \mu$$ on $$\mathcal{C}$$

>$$F(x+) = F(x)$$

Proof.
when $$x \gt 0$$
$$\{(0, x + 1/n]\}_{n \ge 1}$$ is monotonically decreasing and $$\bigcup_{n \ge 1}(0, x+ 1/n] = (0,x] \in \mathcal{B}(\mathbb{R})$$. By [Prop1-2-3](#Prop1-2-3) Monotone continuity from below,
$$
	F(x+) = \lim_{n \rightarrow \infty} \mu\big(
					(0, x+ 1/n]
				\big)
			=\mu \big(
					(0,x]
				\big)
			= F(x)
$$
when $$x = 0$$
For the same reason, $$F(0+) = F(0)$$

when $$x \lt 0$$
We take $$N \in \mathbb{N}$$ with $$x + 1/N \lt 0$$. Then,
$$\{(x+ \frac{1}{N+n},0]\}_{n \ge 1}$$ is monotonically increasing. By Prop 1.2.3, 
$$
F(x+) 
= \lim_{n \rightarrow \infty} \mu\big(
		(x+ \frac{1}{N+n}, 0]
	\big) 
= \mu \big(
		(x,0]
	\big)
= F(x)
$$

> $$\mu_F= \mu$$ on $$\mathcal{C}$$

Proof.
$$\mu_F\big((a,b]\big) = F(b+) - F(a+) = F(b) - F(a)$$
$$
\begin{align*}
	F(b) - F(a) = \begin{cases}
			\mu \big((0,b]\big) - \mu \big((0,a]\big)
				\quad (0 \le a \le b)\\
			\mu \big((0,b]\big) + \mu \big((a,0]\big)
				\quad (a \le 0 \le b)\\
			\mu \big((b,0]\big) + \mu \big((a,0]\big)
				\quad (a \le b \le 0)\\
		\end{cases}
\end{align*}
$$
If we care $$[0,b) = (0, a] \cup (a, b] \quad ( 0 \le a \le b)$$,
$$F(b) - F(a) = \mu \big((a,b]\big)$$
Simiraly,
$$
\begin{align*}
	\mu_F\big((a, \infty]\big) &= F(\infty) - F(a+)\\
		&= F(\infty) - F(a)\\
		&= \mu \big((a, \infty]\big)
\end{align*}
$$


$$
\begin{align*}
	F(b) - F(a) &= F(b) - F(c) + F(c) - F(a)\\
		&\lt \Big( \sum_{i=1}^K F(b_i) - F(a_i)\Big) + 2 \eta\\
		& \le \Big( \sum_{i=1}^{\infty} F(b_i) - F(a_i)\Big) + 2 \eta
\end{align*}
$$
