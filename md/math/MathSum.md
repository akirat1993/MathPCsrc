[TOC]

## 実数の構成

* [ペアノの公理を満たす集合の構成(英語)(ZF公理系 分出公理等を仮定!?)](https://math.stackexchange.com/questions/68659/set-theoretic-construction-of-the-natural-numbers)
  
* [ピアノの公理から実数,複素数まで構成](http://mathematics-pdf.com/pdf/construction_of_numbers.pdf)
  
    丁寧で凄く良い資料.ピアノの公理を満たす集合を自然数とすることから出発して(公理を満たす集合が存在することは証明しない)、整数、有理数、実数、複素数を順に構成する教科書です。順序、絶対値、最大公約数、素数なども扱ってます.自然数の整列性、有理数・実数の稠密性、実数の完備性、Archimedesの性質 などを証明.

## 代数

* [2項関係,順序](./relation_order.md)
* 体上の多項式に関する除法定理(Remainder Theorem)
* [複素数係数の多項式の因数分解](http://www.ms.u-tokyo.ac.jp/activity/documents/tsuji.pdf#search=)
* [多項式の積の可換(associativity) 証明](https://math.stackexchange.com/questions/77671/how-to-show-associativity-of-multiplication-of-polynomials-in-rx-where-r)

## 微積

### 基礎

* Calculus / Michael Spivak
  
  初学者にもオススメの証明が詳しい微積の入門書.$$\log$$を積分で定義してその逆関数として指数(exponential)を定義しているので$$\forall x \in \mathbb{R}$$に対して$$\exp(x)$$を自然に定義することができるので良い.$$\cos, \sin$$も高校で習ったような半径1の円を考えるのではなく積分で直接定義している点も良かった.$$\epsilon \text{-} \delta$$論法は時たま省略されていたり,証明に少し補足が必要な箇所が数箇所見受けられた
  
* [各点収束,一様収束周り](./calculus_compl.md)

* [連続・微分・1変数積分 教科書](https://math.dartmouth.edu/~doyle/docs/calc/calc.pdf)←例が多くて冗長だったので部分的に参考にした教科書

* [ロルの定理の証明](https://oregonstate.edu/instruct/mth251/cq/Stage7/Lesson/rolles.html),[平均値の定理の証明(英語)](https://www.math.hmc.edu/calculus/tutorials/mean_value/proof_mean.html)
  
* [行列をベクトルで微分するときの公式一覧](https://qiita.com/AnchorBlues/items/8fe2483a3a72676eb96d)
  
* [陰関数定理で偏微分の値が0でない条件はなぜ必要かを直感的に説明している教科書                                                                                                                                                                              ](https://lecture.ecc.u-tokyo.ac.jp/~nkiyono/kiyono/16_6-12.pdf)

### 初等関数

- 乗冪
  - [初めに読むといいかも](http://www.math-konami.com/lec-data/ch23.pdf)
  - [n乗根の存在の証明](http://ckottke.ncf.edu/neu/3150_fa15/nthroots.pdf)
  - [乗冪を実数に拡張](https://math.stackexchange.com/questions/55068/can-you-raise-a-number-to-an-irrational-exponent)

## 集合

* [有限集合の濃度は一意に定まることの証明](./set.md#有限集合の濃度は一意に定まることの証明の補足)

* [ネットに落ちてた濃度の基礎(実数全体と自然数の部分集合全体の濃度は等しいなど)](http://www.math.titech.ac.jp/~kotaro/class/2011/set/lecture.pdf  )
  
  説明が不十分な部分があるため別の資料などを参考にして用いると良い. 
  
  ※ベルンシュタインの定理はWikipedia等を参考にすると良い 
  
* [有限集合の部分集合は有限集合の証明 第一段落、Fact2. A subset of a finite set is finite](http://math.uga.edu/~pete/settheorypart1.pdf)

* [有限集合の和集合は有限集合 URL>Theorem 3 (Fundamental Properties of Finite Sets)](https://sites.math.washington.edu/~lee/Courses/300-2017/finite-sets.pdf  )
  
  証明はないが上記"有限集合の部分集合は有限集合の証明"を用いれば(a)は簡単に示せて、(b),(c)の証明も比較的容易  
  
* [任意の無限集合は加算無限集合をもつ](https://math.stackexchange.com/questions/1403416/infinite-set-always-has-a-countably-infinite-subset)

* [無理数の濃度と実数の濃度は等しい(証明の概略のみ)](https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q11110681666)

* [Ramsey's theorem](https://en.wikipedia.org/wiki/Ramsey%27s_theorem#Infinite_Ramsey_theorem)
  
  鳩ノ巣原理の一般化で前提知識無しで読めるのでオススメ
  
* [Ordered Set (Partial/Total, Well Ordering)](https://www.whitman.edu/mathematics/higher_math_online/section05.03.html)

* [Any infinite totally ordered set contains a monotone sub-sequence ($$x_0 \le x_1 \le x_2 \dots$$ or $$x_0 \ge x_1,\dots$$)](https://math.stackexchange.com/questions/716461/proof-verification-every-sequence-in-bbb-r-contains-a-monotone-sub-sequence)

* [The cartecian product of a finite amount of countable sets is countable](https://math.stackexchange.com/questions/2357899/the-cartesian-product-of-a-finite-amount-of-countable-sets-is-countable)

## 位相空間

* [Topology without tears](./TopologyWithoutTears.md)
  
    位相空間の学び直しに使用したネットに落ちてる教科書.説明が凄く丁寧なので初学者にもオススメ.事前知識は集合論のみ必要.実数の構成とか濃度の概念とか知ってるとつまずくところはないかも.

* [位相空間の定理の補足](./topology.md)

    * 定理:ハウスドルフ空間上のコンパクト集合は閉集合

* [線形位相空間(Topological Vector Space)](http://www.ma.huji.ac.il/~razk/iWeb/My_Site/Teaching_files/TVS.pdf)←まあまあ良かった英語の教科書.

* ノルム空間
    * [有限次元ノルム空間の任意のノルムは同値(p24 A.5)](http://www.ma.noda.tus.ac.jp/u/sh/pdfdvi/13fa-s.pdf)
    
        [保存用p24 A5](https://www.slideshare.net/secret/bwAxb39joMUra5)
    
    * [ノルム全般](./norm.md)
      
        * 定理:ノルムが定まっている有限次元ベクトル空間はR^nと位相同型
        
    * [有限次元線形写像の連続性](https://ja.wikipedia.org/wiki/%E4%B8%8D%E9%80%A3%E7%B6%9A%E7%B7%9A%E5%9E%8B%E5%86%99%E5%83%8F)
    
    * [Subset of finite dimensional norm equal to 1 is compact](https://math.stackexchange.com/questions/895142/proof-of-compactness-for-sets-of-norm-equal-to-one-in-finite-dimensional-normed)
    
    * [Matrix Norm についての資料 少し良い](https://www.uio.no/studier/emner/matnat/ifi/nedlagte-emner/INF-MAT4350/h08/undervisningsmateriale/chap13slides.pdf)
    
    * [Calculation of operator norm when p = 2](https://math.stackexchange.com/questions/1877202/why-is-the-operator-norm-so-hard-to-calculate)
    
    * $$L_p$$ノルム空間
        * $$0 < p < 1$$のとき,$$\sum_{i=1}^n \| x_i - y_i \|^p$$は距離を定める.
            * $$(a+b)^p \le a^p + b^p$$の[証明(今は権限が必要みたいで閲覧不可)](https://matthewhr.files.wordpress.com/2012/09/lp-spaces-for-p-in-01.pdf)
        * $$1 \le p$$のとき, $$ \left( \sum_{i=1}^n | x_i |^p \right)^{1/p}$$
            * $$\lim_{p \rightarrow \infty} \| x \|_p = \| x \|_{\infty}$$の[証明](https://math.stackexchange.com/questions/326172/the-l-infty-norm-is-equal-to-the-limit-of-the-lp-norms/326266)
            * [p-norm is monotone decreasing](https://bit.ly/2HVxCuT)

## グラフ理論

* [Algorithm Design / Jon Kleinberg, Eva Tardos-1st. ed.](http://www.icsd.aegean.gr/kaporisa/index_files/Algorithm_Design.pdf)
  
    * 最大流問題などネットワーク問題について丁寧な証明つきで載っているの初学者にオススメ
* Detail  
        ISBN 0-321-29535-8  
        Prepress and Manufactureing Caroline Fell  
        Printer: Courier Westford  
    
* [最小費用流(Minumum Cost Flow)](MCF.md)
  
    最小費用流を解くためのアルゴリズムが証明つきで詳しく載っているのでオススメ.負の費用を扱う方法など拡張も載っている点もGood

* [スペクトラル・クラスタリング](spectral.md)
  
* オススメされた

    * ネットワーク・大衆・マーケット ―現代社会の複雑な連結性についての推論
      

## 線形代数

* 線形空間と線形写像
    * [テキスト1](http://staff.miyakyo-u.ac.jp/~k-taka2/pdf/linalg/chap5.pdf   )
    
    * [テキスト2](http://wwwa.pikara.ne.jp/yoshifumi/FLA/FLA-7.pdf  )
      
      Prop7.1.7 線形写像が同型(全単射)である必要十分条件  
    
    * [行列式(det)は連続関数であることの証明(英語)](https://math.stackexchange.com/questions/1314411/proof-that-determinant-is-continuous-using-epsilon-delta-definition)
    
    * [半正定値行列の同値条件(対称行列,エルミート行列)](https://risalc.info/src/positive-semi-definite-properties.html)
    
    * [コレスキー分解](choleskey.md)
    
* 行列  
    * [特異値分解(singular value decomposition) 未読](https://wiki.math.ntnu.no/_media/tma4205/2017h/svd.pdf )
      



## 確率(probability)

### 並び替え(sort)

* [重み付きランダムソート(Weighted Random Sampling)](./WRS.md)



### 確率論

+ [Measure Theory and Probability Theory](./measure_and_probability_theory1.md)
  
  + [~Chapter1-3](measure_and_probability_theory1.md)
  + [Chapter1.4~Chapter1-5](measure_and_probability_theory2.md)
  
  測度論と確率論についてscrachから勉強出来る良書.証明が省略されている場合があるので,その部分について上記で補足.自分で補足しながら勉強することで理解が深まるのでその点でも良い教科書.前提知識はある程度必要で集合論・濃度・位相空間ぐらい勉強した後に学習した方が理解が深まると思う.濃度については(countable union of countable set is also countable)ぐらいの証明を理解しとけば十分.190523時点でカラテオドリの定理まで学習(私自身はフビニの定理くらいまではこの教科書で勉強するまでに授業で学習済み)
  
+ ベイジアンネットワーク

    * [グラフィカルモデル 渡辺 有祐](./PGM_TB01.md)

+ [多変量正規分布について良さそうな教科書](http://www012.upp.so-net.ne.jp/doi/math/anova/m_normal.pdf)

## 最適化(Optimization)

+ 0-1整数計画  
    * [整数計画法における定式化入門](http://web.tuat.ac.jp/~miya/fujie_ORSJ.pdf)
      
      入門書として最適化教科書.定式化のテクニックもいくつか載ってる.例えば線型方程式のうち$$p$$個のみ満たす制約の入れ方(big-M).区分線形関数上の点の表現の仕方.論理積.



## 測度論

* [Measure Theory and Probability Theory](./measure_and_probability_theory1.md)
  
  測度論と確率論についてscrachから勉強出来る良書.証明が省略されている場合があるので,その部分について上記で補足.自分で補足しながら勉強することで理解が深まるのでその点でも良い教科書.前提知識はある程度必要で集合論・濃度・位相空間ぐらい勉強した後に学習した方が理解が深まると思う.濃度については(countable union of countable set is also countable)ぐらいの証明を理解しとけば十分.190523時点でカラテオドリの定理まで学習(私自身はフビニの定理くらいまではこの教科書で勉強するまでに授業で学習済み)
  
  - [~Chapter1-3](measure_and_probability_theory1.md)
  - [Chapter1.4~Chapter1-5](measure_and_probability_theory2.md)



## 凸関数

* [凸関数全般](./convex.md)

  * 定義:凸集合,凸関数
  * 定理:R上の任意のノルムは凸関数
  * 凸関数の勾配の単調性$$ \langle \nabla f(x) - \nabla f(y), x - y \rangle \ge 0$$

* [First and second order characterization(下記の証明)](http://www.princeton.edu/~amirali/Public/Teaching/ORF523/S16/ORF523_S16_Lec7_gh.pdf)

  $$f(y) \ge f(x) + \nabla ^T f(x) (y-x), \nabla^2 f(x) \ge 0$$ 

* [停留点が最小値の証明(stationary point is a global minimum)](https://people.seas.harvard.edu/~yaron/AM221-S16/lecture_notes/AM221_lecture8.pdf)

* [二階微分が半正定値ならば凸関数の証明(second derivative is nonnegative everywhere implies convex)](http://math.ucr.edu/~res/math133/convex-functions.pdf)



## 幾何学

* [図形全般](./geom.md)
  * 平行多面体,楕円,アフィン変換による像
* [楕円の離心率・法線ベクトル・パラメータ表示](./GEO_lat.md)



## その他

* [異常検知と変化検知(井出剛 杉山将)](./異常検知と変化検知.md)

* [入門 機械学習による異常検知 Rによる実践ガイド(井手剛)](機械学習による異常検知.md)

* [マップマッチング補足](Frechet.md)