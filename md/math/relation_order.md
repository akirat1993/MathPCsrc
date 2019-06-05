### Def(binary_relation)

> Given two sets $$X$$ and $$Y$$, a **binary relation (multivalued function)** on $$R$$ from $$X$$ to $$Y$$ is a subset of $$X \times Y$$.
>
> $$(x,y) \in R$$ is read "$$x$$ is R-related to $$y$$", and is denoted by $$xRy$$.
>
> Note:
>
> * The set $$X$$ is called the **set of departure** and the set of $$Y$$ is called the **set of destination or codomain**.
>
> * A binary relation is also called a **correspondence**.
>
> * When $$X=Y$$, a binary relation is called a **homegeneous relation**.
>
> * To emphasize the fact $$X$$ and $$Y$$ are allowed to be different, a binary relation is also called a **heterogeneous relation**.
>
> * The **domain** of $$R$$ is defined as following
>
>   $$D \equiv \{ x \in X \mid  \exists y \in Y \text{ with } xRy\}$$ 
>
> * The **range or image** of $$R$$ is defined as following
>
>   $$I \equiv \{ y \in Y \mid  \exists x \in X \text{ with } xRy\}$$
>
> * The **field** of $$R$$ is the union of its domain and range.
>
>   $$D \times I$$



### Def(asymmetric_relation)

> An **asymmetric relation** is a *binary relation* $$R$$ on a set $$X$$ such that $$aRb \Rightarrow \lnot bRa$$ 



### Def(transitive_relation)

> An **transitive relation** is a *binary relation* $$R$$ on a set $$X$$ such that 
>
> $$aRb \land  bRc \Rightarrow aRc \quad \forall a,b,c \in X$$



### Def(connex_relation)

> A homogeneous relation $$R$$ over a set $$X$$ is **connex**, or a relation $$R$$ having the property of **connexity** when
>
> $$xRy \lor yRx \quad \forall x,y \in X$$
>
> A homogeneous relation $$R$$ over a set $$X$$ is **semiconnex relation**, or a relation $$R$$ having the property of **semiconnexity** when
>
> $$xRy \lor yRx \quad \forall x,y \in X \text{ with } x \ne y$$



### Def(Total order)

> A binary relation $$\le$$ is a **total order** on a set $$X$$ if the following statements hold for all $$a, b$$ and $$c$$ in $$X$$.
>
> - **Antisymmetry**
>
>   $$a \le b \land b \le a \Rightarrow a = b$$
>
> - **Transitivity**
>
>   $$a \le b \land b \le c \Rightarrow a \le c$$
>
> - **Conncexity**
>
>   $$a \le b$$ or $$b \le a$$
>
> Note:
>
> - *total oder* is also called **simple order, linear order, or full order**
> - A set paired with a total order is called a **chain**, a **total ordered set**, a **simply ordered set**, or a **binary ordered set**.
>
>
> For each *total order* $$\le$$ there is an associated asymmetric transitive semiconnex relation $$<$$, called a **strict total order** or **strict semiconnex order**, which can be defined in two equivalent ways:
>
> *  $$a<b$$ if $$a \le b \land a \ne b$$
> * $$a<b$$ if not $$b \le a$$
>
> 上の2つの定義が同値であることは容易に示せるので証明略
>
> $$<$$がasymmetric, transitive, semiconnexであることは容易に示せる.