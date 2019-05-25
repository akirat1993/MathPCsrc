[TOC]

### 重みの初期値

* Xavierの初期値->重み=randn*(層のノードの数によって変化させる係数)
  SSDのextra_netのConv層のweightで使われていた.ただし,biasではconstが使われている.

### パラメータ調整

* ハイパーパラメータのopunaの自動枝刈りの機能が強力そう.
  深層学習において,ここでいう枝刈りとは最初に指定したepoch数に達してなくても「学習率がこれ以上下がらなそうだったり」、「lossが大きすぎる場合」は途中で学習を終了し,別のハイパーパラメータを探索することをいう.
  
[枝刈りの様子を視覚的に描写](https://qiita.com/koshian2/items/107c386f81c9bb7f8df3)
  
  [Optunaの公式サイト 実際に使う時](https://optuna.readthedocs.io/en/latest/reference/trial.html)

### ネットワークの可視化

https://github.com/HarisIqbal88/PlotNeuralNet

#### データセットについて

* CPUでデータを読み込んで訓練時にGPUを使用する場合は`torch.utils.data.DataLoader`の`pin_memory=True`とすることでデータをGPUに移動することきの時間が短縮される[参考文献](https://discuss.pytorch.org/t/when-to-set-pin-memory-to-true/19723)

### データセットについて

### アノテーション形式について

VOCフォーマット`<xmin>`は1始まりでWまで



## 理論

### 複数の特徴量をまとめる関数

$$f$$は任意の$$ \{\mathbf{x}_i\}_{i=1}^n \subset \mathbb{R}^m$$と任意の$$n$$次の置換$$\rho$$に対して,
$$
f(\mathbf{x}_1, \dots   ,\mathbf{x}_n )= f(\mathbf{x}_{\rho(1)}, \dots   ,\mathbf{x}_{\rho(n)} )
$$
を満たしている.

この時,$$f$$は任意の$$ \{\mathbf{x}_i\}_{i=1}^n \subset \mathbb{R}^m$$と任意の$$n$$次の置換$$\rho, \sigma$$に対して,
$$
f(\mathbf{x}_{\sigma(1)}, \dots   ,\mathbf{x}_{\sigma(n)} )
= f(\mathbf{x}_{\rho(1)}, \dots   ,\mathbf{x}_{\rho(n)} )
$$
が成立することを示せ.





>  線形関数では複数の特徴量をまとめる関数は実質的に構成できない.

$$\mathbf{x}_i$$:$$i$$番目の細胞の特徴量とする

任意の$$ \{\mathbf{x}_i\}_{i=1}^n \subset \mathbb{R}^m$$ただし $$\mathbf{x}_i =  (x_{i1}, \cdots ,x_{im} )^T \in \mathbb{R}^m $$,任意の$$n$$次の置換$$\sigma, \rho$$に対して,
$$
f(\mathbf{x}_{\sigma(1)}, \dots   ,\mathbf{x}_{\sigma(n)} )
= f(\mathbf{x}_{\rho(1)}, \dots   ,\mathbf{x}_{\rho(n)} )
$$
を満たす関数$$f: \mathbb{R}^{n \times m} \rightarrow \mathbb{R}$$を求めたい.上記は
$$
f(\mathbf{x}_1, \dots   ,\mathbf{x}_n )= f(\mathbf{x}_{\rho(1)}, \dots   ,\mathbf{x}_{\rho(n)} )
$$
を満たす$$f$$を求めることと同値であることは容易に分かる.

まず,$$f$$を深層学習でよく用いられている線形結合の形に限定して考える.つまり
$$
f(\mathbf{x}_1, \dots   ,\mathbf{x}_n )
= \sum_{1 \le i \le n, 1\le j \le m} a_{ij}x_{ij} + b_{ij}
$$
とする.

この時,任意の$$ \{\mathbf{x}_i\}_{i=1}^n \subset \mathbb{R}^m$$,任意の$$n$$次の置換$$\sigma$$に対して仮定より
$$
\sum_{1 \le i \le n, 1\le j \le m} a_{ij}x_{ij} + b_{ij}
= \sum_{1 \le i \le n, 1\le j \le m} a_{ij} x_{\sigma(i)j} + b_{ij} \tag{*1}
$$
が成立する.$$1 \le i_1 < i_2 \le n$$,$$1 \le j_0 \le m$$を任意に固定し,$$i_1$$と$$i_2$$を入れ替える互換を$$\sigma$$とする.このとき,
$$
\begin{align*}
x_{ij} 
= \begin{cases}
	1  & \text{if } i = i_1, j = j_0\\
	0 & \text{otherwise}
\end{cases} 
\end{align*}
\label{Eq}
$$
とする.
(*1)より$$a_{i_1 j_0} = a_{i_2 j_0}$$が成立.よって$$a_j \equiv a_{1j} = \cdots = a_{nj}$$,$$b = \frac{\sum_{i=1}^n \sum_{j=1}^m b_{ij} }{nm}$$
$$
\begin{align*}
	f(\mathbf{x}_1, \dots   ,\mathbf{x}_n )
	&= \sum_{1 \le i \le n, 1\le j \le m} a_j x_{ij} + b\\
	&= \sum_{1 \le i \le n}
		\left(
			\sum_{1\le j \le m} a_j x_{ij} + b_{ij}
		\right)
\end{align*}
$$
となる.

