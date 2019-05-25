[TOC]

## 定義

### 各点収束

> Def(各点収束)
>
> $$S$$:集合, $$(M,d)$$:距離空間,任意の$$n \in \mathbb{N}_{>0}$$に対して$$f_n : S \to M$$とする.
>
> このとき関数列$$\{ f_n\}_{n=1}^{\infty}$$が$$f:S \to M$$に各点収束するとは,
>
> 任意の$$x \in S$$に対して,

$$
\lim_{n \to \infty} f_n(x) = f(x)
$$

> が成立することをいう.
>
> すなわち任意の$$x \in S$$と$$\epsilon > 0$$に対して,$$N \in \mathbb{N}_{>0}$$が存在して

$$
n > N \Rightarrow d(f_n(x), f(x)) < \epsilon
$$

> が成立することをいう.
>
> また,単に関数列$$\{ f_n\}_{n=1}^{\infty}$$が各点収束するとは
>
> 関数$$f:S \to M$$が存在して$$\{ f_n\}_{n=1}^{\infty}$$が$$f$$に各点収束することをいう.



### 一様収束

> Def(一様収束)
>
> $$S$$:集合, $$(M,d)$$:距離空間,任意の$$n \in \mathbb{N}_{>0}$$に対して$$f_n : S \to M$$とする.
>
> このとき関数列$$\{ f_n\}_{n=1}^{\infty}$$が$$f:S \to M$$に一様収束するとは,
>
> 任意の$$\epsilon >0$$に対し$$N \in \mathbb{N}_{>0}$$が存在し

$$
x \in S, n >N 
\Rightarrow 
d\left( f_n(x), f(x)\right) < \epsilon
$$

> が成立することをいう.
>
> また,単に関数列$$\{ f_n\}_{n=1}^{\infty}$$が一様収束するとは
>
> 関数$$f:S \to M$$が存在して$$\{ f_n\}_{n=1}^{\infty}$$が$$f$$に一様収束することをいう.



### 絶対一様収束

> Def(絶対一様収束)
>
> $$S$$:集合, $$(M,\| \cdot \|)$$:ノルム空間,任意の$$n \in \mathbb{N}_{>0}$$に対して$$f_n : S \to M$$とする.
>
> この時$$\sum_{n=1}^{\infty} f_n(x)$$が絶対一様収束するとは,
>
> $$S_n(x) := \sum_{k=1}^n \| f_k(x) \|$$と定義した時に$$\{S_n\}_{n=1}^{\infty}$$が一様収束することをいう.



## 定理

### 収束列の定数倍は収束列

> $$(X, \| \cdot \|)$$を$$K$$ ($$\mathbb{R}$$ or $$\mathbb{C}$$ )上のノルム空間とする.この時$$\{ x_n \}_{n \ge 1} \subset X$$が$$x$$に収束するなら,任意の$$\alpha \in K$$に対して$$\{\alpha x_n\}_{n \ge 1}$$は$$\alpha x$$に収束する

Proof.

$$\alpha = 0$$の時は自明なので,$$\alpha \ne 0$$に対して示す.任意の$$\epsilon >0$$に対して仮定より自然数$$N$$が存在して,$$n > N$$ならば$$\| x_n - x\| < \frac{\epsilon}{|\alpha|}$$が成立する.よって
$$
n > N 
\Rightarrow 
\| \alpha x_n - \alpha x \| = |\alpha| \|x_n - x \| < \epsilon
$$
より成立.

### 2つの収束列の和は収束列

> $$(X, \| \cdot \|)$$を$$K$$ ($$\mathbb{R}$$ or $$\mathbb{C}$$ )上のノルム空間とする.この時$$\{ x_n \}_{n \ge 1} \subset X$$が$$x$$に収束し,$$\{ y_n \}_{n \ge 1} \subset X$$が$$y$$に収束するなら,$$\{ x_n + y_n \}_{n \ge 1}$$は$$x + y$$に収束する



