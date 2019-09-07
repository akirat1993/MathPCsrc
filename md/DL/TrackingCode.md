[TOC]

## スクリプト

### SORT

[Simple Online and Realtime Tracking](https://arxiv.org/abs/1602.00763)の実装

`ds:/data0/akirat/py3_util/MySORT.py>unit_SORT_tracking`

`ds:/data0/share/deep_learning/SORT`

`ds:/data0/akirat/sgw/seamless_tagging`



### 検知/追跡/描写のコード

* 動画から物体検知(M2Det)及び,追跡(SORT)までの一覧の流れを実行するスクリプト
  `ds:/data0/share/deep_learning/M2DetSORT.zip`

  `local:/Users/akirat/backup/M2DetSORT.zip`



## M2Det

### 概要

* ディレクトリパス

  (初盤)渡○さん`ds:/data0/akirat/MOT/M2Detw`

* 推論ファイル

  `exec/detect_video.sh`

* 学習させる場合

  1. `data/VOCdevkit`以下にデータを追記
  
  2. `/configs/m2det800_vgg.py`>`dataset =`を編集
  
  3. `train.py`を実行
  
     

### 変更点

* `utils/nms_wrapper.py>nms`の`return cpu_soft_nms(dets, thresh, method = 1)`となっているところをそのまま使うと同じ人物を何重にも検知してしまっていましたが,`return cpu_nms(dets, thresh)`と変更したら上手くいきました.
* `M2DetW/.python-version`の部分を自分のpythonのバージョンに変更



## 結果

### 元データ

- **camera位置**:camera0,1→斜め上, camera4→人の背丈視点
- **撮影時の服装**:TypeA→自由, TypeB→トップス白,パンツ黒
- **撮影シーン(S)**:S1→対面交差,S2→対角線交差,S3→ランダムな動きを入れならが端から端に移動,S4→自由行動,S5→障害物あり対面交差,,S6→障害物ありUターン



### 検知+トラッキング

####Pretrainの(YOLOv3,M2Det)+SORTアルゴリズムを適応した結果

``` bash
ds:/data0/share/AIST_Pana_Labo/201711/public/track
	README.txt/
	PreM2DetSORT/
		*M2Det.csv 検知結果
		*M2Det.mp4 検知結果(動画)
		*SORT.csv 追跡結果
		*SORT.mp4 追跡結果(動画)
	PreYOLOv3SORT/
```

**csvフォーマット**

```bash
<frame>,<obj_id>,<bb_left>,<bb_top>,<bb_right>,<bb_bottom>,<obj_conf>,<class_conf>,<class_id>
	※<frame>は1始まり
	※int型:<frame>,<obj_id>,<class_id>
	※float型:<bb_left>,<bb_top>,<bb_right>,<bb_bottom>,<obj_conf>,<class_conf>
	※<bb_left>は相対位置ではなくピクセルを表す
	※トラッキング前は<obj_id>は-1
	※トラッキング後は<obj_conf>と<class_conf>は1を代入
	※<obj_id>,<classs_conf>,<class_id>が無い場合は-1を代入
```



## Backup

### 動画をMacで再生できるように変換

```
ffmpeg -i original.mp4 -vf scale=1920:-1 out_movie.mp4
```

`scale=1920`は横幅を1920,縦幅は元動画と同じaspect比を保つように設定



## Backup2



## 検知スクリプト

```
CUDA_VISIBLE_DEVICES=1 python detect_video.py --video test_video/sgw/camera0/TypeA_S1_P8.mp4 --model_def data/TypeA_yolo/config/yolov3.cfg --class_path data/TypeA_yolo/config/classes.txt --weights_path checkpoints/TypeA_yolo_e149.pth
```



| 適応カメラ  | 物体検知モデル    | トラッキング | ファイル名                                                   |
| :---------- | :---------------- | :----------- | :----------------------------------------------------------- |
| camera0,1,4 | M2Det(Pretrained) | SORT         | Tracking結果: `camera番号_Type[A|B]_S(シーン番号)_P(撮影人数)_Pretrain_M2Det_M2DetSort.[mp4|csv]` 検知結果 `camera番号_Type[A|B]_S(シーン番号)_P(撮影人数)_Pretrain_M2Det.[csv|mp4]` |

動画やカメラについて

- **camera位置**:camera0,1→斜め上, camera4→人の背丈視点
- **撮影時の服装**:TypeA→自由, TypeB→トップス白,パンツ黒
- **撮影シーン(S)**:S1→対面交差,S2→対角線交差,S3→ランダムな動きを入れならが端から端に移動,S4→自由行動,S5→障害物あり対面交差,,S6→障害物ありUターン

末尾が`.csv`は以下のフォーマット

```
<frame>,<obj_id>,<bb_left>,<bb_top>,<bb_right>,<bb_bottom>,<obj_conf>,<class_conf>,<class_id>
```

- `<class_conf>`はBBのクラス確率で最大のものの確率
- 追跡前は`<obj_id>`は-1
- 追跡後は`<class conf>`は1
- 動画の初めのフレーム`<frame>`は1
- `<bb_left>`~`<bb_bottom>`はfloat型(ピクセルの場所を指定)



検知/トラッキングについて以下の項目について頑強か検証したい.

```
・人数の違い
人数が少ないものを学習に用いているので,その学習が人数が多い場合でも有効か検証
・学習されていない服装でも検知できるのか?
TypeA(服装バラバラ)⇆TypeB(服装統一)
・カメラポジションとアングル
今回,学習に用いたのは上から撮影したcamera0の動画
-別の上から撮影したcamera1
-横から撮影したcamera4
(*3)YOLO形式は以下
<bb_left>,<bb_top>,<bb_right>,<bb_bottom>,<conf>,<class conf>,<class id>,<frame>
※frameは1始まり
(*4)MOT形式は以下
`<frame>, <id>, <bb_left>, <bb_top>, <bb_width>, <bb_height>, <conf>, <x>, <y>, <z>`
※frameは1始まりの連番
CUDA_VISIBLE_DEVICES=1 python detect_video.py --video test_video/sgw/camera0/TypeA_S1_P8.mp4 --model_def data/TypeA_yolo/config/yolov3.cfg --class_path data/TypeA_yolo/config/classes.txt  --weights_path checkpoints/TypeA_yolo_e149.pth
```
