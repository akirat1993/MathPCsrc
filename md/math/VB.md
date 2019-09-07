[TOC]

# 変分ベイズVariational_Bayesian

## 参考資料

* [このページ](http://users.umiacs.umd.edu/~xyang35/files/understanding-variational-lower.pdf)と[このページ](https://qiita.com/kenmatsu4/items/b029d697e9995d93aa24)を基にまとめている.

* [VAEの元論文(主に確認用に使用)](https://arxiv.org/abs/1312.6114)

* [VAEの説明 英語(未読)](http://anotherdatum.com/vae.html)

## 内容

### 変分ベイズ

* 変分ベイズ(Variational_Bayesian)とは?

  観測されている変数から観測されていない変数の推論を最適化を用いて行う手法

* Problem setup

  * 観測データ$$X$$は(パラメータを持っている)潜在変数$$Z$$から確率的に生成されているとする($$X$$,$$Z$$は確率変数)

  * $$P(X)$$を$$X$$の確率分布,$$p(X)$$を確率密度関数とする.

  * 上記の仮定より実際には$$p(Z)$$と$$p(X | Z)$$**しか存在しない**ことに注意する.この時,Bayes's Theoremを用いると$$P(Z|X)$$を下記の式から
    $$
    p(Z | X) 
    = \frac{p(X | Z) p(Z)}{p(X)}
    = \frac{p(X | Z) p(Z)}{ \int_Z p(X, Z)}
    $$
    

* 変分下限(Variational_Lower_bound)の導出
  $$
  \begin{align*}
  	\log\,p(X)
  	&= \log \int_Z p(X,Z)\\
  	&= \log \int_Z p(X,Z) \frac{q(Z)}{q(Z)} \\
  	&= \log \left( \mathbb{E}_q \left[ \frac{p(X,Z)}{q(Z)} \right]  \right)\\
  	&\ge \mathbb{E}_q \left[ \log \frac{p(X,Z)}{q(Z)} \right] 
  		\quad \because \text{Jensen's inequality}\\
  	&= \mathbb{E}_q [\log p(X, Z)] + H[Z]
  		\quad \text{variational lower bound/ELBO}\\
  	&= L
  \end{align*}
  $$
  where

  * $$H[Z] =  - \mathbb{E}_q [q(Z)]$$(Shannon entropyと呼ぶ)

  * $$q(Z)$$ is approximation of the true posterior distribution of $$p(Z \mid X)$$

  特記事項

  * [Jensen's inequalityの証明(別タブで開くと良い)](convex.md#イェンセンの不等式Jensen's_inequality)
  * $$p(X)$$を最大にするために,ELBO(evidence lower bound)を最大にする場合がある

* VBのMain Idea

  approximation $$q(Z)$$とtrue distribution $$p(Z |X)$$近さはKullback-Leibler(KL) divergenceで測ることができる.
  $$
  \begin{align*}
  	KL[q(Z)||p(Z|X)] 
  	&= \int_Z q(Z) \log \frac{q(Z)}{p(Z|X)}\\
  	&= - \int_Z q(Z) \log \frac{p(Z|X)}{q(Z)}\\
  	&= - \left(
  			\int_Z q(Z) \log \frac{p(X, Z)}{q(Z)}
  			- \int_Z q(Z) \log p(X)
  		\right)\\
  	&= - \int_Z q(Z) \log \frac{p(X, Z)}{q(Z)}
  		+ \log p(X) \int_Z q(Z) \\
  	&= -L + \log p(X)
  \end{align*}
  $$
  よって,
  $$
  L = \log p(X) - KL[q(Z)||p(Z|X)] \tag{1}
  $$
  

  となる.つまり,$$\log p(X)$$とELBOの差は真の分布$$p(Z|X)$$と近似$$q(Z)$$のカルバック情報量となる.言い換える真の分布と近似が一致する時に限り,$$\log p(X)$$とELBOは一致する.



### VAE

#### 変分下限Lの式変形

$$
p(Z|X) = \frac{p(X|Z) p(Z)}{p(X)}
$$

を用いると
$$
\begin{align*}
	KL[q(Z)|| p(Z|X)]
	&= \int_Z q(Z) \log \frac{q(Z)}{p(Z|X)}\\
	&= \int_Z q(Z) (\log q(Z) - \log {p(Z|X)})\\
	&= \int_Z q(Z) (\log q(Z) - \log p(X|Z) - \log p(Z) + \log p(X))\\
	&= \log p(X) + \int_Z q(Z) (\log q(Z) - \log p(Z)) - \int_Z q(z) \log p(X | Z)\\
	&= \log p(X) + \int_Z q(Z) \log \frac{q(Z)}{p(Z)} - \mathbb{E}_q[\log p(X|Z)]\\
	&= \log p(X) + KL[q(Z)|| p(Z)] - \mathbb{E}_q[\log p(X|Z)]\
\end{align*}
$$
となる.

これまでの議論において$$p(Z|X)$$の近似$$q(Z)$$を$$q(Z|X)$$と置き換えても同じ議論ができるので,**今後は置き換えたものを用いる**.この時,上式は
$$
KL[q(Z|X)|| p(Z|X)] 
= \log p(X) + KL[q(Z|X)|| p(Z)] - \mathbb{E}_q[\log p(X|Z)]
$$
となる.

また,[変分ベイズ>式(1)](#変分ベイズ)において$$q(Z)$$を$$q(Z|X)$$と置き換えることで,
$$
L = \log p(X) - KL[q(Z|X)||p(Z|X)] \tag{2}
$$
となる.よって,
$$
L = - KL[q(Z | X)|| p(Z)] + \mathbb{E}_{q(Z|X)} [\log p(X|Z)] \tag{3}
$$

#### VAEの仮定

1. 潜在変数(prior over the latent variable)$$p(Z)$$が多変量標準正規分布$$N(0, I)$$に従っている.

2. $$p(X|Z)$$が多変量正規分布(multivariate Gaussian)もしくはBernoulli(in the case of binary data)に従っている.

   ※実際$$p(X|Z)$$の分布は何でも良い気がする.**大事なことは分布のパラメーターがデコーダーによって与えられているということ.**

3. 真の事後分布$$p(Z|X)$$がdiagonal covarianceを持った多変量正規分布に従っていると仮定する.

   ---

   ※ちなみに,$$p(X|Z)$$の平均が$$Z$$の線形結合となっている場合は[この公式](異常検知と変化検知.md#多変量正規分布のベイズ公式p97)より3.の仮定がなくても正規分布に従うことが分かる.

   ---

   この時,その近似である$$q(X|Z)$$もdiagonal covarianceを持ったガウス分布に従っていると考えるのが妥当であるから,
   $$
   q(Z | X) = \mathcal{N}(Z; \mu, {\sigma^2} I)
   $$
   と表せる.ここで,$$Z$$の次元を$$J$$とすると$$\sigma^2 \in \mathbb{R
   }^J_{>0}$$,$$I \in \mathbb{R}^{J\times J}$$は単位行列 ,$$\sigma^2 I \in \mathbb{R}^{J\times J}$$は$$(i,j)$$成分が$$i=j$$の時$$\sigma^2_j$$そうでないとき$$0$$となっている行列を表すことにする.また,分布のパラメータ$$\mu$$と$$\sigma^2$$は**エンコーダーによって与えられているものとする.**

#### VAEの目標

* データ$$X$$が観測された事実が尤もらしくなるように,生成分布であるデコーダー$$p(X|Z)$$の(パラメータを)学習

* 真の事後分布$$p(Z|X)$$を近似するエンコーダー$$q(Z|X)$$の(パラメータを)学習

を同時に行う手法.

その為に[変分下限Lの式変形> 式(2)](#変分下限Lの式変形)の式に現れる変分下限$$L = \log p(X) - KL[q(Z|X)||p(Z|X)] $$の最大化を目指す.上の(2)式は計算しずらいので,式変形した[式(3)](#変分下限Lの式変形)である$$L = - KL[q(Z | X)|| p(Z)] + \mathbb{E}_{q(Z|X)} [\log p(X|Z)]$$を最大化する(VAEの仮定より**2つの項は計算可能である**.(計算方法については後述)



---

**補足(尤度最大化の具体例)**

コインを1,000回投げて800回表が出た時にコインを1回投げた時に表が出る確率を推定する場合を考える.表が出る確率(パラメータ)が1/2とすると上記の観測結果が得られる確率(尤度)は非常に小さくなるので表が出る確率は1/2でないことが推測される.一方,表が出る確率が0.8だとすると上記の観測結果が得られる確率は最大になり,尤もらしいパラメータであると推測される.

---



#### カルバック情報量の計算

$$ KL[q(Z | X)|| p(Z)]$$を考える.VAEの仮定より$$q(Z | X) = \mathcal{N}(Z; \mu, \sigma^2 I)$$であり,$$\mu$$と$$\sigma^2$$はエンコーダーの出力となっている.仮定より$$p(Z)$$は多変量標準正規分布であるのでカルバック情報量$$ KL[q(Z | X)|| p(Z)]$$は[この公式より](./kl.md#多変量正規分布のKLダイバージェンス),$$Z$$の次元を$$J$$とすると,
$$
KL[q(Z | X)|| p(Z)] 
 = -\frac{1}{2} \sum_{j=1}^J 
 	\left(
 		1 + \log \sigma^2_j - \mu_j^2 - \sigma^2_j
 	\right)
$$
と表せる.



#### 復元誤差reconstruction_errorの計算

$$\mathbb{E}_{q(Z|X)} [\log p(X|Z)]$$を大きくする為には,入力データ$$x$$を($$q(Z|X)$$に従って)エンコードしたデータ$$E(x)$$を生成元とした時に$$X$$が生成される確率$$p(x|E(x))$$が大きくなければならないので,$$-\mathbb{E}_{q(Z|X)} [\log p(X|Z)]$$は復元誤差(reconstraction error)と呼ばれる.

また,$$\mathbb{E}_{q(Z|X)} [\log p(X|Z)]$$の近似としてモンテカルロ法,すなわち
$$
\mathbb{E}_{q(z|x)} [\log p(x|z)]
\approx \frac{1}{L} \sum_{\ell = 1}^L \log p(x|z^{(\ell)})
$$
が用いられることがある.ただし,$$z^{(\ell)} = \mu + \sigma \odot \epsilon^{(\ell)}$$ and $$\epsilon^{(\ell)} \sim \mathcal{N}(0,I)$$であり$$\mu$$,$$\sigma$$はエンコーダーによって取得される.(実際のコードでは$$L=1$$となっていることが多い).この時,$$p(x|z)$$はVAEの仮定よりベルヌーイ分布か正規分布でありパラメータはデコーダーによって得られるので**右辺は計算可能**.



#### 損失関数

以上の議論より,損失関数$$\mathcal{L}(X)$$(最小化)は以下のようになる.
$$
\begin{align*}
	\mathcal{L}(X)
	&\equiv -L \\
	&= KL[q(Z | X)|| p(Z)] - \mathbb{E}_{q(Z|X)} [\log p(X|Z)]\\
 	&= -\frac{1}{2} \sum_{j=1}^J 
 		\left(
 			1 + \log \sigma^2_j - \mu_j^2 - \sigma_j^2
 		\right)
 		- \mathbb{E}_{q(Z|X)} [\log p(X|Z)]\\
\end{align*}
$$


### 非正則化異常度

#### 参考文献

* [論文](https://confit.atlas.jp/guide/event-img/jsai2018/2A1-03/public/pdf?type=in)
* [解説記事](https://qiita.com/shinmura0/items/811d01384e20bfd1e035)

#### 仮定

* VAEでは$$p(X|Z)$$はベルヌーイ分布か正規分布と仮定していたが,今回はがdiagonal covarianceを持った正規分布(multivariate Gaussian)に従っていると仮定する.つまり,$$p(x|z) = \mathcal{N}(x;\mu, \sigma^2 I)$$と表されるとする.また,分布のパラメータ$$\mu$$と$$\sigma^2$$はデコーダーによって与えられるものとする.

残りはVAEの仮定と同じ.

#### 損失関数

今回はVAEの損失関数
$$
KL[q(z | x)|| p(z)] - \mathbb{E}_{q(z|x)} [\log p(x|z)]
$$
に現れる$$\mathbb{E}_{q(z|x)} [\log p(x|z)]$$を$$\log p(x|\mu_z)$$で近似する.ただし,$$\mu_z$$は正規分布である$$q(z|x)$$の平均を表す(エンコーダーによって得られる).

また$$\mu_z$$はエンコーダーによって得られるため,$$x$$に依存していることと,$$p(x|z)$$は正規分布であることを考慮すると$$p(x|\mu_z) = \mathcal{N}(x;\mu_x, \sigma^2_x I)$$と表すことができ,仮定より$$\mu_x$$,$$\sigma^2_x$$はデコーダーに$$\mu_z$$を代入した時の出力である.

以上をまとめると,本手法の損失関数$$\mathcal{L}_{VAE}(x)$$は以下のように表すことが出来る.

($$N_x$$は入力次元数,$$N_z$$は潜在空間の次元数)
$$
\begin{align*}
	\mathcal{L}(x)
  &= KL[q(z | x)|| p(z)] - \mathbb{E}_{q(z|x)} [\log p(x|z)]\\
  &\approx KL[q(z | x)|| p(z)] - \log p(x|\mu_z)\\
  &=  KL[q(z | x)|| p(z)] - \log \left(
    \frac{|\sigma^2_x I|^{-1/2}}{(2\pi)^{N_x/2}}
      \exp(
        -\frac{1}{2}(x - \mu_x)^{T}(\sigma^2_x I)^{-1}(x-\mu_x)
       )
   	\right)\\
   &= D_{VAE}(x)
   	+ \frac{1}{2}\log |\sigma_x^2 I |
   	+ \frac{1}{2}\log (2\pi)^{N_x}
   	+ \frac{1}{2} \sum_{i=1}^{N_x} \frac{(\mu_{x_i} - x_i)^2}{\sigma^2_{x_i}}\\
   &= D_{VAE}(x)
   	+ \frac{1}{2} \sum_{i=1}^{N_x} \log \sigma_{x_i}^2
    + \frac{1}{2} \sum_{i=1}^{N_x} \log 2\pi
    + M_{VAE}(x)\\
   &= D_{VAE}(x)
   	+ \frac{1}{2} \sum_{i=1}^{N_x} \log 2\pi \sigma_{x_i}^2
   	+ M_{VAE}(x)\\
   &= D_{VAE}(x) + A_{VAE}(x) + M_{VAE}(x)\\
   &\equiv \mathcal{L}_{VAE}(x)
\end{align*}
$$
ただし,
$$
\begin{align*}
	D_{VAE}(x) 
		&= KL[q(z | x)|| p(z)] 
		= \frac{1}{2} \sum_{j=1}^{N_z} 
 		\left(
 			- \log \sigma^2_{z_j} - 1 + \sigma_{z_j}^2 + \mu_{z_j}^2 
 		\right) \\
 	A_{VAE}(x)
 		&= \frac{1}{2} \sum_{i=1}^{N_x} \log 2\pi \sigma_{x_i}^2\\
 	M_{VAE}(x)
 		&= \frac{1}{2} \sum_{i=1}^{N_x} \frac{(\mu_{x_i} - x_i)^2}{\sigma^2_{x_i}}
\end{align*}
$$
である.ただし

**学習時は**$$\mathcal{L}_{VAE}(x)$$**の最小化を目指す**

#### 従来の異常度について

[変分下限Lの式変形 式(2)](#変分下限Lの式変形)より
$$
\mathcal{L}_{VAE}(x) 
\approx \mathcal{L}(x)
= -L
= -\log p(X) + KL[q(Z|X)||p(Z|X)]
$$
であり,学習が上手くいった場合は$$KL[q(Z|X)||p(Z|X)]$$が十分小さくなると考えると,右辺は$$-\log p(X)$$となるので異常度とすることが出来る.



#### 提案手法の異常度について

正常と異常を区別するための非正則化異常度$$\mathcal{L}_{VAE,M}(x)$$は以下で定義される.
$$
\mathcal{L}_{VAE,M}(x)
\equiv M_{VAE}(x)
$$
損失関数$$\mathcal{L}_{VAE}(x)$$から正規分布の正規化定数の対数$$A_{VAE}(x)$$とVAEの正則化項$$D_{VAE}(x)$$を取り除いたので**非正則化**異常度と呼ばれる.

---

構造が多様な製品に対しても有効な異常度$$\mathcal{L}_{VAE,M}(x)$$を定義したことが成果だと主張している.論文の実験データとなっているネジ穴データセットにおいて,従来手法の異常度$$\mathcal{L}_{VAE}(x)$$を用いた場合, 画像間で差分が大きいネジ穴の溝の部分は正常でも異常と判別されるが異常度$$\mathcal{L}_{VAE,M}(x)$$を用いた場合には正常のものは正常と判別できている.

---

#### 学習

##### 概要

* 正常品と異常品の両方を入力として(ラベルがついてなくても良い)$$\mathcal{L}_{VAE}(x)$$を損失関数としてVAEの学習を行う. 
* テストデータ以外で$$\mathcal{L}_{VAE,M}(x)$$を求めて閾値を決定する

※論文では640x480の画像を96x96に切り取って学習及びテストを行っている.

##### 詳細

* 初めの畳み込み層のチャネル数$$N_c \in \{16,32,64\}$$
* 潜在空間の次元数$$N_z \in \{2,5,10,20,50,100\}$$