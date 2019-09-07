

[TOC]

## 最適化問題の基本用語

### GAP

実行可能領域で目的関数が非負の値をとる最小化問題を考える.最適化アルゴリズムを実装している時にある時点でのGAPを以下で定義する.$$\check{f}$$を現在見つかっている下界の中で最大のものだとする.$$f^*$$を最適解の目的関数値とする(多くの場合,現時点では見つかっていない).$$f$$を現在見つかっている最良の解とする.この時,$$\check{f} \le f^* \le f$$, $$0 \le f^*$$が成立しておりGAPは以下で表される.
$$
\frac{f -  \check{f}}{f}
$$


## 最適化問題一覧

### 混合整数二次錐計画MISOCP

MISOCP(Mixed Integer Second Order Cone Programming) 

ある程度ソルバーでも解ける問題らしい

$$
\begin{align*}
    &\underset{\boldsymbol{x}}{\text{minimize}}
        & & \boldsymbol{c}^T \boldsymbol{x}\\
    &\text{subject to}
        & & A \boldsymbol{x} = \boldsymbol{b}\\
    &   & & \boldsymbol{x} \succeq 0\\
    &   & & \boldsymbol{x}_j \in [l_j, u_j] &(j \in J)\\
    &   & & \boldsymbol{x}_j \in \mathbb{Z} &(j \in J)
\end{align*}
$$

where $$\boldsymbol{c} \in \mathbb{R}^n, A \in \mathbb{R}^{m,n}, \boldsymbol{b} \in \mathbb{R}^m, l_j, u_j \in \mathbb{R}$$ and $$\boldsymbol{x} \succeq 0$$ denotes that $$\boldsymbol{x} \in \mathbb{R}^n$$ consists of *noc* part vectors $\boldsymbol{x}_i \in \mathbb{R}^{k_i}$ lying in second order cones defines by
$$
\mathcal{K}_i = \{
	\boldsymbol{x}_i = (\boldsymbol{x}_{i0}, \boldsymbol{x}_{i1}^T)^T 
		\in \mathbb{R} \times \mathbb{R}^{k_i -1} \mid
	\| \boldsymbol{x}_{i1} \|_2 \le \boldsymbol{x}_{i0}
\}
$$
つまり,$$\boldsymbol{x} = (\boldsymbol{x}_1^T, \boldsymbol{x}_2^T, \dots ,)^T$$であり任意の$$i$$に対して,$$\boldsymbol{x}_i \in \mathcal{K}_i $$



### 混合01二次錐計画

$$
\begin{align*}    &\underset{\boldsymbol{x}}{\text{minimize}}        & & \boldsymbol{c}^T \boldsymbol{x}\\    &\text{subject to}        & & A \boldsymbol{x} = \boldsymbol{b}\\    &   & & \boldsymbol{x} \succeq 0\\    &   & & \boldsymbol{x}_j \in \{0,1\} &(j \in J \subset \{1,\dots \})\\\end{align*}
$$



## 最適化問題における現在の研究潮流

線形$$\subset$$ニ次錐$$\subset$$半正定値$$\subset$$凸最適化

→現在は半正定値問題なら上手く解けることが知られているので, 研究テーマとしてはより一般的な凸最適化もしくは最新の研究成果を組み合わせながら実問題や別の問題に適応するなどが推奨される?

一方,非凸最適化は解きにくい

九大の脇先生→多項式最適化(最近の流行りの研究で目的関数と制約式が多項式)



## 最適化問題の変形テクニック

### 特定のパスを除く制約

$$\mathcal{P}$$を除きたいパスの集合,$$x_a$$を枝$$a$$を通る時に1,通らない時に0をとる変数だとすると
$$
\sum_{a \in P} x_a \le |P| -1 \quad (\forall P \in \mathcal{P})
$$


### スイッチ制約

定数$$v_{\min}, v_{\max}$$と変数$$x \in \{0,1\}, v \in \mathbb{R}$$が与えられたとする.この時
$$
\begin{align*}
	v_{\min} &\le v \le v_{\max} \quad &\text{if  } x = 1\\
	&v = 0 &\text{if  } x =0
