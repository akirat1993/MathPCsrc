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

[Semantic Image Synthesis with Spatially-Adaptive Normalization](https://arxiv.org/pdf/1903.07291.pdf)