## VAEを解説

理解が曖昧なので,測度論→確率をやってからまた更新します.

### 仮定

* データ$$x \in X$$は特徴空間$$Z$$上の標準正規分布$$\mathcal{N}(\mathbb{0},I)$$に従う点$$z$$から条件付き確率$$p(x \mid z)$$に従って得られていると考える.

* $$p(z \mid x)$$は正規分布に従う(この仮定が特徴空間上で近ければデータも近いという性質を生み出す)

* Encoder $$q(z \mid x)$$
  データ$$x$$が与えられた時にそのデータが特徴空間上のどこからきたのか$$p(z \mid x)$$を近似する条件付き分布$$q(z \mid x)$$

* Decoder $$D:Z \to X$$

  は.$$x$$が与えられた時,$$| D(z) - x|$$が小さいなら$$p(x \mid  z)$$が大きく,逆に$$| D(z) - x|$$が大きいなら$$p(x \mid z)$$が小さいという性質を満たしているとする.($$z \sim q(z \mid x)$$とする)

  これは復元が上手くいくなら$$z$$は$$x$$の生成元になっている可能性が高い.$$z \sim q(z \mid x)$$であることを踏まえるとEncoderが真の分布$$p(z \mid x)$$を上手く近似できていると言える.

  この時以下が成立

  $$
\int q(z \mid x) \| D(z) - x \|dz \text{ is small} \\
  \Rightarrow
  \int q(z \mid x) \log p(x \mid z) dz = E_{z \sim q(z \mid x)}[\log p(x \mid z)] \text{ is large}
  $$
  
  
  Proof.

  $$\int q(z \mid x) \| D(z) - x \|dz$$が小さいとすると,
$$
  \int_{z:\| D(z) - x \| \text{ is small} } q(z \mid x) dz
  $$
  は大きく,逆に
  $$
  \int_{z:\| D(z) - x \| \text{ is large}} q(z \mid x) dz
  $$
  は小さくなるはずである.この時
  $$
  \begin{align*}
  	\int q(z \mid x) \log p(x \mid z) dz
  	= &\int_{z:\| D(z) - x \| \text{ is small}} q(z \mid x) \log p(x \mid z) dz\\
  		+ &\int_{z:\| D(z) - x \| \text{ is large}} q(z \mid x) \log p(x \mid z) dz\\
  		+ \text{ other}
  \end{align*}
  $$
  であり第1項に関してはDecoderの仮定より$$p(x \mid z)$$は大きくまた$$q(z \mid x)$$の積分に関する考察により一項目は大きくなる.2項目以降に対しても同様の考察により右辺は大きくなる.
  
  

$$\| \cdot \|$$はノルムを表しているとする.

$$q(z \mid x)$$の$$p(z \mid x)$$に関するカルバック・ライブラー情報量$$KL(q(z \mid x) \| p(z \mid x))$$の最小化を目指す.[page2→2.2 Variational Lower Bound](https://nzw0301.github.io/notes/vae.pdf)に記載されている式変形を用いると

$$
0 \le KL(q(z \mid x)\| p(z \mid x)) 
= \log p(x) - \int q(z \mid x) \log p(x \mid z) dz + KL(q(z \mid x) \| p(z))
$$
となるので,
$$
\int q(z \mid x) \log p(x \mid z) dz - KL(q(z \mid x) \| p(z))
$$
の最大化に帰着される.2項目に関しては$$q(z \mid x)$$は深層学習のネットワークから得られ,正規分布$$p(z)$$は標準正規分布に従っているのだから直接計算できる.また1項目についてはDecoderの仮定より$$\int q(z \mid x) \| D(z) - x \|dz$$を小さくすればよいので$$q(z \mid x)$$からデータを任意にとってきて復元誤差をできるだけ小さくすればよい.(Reparametaraization Trick)などを使う

[解説詳しそう](http://www.1-4-5.net/~dmm/ml/vae.pdf)

[VAE元論文](https://arxiv.org/pdf/1312.6114.pdf)