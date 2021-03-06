[TOC]

### Def(field)

> A *field* is a set $$F$$ together with two operations
>
> *addition*:$$F \times F \to F:(a,b) \mapsto a+b$$ and
>
> *multiplication*:$$F \times F \to F: (a,b) \mapsto a \cdot b$$
>
> satisfying the following properties for $$\forall a,b,c \in F$$
>
> * **Associativity** of addition and multiplication:
>
>   $$a+(b+c) = (a+b) + c$$ and $$a \cdot (b \cdot c) = (a \cdot b) \cdot c$$.
>
> * **Commutativity** of addition and multiplication:
>
>   $$a+b = b + a$$ and $$a \cdot b = b \cdot a$$
>
> * Additive and multicative **identity**:
>
>   $$\exists 0, 1 \in F$$ such that $$a+0 = a$$ and $$a \cdot 1 = a$$.
>
> * **Additive inverses**:
>
>   $$\forall a \in F, \exists -a \in F$$, called the *additive inverse* of $$a$$, such that $$a + (-a) = 0$$.
>
> * **Multiplicative inverses**:
>
>   $$\forall a \in F \text{ with } a \neq 0, \exists a^{-1} \in F$$, called *multiplicative inverse* of $$a$$ such that $$a \cdot a^{-1} = 1$$.
>
> * **Distibutivity** of multiplication over addition:
>
>   $$a \cdot (b + c) = (a \cdot b) + (a \cdot c)$$.
>
> Note:
>
> * $$a + b$$ is called the *sum* of $$a$$ and $$b$$.
> * $$a \cdot b$$ is called the *product* of $$a$$ and $$b$$.
>
> 上記の定義から以下は簡単に示せる(証明略)
>
> $$a \cdot 0 = 0,-a = (-1)  \cdot a \quad \forall a \in A$$
>
> $$ab=0 \Rightarrow a = 0 \lor b = 0 \quad \forall a, b \in A$$



### Def(absolute_value)

> A real-valued function $$v$$ on a field $$F$$ is called an **absolute value** if it satisfied the following four axioms.
>
> * Non-negativity
>
>   $$v(a) \ge 0$$
>
> * Positive-definiteness
>
>   $$v(a) = 0 \Leftrightarrow a = \boldsymbol{0}$$
>
> * Multiplicativity
>
>   $$v(ab) = v(a) v(b)$$
>
> * Subadditivity or the triangle inequality
>
>   $$v(a+b) \le v(a) + v(b)$$
>
> Where $$\boldsymbol{0}$$ donotes the additive identity element of $$F$$.
>
> * It follows from positive-definiteness and multiplicativity that $$v(\boldsymbol{1}) = 1$$, where $$\boldsymbol{1}$$ denotes the multiplicative identity element of $$F$$(証明略).
> * $$v(-a) = v(a)$$ for every $$a \in F$$(下記に証明)
>
> If $$v$$ is an absolute value on $$F$$, then the function $$d$$ on $$F \times F$$, defined by $$d(a,b) \equiv v(a -b)$$, is a metric(証明略). 

$$v(-a) = v(a)$$ for every $$a \in F$$であることを示す.

$$1 = v(\boldsymbol{1}) = v(-\boldsymbol{1} \cdot -\boldsymbol{1}) = v(-\boldsymbol{1}) v(-\boldsymbol{1})$$

であるので,$$v(-\boldsymbol{1}) = 1$$であることに注意すると,任意の$$a \in F$$に対して$$v(-a) = v(-\boldsymbol{1} \cdot a) = v(-\boldsymbol{1}) v(a) = v(a)$$



### Def(valued_field)

> $$(K, | \cdot |)$$ is called a **valued field** if $$K$$ is a field and $$| \cdot |: K \to \mathbb{R}$$ is an absolute value.



### Def(vector)

