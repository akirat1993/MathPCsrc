

[TOC]

### Def(近傍:neighbourhood)

> Let $$(X, \tau)$$ be a topological space, $$N \subset X$$, $$p \in N$$. Then $$N$$ is said to be a **neighbourhood** of a point $$p$$ if there exists an open set $U$ such that $$p \in U \subset N$$.



### Def(孤立点:isolated_point)

> Let $$(X, \tau)$$ be a topological space and $$S \subset X$$. Then a point $$x \in S$$ is called an isolated point of  $$S$$ if there exists $$U \in \tau$$ such that $$U \cap S = \{x \}$$.
>
> - This is equivalent to saying that the singleton $$\{x\}$$ is an open set in the topological space $$S$$ (considered as a subspace of $$X$$).(証明略)

### ハウスドルフ空間上のコンパクト集合は閉集合

> Let $$(X, \tau)$$ be a Hausdorff space and $$K \subset X$$ is compact. Then $$K$$ is closed.

Proof.

$$x \in X \setminus K$$を固定する.Hausdorff spaceであることから任意の$$y \in K$$に対して$$U_y, V_y \in \tau$$が存在して$$x \in U_y, y \in V_y, U_y \cap V_y = \emptyset$$を満たす.また,$$\{ V_y \mid y \in K \}$$は$$K$$のopen coveringであるから$$K$$のコンパクト性よりfinite set $$F$$が存在して$$\{ V_y \mid y \in F\}$$がfinite subcoverとなる.ここで,$$U \equiv \bigcap_{y \in F} U_y$$と定義すると$$U$$は$$x$$のneighborhoodであり$$U \cap K = \emptyset$$であるから$$K$$ はclosed.

