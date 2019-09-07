[TOC]

# Dockerについて

## コマンド解説s

### 説明で使用する記号

- `CONTAINER`->CONTAINER IDを表すことにする.

  CONTAINER IDの確認方法はコンテナを起動してないターミナル上で`docker container ls -a`と打つ.詳細は[ls](#ls)

  ※dockerの各種コマンドに置いて,IDを全て打つ必要はなく**最初の3文字くらいで十分**

  例えば,`docker rm ce519f4e4476`と打つ代わりに`docker rm ce5`でOK



### run

イメージからコンテナを起動する

```bash
#コマンド例
$docker run -it -p 8111:80 -v $PWD/data:/root/vatic/data npsvisionlab/vatic-docker /bin/bash
```

- `-it`

  インタラクティブなシェルを生成するためのオプション(pseudo-TTYをコンテナの標準入力に接続)

- `-p 8111:80`

  コンテナ80番のポートをホストの8111ポートに割り当てる

- `-v /var/www:/var/html`

  `volume`:ホストの`/var/www`をコンテナ内の`/var/html`からアクセスできるようにする(ホストの`/var/www`をコンテナ内の`/var/html`にマウント)

- `/bin/bash`

  コンテナ内で`/bin/bash`を実行する?

### ls

```bash
#起動中のコンテナを表示
docker container ls
#停止中のコンテナを含めて表示
docker container ls -a
```

### start

```bash
#コンテナの起動
docker start CONTAINER
```

### stop

```bash
#コンテナの停止
docker stop CONTAINER
```

### attach

```bash
#起動してるコンテナに接続(ターミナルがフリーズした場合はEnterキーを押す)
docker attack CONTAINER
```

※起動しているかどうかは`docker container ls -a`で確認できる.(`STATUS`が`Exited`の場合は起動していない,`Up 数字 seconds`の場合は起動している)

※起動していない場合は`docker start CONTAINER`で起動させた後にattachする



### detach

コンテナの起動中に以下のコマンドを打つ

* コンテナを起動したまま抜ける場合

  `Ctrl-p Ctrl-q`;コントロールキーを押しながら`p`を入力した後に,コントロールキーを押しながら`q`

  ※コンテナに入り直す場合は`docker attack CONTAINER`

  ※コンテナを停止させる場合は`docker attack stop`,停止させたコンテナに入る場合は`docker start CONTAINER`のコマンドでコンテナを起動させて`docker attach CONTAINER`でコンテナに入り直す

* コンテナを停止させて抜ける場合

  `Ctrl-d`や`exit`と打つ

  停止させたコンテナに入る場合は`docker start CONTAINER`のコマンドでコンテナを起動させて`docker attach CONTAINER`でコンテナに入り直す



## 参考資料

- [Dockerコマンドメモ](https://qiita.com/curseoff/items/a9e64ad01d673abb6866)
- [Docker Document 日本語](http://docs.docker.jp/engine/reference/commandline/run.html#p-expose)
- [Docker Document](https://docs.docker.com/engine/reference/commandline/run/)



# Docker毎の解説



## VATIC

### 概要

**フレーム間の補完機能がある**動画のトラッキング用のアノテーションツール



### 使い方

#### 説明で用いる記号

* `CONTAINER`->CONTAINER IDを表すことにする.

  CONTAINER IDの確認方法はコンテナを起動してないターミナル上で`docker container ls -a`と打つ.詳細は[ls](#ls)

  ※dockerの各種コマンドに置いて,IDを全て打つ必要はなく**最初の3文字くらいで十分**

  例えば,`docker rm ce519f4e4476`と打つ代わりに`docker rm ce5`でOK



1. ローカル環境に以下のようなディレクトリを作成

   ```bash
   data 
   ├── labels.txt #アノテーションしたい対象ラベル
   └── videos_in 
       └── test.mp4 #アノテーションしたい動画をvideos_in直下に配置(1動画のみ)
   ```

   Labels.txtの中身は例えばこんなの

   ```txt
   person
   cat
   dog
   ```

2. イメージからコンテナを起動する

   コマンドの`PATH_TO_DATA`は1.で作成したdataのパス.

   以下のコマンドをローカルで実行

   `$docker run -it -p 8111:80 -v PATH_TO_DATA:/root/vatic/data npsvisionlab/vatic-docker /bin/bash`

   ->`root@数字とアルファベットの列:/#`が表示されればOK

   ※数字とアルファベットの列はContainer ID

   ※`8111`はホストのポートのことでアノテーションを実行する時に用いる

   ※コマンドの意味の詳細は[ここ](#run)

3. ファイルの修正(`ducker run`する度に必要)

   ```bash
   vi /root/vatic/clip.py
   
   Line No.933, 934
   file.write("<height>{0}</height>".format(video.width))
   file.write("<width>{0}</width>".format(video.height))
   >>
   file.write("<height>{0}</height>".format(video.height))
   file.write("<width>{0}</width>".format(video.width))
   ```

   ```bash
   vi /root/vatic/example.sh
   
   #動画が分割されるのを防ぐ
   #通常だと一つの動画が数百フレーム程度で分割されてしまうので,フレーム数を指定
   #動画のフレーム数より多ければ動画全てをアノテーションすることになる
   Line No.7
   TURKOPS="--offline --title HelloTurk!"
   >>
   TURKOPS="--offline --title HelloTurk! --length 10000"
   ```

4. アノテーションを実行

   以下のコマンドをコンテナ上で実行

   `bash /root/vatic/example.sh`

   上記を実行した後に最後にURLが表示されるので(動画の長さによって個数は変わる),URLをブラウザで開く.うまくいかない場合は`:8111`(数字は`docker run`で指定したport番号)を`localhost`の後ろに追記

5. (作業の中断したい場合)

   下記3.のコンテナから抜ける操作は**いつでも実行可能**

   1. ブラウザ上の`Save Works`をクリック

   2. ブラウザのタブを閉じる

   3. [コンテナから抜ける](#detach)

      ※PCを再起動しても作業は保存されるけど,その場合は再起動前にコンテナを停止させとく方が良いと思う

   4. コンテナに再び入って再度`bash /root/vatic/example.sh` を実行してアノテーションを開始

6. 動画1本のアノテーションが終了して保存する

   コンテナ上で`/root/vatic`に移動した後に(`~/vatic#`と表示される)以下のコマンドを実行

   `turkic dump currentvideo -o /root/vatic/data/VOC/ --pascal --pascal-skip 1`

   ※`--pascal-skip 1`のオプションをつけることにより、全てのフレームのデータを出力できます。

   ※`-o /root/vatic/data/VOC`は出力ディレクトリ名.

   `docker run`コマンドで`/root/vadic/data`がローカルの`data`にマウントされてるのでアノテーション結果が保存されている`VOC`はローカル環境の以下の場所に作成される

   ```bash
   data/
   ├── VOC #ここに結果は保存
   ├── frames_in #
   ├── labels.txt
   ├── videos_in
   └── videos_out
   ```

7. 次の動画に移る場合は以下を実行(作業を)

   1. 生成された上記の`VOC`のディレクトリを退避

   2. 6.の`data`ディレクトリ直下の`frames_in`,`videos_out`を削除

   3. `videos_in`に新規の動画を入れる

   4. データベースの初期化

      コンテナ上で`/root/vatic`に移動した後に(`~/vatic#`と表示される)

      ``` bash
      turkic setup --database --reset
      > Reset database? y #yと入力
      ```

   5. **キャッシュの削除**

      ※忘れると前の動画が表示される

      * chromeの場合

        `Chorome(ファイルの横)>閲覧履歴の削除>「キャッシュされた画像の削除」にチェック`

      * safariの場合

        `履歴 > 履歴を消去 > 直近１時間, 履歴を消去`

   6. コンテナ上で`bash /root/vatic/example.sh`を実行

8. アノテーション作業が全て終わった場合

   * [コンテナから抜ける](#detach)

   * docker コンテナの削除
     ローカル環境上で`docker rm CONTAINER`を入力

### 参考文献

* [FLT 渡邊さん まとめ](https://github.com/FLTwatanabe/annotation)