\end{align*}
$$
の制約式は$$v_{\min}x \le v \le v_{\max}x$$と等価



### 目的関数に2乗を含む時に二次錐計画に変換

以下のように目的関数に$$x^2$$を含む時
$$
\begin{align*}
    &\underset{x \ge 0}{\text{minimize}}
        & & x^2 \\
    &\text{subject to}
        & & x \in \mathcal{F}
\end{align*}
$$

以下のように二次錐計画に変形することができる.$$t+1 \ge 0$$のとき
$$
t \ge x^2
\Leftrightarrow 
(t+1)^2 \ge (t -1)^2 + (2x)^2 
\Leftrightarrow 
(t+1) \ge \sqrt{(t -1)^2 + (2x)^2 }
$$
であるので,上記の最適化問題は以下のように書き表せる.
$$
\begin{align*}
    &\underset{t, x \in \mathbb{R}}{\text{minimize}}
        & & t \\
    &\text{subject to}
        & & x \in \mathcal{F}\\
    &   & & 
   		\left(
   			\begin{array}{c}
   				t+1\\
   				t-1\\
   				2x
   			\end{array}
   		\right) \in \mathcal{K}
\end{align*}
$$
ただし$$\mathcal{K}$$は以下のように定義する.
$$
\mathcal{K} \equiv \{
	\boldsymbol{x} = (\boldsymbol{x}_0, \boldsymbol{x}_1) \in \mathbb{R} \times \mathbb{R}^{n-1}
	\mid
	\boldsymbol{x}_0 \ge \| \boldsymbol{x}_1 \|_2
\}
$$



### 目的関数が分数の場合

####例1

$$c>0$$を定数として以下の最適化問題を考える
$$
\begin{align*}
    &\underset{x \ge 0, u \in \mathbb{R}}{\text{minimize}}
        & & \frac{c}{x} 
\end{align*}
$$
この時上記は以下の最適化問題と同値
$$
\begin{align*}
    &\underset{x \ge 0}{\text{minimize}}
        & & u\\
    &\text{subject to}
        & & u \ge \frac{(\sqrt{c})^2}{x}
\end{align*}
$$
ここで制約式より$$u \ge 0$$であるので$$u+x \ge 0$$であることに注意すると
$$
u \ge \frac{(\sqrt{c})^2}{x}
\Leftrightarrow
(u+x)^2 \ge (u-x)^2 + 2(\sqrt{c})^2
\Leftrightarrow
 u + x \ge \sqrt{(u-x)^2 + (s\sqrt{c})^2}
$$
であるので
$$
\begin{align*}
    &\underset{x \ge 0}{\text{minimize}}
        & & u\\
    &\text{subject to}
        & & 
   		\left(
   			\begin{array}{c}
   				u + x\\
   				u -x \\
   				2\sqrt{c}
   			\end{array}
   		\right) \in \mathcal{K}
\end{align*}
$$

#### 例2

 $$a,b,c \in \mathbb{R}$$は$$a \ge 0, b > 0, b + c >0$$を満たしている定数として以下の最適化問題を考える
$$
\begin{align*}
    &\underset{x \in \{0,1\}}{\text{minimize}}
        & & \frac{ax}{b + cx}
\end{align*}
$$
この時,$$x^2 = x$$であることに注意すると
$$
\begin{align*}
    &\underset{x \in \{0,1\}}{\text{minimize}}
        & & a u\\
    &\text{subject to}
        & & u \ge \frac{x^2}{b + cx}
\end{align*}
$$
制約式を満たしてい流とき$$u+(b+cx) \ge0$$であることに注意すると,上記と同様に
$$
u \ge \frac{x^2}{b + cx}
\Leftrightarrow
 u (b + cx) \ge x^2
\Leftrightarrow
	(u+b+cx)^2 \ge (u - (b+cx))^2 + (2x)^2
$$
であるので,
$$
\begin{align*}
    &\underset{x \in \{0,1\}}{\text{minimize}}
        & & au\\
    &\text{subject to}
        & & 
   		\left(
   			\begin{array}{c}
   				u + b + cx\\
   				u - (b + cx) \\
   				2x
   			\end{array}
   		\right) \in \mathcal{K}
\end{align*}
$$




