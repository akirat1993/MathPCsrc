
[TOC]
# Spectral Clustering


## Formalization
###Given  
* An undirected graph $$G=(V, E)$$ ($$|V| = n$$)
* The edge $$(v_i, v_j)$$ is weighted by similarity $$w_{i,j}$$

###Optimization problem
$$
\begin{align*}
    &\underset{A_i \subset V}{\text{minimize}}
        & & \sum_{i=1}^{k} 
            \frac{\text{cut}(A_i, \overline{A_i})}
                {\text{Vol} (A_i)}\\
    &\text{subject to}
        & & \bigsqcup_{i = 1}^k A_i = V
\end{align*}
$$
where $$\overline{A}$$ is the complement of $$A$$, and "cut(A)" and "vol(A)" $$(A \subset V)$$ are defined by
$$
\begin{align*}
    \text{cut}(A, \overline{A}) 
        &= \sum_{v_i \in A, v_j \in \overline{A}} w_{i,j}\\
    \text{vol}(A)
        &= \sum_{v_i \in A} d_i
         = \sum_{v_i \in A} \sum_{v_j \in V} w_{i,j}
\end{align*}
$$
We denote $$d_i$$ by the degree of node $$v_i$$.

## Preparation
> Def(unnormalized graph Laplacian matrix)  
> We denote $$D$$ by the degree matrix defined by  

$$
D = \text{diag}(d_1, \dots ,d_n)
 = \begin{pmatrix}
       d_1 & & &\\
       & d_2 & &\\
       & & \ddots& \\
       & & & d_n
   \end{pmatrix}
$$

> We denote $$L \equiv D - W$$ be the unnormalized graph Laplacian matrix  

-
> Theorem1  
> For every vector $${f} \in \mathbb{R}^n$$ we have

$$
f' L f = \frac{1}{2} \sum_{i,j} w_{i,j} (f_i - f_j)^2
$$

(proof)
$$
\begin{align*}
    f'L f &= f'(D -W)f\\
        &= \sum_{i} d_i f_i^2 - \sum_{i,j} w_{i,j} f_i f_j\\
        &= \frac{1}{2}\big(
                \sum_{i} d_i f_i^2- \sum_{i,j} w_{i,j} f_i f_j + \sum_{j} d_j f_j^2
            \big)\\
        &= \frac{1}{2} \sum_{i,j} w_{i,j}(f_i - f_j)^2
\end{align*}
$$

-
> Theorem2  
> For $$A_l \subset V, h_l \equiv (h_{1,l}, \dots , h_{n,l})' \in \mathbb{R}^n$$, where 

$$
h_{i,l} \equiv \frac{\mathbb{1}_{A_l}(v_i)}{\sqrt{\text{vol}(A_l)}}
$$

> and 

$$
\mathbb{1}_{A_l}(v_i) \equiv \begin{cases}
       1 \quad &(v_i \in A_l)\\
       0 \quad &(\text{otherwise})
   \end{cases}
$$

> Then, we have

$$
h'_l L h_l = \frac{\text{cut}(A_l, \overline{A_l})}{\text{vol}(A_l)}
$$

(proof)
$$
\begin{align*}
    h'_l L h_l 
        &= \frac{1}{2} \sum_{i,j} w_{i,j}(h_{i,l} - h_{j,l})^2\\
        &= \frac{1}{2} \sum_{i,j} w_{i,j} \Big(
                \frac{\mathbb{1}_{A_l}(v_i)}{\sqrt{\text{vol} A_l}}
               -\frac{\mathbb{1}_{A_l}(v_j)}{\sqrt{\text{vol} A_l}}
            \Big)\\
        &= \sum_{v_i \in A_l, v_j \in \overline{A_l}} w_{i,j} \frac{1}{\text{Vol}(A_l)}\\
        &= \frac{\text{cut}(A_l, \overline{A_l})}{\text{Vol}(A_l)}
\end{align*}
$$

-
> Theorem3  
> $$h_l' D h_m = \delta_{l,m}$$

(proof)  

$$
\begin{align*}
    h'_l D h_m &= \sum_{i} d_i h_{i,l} h_{i,m} \\
        &= \sum_{i} d_i 
             \frac{\mathbb{1}_{A_l}(v_i)}{\sqrt{\text{vol} A_l}}
             \frac{\mathbb{1}_{A_l}(v_i)}{\sqrt{\text{vol} A_m}}\\
        &= \delta_{l,m}
\end{align*}
$$

## Relaxation
$$
\begin{align*}
  &\underset{A_i \subset V}{\text{minimize}}
     & & \sum_{i=1}^{k} 
         \frac{\text{cut}(A_i, \overline{A_i})}
             {\text{Vol} (A_i)}\\
 &\text{subject to}
     & & \bigsqcup_{i = 1}^k A_i = V\\