> A *vector space* over a filed $$F$$ is a set $$V$$ together with two operations 
>
> * *vector addition*(or simply *addition*):$$V \times V \to V:(v,w) \mapsto v + w$$
> * *scalar multiplication* $$F \times V \to V: (a,v) \mapsto av$$
>
> that satisfy the eight axioms listed below.
>
> 1. **Associativity** of addition:
>
>    $$u + (v + w) = (u+v) +w  \quad \forall u,v,w \in V$$
>
> 2.  **Commutativity** of addition:
>
>    $$u + v = v + u \quad \forall u, v \in V$$
>
> 3. **Identity element** of addition:
>
>    $$\exists \mathbf{0} \in V$$, called the *zero vector*, such that $$v + \mathbf{0} = v$$  for all $$ v \in V$$
>
> 4. **Inverse elements** of addition:
>
>    $$\forall v \in V, \exists -v \in V$$, called the *additive inverse* of $$v$$, such that $$v + (-v) = \mathbf{0}$$.
>
> 5.  **Compatibility** of scalar multiplication with field multiplication:
>
>    $$a(bv) = (ab)v \quad \forall a,b \in F, v \in V$$
>
> 6. Identity element of scalar multiplication:
>
>    $$1 v = v \quad \forall v \in V$$, where $$1$$ denotes the *multiplicative identity* in $$F$$.
>
> 7. **Distributivity** of scalar multiplication with respect to vector addition:
>
>    $$ a(u+v) = au + av \quad \forall a \in F, u,v \in V$$
>
> 8. Distributivity of scalar multiplication with respect to field addition
>
>    $$(a+b)v = av + bv$$
>
> Note
>
> * Elements of $V$ are commoly colled *vectors*.
> * Elements of $$F$$ are commonly called scalars.
>
> 上記の定義から以下は簡単に示せる.
>
> $$0 \cdot v  = \mathbf{0} \quad \forall v \in V$$ where $$0$$ is additive identity in $$F$$.
>
> $$(-1)v = -v \quad \forall v \in V$$ Where $$-1$$ is additive inverse of the multiplicative identity in $$F$$.



### Def(Linear_subspace)

> If $$V$$ is a vector space over a field $$K$$ and if $$W$$ is a subset of $$V$$, then $$W$$ is a *subspace* of $$V$$ if under operations of $$V, W$$ is a vector space over $$K$$.
>
> Equivalently, a noempty subset $$W$$ is a subspace of $$V$$ if
>
> $$\forall w_1, w_2 \in W \text{ and } \forall a, b \in K \Rightarrow a w_1 + b w_2 \in W $$
>
> 同値性は容易に示せるので省略



### Def(codimension)

> If $$W$$ is a linear subspace of a finite-dimensional vector space $$V$$, then the codimension of $$W$$ in $$V$$ is the difference between the dimensions:
>
> $$\text{codim}(W) = \dim (V) - \dim(W)$$



### Def(maximal_proper_subspace)

> A (proper) *linear subspace* is said to be **maximal proper subspace** if its any proper superset is (original) *linear space*.
>
> * The dimension of maximal proper subspace of $$n$$-dimensional linear space is $$n-1$$.(証明略)
> * A linear subspace $$W$$ of finite-dimensional vector space $$V$$ is maximal proper subspace if and only if the codimension of $$W$$ is one.

(2つ目のProof)

$$W$$のcodimensionが1である時にmaximal proper subspaceであることを証明する.

$$W$$の基底を$$e_1,\dots e_{n-1}$$と表すことにする.$$W$$を真に含む任意のlinear subspace$$M$$は$$W$$に含まれていない元を少なくとも1つは含んでいるのでそれを$$e_n$$とする.この時$$e_1, \dots ,e_n$$は一次独立である(背理法で示せる)であるので元の線形空間$$V$$の基底である.また$$M$$はlinear subspaceであるので$$e_1, \dots ,e_n$$ によって張られる空間を$$M$$は含んでおり,$$e_1, \dots e_n$$は$$V$$の基底であったので,$$M = V$$である.ゆえに$$W$$はmaximal proper subspaceである.



### 内積空間inner_product_space

> 内積空間(inner product space)
>
> An inner product space is a vector space $$V$$ over the fielf $$F$$ ($$\mathbb{R}$$ or $$\mathbb{C}$$) together with an inner product $$\langle \cdot , \cdot \rangle: V \times V \to F$$ that satisfies the following three properties for ll vectors $$x,y,z \in V$$ and all scholars $$a \in F$$.
>
> * Conjugate symmetry.
>
>   $$\langle x, y \rangle = \overline{\langle x, y \rangle}$$
>
> * Linearity in the first argument:
>
>   $$\langle a x, y \rangle = a \langle x, y \rangle$$
>
>   $$\langle x + y , z \rangle = \langle x ,z \rangle + \langle y, z \rangle$$
>
> * Positive definite:
>
>   $$\langle x, x \rangle > 0$$, $$x \in V \setminus \{ \mathbf{0} \}$$



