[TOC]

### 部分空間は斉次方程式の解空間

> $$W$$を$$n$$次元ベクトル空間$$V$$上の部分空間(subspace)とする.$$W$$の次元数は$$k (1 \le k \le n)$$とする.$$W^{\bot}$$ ($$W$$の直交補空間)の正規直交基底を$$e_{k+1},\dots ,e_n$$とすると
>
> $$W = \{ x \in V \mid \langle e_j, x \rangle = 0, k+1 \le j \le n\}$$
>
> である.

(Proof)

1次独立なベクトルを順にとっていくことで$$W$$の基底を求めることができる(次元数$$k$$が定まる)ことに注意.また,$$V = W \oplus W^{\bot}$$であり,シュッミットの直交化法を用いるて$$W$$の正規直交基底を$$e_1, \dots ,e_k$$とした時,$W^{\bot}$の定義より $$V$$の正規直交基底を,$$e_1,\dots ,e_n$$となっている.

ここで,$$x \in V$$を任意にとると$$x = \sum_{i=1}^n \lambda_i e_i$$と表されるので,
$$
\langle e_j, \sum_{i=1}^n \lambda_i e_i \rangle
= \sum_{i=1}^n \lambda_i \langle e_j, e_i \rangle
= \lambda_j
$$
であるので,$$x$$が問題文中の集合に含まれるなら,$$k+1 \le \forall j \le n$$に対して$$\lambda_j = 0$$となるので,$$W$$の元である.逆に$$x \in W$$であるなら,$$x = \sum_{i=1}^k \lambda_i e_i$$と表されるので$$k+1 \le \forall j \le n$$に対して,$$\langle e_j, x \rangle = 0$$であるので文中の集合に含まれる.

