[TOC]

### 多変量正規分布のKLダイバージェンス

> 2つの$$d$$次元多変量正規分布$$p(x) = \mathcal{N}(x; \mu_1, \Sigma_1), q(x) = \mathcal{N}(x; \mu_2, \Sigma_2)$$のKLダイバージェンス$$KL[P(X)||Q(X)]$$は以下である.
>
> $$KL[P(X)||Q(X)] = \frac{1}{2} \left(    \log \frac{|\Sigma_2|}{|\Sigma_1|}     + \mathrm{Tr}[\Sigma_2^{-1} \Sigma_1]     + (\mu_1 - \mu_2)^T \Sigma_2^{-1} (\mu_1 - \mu_2)    - d  \right)$$
>
> [参考資料](http://sucrose.hatenablog.com/entry/2013/07/20/190146)

平均$$\mu$$,共分散行列$$\Sigma$$の$$d$$次元多変量正規分布は以下で与えられる.
$$
\mathcal{N}(x; \mu, \Sigma) 
\equiv \frac{|\Sigma|^{-1/2}}{(2\pi)^{d/2}} \exp 
	\left( -\frac{1}{2}(x - \mu)^T \Sigma (x -\mu) \right)
$$
ここで,$$p(x) = \mathcal{N}(x; \mu_1, \Sigma_1), q(x) = \mathcal{N}(x; \mu_2, \Sigma_2)$$の間のKL情報量
$$
KL[P(X)||Q(X)] \equiv \int p(x) \log \frac{p(x)}{q(x)} dx
$$
を計算する.まず,$$\log \frac{p(x)}{q(x)}$$を整理する.
$$
\begin{align*}
	\log \frac{p(x)}{q(x)} 
	&= \log p(x) - \log q(x)\\
	&= \frac{1}{2} \left(
			\log \frac{|\Sigma_2|}{|\Sigma_1|} 
			+ (x - \mu_2)^T \Sigma_2^{-1} (x - \mu_2)
			- (x - \mu_1)^T \Sigma_1^{-1} (x - \mu_1)
		\right)
\end{align*}
$$
よって,
$$
KL[P(X)||Q(X)] 
= \frac{1}{2} \left(
	 \log \frac{|\Sigma_2|}{|\Sigma_1|}
	+ \mathbb{E}_p \left[ 
			(x - \mu_2)^T \Sigma_2^{-1} (x - \mu_2)
		\right]
	- \mathbb{E}_p \left[ 
			(x - \mu_1)^T \Sigma_1^{-1} (x - \mu_1)
		\right]
\right)
$$
となる.

また,$$K$$を体($$\mathbb{R}$$),$$x \in K^n, A \in K^{n \times n}$$とすると簡単な計算からトレースについて$$x^TAx= \mathrm{Tr} [x^T A x] = \mathrm{Tr} [ A x x^T]$$が一般に成立することに注意すると,
$$
\begin{align*}
	\mathbb{E}_p[(x - \mu_2)^T \Sigma_2^{-1} (x - \mu_2)]
	&= \mathbb{E}_p\left[
			 \mathrm{Tr}[\Sigma_2^{-1}(x - \mu_2)(x - \mu_2)^T]
		\right]\\
	&= \mathrm{Tr} \left[
			\mathbb{E}_p \left[
					\Sigma_2^{-1}(x - \mu_2)(x - \mu_2)^T
				\right]
		\right]\\
	&= \mathrm{Tr} \left[
			\Sigma_2^{-1} \left(
				\mathbb{E}_p [x x^T] - \mathbb{E}_p [x \mu_2^T]
				- \mathbb{E}_p [\mu_2 x^T] + \mathbb{E}_p [ \mu_2 \mu_2^T]
				\right)
		\right]\\
		
\end{align*}
$$
また,平均の定義より$$\mathbb{E}_p[x] = \mu_1$$であるので,$$\mathbb{E}_p[x \mu_2^T] = \mu_1 \mu_2^T, \mathbb{E}_p[\mu_2 x^T] = \mu_2 \mu_1^T$$である.

また,分散の定義より
$$
\begin{align*}
	\Sigma_1 
	&\equiv \mathbb{E}_p[(x - \mu_1)(x - \mu_1)^T]\\
	&= \mathbb{E}_p [x x^T] - \mathbb{E}_p [x \mu_1^T]
		- \mathbb{E}_p [\mu_1 x^T] + \mathbb{E}_p [ \mu_1 \mu_1^T]\\
	&= \mathbb{E}_p [x x^T]- \mu_1 \mu_1^T
\end{align*}
$$
であるので,
$$
\begin{align*}
	\mathbb{E}_p[(x - \mu_2)^T \Sigma_2^{-1} (x - \mu_2)]
	&= \mathrm{Tr} \left[
			\Sigma_2^{-1} \left(
				\mathbb{E}_p [x x^T] - \mathbb{E}_p [x \mu_2^T]
				- \mathbb{E}_p [\mu_2 x^T] + \mathbb{E}_p [ \mu_2 \mu_2^T]
				\right)
		\right]\\
	&= \mathrm{Tr} \left[
			\Sigma_2^{-1} \left(	
				\Sigma_1 + \mu_1 \mu_1^T 
				- \mu_1 \mu_2^T - \mu_2 \mu_1^T + \mu_2 \mu_2^T
			\right)
		\right]\\
	&= \mathrm{Tr} \left[
			\Sigma_2^{-1} \left(
				\Sigma_1 + (\mu_1 - \mu_2) (\mu_1 - \mu_2)^T
			\right)
		\right]\\
	&= \mathrm{Tr}[\Sigma_2^{-1} \Sigma_1] 
		+ (\mu_1 - \mu_2)^T \Sigma_2^{-1} (\mu_1 - \mu_2)
\end{align*}
$$
また第3項についても同様に計算を行うと
$$
\begin{align*}
	\mathbb{E}_p[(x - \mu_1)^T \Sigma_1^{-1} (x - \mu_1)]
	&= \mathbb{E}_p\left[
			 \mathrm{Tr}[\Sigma_1^{-1}(x - \mu_1)(x - \mu_1)^T]
		\right]\\
	&= \mathrm{Tr} \left[
			\Sigma_1^{-1}\mathbb{E}_p \left[
					(x - \mu_1)(x - \mu_1)^T
				\right]
		\right]\\
	&= \mathrm{Tr} \left[
			\Sigma_1^{-1} \Sigma_1
		\right]\\
	&= d
\end{align*}
$$
ゆえに,
$$
KL[P(X)||Q(X)] 
= \frac{1}{2} \left(
		\log \frac{|\Sigma_2|}{|\Sigma_1|} 
		+ \mathrm{Tr}[\Sigma_2^{-1} \Sigma_1] 
		+ (\mu_1 - \mu_2)^T \Sigma_2^{-1} (\mu_1 - \mu_2)
		- d
	\right)
$$
