## 論文
### MOT16入力形式
det.txt

`<frame>, <id>, <bb_left>, <bb_top>, <bb_width>,<bb_height>, <conf>, <x>, <y>, <z>`

```
1,-1,772.68,455.43,41.871,127.61,2.1262,-1,-1,-1
1,-1,717.79,451.29,44.948,136.84,1.7969,-1,-1,-1  
```
※bb=Bounding Box  

※idは人のID(trackingしていない場合は-1)
※`<conf>`検知の信頼度 (確率ではない負の値もとるし,1より大きい正の

### 精度比較のための形式  
`/Users/akirat/project/AIST/DeepSort/data/2akira`

`<id>, <frame>, <bb_left>, <bb_top>, <bb_right>, <bb_bottom>, <DontCate> `

※原点は左上 x軸は右向き y軸は下向きが正の方向  

※DontCare:追跡矩形情報を無視するか否かのフラグ(1:無視する,0:しない)(省略可)

###GMMCPの出力 
`<frame>,<id>,<bb_left>,<bb_top>,<bb_right>,<bb_bottom>`  

※原点は左上 x軸は右向き y軸は下向きが正の方向

### Yoloの出力フォーマット
**ディレクトリ構造**  

```
2akira/
    match5-c0_f1.png
    .
    match5-c0_f9000.png
    match5-c0.avi
    match5-c1_f1.png
    .
    match5-c1_f9000.png
    match5-c1.avi
    .
    match5-c3.avi
    pred_c0_f1.txt
        <left> <top> <right> <bottom>
            ※原点は左上 x軸は右向き y軸は下向きが正の方向
            *スペース区切り
    .
    pred_c0_f9000.txt
    .
    pred_c3_f9000.txt
```



```
pred/
    pred_c0_f1.jpg
    pred_c0_f1.txt
        <bb_left> <bb_top> <bb_right> <bb_bottom> <pro>
            ※原点は左上 x軸は右向き y軸は下向きが正の方向
            *スペース区切り
            *pro=probability 0~1
    .
    pred_c0_f9000.jpg
    pred_c0_f9000.txt
    .
    pred_c1_f1.jpg
    pred_c1_f1.txt
    .
    pred_c2_f1.jpg
    pred_c2_f1.txt
    .
    pred_c3_f1.jpg
    pred_c3_f1.txt
```

###比較実験用ディレクトリ構造DeepSort用
--mot_dir=./MOT16/train

MOT17/test/MOT17-01-DPM

```
/Users/akirat/project/AIST/data/exp/
    train/
        match5-c0/
            det/det.txt
            img1/
                000001.png
                .
                009000.png
        match5-c1
        match5-c2
        match5-c3
```


### Related Work
* 高速だけと精度が悪い(C++Sort)

* 遅いけど精度が高い(GMMCP)  

* C++SORTの改良(appereanceを入れた)  
  
    [deep C++ Sort  GitHub](https://github.com/nwojke/deep_sort)

の2つ及び応用先(スポーツ)のRelated Workをまとめる


## 関連研究
[A Causal And-Or Graph Model for Visibility Fluent Reasoning in Tracking Interacting Objects](https://arxiv.org/pdf/1709.05437.pdf)


###概要  
動画から人や車といった物体の認識だけでなく,人が車に乗った(含まれた)なども合わせて予測する手法.最新の手法を組み合わせて事前確率を計算し考えうる物体の状(visible/occluded/contained)の列で最も確率が高いものを0-1整数計画によって定式化している.また,以下に挙げられる最新の既存研究の技術を総動員したアルゴリズムとなっている.

* Objective Detection(物体の位置と車などのカテゴリを予測する)
* 画像から特徴量を抜き出す技術(appearance description)
* 画像から人の骨格の位置を抜き出す技術(human skelton estimation)
* semantic segmentation(車のドア・トランクなどのパーツの位置を特定)

###所感 
論文では乗用車の乗車・下車が数多く含まれた動画において,追跡精度をKSPと比較していてKSPが精度の面では惨敗している.一方で提案手法のネックと思われる計算時間や事前学習に要した時間などは論文中の記載が一切無いため(隠していると思われる)きちんとした比較はなされていない.類似研究としてIntroductionで軽く述べるのがいいのではないかと思う.

###詳細

####入力(I​)
監視カメラの映像(1台でもOK)
####出力(M)
各時刻の人や車(object)の位置(location),visible state(visible/occuluded/contained),行動(action),特徴量(appearance features) 
※人(ojbect)が車のドアを開けるなどがaction

####定式化
最適解を$M^*$とするとベイズの定理より  
$$
\begin{align*}
    M^* &= \underset{M}{argmin} p(M \mid I)\\
        &\propto \underset{M}{argmin} p(I \mid M) \cdot p(M)
\end{align*}
$$
であるので,
$$
M^* = \underset{M}{argmin} \log{ \left( p(I \mid M) \cdot p(M)\right)}
$$
である.  

$$\log{p(M)}$$について

移動距離に対する確率$$\Phi(\ell_{t+1}^i, \ell_t^i, s_t^i)$$と行動に伴うvisible state変化に関する確率$$\Psi(s_{t+1}^i, s_t^i, a_t^i)$$の和によって定義.  

* $$\ell_t^i$$:時刻$$t$$でのobject$$i$$の位置(location)
* $$s_t^i$$:時刻$$t$$でのobject $$i$$のvisible state(visible/occuluded/contained)
* $$a_t^i$$:時刻$$t$$でのobject $$i$$の行動(action)
  

$$\Phi$$:単位時間での移動距離が閾値より大きい場合は確率を小さく設定  

$$\Psi$$:車のドアを閉めるときなどは人のvisible stateがvisible->containedになりやすいことなどを考慮

$$\log{p(I \mid M)}$$について

出力(M)と映像(I)の一貫性を表し,認識率$$\Upsilon(\ell_t^i, \phi_t^i, s_t^i)$$と行動と映像の一貫性を表す$$\Gamma(\ell_t^i, \phi_t^i, a_t^i)$$の和  

* $$\phi_t^i$$:時刻$$t$$でのobject $$i$$の特徴量

$$\Upsilon$$について:  

* visible stateがvisible->物体の認識率  
* contained->containerの認識率  
* occluded->trackletアルゴリズムを適応して認識率を定義(背景差分などを利用する方法)  

$\Gamma$について:  

* objectが人間->人間がドアを空けた時(action毎)の関節の位置を正規分布に従うと過程して確率に変換
* objectが車->ドアが空けられたとき(action毎)の画像特徴量の平均値とのユークリッド距離を確率に変換

#### アルゴリズム
各物体(object)ごとに各時刻に対しvisible/occluded/containedの層のノードを用意し,定式化の値が大きくなるようにobjectのvisible stateの遷移を求める(0-1整数計画)
イメージはFigure5

---
### 評価指標(MODP,MODA,MOTP,MOTA)
[参考URL](https://catalog.ldc.upenn.edu/docs/LDC2011V03/ClearEval_Protocol_v5.pdf),[fragment](http://shodhganga.inflibnet.ac.in/bitstream/10603/124099/13/13_chapter%205.pdf)

#### Term
* False Negative:undetected ground truth data
* False Positive: detected boxes that do not overlay any ground truth area

####Ovarlap Ratio
* $$G_i^{(t)}$$:i^th ground truth object t^th frame
* $$D_i^{(t)}$$:detected object for $$G_i^{(t)}$$
* $$N_G^t$$: the number of ground truth objects in the i^th frame

$$
\text{Overlap Ration}(i,t) =
    \frac
        {| G_i^{(t)} \cap D_i^{(t)}|}
        {| G_i^{(t)} \cup D_i^{(t)}|}
$$

####Non-binary Decision Threholding
$$
\text{(Non-binary) Thresholded Overlap Ration}(i,t) =
    \frac{T_{NB}}{| G_i^{(t)} \cup D_i^{(t)}|}
$$
where, 
$$
T_{NB} = 
\begin{cases}
    | G_i^{(t)} \cup D_i^{(t)}|, 
        \text{if}
        \frac
            {| G_i^{(t)} \cap D_i^{(t)}|}
            {| G_i^{(t)} \cup D_i^{(t)}|} \ge \text{THRESHOLD}\\
    | G_i^{(t)} \cap D_i^{(t)}|, otherwise
\end{cases}
$$
####Binary Decision Threholding
$$
\text{(Binary) Thresholded Overlap Ration}(i,t) =
    \frac{T_B}{| G_i^{(t)} \cup D_i^{(t)}|}
$$
where, 
$$
T_B = 
\begin{cases}
    | G_i^{(t)} \cup D_i^{(t)}|, 
        \text{if}
        \frac
            {| G_i^{(t)} \cap D_i^{(t)}|}
            {| G_i^{(t)} \cup D_i^{(t)}|} \ge \text{THRESHOLD}\\
    0, otherwise
\end{cases}
$$

####Multiple Object Detection Precision(MODP)
* $$N_{mapped}^t$$: the number of mapped object sets in frame $$t$$


$$
MODP(t) = \frac{1}{N_{mapped}^t}
\sum_{i=1}^{N_{mapped}^t} \text{(Thresholded) Ovarlap Ration}(i,t)
$$
If $$N_{mapped}^t = 0$$, then MODP is forced to a zero value.

$$
\text{N-MODP} = \frac
    {
        \sum_{t=1}^{N_{frames}} MODP(t)
    }
    {N_{frames}}
$$

####Multiple Object Detection Accuracy(MODA)
* $$m_t$$: the number of misses
* $$fp_t$$: the number of false positives
* $$c_m$$ and $$c_f$$ are the cost functions for the missed detects and false alarm penelties.
* $$N_G^t$$: the number of ground truth objects in the i^th frame.

$$
MODA(t) = 1 - \frac
    {c_m(m_t) + c_f(fp_t)}
    {N_G^t}
$$

$$
N-MODA = 1 - 
    \frac
        {
            \sum_{i=1}^{N_{frames}} (c_m(m_i) + c_f(fp_i))
        }
        {
            \sum_{i=1}^{N_{frames}} N_G^i
        }
$$

####Multiple Object Tracking Precision(MOTP)
* $$N_{mapped}$$: mapped objects over the entire track as opposed to just the frame
* $$N^t_{mapped}$$ : the number of mapped objects in the i^th frame

$$
MOTP = \frac
        {
            \sum_{i=1}^{N_{mapped}} \sum_{t=1}^{N_{frames}} \frac{
                |G_i^{(t)} \cap D_i^{(t)}|
            }
            {
                |G_i^{(t)} \cup D_i^{(t)}|
            }
        }
        {
            \sum_{t=1}^{N_{frames}} N^t_{mapped}
        }
$$

####Multiple Object Tracking Accuracy(MOTA)
* $$m$$: the number of missed tracks
* $$fp$$: the total number of false alarm tracks
* $$id_{switches}$$: the total number of ID switches made by the system output for any given reference ID

$$
MOTA = 1 - \frac
        {
            \sum_{i=1}^{N_{frames}}
                \left(
                    c_m(m_i) + c_f(fp_i) + log_e(id_{switches})
                \right)
        }
        {
            \sum_{t=1}^{N_{frames}} N_G^t
        }
$$



