[TOC]

## 教科書

[テキスト](http://www.infra.kochi-tech.ac.jp/takagi/Geomatics/2GeoCoord.pdf)

※本文中(地球を回転楕円体とする緯度経度の座標変換)の$$(N \cos \phi, 0, - \frac{b^2}{a^2} N \sin \phi)$$は$$(N \cos \phi, 0, \frac{b^2}{a^2} N \sin \phi)$$の誤りである.



##  内容

#### 楕円の方程式から2つの焦点からの距離や離心率が一定であることを示す

> 楕円の方程式から2つの焦点からの距離が一定であることを示す.
>
> $$a > b > 0$$とし楕円の方程式が

$$
\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1 \tag{*1}
$$

> で与えられているとする.($$a$$を長軸半径semi-major axis, $$b$$を短軸半径semi-minor axsis)この時$$f := \sqrt{a^2 -b^2}$$と定義する.(後に焦点距離であることが分かる).また方程式を満たす座標$$(x_0, y_0)$$を任意にとってくる.このとき,$$(x_0, y_0)$$とfocus$$(f,0)$$の距離$$r_1$$と$$(x_0, y_0)$$とfocus$$(-f,0)$$の距離$$r_2$$の距離の和$$r_1 + r_2$$は$$2a$$となる.
>
> また,離心率(eccentricity)を$$e := \sqrt{1 - (\frac{b}{a})^2}$$,準線(Directrix)を$$x := - \frac{a}{e}$$と定める.
> このとき,方程式の任意を満たす任意の座標$$(x_0, y_0)$$に対して,焦点$$(-f, 0)$$までの距離と準線までの距離の比は$$e:1$$になる.

(Proof)
$$
\begin{align*}
	r_2 
	&= \sqrt{(x_0 +f)^2 + y_0^2} \\
	&= \sqrt{(x_0 +f)^2 + (1 - \frac{x_0^2}{a^2})b^2} \quad \because (*1)\\
	&= \sqrt{x_0^2\cdot \frac{a^2 - b^2}{a^2} + 2fx + b^2 + f^2}\\
	&= \sqrt{(\frac{fx_0}{a})^2 + 2fx_0 + a^2} \quad \because \text{definition of } f\\
	&= \sqrt{(\frac{fx_0}{a} + a)^2}\\
	&= \frac{fx_0}{a} + a \quad \because \text{we show below}
\end{align*}
$$
ここで楕円の方程式より$$|x_0| \le a$$であるので$$\frac{fx_0}{a} + a \ge -f+a \ge 0$$.

同様にして$$r_1 = -\frac{fx_0}{a} + a$$となるので$$r_1 + r_2 = 2a$$

[参考資料 英語](https://math.stackexchange.com/questions/336622/analytic-geometry-high-school-why-is-the-sum-of-the-distances-from-any-point)

(Proof2)

$$a = \frac{\sqrt{a^2}}{a} \le \frac{a}{\sqrt{a^2 + b^2}}$$より$$-\frac{a}{e} = - \frac{a^2}{\sqrt{a^2 - b^2}} \le -a \le x_0$$

$$e:1 = \sqrt{(x_0 +f )^2 + y_0^2}:x_0 + \frac{a}{e}$$を示せば十分.$$e$$の定義より$$f = ae$$であることと上記の計算より,
$$
\sqrt{(x_0 +f )^2 + y_0^2} 
=  \frac{fx_0}{a} + a
= ex_0 + a
$$
[離心率について分かりやすい資料](http://examist.jp/mathematics/math-3/quadratic-curve/risinritu/)

#### 楕円の方程式から楕円上の点$(x_0, y_0)$における法線ベクトルを求める.

> $$a,b > 0$$楕円の方程式が

$$
\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1
$$

> で与えられているとする.このとき,楕円上の点$$(x_0, y_0)$$における法線ベクトルは

$$
\left(
	\frac{2 x_0}{a^2}, \frac{2 y_0}{b^2}
\right)
$$

> である.

(Proof)

野村隆昭著 微分積分学講義 > 6.12 条件付き極値問題(p161)を参考にする

関数$$k: \mathbb{R}^2 \to \mathbb{R}$$のレベル$$t \in \mathbb{R}$$の等高線$$L_t: k(x,y) = t$$を考え,曲線$$L_t$$の法線ベクトルについて考察する.$$A(a,b)$$が次の3つを満たしているとする.

1. $$t = k(a,b)$$
2. $$k(a,b)$$は$$A$$の近傍で偏微分可能である.
3. $$A$$は$$L_t$$の非特異点であるとする.すなわち$$g(x,y) = k(x,y) -t$$としたときに,$$g_x(a,b) = g_y(a,b) = 0$$は成立しないとする.

ここで$$g_y(a,b) \ne 0$$と仮定する.陰関数定理より$$A$$の近傍で$$y = \psi(x)$$と解ける.点$$A$$における$$L_t$$の接線$$l$$は,$$y = \psi (x)$$の点$$A$$における接線に他ならないから,$$l$$の傾きは$$\psi'(a) = - \frac{g_x(a,b)}{g_y(a,b)} = - \frac{k_x(a,b)}{k_y(a,b)} $$.したがって,$$l$$の方向ベクトルは$$\mathbf{d} := (1,  - \frac{k_x(a,b)}{k_y(a,b)})$$であり,関数$$k$$の勾配$$\nabla k(a,b)$$との内積を計算すると,
$$
\nabla k(a,b) \cdot \mathbf{d} = 0
$$
以上の議論は$$k_x(a,b) \ne 0$$と仮定しても同様であるから,$$\nabla k(a,b)$$は$$A$$での法線ベクトルとなる.

ここで楕円の法線ベクトルについて考える.$$k(x,y):= \frac{x^2}{a^2} + \frac{y^2}{b^2}$$,$$t=1$$を上記の議論に当てはめると,楕円上の点$$(x_0, y_0)$$は$$k(x_0,y_0)  = 1$$を満たし$$k_x(x,y) = \frac{2x}{a^2},k_y(x,y) = \frac{2y}{b^2}$$であるから$$k$$は$$(x_0, y_0)$$の近傍で偏微分可能であり,$$k_x(x,y) =k_y(x,y) =0$$となるときは$$x = y = 0$$である時に限るから$$(x_0, y_0)$$は$$L_t$$非特異点である.ゆえに$$\nabla k(x_0,y_0) = \left( \frac{2 x_0}{a^2}, \frac{2 y_0}{b^2} \right)$$は$$(x_0, y_0)$$における法線ベクトルである.



#### 楕円のパラメータ表示

> $$a, b > 0$$を定数とし,

$$
A := \left\{
	(x,y) \in \mathbb{R}^2 \mid \frac{x^2}{a^2} + \frac{y^2}{b^2} = 1 
	\right\}
$$

> と定義する.この時$$A$$の任意の元$$(x,y)$$に対し$$0 \le \theta < 2\pi$$で$$x = a \cos \theta, y = b \sin \theta$$を満たす$$\theta$$が唯一存在する.

(存在性)

$$X := \frac{x}{a}, Y:= \frac{y}{b}$$と定義すると,$$(x,y)$$は$$A$$の元であるので$$X^2 + Y^2 = 1$$.この方程式は円周を表すので,$$0 \le \theta < 2\pi $$で$$X = \cos \theta, Y = \sin \theta$$を満たす$$\theta$$が唯一存在する.このとき,$$x = aX = a \cos \theta$$,$$y = b Y = b \sin \theta$$である.

(一意性)

$$0 \le \theta \ne \phi < 2\pi$$が$$x = a \cos \theta  = a \cos \phi, y = b \sin \theta = b \sin \phi$$を満たしているとすると,
$$
(\theta = 2\pi - \phi )
\land 
\theta = 
\begin{cases}
	\pi - \phi \;\;\mbox{if}\;\; 0 \le \phi \le \pi\\
    3 \pi - \phi \;\;\mbox{if}\;\; \pi < \phi < 2\pi\\
\end{cases}
$$
より矛盾.



