[TOC]

## 概要

中学2年生まで長崎で育ち,中学3年と高校の3年間を沖縄で過ごす(高校まで公立校).大学では数学を専攻し,現在は応用数学専門の博士課程2年.企業との共同研究を通して実問題の解決に取り組みつつ,趣味で純粋数学を英語で学び直し中

### 専門

**深層学習,グラフ理論,最適化,機械学習**

### キーワード

* 深層学習
  敵対的学習(GAN), AE,ドメイン適応,異常検知, 畳み込みネットワーク(CNN), 物体検出
* グラフ理論
  避難計画,辞書式最速流,最小費用流,最大流
* 最適化
  0-1整数計画
* 機械学習
  ガウス過程回帰・分類,スパースモデリング,クラスタリング,サポートベクターマシン(SVM)

### 経験

* 辞書式最速流を深層学習を用いた避難時間の最速避難時間の見積もり
* SSDを用いた物体検出
* IntroVAE(GANとVAEを組み合わせた手法)を用いた異常検知
* 実問題に関する整数計画の定式化

### 取得スキル

* Pytorch,Caffe, Chainer, Kerasなど深層学習モジュールを用いたデータ並列型のマルチGPUの実装及びOptunaを用いたハイパーパラメータ探索.
* klearnなどPythonモジュールを用いた回帰・分類問題の実装及びplotlyやmatplotlibを用いた結果の可視化



## 研究活動

### 査読付き論文

