[TOC]

## 190610Nvidiaワークショップ@産総研

**精度を落とさず深層学習を高速化させる手法**

○手法概要

精度に与える影響が小さい部分の計算は16FPで計算を高速化させる(他は32FP)で計算

3x高速化が見込める

○実装方法

pytorchでは数行で組み込み可能

○16FPと32FPの担当

16FP→ReLU, GEMM, Conv2d

32FP→Softmax, Loss, LossGrad

○その他

Graph Convolution



**DALI Data Loading Library**

cropなどの画像の前処理はcpuで行うため高速化のボトルネックとなっている.それを解決するために画像処理をGPUで処理させる?



**CUDAのその他モジュールとの連携**

sklearnやpandasなどのモジュールがCUDAと連携することで計算が高速化

networkXとcudaとの連携



**その他面白かったこと**

NVIDIA自身も最先端技術の開発に携わりマーケットを広げようと努力してる



**自分メモ**

[GXBOOST](https://qiita.com/yh0sh/items/1df89b12a8dcd15bd5aa)



## 190730 SGW

- Reduced Basis Methods for Partial Differential Equations
  パラメータ付られた偏微分方程式を解く手法(初めに初期解を真面目に解いて,解空間を正規直交化に張る,基本パラメータに対して解空間が連続的なものになることを想定している)



## 190731 ABCIワークショップ

* 富士通:**大規模並列計算で精度向上**に役立った学習率のスケジュール手法の紹介(**Warm-Up**,**Arc-cotangent**→計算コストの増加無し,**L2ノルム**に基づき学習率を層毎にスケーリング→計算コスト増加)

* 日揮:個人の特性(オーナーシップ・バランス)

  自然燃焼型/可燃型(周りのモチベーションが上がると自分も上がる)/不燃型/消化型

* 楽天:言語処理の最新モデルBERT

* 楽天:GBDT(Gradient Boosting Decision Tree)

* ソニー:深層学習をGUIで提供.誰でも簡単に深層学習が出来る

  





