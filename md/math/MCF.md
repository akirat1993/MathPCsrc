[TOC]

# 最小費用流 (Minumu Cost Flow)

## 概要

決まった量を始点から終点まで流す際にかかる費用を最小にする問題.

## 教科書

### 教科書1

[Minimum cost flows Amaury Pouly, November 23, 2010](http://perso.ens-lyon.fr/eric.thierry/Graphes2010/amaury-pouly.pdf)

#### 概要

Minimum Cost Flow のアルゴリズム2つ及び計算量についての記述.証明も詳しいので読みやすかった.

+ アルゴリズムの方針(うろ覚え)
「最小費用条件」をいうものを適切に定めることで,最小費用条件を満たしているフローが最小費用流であることが示される.フロー0からスタートして重みを適切に定めたグラフ上でソースからシンクへの最短路を求めてフローを追加することで最小費用条件を常に満たされるプリフロー(容量制約のみを満たしたフローでフロー整合条件が満たされたいない)が作成できる.フローの追加作業を繰り返し行い,流したい流量まで流れた段階になったときフローであることを示すことでそれが最小費用流であることが示される.
+ 特徴
	+ **枝のコストが負の場合にも対応**
	+ 容量制約にlower bandとupper band(upper bandは$$\infty$$もOK)がある場合に対応.
	+ 始点(surplus)、終点(demand)も複数ある場合に対応.
+ アルゴリズムの計算量
	+ アルゴリズム1 
	ノード数を$$n$$,枝数を$$m$$の有向グラフが与えられているとする.
	また、各枝に対して非負の距離が定まっているとする.
	このとき、各枝に対してあるノード$$v_0 \in V$$からの距離を表す関数$$d:V \rightarrow \mathbb{R}_{\ge 0}$$を求めるアルゴリズムの計算量を$$f$$とする.(例えばDijkstra's algorithm with a binary heapを用いると$$f = \mathcal{m\log(n)}$$らしい.)
	このとき,Minimum Cost Flow を求めるアルゴリズムの計算量は$$\mathcal{O}(Bf)$$
	+ アルゴリズム2
	計算量がアルゴリズム1に比べて非常に大きいので略.

#### 補足

##### Removing nonzero lower bounds complement

> Let flow $$\tilde{f}^*$$ is the solution of following minimum cost flow problems (1).

$$
\begin{align*}
\min_{\tilde{f}} 
	&\sum_{e \in A} c(e) \tilde{f}(e)\\
\text{subject to} 
	&\sum_{e \in N^+(v)} \tilde{f}(e) - \sum_{e \in N^-(v)} \tilde{f}(e)
		= b(v) - \sum_{e \in N^+(v)} l(e) + \sum_{e \in N^-(v)} l(e)\\
	& 0 \le \tilde{f}(e) \le u(e) - l(e) 
\end{align*}
$$

>
> Then, if we define $$f^* \equiv \tilde{f}^* + l(e)$$, $$f^*$$ is the solution of following minimum cost flow problems (2).

$$
\begin{align*}
\min_{f} 
	&\sum_{e \in A} c(e) f(e)\\
\text{subject to} 
	&\sum_{e \in N^+(v)} f(e) - \sum_{e \in N^-(v)} f(e) = b(v)\\
	& l(e) \le f(e) \le u(e) 
\end{align*}
$$

(Proof)
It is easy to show $$f^*$$ satisfies all the constraints of problem (1). (skip detail)
Let $$f$$ be a flow that satisfies all the constraints of problem(2). Then, we define the $$\tilde{f}$$ with $$f(e) = \tilde{f}(e) + l(e)$$. Since $$f$$ satisfies all the constraints of problem (2), it is easy to show $$\tilde{f}$$ satisfies the all the constraints of problem (1). Therefore,
$$
\begin{align*}
	\sum_{e \in A} c(e) f^*(e) 
		&= \sum_{e \in A} c(e) \tilde{f}^* - \sum_{e \in A} c(e) l(e)\\
		& \le \sum_{e \in A} c(e) \tilde{f} - \sum_{e \in A} c(e) l(e)\\
		&= \sum_{e \in A} c(e) f(e) 
\end{align*}
$$


##### Lemma 2.3.1 complement
> There exists $$f^\circ$$, a minimum cost flow such that 

$$
\begin{align*}
f^\circ (e_0) \lt \sum_{v \in V} |b(v)| + \sum_{e \in A, u(e) \lt \infty} u(e)
	\quad (\text{for all } e_0 \in A)
\end{align*}
$$

(Proof.)
If we apply theorem 2.1.3 to $$f^\circ$$: we can decompose $$f^\circ$$ into  cyclic $$\mathcal{W}$$ and paths $$\mathcal{P}$$ .Moreover, in  the proof of theorem, we properly define $$f(P) \quad (P \in \mathcal{W} \cup \mathcal{P})$$ such that
$$
\begin{align*}
	f^\circ (e_0) &= \hat{f} (e_0)  
		\equiv \sum_{P \in \mathcal{P}} \delta_{e_0}(P) f(P) + 
		\sum_{W \in \mathcal{W}} \delta_{e_0}(W) f(W)
		\quad (\text{for all } e_0 \in A)
\end{align*}
$$
Therefore, the objective function of minimum cost flow problem is as follows
$$
\begin{align*}
	\sum_{e \in A} c(e) f^\circ(e) 
		&= \sum_{p \in \mathcal{P}} \Big\{
					\sum_{e \in A} \delta_{e}(P) c(e)
				\Big\} f(P) + 
			\sum_{W \in \mathcal{W}} \Big\{
					\sum_{e \in A} \delta_{e}(W) c(e)
				\Big\} f(W)\\
		&= \sum_{P \in \mathcal{P}} c(P) f(P) + \sum_{W \in \mathcal{W}} c(W) f(W)
\end{align*}
$$
Now pick a cycle $$W$$ such that $$f(W) \gt 0$$. Then we must have $$c(W) \le 0$$ since $$f^\circ$$ is a minumum cost flow; otherwise we can set $$f(W) = 0$$ and because we have zero lower bounds, we obtain a feasible flow of strictly lesser cost than $$f^\circ$$. Furthermore, if $$c(W) = 0$$ then we can set $$f(W) = 0$$ and obtain a feasible flow of the same cost. So we can assume that if $$f(W) \gt 0$$ then $$c(W) \lt 0$$.
But remember that $$f^\circ$$ is a minimum cost flow so if there is a cycle $$W$$ such that $$c(W) \lt 0$$ then at least one edge $$e_{W}$$ of $$W$$ must be saturated, that is $$f^\circ(e_W) = u(e_W) \lt \infty$$ otherwise we could push some more flow on W and get a better flow. Let $$W^+ = \{ W \mid f(W) \gt 0\}$$ and $$AW = \{e_W, W \in W^+\}$$. Then we have:
$$
\begin{align*}
	\sum_{W \in \mathcal{W}} \delta_{e_0}(W)f(W) 
	&\le \sum_{W \in \mathcal{W}^+} f(W) 
		\quad (\because \text{add positive, exclude negative})\\
	&= \sum_{e \in AW}	f^\circ (e)\\
	&\le \sum_{e \in AW} u(e)\\
	&\le \sum_{e \in A, u(e) \lt \infty}
\end{align*}
$$
....(the rest of proof is same as textbook)

##### 2.4 Removing negative costs  proof

> We define new problem as follows.The set of arcs is denoted by

$$
\begin{align*}
A' &\equiv A_+ \sqcup A_- \\
&= \{e' \in A \mid c(e') \ge 0\} \sqcup
	\{ e' \mid e' = \tilde{e}, e \in A, c(e) \lt 0\}
\end{align*}
$$

> , and the cost $$c'$$ and capacity $$u'$$ is defined as follows

$$
\begin{align*}
c'(e') \equiv \begin{cases}
		c(e') \quad (e' \in A_+)\\
		-c(\tilde{e'}) \quad (e' \in A_-)
	\end{cases}
u'(e') \equiv \begin{cases}
		u(e') \quad (e' \in A_+)\\
		u(\tilde{e'}) \quad (e' \in A_-)
	\end{cases}
\end{align*}
$$

> Then, the new minimum cost flow problem (1) is as follows

$$
\begin{align*}
\min_{f'} 
	&\sum_{e' \in A'} c'(e) f'(e)\\
\text{subject to} 
	&\sum_{e' \in N'^+(v)} f'(e') - \sum_{e' \in N'^-(v)} f'(e')
		= b(v) - \sum_{e' \in N'^-(v),  e' \in A_{-}} u'(e') + \sum_{e' \in N'^+(v), e' \in A_-} u'(e')
			\quad (\forall v \in V)\\
	& 0 \le f'(e') \le u(e') \quad ( \forall e' \in A')
\end{align*}
$$

> Let flow $$f'^*$$ is the solution of this problem, and we denote the flow $$f^*$$ for the original problem as follows

$$
\begin{align*}
f^*(e) \equiv \begin{cases}
		u(e) -f'^*(\tilde{e}) \quad (c(e) \lt 0)\\
		f'^*(e) \quad(\text{otherwise})
	\end{cases}
\end{align*}
$$



> Then, $$f^*$$ is the solution of the below problem

$$
\begin{align*}
\min_{f} 
	&\sum_{e \in A} c(e) f(e)\\
\text{subject to} 
	&\sum_{e \in N^+(v)} f(e) - \sum_{e \in N^-(v)} f(e) = b(v)\\
	& 0 \le f(e) \le u(e) 
\end{align*}
$$

(Proof)
$$
\begin{align*}
	\sum_{e \in N^+(v)} f^*(e) 
		= \sum_{e \in N^+(v), c(e) \ge 0} f^*(e) + \sum_{e \in N^+(v), c(e) \lt 0} f^*(e)
\end{align*}
$$

$$
\begin{align*}
	\sum_{e \in N^+(v), c(e) \ge 0} f^*(e) 
		= \sum_{e' \in N'^+(v), e' \in A_+} f'^*(e') 
\end{align*}
$$

$$
\begin{align*}
	\sum_{e \in N^+(v), c(e) \lt 0} f^*(e) 
		&= \sum_{e \in N^+(v), c(e) \lt 0} u(e) - f'^*(\tilde{e})\\
		&= \sum_{\tilde{e} \in N'^-(v), \tilde{e} \in A_-} u(\tilde{\tilde{e}}) - f'^*(\tilde{e})\\
		&= \sum_{e' \in N'^-(v), e' \in A_-} u'(e') - f'^*(e')
\end{align*}
$$

Therefore, 
$$
\begin{align*}
	\sum_{e \in N^+(v)} f^*(e) 
		= \sum_{e' \in N'^+(v), e' \in A_+} f'^*(e') \,+ \sum_{e' \in N'^-(v), e' \in A_-} u'(e') - f'^*(e')
\end{align*}
$$
Similarly, 
$$
\begin{align*}
\sum_{e \in N^-(v)} f^*(e) 
	= \sum_{e' \in N'^-(v), e' \in A_+} f'^*(e') \,+ \sum_{e' \in N'^+(v), e' \in A_-} u'(e') - f'^*(e')
\end{align*}
$$
Therefore, 
$$
\begin{align*}
	\sum_{e \in N^+(v)} f^*(e) - \sum_{e \in N^-(v)} f^*(e)  = b(v)
\end{align*}
$$


Now, we conclude that $$f^*$$ satisfies all the constraints of original problem.
Next, we show that $$f^*$$ makes the objective value minimum among all the flows that satisfies the constraints.
The objective value for $$f^*$$ is 
$$
\begin{align*}
\sum_{e \in A} c(e) f^* (e) 
&= \sum_{e \in A, c(e) \ge 0} c(e) f'^*(e) + 
	\sum_{e \in A, c(e) \lt 0} c(e) \big(
			u(e) - f'^*(\tilde{e})
		\big)\\
&= \sum_{e' \in A_+} c'(e') f'^*(e') + \sum_{e' \in A_-} c(\tilde{e'}) \big(
		u(\tilde{e'}) - f'^*(e')
	\big)\\
&= \sum_{e' \in A'} c'(e') f'^*(e') + \sum_{e \in A, c(e) \lt 0} c(e) u(e)
\end{align*}
$$
Now, we pick up a flow $$f$$ for original problem, which satisfies all the constraints, and we also define flow $$f'$$ for new problem as follows
$$
\begin{align*}
f'(e') = \begin{cases}
	f(e') \quad (\text{if } e' \in A_+)\\
	u(\tilde{e'}) - f(\tilde{e'})  \quad (\text{if } e' \in A_-)
\end{cases}
\end{align*}
$$
Then, since
$$
\begin{align*}
f(e) = \begin{cases}
	f'(e) \quad (\text{if } c(e) \ge 0)\\
	u(e) - f'(\tilde{e}) \quad (\text{otherwise})
\end{cases}
\end{align*}
$$
we can show 
$$
\begin{align*}
\sum_{e \in A} c(e) f(e) 
= \sum_{e' \in A} c'(e') f'(e') + \sum_{e \in A, c(e) \lt 0} c(e) u(e) 
\end{align*}
$$
Moreover, since $$f'$$ satisfies all the constraints of new problem (we show later),
$$
	\sum_{e \in A} c(e) f^*(e) \le \sum_{e \in A} c(e) f(e)
$$
It shows that $$f^*$$ is the solution of original problem.

> $$f'$$ satisfies all the constraints of new problem

Proof.
Since,  $$0 \le f'(e') \le u'(e') $$ (for all $$e' \in A'$$) is easy to show, we skip the detail.
$$
\begin{align*}
	\sum_{e' \in N'^+(v)} f'(e') 
		&= \sum_{e' \in N'^+(v), e' \in A_+} f'(e') + 
			\sum_{e' \in N'^+(v), e' \in A_-} f'(e')\\
		&= \sum_{e \in N^+(v), c(e) \ge 0} f(e) + 
			\sum_{e \in N^-(v), c(e) \lt 0} u(e) - f(e) 
\end{align*}
$$
Similarly
$$
\begin{align*}
	\sum_{e' \in N'^-(v)} f'(e') 
		&= \sum_{e \in N^-(v), c(e) \ge 0} f(e) + 
			\sum_{e \in N^+(v), c(e) \lt 0} u(e) - f(e) 
\end{align*}
$$
Therefore, 
$$
\begin{align*}
	\sum_{e' \in N'^+(v)} f'(e') - \sum_{e' \in N'^-(v)} f'(e') 
		&= b(v) - \sum_{e \in N^+(v), c(e) \lt 0} u(e) +  \sum_{e \in N^-(v), c(e) \lt 0} u(e)\\
		&= b(v) - \sum_{e' \in N'^-(v), e' \in A_-} u'(e') +  \sum_{e' \in N'^+(v), e' \in A_-} u'(e')
\end{align*}
$$

##### Theorem 2.6.1 complement

> We asuume that  $$f'(e) \ge 0$$ for all $$e \in A_G$$. Then,

$$
\begin{align*}
	\sum_{e \in N^+_G(v)} f'(e) - \sum_{e \in N^-_G(v)} f'(e) = 0
\end{align*}
$$

(Proof)
$$
\begin{align*}
	\sum_{e \in N^+_G(v)} f'(e) - \sum_{e \in N^-_G(v)} f'(e) 
		= \Big(
				\sum_{e \in N^+(v)} f'(e) + \sum_{e \in N^-(v)} f'(\tilde{e})
			\Big) -
			\Big(
				\sum_{e \in N^-(v)} f'(e) + \sum_{e \in N^+(v)} f'(\tilde{e})
			\Big)
\end{align*}
$$
the rest of proof is same



##### Lemma 2.8.3 modification MCNF
I change the assumption because the lemma is wrong.
(For example, Let $$e = (s,v)$$, $$d(v) < c(e)$$)

> Assume there is a source node $$s \in V$$ such that every node $$v \in V$$ is accessible from $$s$$, Let $$d$$ be a potential function and $$\pi = -d$$. Then if there is no negative cost cycle in the network, the following two conditions are equivalent:
> (i) $$d(v)$$ is the shortest path distance from $$s$$ to $$v$$ with respect to $$c$$.
> (ii) $$d(s) = 0$$ and $$c^\pi(e) \ge 0$$ for all $$e \in A$$.
> We add assumption that
> **$$d(v)$$ is greater than or equal to the shortest path distance from $$s$$ to $$v$$ with respect to $$c$$.**

(Proof)
(i) $$\Rightarrow$$ (ii) is same as the textbook.
(ii) $$\Rightarrow$$ (i)
By assumption, for all $$e = (u,v) \in A$$
$$
\begin{align*}
	c^\pi(e) \ge 0 
		\Rightarrow c^{-d}(e) \ge 0
		\Rightarrow c(e) + d(u) - d(v) \ge 0
		\Rightarrow d(v) \le d(u) + c(e)
\end{align*}
$$
Let $$(s=v_0, v_1,\dots, v_n=v)$$ be a path from $$s$$ to $$v$$, $$e_i = (v_{i-1}, v_i) \quad (i \in \{1,2, \cdots, n\})$$. Then,
$$
\begin{align*}
	d(v) & = d(v_n)\\
		& \le d(v_{n-1}) + c(e_n)\\
		& \le d(v_{n-2}) + c(e_{n-1}) + c(e_n)\\
		& \le \sum_{i=1}^n c(e_i)
\end{align*}
$$
Since $$d(v)$$ is greater than or equal to the shortest path distance from $$s$$ to $$v$$ with respect to $$c$$, (ii) $$\Rightarrow$$ (i)
