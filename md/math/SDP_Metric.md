## 半正定値行列から誘導される擬距離

> $$V$$を$$F = \mathbb{R}$$ or $$\mathbb{C}$$上のベクトル空間とする.また$$V$$には内積の条件うち$$\langle a, a \rangle = 0 \Rightarrow a \in \mathbf{0}$$ (零ベクトル)のみを満たさない内積に似た関数$$\langle \cdot, \cdot \rangle : V \times V \rightarrow F$$が定まっているとする.この時,関数$$d: V \times V \rightarrow [0, \infty )$$を$$d(x,y) := \sqrt{ \langle x - y, x - y \rangle}$$と定義すると,$$d$$は擬距離(pseudometric)である.
> また、内積が定まっている場合は$$d$$は距離(metric)である.(証明略)

Proof.  

1. $$d(x,y) \ge 0$$  
   正値性(positive-definiteness)より自明.  
   1'. $$d(x,x) = 0$$  
   正値性(positive-definiteness)より$$x$$が零ベクトルならば,$$\langle x, x \rangle = 0$$であるので$$d(x,x) = \sqrt{\langle x -x, x-x \rangle}= 0$$  
2. $$d(x, y) = d(y,x)$$  
   線型性(Linearity)より
   $$d(x,y) = \sqrt{\langle x -y, x-y \rangle} = \sqrt{\langle y -x, y-x \rangle} = d(y,x)$$  
3. $$d(x, z) \le d(x,y) + d(y,z)$$  
   内積の条件から$$\langle a, a \rangle = 0 \Leftrightarrow a = 0$$を除いた,性質を用いて三角不等式$$\| a + b \| \le \| a\| + \|b\|$$が示される.ただし、$$\|\cdot\| = \sqrt{\langle \cdot,\cdot \rangle}$$.
   詳細は「基礎講義　線形代数学 二木昭人 p137-140」を参照.
   ゆえに,三角不等式に$$a = x - y, b = y-z$$を代入すると,

$$
\begin{align*}
		&\| a + b \| \le \| a\| + \|b\|\\
	\Leftrightarrow & \| x - z \|  \le \|x - y \| + \| y - z\|\\
	\Leftrightarrow & d(x,z) \le d(x,y) + d(y,z)
\end{align*}
$$

`

>$$A$$は$$n$$次の半正定値対称行列
>$$\langle \cdot, \cdot \rangle :\mathbb{R}^n \times \mathbb{R}^n \rightarrow \mathbb{R}, \langle a, b \rangle := a^T A b$$を定義する.このとき,$$\langle \cdot, \cdot \rangle$$は内積の条件のうち「$$\langle a, a \rangle \Rightarrow a \text{ is zero vector}$$」のみを満たさない関数である.

Proof.
$$A$$の対称性より内積の対称性(symmetry)、行列の線型性により内積に線型性(Linearity)、$$A$$の半正定値性によって内積の正値性が示される.(詳細は略)



> $$\mathbb{R}^n$$上に対称半正定値行列$$A$$によって定まる関数$$d_{\mathbb{R}^n}: \mathbb{R}^n \times \mathbb{R}^n \rightarrow [0, \infty), d_{\mathbb{R}^n}^A (x, y) = \sqrt{(x-y)^T A (x-y)} \quad (\forall x,y \in \mathbb{R}^n)$$を定義する.このとき,$$d_{\mathbb{R}^n}^A$$は擬距離(pseudometric)である.

Proof.



本題の証明に戻る.
$$\mathbb{R}^n$$は$$\mathbb{R}$$上のベクトル空間であり,
$$
\begin{align*}
	d_{\mathbb{R}^n}^A (x, y) &= \sqrt{(x-y)^T A (x-y)}\\
		&= \sqrt{\langle x - y, x-y \rangle}
\end{align*}
$$
である.よって$$d_{\mathbb{R}^n}^A (x, y)$$は擬距離(pseudometric).

