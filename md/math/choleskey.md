### コレスキー分解の補足

> Assume $$K = \mathbb{R} \text{ or } \mathbb{C}$$, $$A \in K^{(n+1) \times (n+1)}$$ is *positive definite and Hermite*. Write

$$
A = 
\left(
	\begin{array}{c}
		a_{11} & A_{12}\\
		A_{21} & A_{22}
	\end{array}
\right)
$$

> with $$a_{11} \in K,  A_{21} = A_{12}^*$$, and $$A_{22} = K^{n \times n}$$, and *define* the Schur complement of $$A$$ with respect to $$a_{11}$$ as 
>
> $$ S = A_{22} - \frac{1}{a_{11}} A_{21} A_{12}$$.
>
> Then also $$S$$ is positive definite and Hermite.

Proof.

$$A$$はpositive definiteより,主行列式(*minor of a matrix* $$A$$)は全て正であるので特に$$a_{11}$$は正.よって$$S$$は定義できることに注意.エルミート性(Hermite)は自明であるので,positive definiteであることのみ示す.

任意に$$x \in K^{n} \setminus \{ \boldsymbol{0} \}$$をとり,$$y \in  K^{n+1}$$を以下のように定義する.
$$
y =
\left(
	\begin{array}{c}
		-\frac{1}{a_{11}} A_{12} x\\
		x
	\end{array}
\right)
$$
この時$$y \neq \boldsymbol{0}$$であるので$$A$$の正定値性から$$y^* A y > 0$$である.一方,Schur complementの定義より
$$
A =
\left(
	\begin{array}{c}
		1 & 0\\
		\frac{1}{a_{11}}A_{21} & \boldsymbol{I}
	\end{array}
\right)
\left(
	\begin{array}{c}
		a_{11} & 0\\
		0 & S
	\end{array}
\right)
\left(
	\begin{array}{c}
		1 & \frac{1}{a_{11}} A_{12}\\
		0 & \boldsymbol{I}
	\end{array}
\right)
$$
であることに注意すると,
$$
\begin{align*}
y^* A y
&= \left(
	\begin{array}{c}
		-\frac{1}{a_{11}} x^* A_{12}^* & x^*\\
	\end{array}
	\right)
	\left(
	\begin{array}{c}
		1 & 0\\
		\frac{1}{a_{11}}A_{21} & \boldsymbol{I}
	\end{array}
	\right)
	\left(
	\begin{array}{c}
		a_{11} & 0\\
		0 & S
	\end{array}
	\right)
	\left(
	\begin{array}{c}
		1 & \frac{1}{a_{11}} A_{12}\\
		0 & \boldsymbol{I}
	\end{array}
	\right)
	\left(
	\begin{array}{c}
		-\frac{1}{a_{11}} A_{12} x\\
		x
	\end{array}
	\right)\\
&= \left(
	\begin{array}{c}
		0 & x^*\\
	\end{array}
	\right)
	\left(
	\begin{array}{c}
		a_{11} & 0\\
		0 & S
	\end{array}
	\right)
	\left(
	\begin{array}{c}
		0\\
		x
	\end{array}
	\right)\\	
&= x^* S x
\end{align*}
$$
よって,$$S$$はpositive definiteである.



### コレスキー分解

> Let $$K = \mathbb{R} \text{ or } \mathbb{C}$$
>
> An *invertible* matrix $$A \in K^{n \times n}$$ admits a *Choleskey factorization* $$A = L L^*$$ with a *lower triangular matrix* $$L \in K^{n \times n}$$, if and only if $$A$$ is *Hermite* and *positive definite*.

(Proof)

$$A = L L^*$$と表せたとする.$$A$$のHermite性は簡単に示せるので省略.positive definite性のみ示す.$$x \in K^{n} \setminus \{ \boldsymbol{0} \}$$を任意にとると
$$
x^* A x = \| L^* x \|_2^2
$$
である.また$$A$$はinvertibleであるので$$\det A \ne 0$$である.よって,
$$
0 \ne \det A = \det L L^* = \det L \det L^* = \| \det L^* \|^2
$$
であるので,$$\det L^* \ne 0$$.ゆえに$$L^*$$はinvertibleであるので$$L^* x \ne 0$$.よって$$x^* A x > 0$$,つまり$$A$$はpositive definite.

次に$$A$$がHermiteかつ正定値である時に$$A = L L^*$$を満たす.lower trianguler matrix $$L \in K^{n \times n}$$が存在することを$$n$$に関する帰納法で示す.

[1] $$n=1$$のとき

$$A = (a)$$とすると,$$A$$が正定値であることから,主行列式(*minor of a matrix* $$A$$)は全て正であるので特に$$a >0$$.よって,$$L = (\sqrt{a})$$と置けば良い.

[2] $$n$$のとき成立していると仮定するとき,$$n+1$$でも成立することを示す.
$$
A = 
\left(
	\begin{array}{c}
		a_{11} & A_{12}\\
		A_{21} & A_{22}
	\end{array}
\right)
$$
with $$a_{11} \in K,  A_{21} = A_{12}^*$$, and $$A_{22} = K^{n \times n}$$,
$$
S = A_{22} - \frac{1}{a_{11}} A_{21} A_{12}
$$
と定義する.この時[コレスキー分解の補足](#コレスキー分解の補足)より$$S \in K^{n \times n}$$は正定値エルミート行列である.よって,帰納法の仮定より$$S = L_S L_S^*$$を満たすlower triangular matrix $$L_S \in K^{n \times n}$$が存在する.$$A$$が正定値であることから$$a_{11} >0$$であることに注意すると
$$
L \equiv 
\left(
	\begin{array}{c}
		\sqrt{a_{11}} & 0\\
		\frac{1}{\sqrt{a_{11}}} A_{21} & L_S
	\end{array}
\right)
$$
とすることでlower triangular matrix $$L$$を定義することができて,簡単な計算から$$L L^* = A$$を示せる.





