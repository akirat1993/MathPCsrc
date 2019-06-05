[TOC]

### 平行線のfree_space

> $$V$$を内積$$\langle \cdot,\cdot \rangle$$が定まっている$$\mathbb{R}$$上のベクトル空間とする.
>
> $$V$$上の2つの平行な直線$$P'(s) = p_0 + s (p_1 - p_0), Q'(t) = q_0 + t (q_1 - q_0)$$を考える.
>
> ただし,$$  p_1 - p_0 \ne \boldsymbol{0}$$, $$q_1 - q_0 = \alpha (p_1 - p_0) \quad \alpha \in \mathbb{R} \setminus \{0\}$$とする.
>
> この時,free space
>
> $$F_\epsilon \equiv \{(s,t) \in \mathbb{R}^2 \mid \| P'(s) - Q'(t)\| \le \epsilon \}$$は
>
> 空集合または,傾き$$\frac{1}{\alpha}$$の2本の平行線で囲まれた領域(横軸は$s$に対応)のいずれかである.

Proof

$$p_s \equiv P'(s)$$と簡易表示をして$$p_s$$と$$Q'(t)$$との距離$$d(p_s, Q'(t))$$を求める.
$$
\begin{align*}
	d(p_s, Q'(t))^2
	&= \| q_0 + t\alpha(p_1 - p_0) - p_s\|^2\\
	&= \langle
		(q_0 - p_s) + t\alpha(p_1 - p_0), (q_0 - p_s) + t\alpha(p_1 - p_0)
		\rangle\\
	&= \alpha^2 \| p_1 - p_0 \|^2
		\left(
			t + \frac{\langle
				p_1 - p_0, q_0 - p_s
				\rangle}{\alpha \| p_1 - p_0 \|^2}
		\right)
		- \left(
			\frac{\langle
				p_1 - p_0, q_0 - p_s
			\rangle}{\| p_1 - p_0 \|}
			\right)^2
		+ \| q_0 - p_s \|^2
\end{align*}
$$
また,$$p_{s+\delta} = P'(s+ \delta) = p_s + \delta (p_1 - p_0)$$であるので,
$$
\begin{align*}
	d(p_{s+\delta}, Q'(t))^2
	&= \alpha^2 \| p_1 - p_0 \|^2
		\left(
			t + \frac{\langle
				p_1 - p_0, q_0 - p_s
				\rangle}{\alpha \| p_1 - p_0 \|^2}
			- \frac{\delta}{\alpha}
		\right)
		- \left(
			\frac{\langle
				p_1 - p_0, q_0 - p_s
			\rangle}{\| p_1 - p_0 \|}
			\right)^2
		+ \| q_0 - p_s \|^2
\end{align*}
$$
ここで,
$$
\begin{align*}
	F_\epsilon (s) 
	&\equiv \{t \in \mathbb{R} \mid \| P'(s) - Q'(t)\| \le \epsilon \} \\
	&=  \{t \in \mathbb{R} \mid d(p_s, Q'(t)) \le \epsilon \} \\
	&= \{t \in \mathbb{R} \mid d(p_s, Q'(t))^2 \le \epsilon^2 \}
\end{align*}
$$
と定義すると,$$d(p_s, Q'(t))^2$$は$$t$$に関する二次式であり,$$d(p_{s+\delta}, Q'(t))^2$$は$$d(p_s, Q'(t))^2$$を$$t$$軸の方向に$$\frac{\delta}{\alpha}$$だけ平行移動させたものになっている.ゆえに以下の2つのうちのどちらかが成り立つ.

(1)任意の$$s \in \mathbb{R}$$に対して$$F_\epsilon (s) = \emptyset$$である

(2)$$F_\epsilon (s) = [m_s, M_s]$$とすると, 任意の$$\delta \in \mathbb{R}$$に対して,$$F_\epsilon (s+\delta) = [m_s + \frac{\delta}{\alpha}, M_s + \frac{\delta}{\alpha}]$$が成立よって$$F_{\epsilon}$$は傾き$$\frac{1}{\alpha}$$の2本の平行線で囲まれた領域(横軸は$s$に対応)となる.



### Lemma3(線分のfree_space)

> $$P,Q$$を$$\mathbb{R}^2$$上の線分とする.$$P$$の端点を$$p_0, p_1$$とし$$P:[0,1] \to \mathbb{R}^2:s \mapsto p_0 + s(p_1 - p_0)$$,$$Q$$についても同様に定義する.この時,free space $$F_\epsilon \equiv \{(s,t) \in [0,1]^2 \mid \| P(s) - Q(t)\| \le \epsilon \}$$は
>
> $$L_2$$のときintersection of unit square with an ellipse
>
> $$L_1, L_\infty$$のときparalleogram
>
> いずれにせよconvexである.

Proof

$$P'(S): \mathbb{R} \to \mathbb{R}^2: s \mapsto p_0 + s (p_1 - p_0)$$,$$Q'(t)$$についても同様に定義する.

また,$$f: \mathbb{R}^2 \to \mathbb{R}^2:(s,t) \mapsto P'(s) - Q'(t)$$と定義する.このとき,
$$
f(s,t) 
= \left(p_1 - p_0, -(q_1 - q_0) \right)
	\left(
	\begin{array}{c}
		s\\
		t
	\end{array}
	\right)
	+ (p_0 - q_0)
= A
	\left(
	\begin{array}{c}
		s\\
		t
	\end{array}
	\right)
	+ b
$$
where $$A = (p_1 - p_0, -(q_1 - q_0))$$, $$b = p_0 - q_0$$

となるので[affne mapの定義の(ex)より](group.md#Def(affine_map))$$f$$はaffine mapである.

また,$$D_{\epsilon} \equiv \{ x \in \mathbb{R}^2 \mid \|x\| \le \epsilon \}$$と定義すると,$$F_{\epsilon} = f^{-1}(D_{\epsilon}) \cap [0,1]^2 $$であることに注意する.

(1) $$P, Q$$が平行でないとき

$$p_1 - p_0, -(q_1 - q_0)$$は一次独立であるので$$A$$はinvertible.よって,$f$の逆写像$$f^{-1}: \mathbb{R}^2 \to \mathbb{R}^2:y \to A^{-1}(y - b)$$が存在しアフィン変換.

$$L_2$$の場合[楕円のアフィン変換は楕円](geom.md#楕円のアフィン変換は楕円)であるので$$f^{-1}(D_{\epsilon})$$は楕円である

$$L_1, L_{\infty}$$の場合$$D_\epsilon$$は平行多面体(parallelepipeds)であり[平行多面体のアフィン変換による像は平行多面体](geom.md#Def(Parallelepipeds)平行多面体)であることから$$f^{-1}(D_{\epsilon})$$も平行多面体である.

(2) $$P,Q$$が平行であるとき

任意の$$s \in \mathbb{R}$$に対して

$$p_s \equiv P'(s) = p_0 + s(p_1 - p_0)$$

$$g_s: \mathbb{R} \to \mathbb{R}^2: t \mapsto (q_0 - p_s) + t(q_1 - q_0)$$

$$D_{\epsilon} (s) \equiv \{ t \in \mathbb{R} \mid \| Q'(t) - p_s \| \le \epsilon \} = \{ t \in \mathbb{R} \mid \| g_s(t) \| \le \epsilon \}$$

と定義すると$$D_{\epsilon} (s)$$はIntervalである.

実際,任意の,$$t_1, t_2 \in D_{\epsilon} (s)$$と任意の$$\lambda \in [0,1]$$に対して,[任意のR上のベクトルは凸関数](./convex.md#R上の任意のノルムは凸関数である)であることに注意すると,
$$
\begin{align*}
	\| g_s(\lambda t_1 + (1- \lambda)t_2) \|
	&= \| (q_0 - p_s) +  (\lambda t_1 + (1 - \lambda)t_2)(q_1 - q_0)\|\\
	&= \| \lambda \left\{ (q_0 - p_s) + t_1(q_1 - q_0) \right\}
				+ (1 - \lambda) \left\{ (q_0 - p_s) + t_2(q_1 - q_0) \right\}
			\|\\
	&\le \lambda \| (q_0 - p_s) + t_1(q_1 - q_0) \|
		+ (1 - \lambda) \| (q_0 - p_s) + t_2(q_1 - q_0) \|\\
	&= \lambda \|g_s(t_1)\| + (1 - \lambda) \|g_s(t_2)\|\\
	&\le \max \{ \|g_s(t_1)\|, \|g_s(t_2)\|\}\\
	&\le \epsilon
\end{align*}
$$
より,$$\lambda t_1 + (1- \lambda)t_2 \in D_{\epsilon} (s)$$であるので$$D_{\epsilon} (s)$$はIntervalである.また,
$$
\| g_s(t) \| 
= \| (q_0 - p_0) + t (q_1 - q_0) \|
\ge |t| \| q_1 - q_0 \| - \|q_0 - p_0||
$$
であり,$$q_1 - q_0 \ne \boldsymbol{0}$$であるので,$$\| q_1 - q_0 \| > 0$$であるので$$D_{\epsilon} (s)$$は有界である.

次に$$D_{\epsilon} (s) \ne \emptyset$$ならば上限を含むこと背理法で示す.

$$t_1 \equiv \sup D_{\epsilon}(s)$$と定義して,$$t_1 \notin D_{\epsilon}(s)$$と仮定して矛盾を導く

$$h:\mathbb{R} \to \mathbb{R}: t \mapsto \| g_s(t)\|$$と定義すると$$g_s$$と任意のnormはcontinuousなのでその合成写像である$$h$$も連続.$$t_1 \notin D_{\epsilon}(s)$$であるので$$\epsilon < \| g_s(t_1) \|$$であることに注意すると$$t_1$$での連続性から$$\delta > 0$$が存在して$$t_1 - \delta < t < t_1$$ならば$$\epsilon < \| g_s(t) \|$$が成立するがこれは上限の定義に矛盾. よって$$t_1 \in D_{\epsilon}(s)$$である.

下限に関しても同様の議論が行えるので$$D_{\epsilon} (s)$$は空集合もしくは閉区間である.

また,$$P,Q$$は平行であるので$$\alpha \ne 0$$を用いて$$p_1 - p_0  = \alpha (q_1 - q_0)$$と表される.任意の$$\delta \in \mathbb{R}$$に対して,$$p_{s+\delta} = p_s + \delta(p_1 - p_0)$$, $$g_{s+\delta}(t) = (q_0 - p_s) + (t - \delta \alpha)(p_1 - p_0)$$であるので,

$$D_{\epsilon} (s) = [m,M]$$ならば$$D_{\epsilon} (s+\delta) = [m + \delta \alpha,M + \delta \alpha]$$であるので,$$ f^{-1}(D_{\epsilon})$$は傾き$$\alpha$$の2本の平行線に囲まれた閉領域

$$D_{\epsilon} (s) = \emptyset$$ならば$$D_{\epsilon} (s+\delta) = \emptyset$$であるので$$ f^{-1}(D_{\epsilon})$$は空集合







