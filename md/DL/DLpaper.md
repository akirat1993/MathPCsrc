[TOC]

## 距離学習(Metric Learning)

* [時系列非線形データに関する距離学習](https://arxiv.org/pdf/1805.12324.pdf)
  
  アブストのみ読んだ.Kernel Hilert spaceを用いてPeron-Frobenius operatorというものを定義及び提案.従来手法は提案手法の特殊ケースとして与えられる.数学よりで面白そう.

## 深層学習

### トップConference

[画像系のTop Conference](http://www.guide2research.com/topconf/computer-vision)

[Computer ScienceのTop Conference](http://www.guide2research.com/topconf/)

[分野別・最新論文のまとめ](https://paperswithcode.com/sota)

### チェックしたまとめサイト

* CVPR2018
  * [CVPR 2018速報](https://www.slideshare.net/cvpaperchallenge/cvpr-2018-102878612)
    深層学習会の動向について詳しい(p64まで流し読み)
  * CVPR 2018に採択された全979論文のサマリ(未読)[AIが作成](https://drive.google.com/open?id=1xJy-MRn9QGWo4rnYm1Mv49jxwdKrwz31),[人間作成](https://github.com/cvpaperchallenge/CVPR2018_Survey)

### 論文

#### ドメイン適応 Domain Adaptation(DA)

##### 概要

転移学習（Transfer Learning）と呼ばれる学習手法の一種です．十分な教師ラベルを持つドメイン（Source Domaind，ソースドメイン）から得られた知識を，十分な情報がない目標のドメイン（Target Domain, ターゲットドメイン）に適用することで，目標ドメインにおいて高い精度で働く識別器などを学習します.ここで,ドメイン（Domain）とは,データの集まりを指す言葉です.特に,目標ドメインが一切のラベルを持たない場合は、Unsupervised Domain Adaptation (UDA) と呼ばれ,ドメイン適応の中でも特に難しいタスクになります．

##### 研究の推移

* ターゲットドメインのサンプルの分布をソースドメインの分布に近付ける(特徴空間を近づける場合も含む)
* ソースドメインの各クラスの分布にターゲットドメインを合わせる



##### まとめサイト

[SVHNのデータで学習しMNISTで数字分類の精度を測定](https://medium.com/@crosssceneofwindff/domain-adaptation-about-adda-cycada-and-mcd-5f10c57f9ea9)

##### 比較

[以下の3つの手法の概要と比較(SVHNで学習,MNISTでテスト)](https://medium.com/@crosssceneofwindff/domain-adaptation-about-adda-cycada-and-mcd-5f10c57f9ea9)

精度(Source Only 0.63, ADDA 0.78, CyCADA 0.81, MCD 0.97)

1. Adversarial Discriminative Domain Adaptation(ADDA)
2. Cycle-Consistent Adversarial Domain Adaptation(CyCADA)
3. Maximum Classifier Discrepancy for Unsupervised Domain Adaptation (MCD)

* Adversarial Discriminative Domain Adaptation (ADDA)
  $p(z | x_s) = p(z | x_t)$になるように学習する
  * 手順:
    * Pre-training:ソースの画像とラベルを用いてSourceCNNとClassifierを学習
    * Adversarial Adaptation:学習済SourceCNNのパラメータで初期化したTargetCNNを用いてターゲット画像から特徴抽出を行う.どちらのドメインから特徴がやってきたかを識別するDiscriminatorを配置し,Adversarial Learningを行うことでTargetCNNとSourceCNNの出力分布を近づける
    * Pre-trainingで学習したClassifierとAdversarial Adaptationで学習したTargetCNNを用いて,ターゲットのテスト画像でラベル予測を行う
  * 派生
    [M-ADDA:Unsupervised Domain Adaptation with Deep Metric Learning](https://arxiv.org/abs/1807.02552v1)
    ICML2018で発表.TripletLossを用いてソースドメインをクラスタリングできるように学習した後にターゲットドメインのクラスタの重心をソースドメインのクラスタの重心に近づけるLossを提案し敵対的学習で訓練.gitにpytorch実装あり.[日本語解説](https://qiita.com/himatya/items/6fefe5d92152265db95a)
* CyCADA
  * 派生
    CyderGAN?
* Maximum Classifier Discrepancy for Unsupervised Domain Adaptation (MCD)
  ソースとターゲットの特徴抽出後の分布を近づける際に各クラスの分布も考慮する.
  * 派生
    * [Sliced Wasserstein Discrepancy for Unsupervised Domain Adaptation](https://arxiv.org/pdf/1903.04064.pdf)
      Sliced Wasserstein Distanceを用いてより精度を向上させた論文(CVPR2019でAccept)
    * [DeepJDOT:Deep Joint Distribution Optimal Transport for Unsupervised Domain Adaptation](https://arxiv.org/pdf/1803.10081.pdf)(ECCV2018の論文)

#### 異常検知

* 参考資料
  [手法の大別と概要](https://fisproject.jp/2019/03/deep-learning-for-anomaly-detection-1/)
* 論文
  * [Anomaly Detection using One-Class Neural Networks](https://arxiv.org/abs/1802.06360)
    教師無し異常検知手法.One Class SVMをニューラルネットに発展させた手法.SVMのパラメータと深層学習のパラメータを交互に学習?[日本語解説](https://www.smartbowwow.com/2018/12/anomaly-detection-using-one-class.html)
  * [GANomaly: Semi-Supervised Anomaly Detection via Adversarial Training (ACCV 2018)](https://arxiv.org/abs/1805.06725)
    * 疑問
      adversarial lossの部分は機能してる?
    * 説明資料
      [AnoGAN, Efficient-GAN-Anomalyの違いあり](https://qiita.com/masataka46/items/a905465f2a93c90f62ea)
  * [EFFICIENT GAN-BASED ANOMALY DETECTION(Efficient GAN/EGBAD), ICLR(2018)](https://arxiv.org/pdf/1802.06222.pdf)
    * 説明資料
      [日本語資料](https://qiita.com/masataka46/items/49dba2790fa59c29126b)

#### Attention

* 概要
  [Attentionの日本語解説スライド](https://www.slideshare.net/yutakikuchi927/deep-learning-nlp-attention)
  入力系列をEncoderによって一つの固定長ベクトルにするのではなく,Encoder中の各隠れ層をとっておいてdecoderの各ステップで使う(加重平均など)
  (翻訳,文章要約,対話生成)
* [Adaptive Computation Time for Recurrent Neural Networks (ACT)](https://arxiv.org/abs/1603.08983)
  RNNの各出力ステップの計算量を動的に変化させることで精度向上を図る手法.[日本語解説](https://qiita.com/shotasakamoto/items/80809657c4492721b709)



#### 蒸留(Distillation)

* 概要
  一度訓練したモデルが学習した知識を別の軽量なモデルに継承させる.
  実応用の本番環境の計算リソースが十分でない場合の対処を想定.
* 用語
  教師モデル:通常の教師あり学習の方法で訓練したモデル
  生徒モデル:教師モデルの出力を正解ラベルの代わりに使用,あるいは正解ラベルに追加して訓練した軽量なモデル
* 解説記事
  [概要が掴める記事](https://bit.ly/2VQvhX8)
* 論文
  * [Data Distillation (CVPR2018)](https://arxiv.org/abs/1712.04440)
    複数の変換を施した画像を教師モデルに入力、各変換画像に対して得られる教師モデルの出力を平均することで、生徒モデルを訓練するための正解ラベルを得ます。正解ラベルなしデータを正解ラベルありデータに追加して利用することで、正解ラベルありデータのみでの教師あり学習以上の精度が得られることが報告されている.
  * [Born Again Neural Networks (ICML2018)](https://arxiv.org/abs/1805.04770)
    教師モデルと同程度のキャパシティを持つ生徒モデルに蒸留することで、教師モデルを凌ぐ性能の生徒モデルが得られることが報告

#### GAN

* [Wasserstein GAN (CVPR2018)](https://arxiv.org/pdf/1701.07875.pdf)

  * 重要な点
    様々なG ANの学習に組み入れることが可能みたい

  * 概要
    通常のGANの目的は最終的にJensen-Shannon divergenceという距離のもとで真のデータの分布とGeneratoraが作成するデータの分布を一致させることにあるが,Generatorの最適値付近では勾配が0になり学習がうまくいかなくなることが知られており,代わりにWasserstein距離を用いた損失関数を使用することでGANの学習を安定させる手法.

  * 解説
    [大まかな概要 日本語](https://qiita.com/triwave33/items/5c95db572b0e4d0df4f0)
  * 派生
    WGAN-GP

* [目的別GAN+指定した種類の画像を生成するGAN(ACGAN)](https://bit.ly/2yZjWLI)

#### ネットワーク構造

- [Squeeze-and-Excitation Networks(SeNets)](https://arxiv.org/abs/1709.01507)
  CNNに特化したAttention機構でコードも仕組みも超簡単.畳み込み層の各チャネルを均等に出力せず,適応的に重みをかける.これをCNNに追加しても計算量は1%しか増えず,性能の向上が期待される.例えば,ResNet-50に適応することで性能はResNet-101相当になり計算量は半分になる.[解説](https://qiita.com/daisukelab/items/0ec936744d1b0fd8d523)
  ImageNet2017で1位のネットワーク.SENetを使った手法がNIPSお論文でちらほら見かける

- U-Net(入力画像の高次の特徴を残す手法)

  - 概要

    ①Upサンプリング②マージ③全結合層がない④少ない教師データでの学習方法

  * 応用例
    
  [MRI画像から肝臓領域の抽出 & U-Netの簡単な説明](https://lp-tech.net/articles/5MIeh)
    
    [手書き文字のスキャン時に生じたぼやけ・かすれなどのノイズ除去](https://confit.atlas.jp/guide/event-img/jsai2018/4M1-01/public/pdf?type=in)
    
    [細胞のセグメンテーション](https://blog.negativemind.com/2019/03/15/semantic-segmentation-by-u-net/)
    
    [自動歌声分離](https://qiita.com/xiao_ming/items/88826e576b87141c4909)

- [Capsule Network (CapsNet)](https://qiita.com/motokimura/items/cae9defed10cb5efeb62)というNN(特にCNN)の強化版(ニューロンがベクトル)のようなものがあって、PyTorchで実装・およびMNISTで検証した記事がありました

- [Non-local Neural Networks](https://arxiv.org/abs/1711.07971)
  
CNNやRNNは局所的な特徴抽出をするため,画像全体やシーケンス全体の特徴も扱えるようにする手法.全結合層との違いは線形和の重みの部分が類似度になっていること.導入することで動画像の分類や物体検出,領域分割において性能が向上した.[要約記事](https://uiiurz1.hatenablog.com/entry/2018/12/30/152038)

#### 学習時の工夫

* [PackNet CVPR2018](https://arxiv.org/abs/1711.05769)
  
  1つのNNで複数のタスクを学習.畳み込みと全結合層の小さい重みを削除→残りを再訓練して固定.削除した重みを次タスクの学習に利用.単純で強力.pytorch実装あり.