\Leftrightarrow   
  &\underset{A_i \subset V}{\text{minimize}}
     & & \mathrm{Tr}(H'LH)\\
 &\text{subject to}
     & & \bigsqcup_{i = 1}^k A_i = V\\
 &   & & H'DH = I_k\\
\simeq
  &\underset{H \in \mathbb{R}^{n \times k}}{\text{minimize}}
     & & \mathrm{Tr}(H'LH)\\
 &\text{subject to}
     & & H'DH = I_k\\
\Leftrightarrow   
  &\underset{T \in \mathbb{R}^{n \times k}}{\text{minimize}}
     & & \mathrm{Tr}(T'D^{-1/2}LD^{-1/2}T)\\
 &\text{subject to}
     & & T'T = I_k\\
 &   & & (T = D^{1/2}H)
\end{align*}
$$



> We call those of equations (1), (2), (3), and (4) from above. 

proof(1)$$\Leftrightarrow$$(2)
$$
\begin{align*}
    \mathrm{Tr}(H'LH) 
        &= \sum_{l = 1}^k h_l' L h_l\\
        &= \sum_{l=1}^k \frac{\text{cut}(A_l, \overline{A_l})}{\text{vol}(A_l)}
\end{align*}
$$


$$(l, m)$$ element of $$H'DH$$ = $$h'_l D h_m = \delta_{l,m}$$  

proof(3)$$\Leftrightarrow$$(4)

(3)$$\Rightarrow$$(4)  

If $$H$$ is the optimal solution of (3), we set $$T = D^{1/2}H$$. Then, we have $$T'T = H' D^{-1/2} D^{-1/2} H = H' D^{-1} H = I_k$$, thus $$H$$ is the feasible solution of (4). Moreover, we have
$$
\begin{align*}
    \mathrm{Tr}(T' D^{-1/2} L D^{-1/2} T) 
    &= \mathrm{Tr}(H' L H)
\end{align*}
$$
Therefore, the optimal value of (4) is less than or equal to the optimal value of (3). The other is proved in the same way.  

For solving optimization of (4), we show below theorem.

> Theorem4 (Extermal partial trace)  
> 行列$$A \in \mathbb{C}^{n \times n}$$をエルミート行列とし,その固有値を$$\lambda_1,\cdots,\lambda_n$$. 対応する固有ベクトルを$$u_1,\cdots , u_n, \langle u_i, u_j \rangle = \delta_{i,j}$$とする. このとき, 固有値について$$\lambda_1 \le \lambda_2 \le \cdots \le \lambda_n$$が成立しているならば,任意の$$q \in \{1,2,\dots,n\}$$と正規直交系$$\{x_1, \cdots, x_q:x_i \in \mathbb{C}^{n \times n}, \langle x_i, x_j \rangle = \delta_{i,j}\}$$に対して,

$$
\sum_{i=1}^q \lambda_i \le \sum_{i=1}^q x_i^* A x_i
$$

> が成立.さらに,$$x_i = u_i \,(i=1,2,\cdots ,q)$$ ならば等号が成立.

Proof.
$$A$$はエルミート行列なので,固有値は全て実数でありユニタリ行列によって対角化出来ることに注意する.(証明略)  
$$A$$はエルミート行列なので,
$$
U A U^* 
= \begin{pmatrix}
    \lambda_{1} & & \\
    & \ddots & \\
    & & \lambda_{n}
  \end{pmatrix}
= diag(\lambda_1, \dots , \lambda_n)
$$
となるような$$U = (u_1, u_2, \dots , u_n)^*$$をとることができる.
ここで,$$x_1,x_2, \dots , x_q, x_{q+1}, \dots x_{n}$$が$$\mathbb{C}^n$$の正規直交基底になるように$$x_{q+1}, x_{q+1}, \cdots, x_n$$をとる. また, $$X := (x_1, \dots, x_n)$$と定義する.このとき,
$$
\begin{align*}
	X^* A  X
		 = \begin{pmatrix}
			x_1^*\\
			\vdots \\
			x_n^*
			\end{pmatrix} A (x_1, \dots, x_n)
		 = \begin{pmatrix}
				x_1^* A\\
				\vdots \\
				x_n^* A
			\end{pmatrix} (x_1, \dots, x_n)
\end{align*}
$$
ゆえに,$$X^* A  X$$の$$(i,j)$$成分は $$x_i^* A x_j$$ と表される.
ここで任意の正方行列$$B \in \mathbb{C}^n$$に対して$$s$$次主小行列(首座小行列) principal submatrix を $$B_s$$と表記することにする. つまり
$$
\begin{align*}
	B = \begin{pmatrix}
			b_{11} & b_{12} & \cdots &b_{1n}\\
			b_{21} & b_{22} & \cdots & b_{2n}\\
			\vdots & \vdots & \ddots & \\
			b_{n1} & b_{n2} & \cdots &b_{nn}
		\end{pmatrix},
	B_s = \begin{pmatrix}
			b_{11} & b_{12} & \cdots &b_{1s}\\
			b_{21} & b_{22} & \cdots & b_{2s}\\
			\vdots & \vdots & \ddots & \\
			b_{s1} & b_{s2} & \cdots &b_{ss}
		\end{pmatrix}
\end{align*}
$$
このとき,
$$
\sum_{i=1}^q x_i^* A x_i = \mathrm{Tr} \Big[ (X^* A X)_q \Big]
$$
が成立.一方で
$$
\begin{align*}
	(i,j) \text{ element of } X^* A X 
	&= (i,j) \text{ element of } X^* U^* diag(\lambda_1, \dots , \lambda_n)\\
	&= (i,j) \text{ element of } Y^* diag(\lambda_1, \dots , \lambda_n) Y \quad (Y = UX \in \mathbb{C}^n)\\
	&= \sum_{k=1}^n | y_{ki}|^2 \lambda_k
\end{align*}
$$
以上より,
$$
\begin{align*}
	\sum_{i=1}^q x_i^* A x_i 
		&= \mathrm{Tr} \Big[ (X^* A X)_q \Big]\\
		&= \sum_{i=1}^q \sum_{k=1}^n | y_{ki}|^2 \lambda_k\\
		&= \sum_{k=1}^n \Bigg(
				\sum_{i=1}^q | y_{ki}|^2
			\Bigg) \lambda_k
\end{align*}
$$
ここで,$$U,X$$はユニタリ行列であるので,$$Y = UX \in \mathbb{C}^{n \times n}$$もユニタリ行列.(例えば任意の$$a, b \in \mathbb{C}^{n \times n}$$に対して, $$ \langle UXa, UXb \rangle　= \langle a, b \rangle$$ を示せば良い.)
ゆえに,行ベクトルの長さは1であるので,
$$
0 \le \sum_{i=1}^q |y_{ki}|^2
	\le \sum_{i=1}^n |y_{ki}|^2 = 1 
	\quad (k \in \{1,2, \dots , n\})
$$
また,列ベクトルの長さは1であるので,
$$
\sum_{k=1}^n \sum_{i=1}^q |y_{ki}|^2 =  \sum_{i=1}^q \sum_{k=1}^n |y_{ki}|^2 = q
$$
よって, $$\sum_{i=1}^q x_i^* A x_i = \sum_{k=1}^n \Bigg(\sum_{i=1}^q | y_{ki}|^2\Bigg) \lambda_k$$は
$$
\begin{align*}
	\sum_{i=1}^q | y_{ki}|^2 
		= \begin{cases}
				1 \quad (k \in \{1,2, \dots, q\})\\
				0 \quad (others)
			\end{cases}
\end{align*}
$$
のとき最小値$$\lambda_1 + \cdots + \lambda_q$$をとる.
(気持ちとしては出来るだけ小さい$$\lambda_k$$に$$| y_{ki}|$$を割り当てることを考える.)
また, $$x_i = u_i \quad (i=1, 2, \dots ,q)$$ならば,
$$
X^* A X = U U^* diag(\lambda_1, \dots ,\lambda_n) U U^* = diag(\lambda_1, \dots ,\lambda_n)
$$
であるので等号成立.

### Solving below optimization problem

$$
\begin{align*}
     &\underset{T \in \mathbb{R}^{n \times k}}{\text{minimize}}
        & & \mathrm{Tr}(T'D^{-1/2}LD^{-1/2}T)\\
    &\text{subject to}
        & & T'T = I_k\\
    &   & & (T = D^{1/2}H)
\end{align*}
$$
Let $$T$$ be
$$
\begin{align*}
    T \equiv (\mathbf{x}_1, \dots ,\mathbf{x}_k)
\end{align*}
$$
where $$\mathbf{x}_i \in \mathbb{R}^n$$. Considering the constraint, we have
$$
T'T = I_k
	\Leftrightarrow
    \langle \mathbf{x}_i, \mathbf{x}_j \rangle = \delta_{i,j}
$$
, which implices $$\mathbf{x}_i, \dots ,\mathbf{x}_k$$ are orthogonal system. If we see $$D^{-1/2}LD^{-1/2} \in \mathbb{R}^{n \times n}$$ as the $$A$$ of theorem4,
$$
\begin{align*}
    \mathrm{Tr}(T' D^{-1/2} L D^{-1/2} T) 
    = \mathrm{Tr}(T'AT)
    = \sum_{l=1}^k \mathbf{x}_i' A \mathbf{x}_i
\end{align*}
$$

Therefore, if we list eigenvalues of $$A = D^{-1/2} L D^{-1/2}$$ in ascending order $$\lambda_1,\dots, \lambda_n$$ and the corresponding orthgonal system $$\mathbf{u}_1,\dots, \mathbf{u}_k$$, we get the optimal value of $$\sum_{l=1}^k \lambda_k$$ when $$T = (\mathbf{u}_1,\dots, \mathbf{u}_k)$$.

---

When clustering, we set $$H \equiv D^{-1/2}T \in \mathbb{R}^{n \times k}$$ and $$y_i \equiv (h_{i,1}, \dots , h_{i,k}) \in \mathbb{R}^k \quad (i = 1, \dots n)$$, we apply the other clustering method to $$\{y_i \mid v_i \in V\}$$

### Reference
https://www.slideshare.net/pecorarista/ss-51761860
