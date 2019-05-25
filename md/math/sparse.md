スパースモデリングに関しては[今日から出来るスパースモデリング](http://www-adsys.sys.i.kyoto-u.ac.jp/mohzeki/Presentation/lecturenote20150902.pdf )を参考にしました. 

文中で省略されている証明について以下で簡単に補足していますので,必要であれば適宜参照していただると幸いです.

## 1変数の場合
$$\lambda \gt 0$$, $$y \in \mathbb{R}$$を固定する.  
このとき以下の最適化問題を解く.
$$
\begin{align*}
    & \underset{x \in \mathbb{R}}{\text{minimize}}
        & & \left\{
            |x| + \frac{1}{2 \lambda} (y - x)^2
        \right\}
\end{align*}
$$
(解法)
$$
\begin{align*}
    & \underset{x \in \mathbb{R}}{\text{minimize}}
        & & \left\{
            |x| + \frac{1}{2 \lambda} (y - x)^2
        \right\}\\
    = & \underset{}{\text{min}}
        && \left\{
            \underset{x \ge 0 }{\text{minimize}} \left\{
                |x| + \frac{1}{2 \lambda} (y - x)^2
            \right\},
            \underset{x \le 0 }{\text{minimize}} \left\{
                |x| + \frac{1}{2 \lambda} (y - x)^2
            \right\}
        \right\}
\end{align*}
$$
であるので,$$x \ge 0, x \le 0$$の2つに分けて考える.  
$$x \ge 0$$のとき  

$$
|x| + \frac{1}{2 \lambda} (y - x)^2
= x + \frac{1}{2 \lambda} (y - x)^2
= \frac{1}{2 \lambda} (x - (y-\lambda))^2 + y - \frac{\lambda}{2}
$$
ここで, $$\frac{1}{2 \lambda} (x - (y-x))^2 \ge 0$$であり, $$y - \frac{\lambda}{2}$$が定数であることに注意すると,  
(i)  $$ y - \lambda \ge 0$$のとき  
$$x = y - \lambda$$で最小値 $$y - \frac{\lambda}{2}$$をとる.  
(ii) $$ y - \lambda \lt 0$$のとき
$$
\begin{align*}
0 \le x_1 \le x_2 
    &\Rightarrow   0 \le x_1 - (y-\lambda) \le x_2 - (y-\lambda)\\
    &\Rightarrow  \frac{1}{2 \lambda} 
                    \left(
                        x_1 - (y-\lambda)
                    \right)^2 \le
                  \frac{1}{2 \lambda} 
                    \left(
                        x_2 - (y-\lambda)
                    \right)^2 
\end{align*}
$$
より$$x=0$$のとき最小値$$\frac{1}{2 \lambda} (y-x)^2 + y - \frac{\lambda}{2}$$をとる.  
同様に,一方,$$x \le 0$$のとき
$$
|x| + \frac{1}{2 \lambda} (y - x)^2
= -x + \frac{1}{2 \lambda} (y - x)^2
= \frac{1}{2 \lambda} (x - (y+ \lambda))^2 - y - \frac{\lambda}{2}
$$
として上記と同様に求める.

## 多変数の場合
$$\lambda \gt 0$$, $$\mathbf{y} \in \mathbb{R}^N$$を固定する.  
このとき以下の最適化問題を解く.
$$
\begin{align*}
    & \underset{\mathbf{x} \in \mathbb{R}^N}{\text{minimize}}
        & & \left\{
            |\mathbf{x}|_1 + \frac{1}{2 \lambda} || \mathbf{y} - \mathbf{x}||_2^2
        \right\}
\end{align*}
$$
(解法)

$$
\begin{align}
    ||\mathbf{x}||_1 + \frac{1}{2 \lambda} || \mathbf{y} - \mathbf{x}||_2^2
    &= \sum_{i=1}^N |x_i| + \frac{1}{2 \lambda} \sum_{i=1}^N (y_i - x_i)^2\\
    &= \sum_{i=1}^N |x_i| + \frac{1}{2 \lambda} (y_i - x_i)^2
\end{align}
$$
である.ここで,
$$
\begin{align*}
    & \underset{\mathbf{x} \in \mathbb{R}^N}{\text{minimize}}
        & & \sum_{i=1}^N |x_i| + \frac{1}{2 \lambda} (y_i - x_i)^2
        = \sum_{i=1}^N 
            \underset{x_i \in \mathbb{R}}{\text{minimize}}
                \left\{
                    |x_i| + \frac{1}{2 \lambda} (y_i - x_i)^2 
                \right\}
\end{align*}
$$
であることを示す.  
この等式の左側を(左辺),右側を(右辺)と以後表記する.  

1変数の例から任意の$$i \in \{1,\dots ,N\}$$に対して,  
$$|x_i| + \frac{1}{2 \lambda} (y_i - x_i)^2$$が最小値を取るような$$x_i^*$$が存在する.  
そこで,$$\mathbf{x}^* = (x_1^*, \dots , x_N^*)^T$$とする.  
このとき,任意の$$\mathbf{x} = (x_1, \dots , x_N)^T \in \mathbb{R}^N$$に対して,$$\mathbf{x}^*$$の定義より,
$$
    |x_i^*| + \frac{1}{2 \lambda} (y_i - x_i^*)^2 
    \le 
    |x_i| + \frac{1}{2 \lambda} (y_i - x_i)^2 
    \quad( \forall i \in \{1,\dots ,N\})
$$
であるので,
$$
\text{(right)} = \sum_{i=1}^N |x_i^*| + \frac{1}{2 \lambda} (y_i - x_i^*)^2 
    \le 
    \sum_{i=1}^N |x_i| + \frac{1}{2 \lambda} (y_i - x_i)^2
$$
これが任意の$$\mathbf{x} = (x_1, \dots , x_N)^T \in \mathbb{R}^N$$に成り立つので,  
左辺は$$\mathbf{x} = \mathbf{x}^*$$のとき最小値$$\sum_{i=1}^N |x_i^*| + \frac{1}{2 \lambda} (y_i - x_i^*)^2$$をとる.(最小値をとる$$\mathbf{x}$$が存在することが示せた)  
また,(右辺)$$\le$$(左辺)が成立することがわかる.

逆に,
$$
\begin{align*}
        &\underset{\mathbf{x} \in \mathbb{R}^N}{\text{minimize}}
        \sum_{i=1}^N |x_i| + \frac{1}{2 \lambda} (y_i - x_i)^2\\
        \le& \sum_{i=1}^N 
            |x_i^*| + \frac{1}{2 \lambda} (y_i - x_i^*)^2 \\
        =& \sum_{i=1}^N
            \underset{x_i \in \mathbb{R}}{\text{minimize}}
                \left(
                    |x_i| + \frac{1}{2 \lambda} (y_i - x_i)^2
                \right)
        = \text{(right)}
\end{align*}
$$
よって,(左辺)$$\le$$(右辺)

## ベイズの定理
観測行列を$$A \in \mathbb{R}^{m \times n}$$,原情報を$$x \in \mathbb{R}^n$$, 出力情報を$$ y \in \mathbb{R}^m$$とする.  
出力情報は入力情報を観測行列によって変換したものに,ノイズが加えられて得られるとする.
$$
y = Ax+ \rho_0n
$$
ここで$$\rho_0 >0,n \in \mathbb{R^m}$$とする.

観測情報$$A$$と原情報$$x$$,観測情報$$A$$と原情報$$y$$は互いに独立であるから,  
$$P(A \cap x) = P(A) \cap P(x)$$,  
$$P(A \cap y) = P(A) \cap P(y)$$
が成立することに注意すると,
$$
P(x | A,y) P(A) P(y) = P(y | A, x) P(A) P(x)
$$
が成立する.  
(Proof)
$$
\text{(left)} = \frac{P(x \cap A \cap y)}{P(A \cap y)} P(A) P(y)
= \frac{P(y \cap A \cap x)}{P(A \cap x)} P(A) P(x) 
    \frac{P(A \cap x)}{P(A \cap y)} \frac{P(y)}{P(x)}
= \text{(right)}
$$
ゆえに,
$$
P(x | A,y)  = \frac{P(y | A, x)P(x)}{P(y)}
$$
が成立.

##メジャライザー最小化
$$
\begin{align*}
|x - y|_2^2 
&= \sum_{i=1}^n (x_i - y_i)^2\\
&= \sum_{i=1}^n 
    \left(
        x_i - (y_i - \frac{1}{L}\nabla g(y)_i) - \frac{1}{L} \nabla g(y)_i
    \right)^2\\
&= \sum_{i=1}^n 
    \left(
        x_i - (y_i - \frac{1}{L}\nabla g(y)_i) 
    \right)^2
    -\frac{2}{L} \nabla g(y)_i
        \left(
            x_i - (y_i - \frac{1}{L}\nabla g(y)_i)
        \right)
    + \frac{1}{L^2} (\nabla g(y)_i)^2\\
&= \left| 
    x - (y - \frac{1}{L}\nabla g(y)) 
  \right|_2^2
  - \frac{2}{L} \nabla g(y)^T (x-y) 
  - \frac{1}{L^2} |\nabla g(y)|_2^2 
\end{align*}
$$

初めに以下を示す
$$
g(x) \le q_L(x,y)
$$
(Proof)  
$$\nabla g(x)$$はリプシッツ定数$$L$$の連続関数だから,シュワルツの不等式より
$$
\left( \nabla g(x) - \nabla g(x) \right)^T (x - y) 
\le \| \nabla g(x) - \nabla g(x) \|_2 \| x - y \|_2 \le L \| x - y \|_2^2  
$$
$$h: \mathbb{R}^n \rightarrow \mathbb{R}$$を
$$h(x) = \frac{1}{2} L \| x \|_2^2 - g(x)$$と定めると,  
$$\nabla h(x) = Lx - \nabla g(x)$$であり,上式より  
$$
\left( 
    \nabla h(x) - \nabla h(y)
\right)^T (x - y) \ge 0
$$
である. $$h \in C^1$$級であるので,$$h$$は凸関数.ゆえに,
$$
\begin{align*}
    &h(x) \ge h(y) + \left( \nabla h(y) \right)^T (x -y)\\
\Leftrightarrow 
    & g(x) \le q_L(x,y)
\end{align*}
$$
証明のための予備知識  
[URL>Theorem1,2](http://www.princeton.edu/~amirali/Public/Teaching/ORF523/S16/ORF523_S16_Lec7_gh.pdf),[URL > Proposition1.3](https://www.math.cuhk.edu.hk/course_builder/1617/math6211a/cvxop.pdf)

次に以下を示す.

$$g(x) = | y - Ax|_2^2$$とすると,  
$$
\nabla g(x) = - \frac{1}{\lambda} A^T (y - Ax)
$$
(Proof)
$$
 \left (
    \nabla g(x)
 \right)_i
 = \frac{\partial g (x)}{\partial x_i}
 = \frac{1}{2 \lambda} \frac{\partial}{\partial x_i}\sum_{j=1}^m 
    \left(
        y_i - \sum_{i=1}^n a_{ji} x_i
    \right)^2
= - \frac{1}{\lambda} \sum_{j=1}^m a_{ji}
    \left(
        y_i - \sum_{i=1}^n a_{ji}x_i
    \right)
$$
一方,
$$
\left(
    - \frac{1}{\lambda} A^T (y - Ax)
\right)_i
= - \frac{1}{\lambda} \sum_{j=1}^m a_{ji}
    \left(
        y_j - \sum_{i=1}^n a_{ji} x_i
    \right)
$$
次にリプシッツ定数$$L$$は

$$L = \frac{1}{\lambda} |A^T A|_2$$

となることを示す.

(Proof)
$$
|\nabla g(x_1) - \nabla g(x_2)| 
= \frac{1}{\lambda} |A^T A (x_2 - x_1)|_2 \le \frac{1}{\lambda} |A^TA|_2 |x_1 - x_2|_2
$$
ここで,任意の行列$$A \in \mathbb{R}^{n,n}$$に対し,
$$
 |A|_2 := max_{|x|_2 = 1} |Ax|_2
$$
と定義する.  
有限次元ベクトル空間上のノルムが1となる部分集合はコンパクト,    
有限次元線形写像やノルムの連続性を用いることで右辺の集合は最大値を持つことが示される.   
また, $$|A|_2 = max_{|x|_2 = 1} |Ax|_2$$は$$x$$が$$A$$の最大の固有値$$\mu_0$$に対応する固有ベクトルを持つとき最大になり,その値は$$\sqrt{\mu_0}$$