### 一様収束の同値条件

> $$S$$:集合, $$(M, d)$$:完備な距離空間, $$f_n : S \to M$$ ($$n \in \mathbb{N}_{>0}$$)
>
> この時以下は同値
>
> (1)関数列$$\{f_n \}$$は一様収束
>
> (2)$$\lim_{n,m \to \infty} d(f_n(x), f_m(x)) = 0$$
>
> つまり,任意の$$\epsilon >0$$に対して$$N \in \mathbb{N}_{>0}$$が存在して

$$
n,m > N, x \in S 
\Rightarrow
d (f_n(x), f_m(x)) < \epsilon
$$

> [証明の参考資料(日本語)](<http://www.math.keio.ac.jp/~iguchi/Lectures/pdf/2014/Note_MA_7.pdf>)

(Proof) 

(1)=>(2)

任意の$$\epsilon >0$$を1つ固定する.$$\{f_n\}$$は$$f:S \to M$$に一様収束しているとすると,$$N \in \mathbb{N}_{>0}$$が存在して
$$
n > N, x \in S \Rightarrow d(f_n(x), f(x)) < \frac{\epsilon}{2}
$$
が成立する.よって,
$$
n, m > N, x \in S 
\Rightarrow
d (f_n(x), f_m(x)) \le d(f_n(x), f(x)) + d(f(x), f_m(x)) < \epsilon
$$
(2)=>(1)

仮定より任意の$$x \in S$$に対して$$\{f_n(x)\}$$はCauchy列であるので,$$M$$の完備性より$$f_n(x)$$は収束する.よって関数$$f:S \to M$$を
$$
f(x) := \lim_{n \to \infty} f_n(x)
$$
によって定義する.

ここで$$\epsilon >0$$を任意に固定する.仮定より$$N \in \mathbb{N}_{>0}$$が存在して
$$
n, m > N, x \in S 
\Rightarrow
d(f_n(x), f_m(x)) < \frac{\epsilon}{2}
$$
が成立する.ここで任意に自然数$$n > N$$,$$x \in S$$をとると$$f_n(x)$$は$$f(x)$$に収束するので,

$$d(f(x), f_m(x)) < \epsilon / 2$$を満たす自然数$$m > N$$が存在する.ゆえに
$$
d(f(x), f_n(x))
\le
d(f(x), f_m(x)) + d(f_m(x), f_n(x))
< \epsilon
$$

### Mテスト

> $$S$$:集合, $$(M, \| \cdot \|)$$:Banach空間(完備なノルム空間), $$f_n : S \to M$$ ($$n \in \mathbb{N}_{>0}$$)
>
> 任意の$$x \in S$$と任意の$$n \in \mathbb{N}_{>0}$$に対して

$$
\| f_n(x) \| \le M_n
$$

> を満たす数列$$\{ M_n\}_{n=1}^{\infty}$$で無限級数$$\sum_{n=1}^{\infty} M_n$$が収束しているものが存在するとき,
>
> $$\sum_{n=1}^{\infty} f_n(x)$$は絶対一様収束する(特に一様収束もする)

(証明の方針)

 $$S_n := \sum_{k=1}^n \| f_k(x) \|$$と定義し[一様収束の同値条件](#一様収束の同値条件)の(2)が成立することを示す.

(Proof)

$$\epsilon >0$$を任意に固定する.$$\sum_{n=1}^{\infty} M_n$$が収束していることから特にCauchy列であるので,$$N \in \mathbb{N}_{>0}$$が存在して.
$$
n > m > N 
\Rightarrow 
\sum_{k=m+1}^n M_k < \epsilon
$$
が成立する.よって,$$n > m > N, x \in S$$ならば
$$
| S_n - S_m | 
= \left|
		\sum_{k=m+1}^n \| f_k(x) \|
	\right|
= \sum_{k=m+1}^n \| f_k(x) \|
\le \sum_{k=m+1}^n M_k < \epsilon
$$
より$$S_n$$は一様収束する.すなわち,$$\sum_{n=1}^{\infty} f_n(x)$$は絶対一様収束する.

一様収束することは,
$$
\left\|
	\sum_{k=m+1}^n f_n(x)
\right\| 
\le 
\sum_{k=m+1}^n
	\| f_n(x) \|
< \epsilon
$$
より自明([一様収束の同値条件](#一様収束の同値条件)を用いる).



### 各点収束先と一様収束先は一致する

> $$S$$:集合, $$(M,d)$$:距離空間,任意の$$n \in \mathbb{N}_{>0}$$に対して$$f_n : S \to M$$とする.
>
> (1)$$\{ f_n \}$$が$$f : S \to M$$に各点収束していて,
>
> (2)$$\{f_n\}$$が一様収束しているならば,
>
> $$\{f_n\}$$は$$f$$に一様収束している.

(Proof)

$$\{f_n\}$$が関数$$f':S \to M$$に一様収束しているとしてする.

この時,$$f \neq f'$$と仮定して矛盾を導く.

$$f  \neq f'$$とすると$$f(x_0) \neq f'(x_0)$$となる$$x_0 \in S$$が存在する.

この時,$$\epsilon := d(f(x_0), f'(x_0)) >0$$と定義する.

$$\{f_n\}$$は$$f'$$に一様収束しているので,$$N_1 \in \mathbb{N}_{>0}$$が存在して
$$
n > N_1 \Rightarrow d(f_n(x_0), f'(x_0)) < \frac{\epsilon}{2}
$$
が成立する.また,$$\{f_n\}$$は$$f$$に各点収束しているので,$$N_2 \in \mathbb{N}_{>0}$$が存在して
$$
n > N_2 \Rightarrow d(f(x_0), f_n(x_0)) < \frac{\epsilon}{2}
$$
が成立する.よって,$$n > \max \{N_1, N_2\} $$を満たす自然数$$n$$に対して
$$
d(f(x_0), f'(x_0)) 
\le d(f(x_0), f_n(x_0)) + d(f_n(x_0), f'(x_0)) 
< \epsilon
$$
が成立するがこれは$$\epsilon = d(f(x_0), f'(x_0))$$の定義に矛盾.



### 点列と関数列の極限の交換の定理

> Let $$(X,d_1)$$ be a metric space, $$(Y, d_2)$$ be a complete metric space, $$E \subset X$$ and $$p \in E'$$, the set of limit points of $$E$$. Let $$f : E \to Y$$, for each $$n \in \mathbb{N}$$, $$f_n: E \to Y$$ and assume that
>
> (H1) $$\lim_{n \to \infty} f_n(t) = f(t)$$ uniformly on $$E$$ and
>
> (H2) for each $$n \in \mathbb{N}$$, $$\lim_{t \to p} f_n(t) = A_n$$ exists
>
> Then
>
> (a) $$\lim_{n \to \infty} A_n = A$$ exists and
>
> (b)$$\lim_{t \to p} f(t) = A$$. That is, $$\lim_{t \to p} \lim_{n \to \infty} f_n(t) = \lim_{n \to \infty} \lim_{t \to p} f_n(t)$$

Proof (a)

$$A_n$$がCauchy列であることを示せば$$Y$$の完備性より収束することが示せるので,Cauchy列であることを示す.

任意の$$\epsilon > 0$$を固定する.$$f_n$$は$$f$$に一様収束するので自然数$$N$$が存在して$$E$$上の任意の点$$t$$に対して
$$
n > N
\Rightarrow
d_2\left(
	f_n(t), f(t)
\right) < \frac{\epsilon}{4}
$$
を満たす.ここで$$N$$より大きい自然数$$n,m$$をとると(H2)の条件より$$\delta >0$$が存在して
$$
d_1(t,p) < \delta
\Rightarrow
d_2(f_n(t), A_n) < \frac{\epsilon}{4},
d_2(f_m(t), A_m) < \frac{\epsilon}{4}
$$
$$p$$は$$E$$のlimit pointより$$d_1(t,p) < \delta$$を満たす点$$p \in E$$が存在するのでそれを1つ固定すると
$$
d_2(A_n, A_m)
\le
d_2\left(A_n, f_n(t)\right) + d_2\left(f_n(t), f(t)\right)
+ d_2\left(f(t), f_m(t)\right) + d_2\left(f_m(t), A_m\right)
< \epsilon
$$
Proof (b)

任意の$$\epsilon > 0$$を1つ固定する.条件(H1)より自然数$$N'$$が存在して$$E$$上の任意の点$$t$$に対して
$$
n > N'
\Rightarrow
d_2\left(
	f_n(t), f(t)
\right) < \frac{\epsilon}{３}
$$
を満たす.また(a)の結果より自然数$$N (>N')$$が存在して
$$
n > N \Rightarrow d_2(A_n, A) < \frac{\epsilon}{3}
$$
となる.$$n > N_2 (> N_1)$$を満たす自然数$$n$$を1つ固定すると条件(H2)より$$\delta >0$$が存在して
$$
d_1(t,p) < \delta
\Rightarrow
d_2(f_n(t), A_n) < \frac{\epsilon}{3}
$$
を満たす.ゆえに
$$
d_1(t,p) < \delta
\Rightarrow
d_2 (f(t), A) 
\le
d_2(f(t), f_n(t)) + d_2(f_n(t), A_n) + d_2(A_n, A) < \epsilon
$$


### 有限和と極限の交換

> $$(X, \| \cdot \|)$$をノルム空間, $$I$$を有限集合,$$a_{i j} \in X \quad (i \in I, j \in \mathbb{N}_{>0})$$とする.
>
> (H0)任意の$$i \in I$$に対して$$\sum_{j=1}^{\infty} a_{ij}$$が収束するならば,
>
> $$\lim_{m \to \infty} \left(  \sum_{i \in I} \sum_{j=1}^m a_{ij}\right)$$は$$\sum_{i \in I} \sum_{j=1}^{\infty} a_{ij}$$に収束する

(Proof.)

$$A_i := \sum_{j=1}^{\infty} a_{ij}$$と定義する.また$$I$$は空集合ではない(つまり$$0 < |I| < \infty$$)とする.

$$\epsilon >0$$を任意にとる.$$I$$は有限集合であることと条件(H0)を用いると,自然数$$N$$が存在して$$m > N$$ならば任意の$$i \in I$$に対して
$$
\left\| \sum_{j=1}^m a_{ij} - A_i \right\| < \frac{\epsilon}{|I|}
$$
が成立する.ゆえに$$m > N$$ならば
$$
\left\| 
	\sum_{i \in I} \sum_{j = 1}^m a_{ij} - \sum_{i \in I} A_i
\right \|
\le
\sum_{i \in I} 
	\left\|
		\sum_{j=1}^m a_{ij} - A_i
	\right\|
< \epsilon
$$



### 有限和と無限和の交換

> $$(X, \| \cdot \|)$$をノルム空間,$$a_{i j} \in X \quad (i \in \{1,\dots ,k\}, j \in \mathbb{N}_{>0})$$とする.
>
> 任意の$$i \in \{1,\dots,k\}$$に対して$$\sum_{j=1}^{\infty} a_{ij}$$が収束するならば

$$
\sum_{i=1}^k \sum_{j=1}^{\infty} a_{ij}
= \sum_{j=1}^{\infty} \sum_{i=1}^k a_{ij}
$$

> が成立する.

(Proof)

$$\epsilon >0$$を任意に固定する.

仮定より任意の$$i \in \{1,\dots,k\}$$に対して$$\sum_{j=1}^{\infty} a_{ij}$$は収束するので,自然数$$N$$が存在し,任意の$$i$$に対して,
$$
n > N \Rightarrow
\left\| 
	\sum_{j=1}^{\infty} a_{ij} - \sum_{j=1}^{n} a_{ij}
\right\| < \frac{\epsilon}{k}
$$
が成立する.よって,$$n > N$$ならば,
$$
\left\| 
	\sum_{j=1}^n \sum_{i=1}^k a_{ij} 
	- \sum_{i=1}^k \sum_{j=1}^{\infty} a_{ij}
\right\| 
=  \sum_{i=1}^k \left\|
		\sum_{j=1}^n a_{ij} - \sum_{j=1}^{\infty} a_{ij} 
		\right\| 
< \epsilon
$$


### 絶対収束するなら収束する

> $$(X, \| \cdot \| )$$をBanach空間(完備なノルム空間), 任意の自然数$$i$$に対して$$a_i \in X$$とする.
>
> この時$$\sum_{i=1}^{\infty} \| a_i \|$$が収束するなら$$\sum_{i=1}^{\infty} a_i$$も収束する.

(Proof.)

$$S_n := \sum_{i=1}^n a_i$$として$$S_n$$がCauchy列であることを示せば$$X$$の完備性より$$S_n$$が収束することを示せる.$$\epsilon >0$$を任意に1つ固定する.$$\sum_{i=1}^{\infty} \| a_i \|$$が収束するので$$\sum_{i=1}^n \|a_i\|$$はCauchy列でもある.よって自然数$$N>0$$が存在して$$N < m < n$$ならば
$$
\left| 
	\sum_{i=1}^n \| a_i\| - \sum_{i=1}^m \| a_i\|
\right|
=
\left| 
	\sum_{i=m+1}^n \| a_i\| 
\right|
=
\sum_{i=m+1}^n \| a_i\|
< \epsilon
$$
が成立する.よって
$$
\left\| 
	\sum_{i=1}^n  a_i - \sum_{i=1}^m  a_i
\right\|
=
\left\| 
	\sum_{i=m+1}^n  a_i
\right\|
=
\sum_{i=m+1}^n \| a_i\|
< \epsilon
$$
より$$S_n$$はCauchy列であるので収束する



### 無限和の交換

> Interchanging the order of Summation
>
> Let $$(X, \| \cdot \|)$$ be Banach space, $$a_{jk} \in X$$ ($$j, k \in \mathbb{N}_{>0}$$)
>
> If $$\sum_{j=1}^{\infty} \sum_{k=1}^{\infty} \| a_{jk} \| < \infty$$, then $$\sum_{j=1}^{\infty} \sum_{k=1}^{\infty}  a_{jk}  = \sum_{k=1}^{\infty} \sum_{j=1}^{\infty}  a_{jk}$$
>
> The hypothesis really means that 
>
> for each $$j \in \mathbb{N}_{>0}$$,$$\sum_{k=1}^{\infty} \| a_{jk} \| = M_j < \infty$$ and $$\sum_{j=1}^{\infty} M_j < \infty$$
>
> 例えば,有限次元ベクトル空間は任意のノルムに対してBanach spaceになるので,
>
> $$X$$として$$\mathbb{R}$$,絶対値をノルムとすることで定理を用いることができる.
>
> [参考資料 英語](http://www.math.ubc.ca/~feldman/m321/twosum.pdf))

(Proof)

方針:集合$$E$$,集積点$$p$$,関数$$f_n$$を適切に定めて,[点列と関数列の極限の交換の定理](#点列と関数列の極限の交換の定理)を用いる.



$$E:= \{1, \frac{1}{2}, \frac{1}{3}, \dots\}$$,$$p=0$$,任意の$$n, m \in \mathbb{N}_{>0}$$に対して$$t_m = \frac{1}{m}$$,$$f_n : E \to X$$を
$$
f_n(t_m) := \sum_{j=1}^n \sum_{k=1}^m a_{jk}
$$
と定義する.この時,$$f_n(t_m)$$が絶対収束(特に一様収束)することを示す.

任意の$$m, j \in \mathbb{N}_{>0}$$に対して
$$
\left\|
  \sum_{k=1}^m a_{jk}
\right\|
\le
\sum_{k=1}^{m} \| a_{jk} \|
\le 
\sum_{k=1}^{\infty} \| a_{jk} \| 
= M_j
$$
であり,仮定より$$\sum_{j=1}^{\infty} M_j $$は収束するので[Mテスト](#Mテスト)より$$f_n(t_m)$$は絶対収束する.

($$f_n(t_m) =  \sum_{j=1}^n g_j(m)$$と見なして定理を適用する)ので,特に$$f_n(t_m)$$は一様収束する.

また,任意の$$m \in \mathbb{N}_{>0}$$に対して,$$\left\|  \sum_{k=1}^m a_{jk}\right\| \le M_j$$であり$$\sum_{j=1} M_j$$は収束するので,

[絶対収束するなら収束する](#絶対収束するなら収束する)より$$ \sum_{j=1}^{\infty} \sum_{k=1}^m a_{jk}$$は収束する.よって,$$f: E \to X$$を
$$
f(t_m) := \sum_{j=1}^{\infty} \sum_{k=1}^m a_{jk}
$$
と定義することができる.

次に$$f_n$$が$$f$$に各点収束することを示す.

任意の$$\epsilon >0$$と$$m \in \mathbb{N}_{>0}$$を固定する.関数$$f$$の定義より$$N \in \mathbb{N}_{>0}$$が存在して,
$$
n > N \Rightarrow 
\left\|
	\sum_{j=1}^{\infty} \sum_{k=1}^m a_{jk} - \sum_{j=1}^{n} \sum_{k=1}^m a_{jk}
\right\| < \epsilon
\Rightarrow
\|
	f(t_m) - f_n(t_m) 
\| < \epsilon
$$
より,$$f_n$$は$$f$$に各点収束する.ゆえに,[各点収束先と一様収束先は一致する](#各点収束先と一様収束先は一致する)より$$f_n$$は$$f$$に一様収束していることが分かる.

また,任意の$$j \in \mathbb{N}_{>0}$$に対して$$ \sum_{k=1}^m \|a_{jk}\| \le M_j$$ ($$\forall m \in \mathbb{N}_{>0}$$)であるので上に有界.よって$$\sum_{k=1}^{\infty} \left\|a_{jk}\right\|$$は収束するので,特に$$\sum_{k=1}^{\infty} a_{jk}$$も収束する.よって,[有限和と極限の交換](#有限和と極限の交換)より,
$$
\lim_{m \to \infty} f_n(t_m) 
= \lim_{m \to \infty} 
\left(
	\sum_{j=1}^{n} \sum_{k=1}^m a_{jk}
\right)
= \sum_{j=1}^{n} \sum_{k=1}^{\infty} a_{jk} 
= A_n
$$
次に$$\lim_{t \to 0 } f_n(t) = A_n$$であることを証明する.

任意に$$\epsilon >0$$を1つ固定する.$$ \lim_{m \to \infty} f_n(t_m)$$は$$A_n$$に収束するので,自然数$$N$$が存在して,
$$
m > N 
\Rightarrow 
\left\| f_n(t_m) - A_n \right\| < \epsilon
$$
ここで
$$
m > N 
\Leftrightarrow
t_m = \frac{1}{m} < \frac{1}{N}
\Leftrightarrow
t_m \in \left\{
	\frac{1}{N+1}, \frac{1}{N+2},\dots
	\right\}
$$
であるので,$$\delta = \frac{1}{N}$$とすると,
$$
(t \in E ) \land (|t| < \delta) 
\Rightarrow
t \in \left\{
	\frac{1}{N+1}, \frac{1}{N+2},\dots
	\right\}
\Rightarrow
\left\| f_n(t) - A_n \right\| < \epsilon
$$
より証明できた.

これまでの議論より(H1)$$f_n$$は$$f$$に一様収束しており,(H2)$$\lim_{t \to 0 } f_n(t) = A_n$$が存在することから,[点列と関数列の極限の交換の定理](#点列と関数列の極限の交換の定理)より,
$$
\lim_{n \to \infty} A_n 
= \lim_{n \to \infty} 
	\left(
		\sum_{j=1}^n
			\lim_{m \to \infty}
				\left(
					\sum_{k=1}^m a_{jk}
				\right)
	\right)
= \lim_{n \to \infty} \lim_{m \to \infty}
	\sum_{j=1}^n \sum_{k=1}^m a_{jk}
= A
$$
が存在し,
$$
\lim_{t \to 0} f(t)= A
$$
が成立,また$$\lim_{m \to \infty}  f(t_m) = A$$である.実際,任意に$$\epsilon >0$$に対して,$$\lim_{t \to 0} f(t)= A$$であるので,正の数$$\delta >0$$が存在して
$$
t < \delta \Rightarrow \| f(t) - A \| < \epsilon
$$
であり,自然数$$N$$を$$\frac{1}{N} < \delta$$を満たすように1つとると,
$$
m > N \Rightarrow
t_m = \frac{1}{m} < \frac{1}{N} < \delta
\Rightarrow
\| f(t_m) - A\| < \epsilon
$$
また,
$$
\lim_{m \to \infty}  f(t_m)
= \lim_{m \to \infty}  
	\left(
		\sum_{j=1}^{\infty} \sum_{k=1}^m a_{jk}
	\right)
= \lim_{m \to \infty}
	\left(
		\lim_{n \to \infty}
			\left(
				\sum_{j=1}^{n} \sum_{k=1}^m a_{jk}
			\right)
	\right)
= \lim_{m \to \infty} \lim_{n \to \infty}
	\sum_{j=1}^{n} \sum_{k=1}^m a_{jk}
$$
であるので
$$
\lim_{m \to \infty} \lim_{n \to \infty}
	\sum_{j=1}^{n} \sum_{k=1}^m a_{jk}
= \lim_{n \to \infty} \lim_{m \to \infty}
	\sum_{j=1}^{n} \sum_{k=1}^m a_{jk}
$$
次に左辺と右辺を無限級数の形に変形する.

まず左辺について

任意の$$k,n \in \mathbb{N}_{>0}$$に対して,
$$
\sum_{j=1}^n \| a_{jk} \|
\le 
\sum_{j=1}^n \sum_{\ell=1}^k \| a_{j \ell} \|
\le
\sum_{j=1}^n M_j
\le
\sum_{j=1}^{\infty} M_j < \infty
$$
であるので,任意の$$k \in \mathbb{N}_{>0}$$に対して,$$\sum_{j=1}^{\infty} \| a_{jk} \|$$は有界であり上限に収束する.よって,$$\sum_{j=1}^{\infty}  a_{jk} $$も収束するので,
$$
\lim_{m \to \infty} \lim_{n \to \infty}
	\sum_{j=1}^{n} \sum_{k=1}^m a_{jk}
= \lim_{m \to \infty} \lim_{n \to \infty}
	\sum_{k=1}^{m} \sum_{j=1}^n a_{jk}
= \lim_{m \to \infty} 
	\sum_{k=1}^{m} \sum_{j=1}^{\infty} a_{jk}
= \sum_{k=1}^{\infty} \sum_{j=1}^{\infty} a_{jk}
$$

次に右辺について

任意の$$j \in \mathbb{N}_{>0}$$に対して$$\sum_{k=1}^{\infty} a_{jk}$$も収束するのであったから,
$$
\lim_{n \to \infty} \lim_{m \to \infty}
	\sum_{j=1}^{n} \sum_{k=1}^m a_{jk}
= \lim_{m \to \infty} 
	\sum_{j=1}^{n} \sum_{k=1}^{\infty} a_{jk}
= \sum_{j=1}^{\infty} \sum_{k=1}^{\infty} a_{jk}
$$