* Nozomi Hata, Takashi Nakayama, Akira Tanaka, Takashi Wakamatsu, Akihiro Yoshida, Nariaki Tateiwa, Yuri Nishikawa, Jun Ozawa, and Katsuki Fujisawa. Mobility Optimization on Cyber Physical System via Multiple Object Tracking and Mathematical Programming, the Fifth International Workshop on High Performance Big Graph Data Management, Analysis, and Mining (BigGraphs 2018), to be held in conjunction with the 2018 IEEE International Conference on Big Data (IEEE BigData 2018), in Seattle, WA, USA, 2018(共著)
* Katsuki Fujisawa, Toyotaro Suzumura, Hitoshi Sato, Koji Ueno, Satoshi Imamura, Ryo Mizote, Akira Tanaka, Nozomi Hata, Toshio Endo, Advanced Computing and Optimization Infrastructure for Extremely Large-Scale Graphs on Post-peta-scale Supercomputers, Advanced Software Technologies for Post-Peta Scale Computing, Springer, 2018, DOI:https://doi.org/10.1007/978-981-13-1924-2_11(共著)
* Nariaki Tateiwa, Nozomi Hata, Akira Tanaka, Akihiro Yoshida, Takashi Wakamatsu,Takashi Nakayama, Katsuki Fujisawa. Hybrid Vehicle Control and Optimization with a New Mathematical Method, The 5th IFAC Conference on Engine and Powertrain Control, Simulation and Modeling, in Changchun, China, 2018(共著)
* Akira Tanaka, Nozomi Hata, Nariaki Tateiwa, Katsuki Fujisawa. Practical Approach to Evacuation Planning Via Network Flow and Deep Learning, the Fourth Interna- tional Workshop on High Performance Big Graph Data Management, Analysis, and Mining (BigGraphs 2017), to be held in conjunction with the 2017 IEEE International Conference on Big Data (IEEE BigData 2017), in Boston, MA, USA, 2017(主著)[paper](https://biggraphs.org/workshop2017.html) [pptx](https://www.slideshare.net/secret/DttCSitV44tFXf)



### その他論文

* Evacuation Planning via Network Flow and Deep Learning (November 2018) 修士論文



 ### 研究発表

* [Map-Matching Algorithms using Shortest Path Algorithm on Time-Expanded Graph, 4th ISM-ZIB-IMI MODAL Workshop on Mathematical Optimization and Data Analysis (March 2019)](https://www.slideshare.net/secret/MxnKUsDzlc3rdc)

* 次元圧縮と非線形分類器を用いた画像による不良品検知, 日本数学会 異分野・異業種研究交流会2018 ポスター発表

* 深層学習とネットワークフローを用いた避難計画に対するアプローチ,九州大学IMI主催 防災・避難計画の数理モデルの高度化と社会実装へ向けて, (December 1st 2017)

* Prediction of Tsunami Evacuation Completion Time by Network Flow Algorithms and Convolutional Neural Network, 2nd ISM-ZIB-IMI MODAL Workshop on Mathematical Optimization and Data Analysis (September 2017)

* [Tsunami Evacuation Planning via Network Flow and Deep Learning Approaches, 九州大学教育改革シンポジウム2017 ポスターセッション (July 10th 2017)](https://www.slideshare.net/secret/nbchbF2oQtNwNi)

* 辞書式最速流と深層学習を用いた避難完了時間の予測, 日本オペレーションズ・リサーチ学会 2017年春季研究発表会 (March 16th 2017)

  

## 主な研究テーマ

* 画像を用いた外観検知技術の開発(博士過程1年)
  少子高齢化で生産年齢人口が減少する日本の現状や近年のIoT技術の発展を踏まえると工場のIT化は喫緊の課題である.その基幹技術である画像を用いた外観検知技術を確立するために,深層学習などの次元圧縮手法と非線形分類手法を適切に組み合わせたモデルを提案した.一般的にガウス過程分類などの表現能力が高い非線形分類手法は計算量が大きく画像など入力の次元数が大きいと適応できない.そのため深層学習の手法の1つであるオートエンコーダや幾何学的手法であるUMAPなどの次元圧縮手法と組み合わせることで高精度の予測モデルを確立した.さらに深層学習を用いて入力画像に近い良品画像を出力するモデルを開発することで,新しい画像に対してはモデルの出力との差分をとることで異常箇所を特定する教師なし学習モデルの確立,及び複数の予測モデルを組み合わせることで精度を向上させるアンサンブル学習などの技術を開発した.

* 辞書式最速流と深層学習を用いた避難計画に対するアプローチ(修士論文)[paper](https://biggraphs.org/workshop2017.html) [pptx](https://www.slideshare.net/secret/DttCSitV44tFXf),[pdf](https://www.slideshare.net/secret/nbchbF2oQtNwNi)

  地震大国の日本では津波を想定した緊急避難計画の重要性が年々高まっている.グラフ理論を用いることで,ある条件下では最適な避難計画(普遍的最速流・辞書式最速流)を提示することができる一方,計算時間の観点から実用が難しいという課題を抱えている.本研究では複数の人口分布に対し最適な避難計画を事前に計算し,その結果を教師データとして深層学習に与えることで,避難完了時間といった避難計画で重要な情報を予測するアルゴリズムを開発した. 実験には大阪市の淀川区の実データを使用したが,人流も含めた大規模なグラフが入力になることが課題であった.そのため,人の移動を色表現で表し大規模グラフを画像と入力として学習させることで,大規模都市にも適用可能なモデルを構築した.また畳み込みネットワークを用いることで,局所的な混雑が全体に及ぼす影響を加味することに成功した.実データを用いた実験によって,提案モデルが高精度かつ高速度の予測ができることを確認した.

* 確率分布と最短路問題を用いたマップマッチング
  地図データとGPSデータが与えられたときに車両が通過した経路を復元する作業をマップマッチングと呼び,本研究では確率分布と最短路問題を組み合わせた手法を提案した.GPSデータはトンネルや高速道路といった地形の影響を受けて誤差が生じるため誤差ベクトルが従う分布を推定した.また,車両は基本的に最短路を通過すると推測されるため,グラフの各枝に対して誤差ベクトルを基に尤度を重みとして与えることでGPSデータの誤差を反映した最短路問題として定式化した.計算時間や精度の観点から従来手法を上回る成果が挙げられており,IoT社会に広く普及することを期待する.



## 研究活動の様子

私が所属している研究室では約7社との共同研究があり,プロジェクト毎にリーダーとメンバーが割り当てられ学生主体で研究開発を行っている.各プロジェクトの学生リーダーは必要に応じて課題解決のための議論の場を設けて,定式化やプログラム実装の役割分担を行い研究開発及び成果報告を行っている.私は第一期生ということもあり,基本的には全てのプロジェクトにアドバイザー参画し,そのうち2つのプロジェクトに関してはプロジェクト全体の進捗管理や実装の中心的役割を担っている.そのため,実問題に対して適応できる最新技術を論文等で模索するとともに必要に応じて改良や開発を行うことで,研究開発を進めている.