### 内積空間の連続性

> Let $$(V, \langle \cdot , \cdot \rangle)$$ be an inner product space over a field $$\mathbb{R}$$ or $$\mathbb{C}$$ and $$a \in V$$.
>
> Then the function $$f: V \to K : x \mapsto \langle a,  x \rangle$$ is continuous.

It is easy to prove by using Cauchy-Schwarz inequality, hence the proof is left to a reader.



### 内積空間上の点と線分の距離

> Let $$(V, \langle \cdot , \cdot \rangle)$$ be an inner product space over a field $$\mathbb{R}$$ or $$\mathbb{C}$$.
>
> Then we consider the distance between a point $$p \in V$$ and the segment $$a + t n$$ where $$a,n \in V$$ with $$\| n \| = 1$$ and $$t \in [c,d]$$.  

最初に点$$p$$と直線上の点$$a + t n (t \in \mathbb{R})$$の距離を考える.
$$
\begin{align*}
	\| a + t n - p\|^2
	&= \langle tn + (a - p), tn + (a - p) \rangle\\
	&= t^2 \| n \|^2 
		+ t ( \langle n, a- p \rangle + \overline{ \langle n, a - p \rangle}) 
		+ \| a - p \|^2
\end{align*}
$$
よって,$$\langle n , a-p \rangle$$の実部を$$\alpha$$,$$\beta \equiv \| a - p \|^2 \ge 0$$と定義すると,
$$
\| a + t n - p\|^2
	= t^2 + 2 \alpha t + \beta
	= (t + \alpha)^2 + \beta - \alpha^2
$$
であるので,点$$p$$と最も距離が小さい直線上の点$$a_0$$は.
$$
a_0 
= a - \alpha n = a - \frac{1}{2}( \langle n, a- p \rangle + \overline{ \langle n, a - p \rangle})n
$$
である.この時,
$$
\langle a_0 - p , n \rangle
= \langle
		(a - p) - \frac{1}{2} \langle n, a - p \rangle n
			- \frac{1}{2}  \overline{ \langle n, a - p \rangle}n,
		n\rangle
= \frac{1}{2}(
		\langle a - p , n \rangle - 
		\overline{\langle a - p, n \rangle} 
	)
		
$$
となるので,$$V$$が$$\mathbb{R}$$上の内積空間ならベクトル$$a_0 - p$$と$$n$$は直行する.

逆に直線上の点$$a_t \equiv a + tn$$とすると,
$$
\langle a_t - p, n \rangle 
= \langle (a - p) + tn, n \rangle
= \langle a -p , n \rangle + t
$$
であるので,ベクトル$$a_t - p$$と$$n$$が直交するとき,$$t = - \langle a - p , n \rangle$$である.

よって,$$V$$が$$\mathbb{R}$$上の内積空間なら点$$p$$から線分に垂線の足が降ろせれば,垂線の足の距離が点と線分の距離$$\min_{t \in [c,d]}(\| a + t n - p\|)$$になり,下ろせなければ点$$p$$と線分の端点の距離の片方が点と線分の距離になる.



### Def(affine_manifold/hyperplane)

> A subset of $$S$$ of a *linear space* $$V$$ is an **affine manifold** of $$V$$ if $$S = Z + x^*$$ for some linear subspace $$Z$$ of $$V$$ and some $$x^* \in V$$. If $$Z$$ is a maximal proper subspace of $$V$$ then we call $$S$$ a **hyperplane**.



> A set $$S \subset \mathbb{R}^n$$ is a *hyperplane* if and only if $$S = \{ x \in \mathbb{R}^n \mid \langle a, x \rangle = b \}$$ for some $$a \in \mathbb{R}^n \setminus \{ \boldsymbol{0} \}, b \in \mathbb{R}$$  

(Proof)

