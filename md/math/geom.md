[TOC]

### Def(Parallelepipeds)平行多面体

> [Voumes of Parallelepipeds(p4~)](https://www.math.uchicago.edu/~may/VIGRE/VIGRE2007/REUPapers/FINALAPP/Peng.pdf)をまとめた[リンク切れ用](https://www.slideshare.net/secret/GOdfssO2gnHbzb)
>
> シュミットの直交対角化を復習しながら読めば30分~2時間以内に読み終わると思う.
> p4 Volumes of Parallelepipedsから読めばOK
>
> Let $$a, x_1, \dots ,x_k \in \mathbb{R}^n$$. Then $$k$$-dimensional parallelepiped in vector space $$\mathbb{R}^n$$ is defined as
>
> $$P \equiv \{ a + t_1x_1 + \cdots + t_k x_k \mid 0 \le t_i \le 1, i=1,\dots,k\}$$
>
> where the vectors $$x_1,\dots,x_k$$ are called edges of $$P$$.
>
>
> The **volume** of $$P$$ is the product of a certain "base" and "altitude" of $$P$$. The *base* of $$P$$ is the volume of the $$(k-1)$$-dimensional parallelepiped with edges $$x_2,\dots ,x_k$$. The [lemma1(Voumes of Parallelepipeds, p4)](https://www.math.uchicago.edu/~may/VIGRE/VIGRE2007/REUPapers/FINALAPP/Peng.pdf) gives $$x_1 = B + C$$  so that $$B$$ is orthogonal to all of the $$x_i, i \ge 2$$ and $$C$$ is in the span of the $$x_i, i \ge 2$$. The *altitude* is the length of $$B$$.
>
> Note:
>
> * The volume of $$1$$-dimensional parallelepiped is defined the length of the edge.
> * The volume is independent on ordering of the vertices.(showing below)
>
> [Threorem7](Voumes of Parallelepipeds, p5)
>
> n次元の平行多面体の体積は多面体を構成するベクトルを並べた行列の行列式の絶対値で与えられる
>
> Given an $$m$$-dimensional parallelepiped in $$\mathbb{R}^n$$, whose edges are $$\alpha_1, \dots, \alpha_m \in \mathbb{R^n}$$. Define $$A$$ as 

$$
A \equiv \left(
		\begin{array}{c}
			\alpha_1\\
			\vdots\\
			\alpha_m
		\end{array}
	\right)
$$

> Then $$\text{vol}(P)^2 = \det(AA^T)$$.
>
> また,定義通り計算することで**平行多面体のアフィン変換による像は平行多面体であることが示される**



### Def(ellipsoid)

> An ellipsoid, centered $$\boldsymbol{v}$$, is defined by the solutions to $$\mathbf{x}$$ to the equation
>
> $$( \boldsymbol{x} - \boldsymbol{v} )^T A  ( \boldsymbol{x} - \boldsymbol{v} ) = 1$$
>
> where $$A$$ is a positive definite matrix.

直感的な理解.$$A$$はpositive definiteより[コレスキー分解](./choleskey.md#コレスキー分解)によって$$A=LL^T$$を満たす下三角行列$$L$$が存在する.よって,方程式は$$ \| L^T ( \boldsymbol{x} - \boldsymbol{v} ) \|_2^2 = 1$$となる.$$A$$がpositive definiteであることから$$L^T$$はinvertibleである.よって,$$\boldsymbol{y} \equiv \boldsymbol{x} - \boldsymbol{v}$$,$$\boldsymbol{z} \equiv L^T \boldsymbol{y}$$と定義すると$$\| \boldsymbol{z} \|_2^2 = 1$$であることから,$$\boldsymbol{y} \equiv (L^T)^{-1} \boldsymbol{z}$$は原点を中心としたellipsoidを表す.よって,$$\boldsymbol{x} = \boldsymbol{y} + \boldsymbol{v}$$は中心が$$\boldsymbol{v}$$のellipsoidを表す.



### 楕円のアフィン変換は楕円

> Let $$f:\mathbb{R}^n \to \mathbb{R}^n$$ be an affine map. Then, from [the definiton of affine map](./group#Def(affine_map)), there exists $$A \in \mathbb{R}^{n \times n}, b \in \mathbb{R}^n$$ such that $$f(x) = Ax +b$$. Then, if $$A$$ is invertible
>
> (1) $$f$$ maps an ellipse to an ellipse.

Proof (1)

$$x$$が中心$$v \in \mathbb{R}^n$$,正定値行列$$\Sigma  \in \mathbb{R}^{n \times n}$$によって特徴付けられた[楕円上の点](#Def(ellipsoid))つまり,

$$(x - v)^T \Sigma  ( x - v) = 1$$

を満たすとする.この時,$$y \equiv f(x) = Ax +b$$と定義すると$$x = A^{-1}(y -b)$$であるので上式に代入することで
$$
(y - (Av +b))^T (A^{-1})^T \Sigma A^{-1} (y - (Av+b)) = 1
$$
となる.ここで,任意の$$z \in \mathbb{R}^n \setminus \boldsymbol{0}$$に対して$$\Sigma$$が正定値であることに注意すると,
$$
z^T (A^{-1})^T \Sigma A^{-1} z
= (A^{-1}z)^T \Sigma (A^{-1}z) 
> 0
$$
であるので,$$(A^{-1})^T \Sigma A^{-1}$$も正定値である.よって$$y$$は中心$$Av +b$$,正定値行列$$(A^{-1})^T \Sigma A^{-1}$$によって特徴づけられた楕円上の点である.

逆に$$y \in \mathbb{R}^n$$が
$$
(y - (Av +b))^T (A^{-1})^T \Sigma A^{-1} (y - (Av+b)) = 1
$$
を満たしているとする.この時,$$x \equiv A^{-1}(y -b)$$と定義すると$$f(x) = y$$であり$$(x -v)^T \Sigma (x -v) = 1$$が$$y$$に代入することで示せる.ゆえに,
$$
\begin{align*}
	&\{ f(x) \mid x \in \mathbb{R}^n \text{ with } (x - v)^T \Sigma  ( x - v) = 1\}\\
	=
	&\{y \in \mathbb{R}^n \mid 
		(y - (Av +b))^T (A^{-1})^T \Sigma A^{-1} (y - (Av+b)) = 1
	\}
\end{align*}
$$
であるので上記は示せた.





### 