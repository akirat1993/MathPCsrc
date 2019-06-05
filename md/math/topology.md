### ハウスドルフ空間上のコンパクト集合は閉集合

> Let $$(X, \tau)$$ be a Hausdorff space and $$K \subset X$$ is compact. Then $$K$$ is closed.

Proof.

$$x \in X \setminus K$$を固定する.Hausdorff spaceであることから任意の$$y \in K$$に対して$$U_y, V_y \in \tau$$が存在して$$x \in U_y, y \in V_y, U_y \cap V_y = \empty$$を満たす.また,$$\{ V_y \mid y \in K \}$$は$$K$$のopen coveringであるから$$K$$のコンパクト性よりfinite set $$F$$が存在して$$\{ V_y \mid y \in F\}$$がfinite subcoverとなる.ここで,$$U \equiv \bigcap_{y \in F} U_y$$と定義すると$$U$$は$$x$$のneighborhoodであり$$U \cap K = \empty$$であるから$$K$$ はclosed.