$$S$$がhyperplaneと仮定するとmaximal proper subspaceである$$Z$$とベクトル$$x^*$$が存在して, $$S = Z + x^*$$が成立する.$$Z$$はmaximal proper subspaceであるので$$Z$$は$$n-1$$次元であるので,[部分空間は斉次方程式の解空間](./linalg.md#部分空間は斉次方程式の解空間)を用いる事で$$ a \in \mathbb{R}^n \setminus \{ \boldsymbol{0} \}$$が存在して,$$Z = \{ x \in \mathbb{R}^n \mid \langle a, x \rangle = 0 \}$$と表す事ができる.$$x \in Z$$に対して,
$$
\langle a, x + x^* \rangle
= \langle a, x\rangle + \langle a, x^*\rangle
= \langle a, x^*\rangle
$$
であるので,$$b \equiv \langle a, x^*\rangle$$と定義すると$$S = \{ x \in \mathbb{R}^n \mid \langle a, x \rangle = b \}$$ となる.

逆に,$$a \in \mathbb{R}^n \setminus \{ \boldsymbol{0} \}, b \in \mathbb{R}$$  が存在して $$S = \{ x \in \mathbb{R}^n \mid \langle a, x \rangle = b \}$$を満たすとする.

$$Z \equiv \{ x \in \mathbb{R}^n \mid \langle a, x \rangle = 0 \}, W = \langle a \rangle$$ ($$a$$によって張られる空間)と定義すると$$Z = W^{\bot}$$である.$$\mathbb{R}^n = W \oplus W^{\bot}$$であるのでcodimenson of $$Z$$は１である.よって[maximal proper subsetの定義](#Def(maximal_proper_subspace))より$$Z$$はmaximal proper subspaceである(subspaceであることは容易に示せる).

よって,$$\langle a, x^*\rangle = b$$を満たす$$x^*$$を1つ固定すると $$S = Z + x^*$$となる.





### Def(span)

> Let $$S$$ be a noempty subset of a vector space $$V$$. The *span* of $$S$$, denoted by $$\text{span}(S)$$, is the set containing of all linear combinations of vectors in $$S$$. For convenience, we definie $$\text{span}(\emptyset) = \{0\}$$.

(Ex1) Let $$S=\{v_i\}_{i=1}^k \subset V$$, where $$k \in \mathbb{N}_{>0}$$.Then $$\text{span}(S)$$ is also subspace of $$V$$.

[部分空間の同値性](#Def(Linear_subspace))を使えば(Ex1)は容易に示せる.



### Def(group)

> A *group* is a noempty set $$G$$ on which there is definied a binary operation $$(a,b) \rightarrow ab$$ satisfying the following properties:
>
> **Closure**:If $$a$$ and $$b$$ belong to $$G$$, then $$ab$$ is also in $$G$$;
>
> **Associativity**:$$a(bc) = (ab)c$$ for all $$a,b,c \in G$$;
>
> **Identity**: There is an element $$1 \in G$$ such that $$a1=1a=a$$ for all $$a$$ in $$G$$;
>
> **Inverse**:If $$a$$ is in $$G$$, then there is an element $a^{-1}$ in $$G$$ such that $$aa^{-1} = a^{-1}a = 1$$.
>
> A *abelian group* (*commutative group*) is a group satisfying the following properties;
>
> **Commutativity**:$$ab = ba$$.
>
> * binary operationのことを*group law* of $$G$$ということもある
> * $$ab$$を$$a \cdot b$$と表記することもある
>
> [Reference](https://faculty.math.illinois.edu/~r-ash/Algebra/Chapter1.pdf)



### Def(Additive_group)

> An *additive group* is a group of which the group operation is to be thought of as *addition* in some sense. It is usually *abelian*, and typically written using the symbol *+* for its binary operation.



### Def(group_action)

> If $$G$$ is a *group* and $$X$$ is a set, then a (left) *group action* $$\phi$$ of $$G$$ on $$X$$ is a function
>
> $$\phi:G \times X \rightarrow X$$:$$(g,x) \mapsto \phi (g,x)$$
>
> that satisfies the following two axioms (where we denote $$\phi (g,x)$$ as $$g\cdot x$$):
>
> **Identity**:$$e \cdot x = x$$ for all $$x$$ in $$X$$.
>
> where $$e$$ denotes the identity element of the group $$G$$.
>
> **Compatibility**:$$(gh) \cdot x = g \cdot (h \cdot x)$$ for all $$g,h$$ in $$G$$ and all $$x$$ in $$X$$.
>
> The group $$G$$ is said to *act* on $$X$$(on the left). The set $$X$$ is called a (left) G-set.
>
> A *group action* is **transitive** if $$X$$ is non-empty and if for each pair $$x,y$$ in $$X$$ there exists a $$g$$ in $$G$$ such that $$g \cdot x = y$$.
>
> A group action is **faithful (or effective)** (1) if for every two distinct $$g,h$$ in $$G$$ there exists an $$x$$ in $$X$$ such that $$g \cdot x \neq h \cdot x$$; or equivalently, (2) if for each $$g \neq e$$ in $$G$$ there exists an $$x$$ in $$X$$ such that $$g \cdot x \neq x$$. 
>
> A group action is **free (or semi regular or fixed point free)** if,(3) given $$g,h$$ in $$G$$, the existance of an $$x$$ in $$X$$ with $$g\cdot x = h \cdot x$$ implies $$g=h$$. 
>
> Equivalently: (4) If $$g$$ is a group element and there exists an $$x$$ in $$X$$ with $$g \cdot x = x$$ (that is, if $$g$$ has at least one fixed point), then $$g$$ is the identity.
>
>  Note that (5) a fee action on a *non-empty* set is faithful.

(5)は簡単に示せるので略.その他も定義通りだが一応証明を載せる.

Proof (2) $$\Leftrightarrow$$ (1)

逆は自明なので,(2) $$\Rightarrow$$ (1)のみを示す.互いに異なる$$g,h \in G$$を任意にとる.この時$$h^{-1}g = e \Leftrightarrow g=h$$であるので,$$h^{-1}g \neq e$$である.よって,(2)より$$x \in X$$が存在し,$$h^{-1} g \cdot x \neq x$$であるので$$g \cdot x \neq h \cdot x$$.

Proof (3) $$\Rightarrow$$ (4)

任意の$$g \in G$$ に対して$$x \in X$$が存在し,$$g \cdot x = x = e \cdot x$$が成立しているとする.この時(1)の仮定より$$g=e$$, つまり$$g$$はidentity.

Proof (4) $$\Rightarrow$$ (3)

任意の$$g,h \in G$$に対して$$x \in X$$が存在し,$$g \cdot x = h \cdot x$$が成立しているとする.

この時
$$
g \cdot x = h \cdot x 
\Leftrightarrow
h^{-1} \cdot (g \cdot x) = h^{-1} \cdot(h \cdot x)
\Leftrightarrow
(h^{-1} g) x = x
$$
であるので,$$h^{-1}g = e \Leftrightarrow g =h$$となる.

 

### Def(affine_space)

> An *affine space* is a set $$A$$ together with a vector space $$V$$, and transitive and free (right) action of the additive group of $$V$$ on the set $$A$$: $$+:A \times V \rightarrow A$$.  We note that the following properties are always sutisfied.
>
> 1. **Associativity**:$$\forall a \in A, \vec{v}, \vec{w} \in V, a + (\vec{v} + \vec{w}) = (a + \vec{v}) + \vec{w}$$
> 2. **Right identity**:$$\forall a \in A, \vec{0} \in V, a + \vec{0} = a$$
> 3. **Free and transitive action**:For every $$a \in A$$, the mapping $$V \rightarrow A: v \mapsto a + v$$ is a bijection.
>
> The first two properties are simply defining properties of a (right) group action.
>
> The third property characterizes free and transitive actions, the onto character coming from transitivity, and then injective character follows from the action being free.(1)
>
> There is fourth property that follows from 1, 2 above:
>
> 4. **Exsistence of one-to-one transitions**: For all $$v \in V$$, the mapping $$A \to A:a \mapsto a + v$$ is a bijection.
>
> Property 3 is often used in the following equivalent form.
>
> 5. **Subtraction**:For every $$a,b$$ in $$A$$, there exists a unique $$v \in V$$, denoted $$b-a$$ such that $$b = a+v$$ .
>
>
> Every vector space $$V$$ may be considered as an affine space over itself(証明は容易なので略). This means that every element of $$V$$ may be considered eigher as a point or as a vector.
>
> When considered as a point, the zero vector is commonly denoted $$o$$ (or $$O$$, when upper-case letters are used for points) and called the **origin**.

1,2から4が導きだせることは容易に示せるので証明略.

3と5が同値であることは定義から容易に示せるので証明略.

Proof (1)

任意の$$b \in A$$に対して,$$+$$がtransitiveであることから$$b = a + v$$を満たす$$v \in V$$が存在するので,全射.単射性も$$+$$がfreeであることから容易に示せる.



(Ex1)

$$V$$をfield$$F$$上のvector space, $$v \in V, S \equiv \{v_i\}_{i=1}^k \subset V$$ where $$k \in \mathbb{N}_{>0}$$とする.この時$$W \equiv \text{span}(S)$$は[spanの定義](#Def(span))よりベクトル空間である.また,$$A \equiv v + \text{span}(W)$$, $$+:A \times W \to A:(a +w) \mapsto a+w$$と定義する.この時$$+$$は$$A$$上のtransitive and free (right) actionであるので(簡単に証明できるので略),$$A$$はaffine spaceである.

例えば$$V = \mathbb{R}^2, v = (0,1)^t,S = \{ (1,2)^t\}$$とすると$$W$$は原点を通る傾き2の直線を表し,$$A$$は(0,1)を通る傾き2の直線を表す.



### Def(linear_map)

> Let $$V$$ and $$W$$ be vector spaces over the same field $$K$$. A function $$f:V \to W$$ is said to be a *linear map (linear mapping, liniar transformation, linear function)*
>
> if $$\forall \mathbf{u}, \mathbf{v} \in V, \forall c \in K$$ the following two conditions are satisfied:
>
> * **additivity**:$$f( \mathbf{u} + \mathbf{v}) = f(\mathbf{u}) + f(\mathbf{v})$$
> * **homogeneity**: $$f(c\mathbf{u}) = c f(\mathbf{u})$$

(ex)有限次元ベクトル空間の線形関数 linear map of finite-dimensional vector space

$$V,W$$をfield$$K$$上の$$n$$次元ベクトルと$$m$$次元ベクトルとし$$V,W$$の基底を$$\{e_i\}_{i=1}^n \subset V, \{f_i\}_{i=1}^m \subset W$$とする.$$F:V \to W$$をlinear mapとした時に関数$$F$$の行列表現を考える.

$$ \{f_i\}_{i=1}^m$$は$$W$$の基底なので任意の$$i \in \{1,\dots,n\}$$に対して$$F(e_i) = \sum_{j=1}^m a_{ji} f_j = \boldsymbol{a_i}^T \boldsymbol{f}$$ を満たす$$a_{ji}$$が存在する.ここで任意の$$x \in V$$に対して$$x = \sum_{i=1}^n \lambda_i e_i$$を満たす$$\lambda_i \in K$$が存在するので,
$$
F(x) 
= \sum_{i=1}^n \lambda_i F(e_i)
= \sum_{i=1}^n \lambda_i \sum_{j=1}^m a_{ji} f_j
= (\lambda_1, \cdots, \lambda_n)
	\left(
	\begin{array}{c}
		\boldsymbol{a_1}^T\\
		\vdots\\
		\boldsymbol{a_n}^T
	\end{array}
	\right) \boldsymbol{f}
= \boldsymbol{\lambda}^T A^T \boldsymbol{f}
$$
ここで,$$A = (\boldsymbol{a_1}, \dots , \boldsymbol{a_n})$$

特に$$\mathbb{R}^n \to \mathbb{R}^m$$のlinear mapにおいてstandard basisを考える場合は
$$
F(e_i) = \boldsymbol{a}_i^T \boldsymbol{f} = \boldsymbol{a}_i
$$
となるので任意の$$x = (x_1, \dots , x_n)^T \in \mathbb{R}^n$$に対して,
$$
F(x) 
= \sum_{i=1}^n x_i F(e_i)
= \sum_{i=1}^n x_i \boldsymbol{a}_i
= A \boldsymbol{x}
$$


### Def(affine_map)

> A map $$f: \mathcal{A} \to \mathcal{B}$$ between two affine spaces is a *affine map* if it has a linear transformation $$\phi: \mathcal{A} \to \mathcal{B}$$ such that, for $$P,Q \in \mathcal{A}$$, $$f(Q) - f(P) = \phi(Q - P)$$. 
>
> 定義から分かるように$$\mathcal{A}, \mathcal{B}$$は同じ体(field)上のベクトル空間(vector space)を表す.
>
> 以下と同値
>
> A map $$f: \mathcal{A} \to \mathcal{B}$$ between two affine spaces is a *affine map* if it has a linear transformation $$\phi: \mathcal{A} \to \mathcal{B}$$ such that, for any $$Q \in \mathcal{A}$$,
>
> $$f(Q) = f(0_{\mathcal{A}}) + \phi(Q)$$

(ex)$$f:\mathbb{R}^n \to \mathbb{R}^m$$のaffine mapを考える.

$$f:\mathbb{R}^n \to \mathbb{R}^m$$がaffine mapだとする.

Affine mapの定義より任意の$$\boldsymbol{x} \in \mathbb{R}^n$$に対して$$f(\boldsymbol{x}) = f(\boldsymbol{0}) + \phi (\boldsymbol{x})$$を満たす$$\phi:\mathbb{R}^n \to \mathbb{R}^m$$のlinear mapが存在する.[linear mapの例](#Def(linear_map))より$$\phi (\boldsymbol{x}) = A \boldsymbol{x}$$を満たす$$A \in \mathbb{R}^{m \times n}$$が存在するので$$\boldsymbol{b} \equiv f(\boldsymbol{0}) $$と定義すると$$f(\boldsymbol{x}) = A\boldsymbol{x} + \boldsymbol{b}$$と表せる.

逆に$$f:\mathbb{R}^n \to \mathbb{R}^m: \boldsymbol{x} \mapsto  A\boldsymbol{x} + \boldsymbol{b}$$と表せたとする.

$$\phi:\mathbb{R}^n \to \mathbb{R}^m: \boldsymbol{x} \mapsto  A\boldsymbol{x}$$と定義すると$$\phi$$はlinear mapであり$$f(\boldsymbol{x}) = f(\boldsymbol{0}) + \phi(\boldsymbol{x})$$であるので$$f$$はlinear map.



### 定義域を拡張したアフィン写像もアフィン写像

> 任意の$$i \in \{1,\dots,n\}$$に対して$$f_i: X_i \to Y$$がaffine mapとする.この時,
>
> $$f: \prod_{i=1}^n X_i \to Y:\boldsymbol{x} = (x_1, \dots ,x_n)^T \mapsto f_i(x_i)$$と定義すると$$f$$はaffine mapである.

Proof

$$f_i$$はaffine mapより任意の$x_i \in X_i$に対して$$f(x_i) = f_i(0_i) + \phi_i(x_i)$$を満たすlinear map $$\phi_i : X_i \to Y$$が存在する.$$X_1, \dots , X_n, Y$$は同じfield上のvector spaceであるので$$\prod_{i=1}^n X_i$$もvector spaceであることは容易に示せる.よって,$$\phi : \prod_{i=1}^n X_i \to Y: \boldsymbol{x} \to \phi_i (x_i)$$と定義すると,$$\phi_i$$がlinear mapであることから$$\phi$$もlinear mapであることが示せる.よって,任意の$$\boldsymbol{x} \in  \prod_{i=1}^n X_i $$に対して,
$$
f(\boldsymbol{x})
= f_i(x_i)
= f_i(0_i) + \phi_i (x_i)
= f(\boldsymbol{0}) + \phi(\boldsymbol{x})
$$
であるので$$f$$はaffine map.

また,$$\prod_{i=1}^n X_i$$がaffine spaceであることは定義に沿って証明できる.



### アフィン写像の線形和はアフィン写像

> $$f,g:X \to Y$$がaffine mapとする.ただし,$$X,Y$$はfield$$K$$上のvector spaceとする.
>
> この時,任意の任意の$$\alpha, \beta \in K$$に対して$$h: X \to Y: x \mapsto \alpha f(x) + \beta g(x)$$はaffine map

(Proof)

$$f,g$$はaffine mapであるのでlinear maps $$\phi, \psi:X \to Y$$が存在して任意の$$ x \in X$$に対して,
$$
f(x) = f(0) + \phi(x),g(x) = g(0) + \psi(x)
$$
を満たす.また,$$\gamma : X \to Y: x \mapsto \alpha \phi (x) + \beta \psi(x)$$と定義すると$$\gamma$$はlinear mapであり,簡単な計算から
$$
h(x) = h(0) + \gamma(x)
$$
である.よって,$$h$$はaffine map.



>  $$p_0 \equiv P'(0), p_1 \equiv P'(1)$$と定義する.この時,$$P'(S): \mathbb{R} \to \mathbb{R}^2: s \mapsto p_0 + s (p_1 - p_0)$$はaffine mapである.

$$\phi (s): \mathbb{R} \to \mathbb{R}^2: s \mapsto s(p_1 - p_0)$$と定義すると,$$\phi$$はlinear transformationであり任意の$$s_1, s_2 \in\mathbb{R}$$に対して,$$P'(s_1) - P'(s_2) = \phi(s_1 - s_2)(P_1 - P_0) $$であるので$$P'$$はaffine map

