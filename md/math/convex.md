[TOC]

## 定義

### Def(Convex_set)

> Let $$S$$ be a vector space over the some *orderded field*. A set $$C$$ in $$S$$ is said to be **convex** if $$ (1-t)x + ty \in C \quad \forall x,y \in C, \forall t \in (0,1)$$



### Def(convex_function)

> Let $$X$$ be a *convex set* in a real vector space and let $$f:X \to \mathbb{R}$$ be a function.
>
> * $$f$$ is called **convex** if $$\forall x_1, x_2  \in X, \forall t \in [0,1]$$:
>
>   $$f(tx_1 + (1-t)x_2) \le t f(x_1) + (1-t) f(x_2)$$
>
> * $$f$$ is called **strictly convex** if $$\forall x_1 \ne x_2 \in X, \forall t \in (0,1)$$:
>
>   $$f(tx_1 + (1-t)x_2) < t f(x_1) + (1-t) f(x_2)$$
>
> * A function $$f$$ is said to be (strictly) **concave** if $$-f$$ is (strictly) convex.



## 定理

### R上の任意のノルムは凸関数である

> Let $$\| \cdot\|: V \to \mathbb{R}$$ be a norm on a vector space $$V$$ over $$\mathbb{R}$$. Then $$\| \cdot \|$$ is a convex function.

Proof.

任意の$$v, w \in V, \lambda \in [0,1]$$に対して,
$$
\| \lambda v + (1 - \lambda)w \|
\le \lambda\|v\| + (1-\lambda) \|w\|
$$
