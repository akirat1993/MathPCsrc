[TOC]

##Command 
### 7z

* 概要

  高い圧縮率

* インストール

  `brew install p7zip`

* 使用方法:

  解凍:`7z x 2017男性.7z`

* 参考資料

  [7z Macでの使い方](https://qiita.com/ntkgcj/items/afe4863c40680d72a755)

### ssh

* オプション 

  [参考UR](https://euske.github.io/openssh-jman/ssh.html)

    * `L` (ex) `ssh -L` 
  ローカル (クライアント) ホスト上の指定の TCP ポートまたはUnixソケットが、与えられたリモートホスト上のポートに転送されるよう指定します.  
    * `-f`  
      ssh がコマンドを実行する直前に、バックグラウンドに移行するよう指示します。これは-n オプションも含んでいます。  
    * `-N`
      リモートコマンドを実行しません。これはポート転送のみをおこないたい場合に便利です。

### grep  

* 自分のMacでは+(直前の文字・単語の1回以上の繰り返し)は使えない
* 正規表現  
`grep seg[0-9]*\.csv`

### top

* 表示項目を限定

    * 表示単位の変換(MiB->GB->Peta)
        総合情報:`E`,プロセス情報`e`

    * 更新頻度の変更
        起動時:`top -d 5` ->5秒おきに更新`d`はdelay-timeの略
        起動後:`s`を押すと`change delay from ?? to` と表示されるので更新間隔を指定

    * ユーザー(user)指定
        起動時:`top -u {username}`,
        起動後:`u`を押すと`Which User`と聞かれるので指定したいユーザー名を入力

    * コマンドをオプションを含めて表示
        起動時:`top -c`

        起動後:`c`を押すと`COMMAND`にオプションも含めて実行コマンドが表示される

    * 表示項目を指定(プロセスID, PIDやCPU使用率,コマンド名など)
        起動後:`f`(formatの略)を入力すると表示項目を選択できる画面に移行.使い方は一番上に書いてある.(移動は方向キー, `d`や`スペースキー`で項目を表示切り替え,`s`でソート項目の指定`q`で設定完了)

* cpu使用率をみる  
    `top + 1`

  * 仮想メモリはVIRT、物理メモリはRESで確認(defaultの単位はKB)

  * プロセスを強制終了する

    `k`コマンドの後PID入力→シグナル番号入力(強制終了は9)

### ps(process status)

* 用語の定義
    * 端末(TTYやTT)    
        * 仮想端末(pts/{num})   
        Linux(リモートログイン時)→(tmuxを含めた)各window毎に与えられる
        * 実端末(ttys)  
        (Local Mac等)→(tmuxを含めた)各window毎に与えられる

* 基本  
  option無しでは実端末+現在の端末上の現在実行中のプロセスを表示

* Option
    * `u` (`ps u`)  
      自分が作成した**全ての**仮想端末+実端末のプロセスを**cpuやメモリの資料率も含めて**表示
    * `a` (all user)  
      全てのユーザーのprocessを表示

* 便利機能

    * [プロセスの起動時刻を調べる](https://qiita.com/isaoshimizu/items/ee555b99582f251bd295)

        `ps -eo lstart,pid,args `
        `-e`:全プロセスを表示
        `-o`:指定したリスト順の出力形式で表示する(`lstart`->プロセスの起動日時,`pid` ->プロセスID, `args`->文字列の引き数がついたコマンド)

### lsof (ls open file)

* 基本  
	 	読み取り権限があるユーザーが開いたportを確認
* `$lsof -i`  
    プロセスが使用してるportを調べる.NAME->ファイルorポート
* 特定のport番号が空いているか確認  
`lsof -i:{port}`
* ポート{port}が使われていたら削除
`lsof -ti:{port} | xargs kill -9`  
( `-t` プロセスidだけ取得 )

### ln

* example
	* create symbolic link between fils()
		`%ln -s /absolute/path/to/file or Directory/ /absolute/path/to/symlink(exclude /)`
		`-s` symbolic link  
		or  
	    `%cd /path/to/symlink`  
	    `%ln -s /relative/path/to/file or Directory/ ./`  
	* remove symbolic link  
	  `unlink /path/to/symbolic link`  
	* remove all symbolic links in directory
		`%find /path/to/symlink/directory/ -type l -delete`  
		`%cd /path/to/symlink/directory`  
		`% find ./`

### find

* share directory and file recursevely(no change on symbolic link)  
(Directory->rwx, files(.py, image)->rw, .sh->rwx)         
  
``` sh
# give "Others" the right to read, write and xecute Directorys
find /path/to/dir -type d | xargs -I% chmod o=rwx % 
# give "Others" the right to read and write filess
find /path/to/dir -type f | xargs -I% chmod o=rw %
# give "Others" the right to read, write and xecute *.sh files
find /path/to/dir -type f -iname "*.sh" | xargs -I% chmod o=rwx %

変更されたくないないファイルやディレクトリを共有
・変更されたくないディレクトリは読み取りと実行権限だけ与える
変更とはファイル・ディレクトリの削除・追加・移動
・変更されたくないファイルは読み取り権限だけ与える
・*.shファイルのみ読み込みと実行権限を与える
```

* findで検索したファイルを一括で移動させる 
  `find -option | xargs -I% mv % to_path`
  * xargs
    * -I replace-str  
       Replace occurrences of replace-str in the initial-arguments with names read from  standard  input.
        Also,  unquoted  blanks  do  not  terminate  input  items;  instead  the  separator is the newlinecharacter.  Implies -x and -L 1.  

* 特定の文字列を含むファイルや行を表示

    ```
    #aliasという文字列を含むファイルパスを表示
    # -iname "*"で隠しファイルも表示
    # -lでファイル名のみ表示
    find ~/ -type f -name "*" -maxdepth 1 | xargs grep -l alias
    
    #aliasという文字列を含むファイルパスと行番号を表示
    #-nで行番号も表示
    find ~/ -type f -name "*" -maxdepth 1 | xargs grep -n alias
    ```

    

* Option  
    * Set the depth of serch  
    `-mindepth/-maxdepth`  
    * **Base of file**(not path) name matches shell pattern.(case insentitive)  
    `-name(-iname)`  
        * `*`-> any number of characters  
        *  `?`-> any single character  
    * file/directory  
    `-type f/d`

## コマンド逆引き
###Linuxでディレクトリ構造のみコピー   

https://ex1.m-yabe.com/archives/2039

### 再帰的にディレクトリのファイルのみにシンボリックリンクを貼る方法

+ **動機**  
  シンボリックで作成されたディレクトリに新しいファイルやフォルダを追加すると元ディレクトリにファイルやフォルダが追加される仕様になっている.
  そのため,複数人で共有しているデータ(ディレクトリ)に対してシンボリックリンクを用いてディレクトリを作成した場合,そのディレクトリにファイルやディレクトリを追加するのは好ましくない.
  そのため,シンボリックで作成されたディレクトリに新しいファイルやフォルダを追加しても元ディレクトリに追加されない方法を紹介する.

+ **手順**  
  /yyy/yyy/dest\_dirのディレクトリにorigin\_dirのシンボリックリンクを作成する方法(以下,origin_dirの絶対パスを/xxx/xxx/origin\_dirと表す)  
    + ディレクトリ構造のみをコピー  
      `rsync -avz --include "*/" --exclude "*" /xxx/xxx/origin_dir /yyy/yyy/dest_dir`  
    + 変数の定義(TOの末尾のorigin_dirを忘れないこと)  
      `FROM=/xxx/xxx/origin_dir`  
      `TO=/yyy/yyy/dest_dir/origin_dir`  
    + ファイルのみシンボリックを貼る  
      `find $FROM -type f | sed -e 's#'$FROM'/##'| xargs -I% ln -s $FROM/% $TO/%`

+ **コマンドの簡単な解説**  
    + find  
      $FROM以下のファイルの絶対パスを表示  
    + sed  
      $FROMという文字列を空白で置換  
        + 参考資料  
          **sedの/は任意の記号で代用できる(パスを置換する時に超便利)**  
          http://akuwano.hatenablog.jp/entry/20120411/1334114116  
    + xargs  
      パイプ“|”で渡された引数を%として保持し,lnコマンドを実行.つまり `$FROM/%`のシンボリックリンクを`$TO/%`に貼る.

### スクリプト(プロセス)を実行した時刻を調べる

* 背景
  pythonコードの中でログを残すのを忘れていたり`time python`などしてなくてpythonコードを実行した時間が分からない場合に調べる方法(ちなみに`top`コマンドの`TIME`欄はCPUを使用している時間なのでプログラムを実行させた時間と異なる)
  ※既に実行が終わったプロセスの実行時間は分からない

* 手順

  1. プロセスIDを調べる

     ``` bash
     $pgrep -a -u akirat -f "python.*IntroVAE32sPy_v02.py"
     >203548 python IntroVAE32sPy_v02.py --ver 0 -w 15女性 -i 顔+腕 --gpus 1
     >203549 python IntroVAE32sPy_v02.py --ver 0 -w 15女性 -i 顔+肩 --gpus 1
     >203566 python IntroVAE32sPy_v02.py --ver 0 -w 15女性 -i 顔+足 --gpus 1
     >...
     ```

     `-a`->コマンドラインも表示, `-u`->Userを指定, `-f(--full)`->コマンドラインを正規表現で絞り込みマッチ
     並列計算等で1実行で複数プロセスが立ち上がる場合があるので,PIDのみ取得して`top`コマンドで目的のプロセスを取得

     ``` bash
     #正規表現にマッチしたPIDをカンマ区切りで取得 -d(--delimiter)
     $pgrep -d',' -u akirat -f "python.*IntroVAE32sPy_v02.py"
     >337603,329249,335298
     #特定のPIDのみを5秒毎に監視 -d Delay-time -c Command-Line 
     $top -c -d 5 -p 337603,329249,335298
     ```

     `Command`>`top`>`表示項目を限定`を見るとtopコマンドの表示項目を絞ることができる.

  2. プロセスの開始時間を表示

     ``` bash
     #特定のプロセスIDの起動時間(lstart),経過時間(etime),args(コマンド)を表示
     #※-o:出力フォーマットの指定
     ps -o lstart,etime,pid,args -p 337603,335298
                      STARTED     ELAPSED    PID COMMAND
     >Mon Dec 31 13:23:15 2018  3-09:51:33 335298 python IntroVAE32sPy_v02.py --ver 0 -w 15女性 -i 顔+腕 --gpus 1
     >Mon Dec 31 13:24:05 2018  3-09:50:43 337603 python IntroVAE32sPy_v02.py --ver 0 -w 15女性 -i 顔+肩 --gpus 1
     ```

     ※出力フォーマット一部

     | コード | ヘッダ  | 意味                               |
     | ------ | ------- | ---------------------------------- |
     | lstart | STARTED | コマンドが起動された時刻           |
     | etime  | ELAPSED | プロセスが起動されてからの経過時間 |
     | args   | COMMAND | 文字列の引き数がついたコマンド     |

     [psコマンドマニュアル(-oオプションについて詳しい)](https://linuxjm.osdn.jp/html/procps/man1/ps.1.html)
     [psコマンド出力フォーマット(-o)](http://d.hatena.ne.jp/winebarrel/20050719/p2)

## Linuxサーバー
### 使用の基礎

#### 使用する際の注意点

- **ストレージ(HDDやSSDなどのことで画像やテキストなどのプログララムの出力を保存する領域)**の空きがあるか確認する必要がある

* Linuxサーバーを使用する際には**CPU(制御・演算を行うデバイス)**に負荷がかかり過ぎていないか,**メモリ(データやプログラムを一時的に記憶するデバイス)**に空きがあるか確認する必要があります
* **GPU**を使用する場合は**GPUのメモリ**の使用状況も確認する必要あり

#### ストレージ

**プログラム等で出力ファイルがある場合は実行前にストレージの空きがあるか確認しましょう**
Macだと`Appleマーク>このMacについて>ストレージ`等で確認することが出来ます.
Linuxサーバーの場合は`df -h`を用いることで調べることができます(`-h`は`human-readable`の略)
例えば`ds`サーバーの場合

``` bash
$df -h
>ファイルシス   サイズ  使用  残り 使用% マウント位置
>/dev/md126p3     208G  113G   96G   55% /
>..
>/dev/sda1         59T  7.0T   52T   12% /data0
```

となってあり,`/`以下(`/home/akirat/`も含まれる)のストレージは`208G`あってそのうち`113G`使用されており残り`113G`使用可能なことが分かります.同様に`/data0`は`59T`の容量があることが分かります.

#### CPU

**物理的に存在するコア数以上を動かさない**
**各CPUに負荷をかけすぎない(稼働率が100%以上になることようにしない)**

* 使用可能なコア数の確認コマンド`lscpu`使用例と見方(`gtx`の場合)

``` bash
$lscpu
>...
>CPU(s):                56
>コアあたりのスレッド数:2
>ソケットあたりのコア数:14
>Socket(s):             2
>...
>Model name:            Intel(R) Xeon(R) Gold 5120 CPU @ 2.20GHz
```

ソケット(マザーボード上にある、CPUを取り付ける場所)が2つあり各ソケットにコア(CPU)が14個あるので物理的に存在するコア(CPU)の数は28個.
またコアあたりスレッド(CPUで認識されるコア数=論理コア数)が2つなので,サーバーが認識してるコア数(論理コア数)は28*2=56個.
物理的に28コアしかないのにそれを倍に見せかける(一人二役をさせる技術)をハイパースレッディングという.

※(CPU)コア->CPU内にある演算回路のことで,CPUの中には(CPU)コアを複数持つCPUが存在する.(2コアのデュアルコアや4コアのクアッドコアなど)

* 使用中の論理コアの使用率を確認する方法
  `$top`コマンドを押した後に数字の`1`を入力する`gtx`サーバーの例

  ```
  >Tasks: 655 total,  24 running, 623 sleeping,   0 stopped,   8 zombie
  >%Cpu0  : 22.4 us, 28.8 sy,  0.0 ni, 48.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
  >%Cpu1  : 46.5 us, 14.7 sy,  0.0 ni, 38.2 id,  0.0 wa,  0.0 hi,  0.6 si,  0.0 st
  >...
  ```

  論理コアが`0`番目のCPUが22.4%稼働している.


#### メモリ

**使用可能なメモリ(available)を残す**

* 使用可能なメモリは`free -h`コマンド出力の `Mem:`行の`available`の項目
  メモリ全体は`Mem:`行の`total`の部分(`h`オプションは`human`の略)
  `gtx`サーバーの例

  ```bash
  $free -h
  >              total        used        free      shared  buff/cache   >available
  >Mem:           250G         24G         21G        397M        204G        224G
  >Swap:           31G          0B         31G
  ```

  ※`Swap:`はメモリが足りなくなった時に使用されるHDのデータ領域でI/O(入出力)のパフォーマンスが遅い
  ※プロセスがデータ領域を使用する際には使用中のメモリー(`Mem:`行`used`)を始めに確保し,空きメモリ(`Mem:`行`free`)がある限り空き容量をメモリの中でI/Oのパフォーマンスが高いキャッシュ(`Mem`:行`buff/cache`)に割り当てる.そのため`free`コマンドでは空きメモリ(`Mem:`行`free`)は少なく表示されるが,新しいジョブが投入されたときには,キャッシュ(`Mem`:行`buff/cache`)の一部はすぐに開放し新しいジョブのデータ領域として使用できる.その領域が`free -h`コマンド `Mem:`行の`available`項目
  [参考文献 Linux メモリの基礎](https://qiita.com/kunihirotanaka/items/70d43d48757aea79de2d)
  [参考文献 メモリの図解 詳しく説明](http://nopipi.hatenablog.com/entry/2015/09/13/181026)

#### GPU

**GPUメモリ容量以上使わない(プログラムが自動停止する)**

* GPUの利用可能メモリを確認する方法`nvidia-smi `(5秒おきに更新したい場合は`nvidia-smi -l 5` で`l`はloopの略)
  `gtx`サーバーの例

  ``` bash
  $nvidia-smi
  >Wed Jan  2 00:46:39 2019       
  >+-----------------------------------------------------------------------------+
  >| NVIDIA-SMI 410.48                 Driver Version: 410.48                    |
  >|-------------------------------+----------------------+----------------------+
  >| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
  >| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
  >|===============================+======================+======================|
  >|   0  GeForce GTX 108...  Off  | 00000000:18:00.0 Off |                  N/A |
  >| 23%   25C    P8     8W / 250W |     10MiB / 11178MiB |      0%      Default |
  >+-------------------------------+----------------------+----------------------+
  >...
  >+-----------------------------------------------------------------------------+
  >| Processes:                                                       GPU Memory |
  >|  GPU       PID   Type   Process name                             Usage      |
  >|=============================================================================|
  >|    1    329249      C   python                                      1703MiB |
  >|    1    331339      C   python                                      1703MiB |
  
  ```

  Gls
  
  PUの0番目が「GeForce GTX 1080 Ti」(`nvidia-smi -L`コマンドで一覧表示)でメモリ11178MiB中10MiBのみ使用されている.プロセスID(PID)329249がGPUの1番目を使用しててメモリは1703MiB使用.



### 使用頻度が高いコマンド

##### CeontOSのバージョンを確認

```bash
$cat /etc/redhat-release 
>>CentOS Linux release 7.4.1708 (Core)
```

[LinuxのOSバージョンを調べる](http://uguisu.skr.jp/Windows/linux_os_version.html)

##### 新規アカウント作成

``` bash
sudo su -
useradd username
passwd username
```



### .bash_profileと.bashrcの使い分け

- sshログイン時 `.bash_profile`->`.bashrc`の順に実行される
- ログインしてる状況で新たにシェル(bash)が起動した際は`.bashrc`のみ実行

[参考資料](https://qiita.com/shyamahira/items/260862743e4c9794b5d2)



### root権限がないサーバーでパッケージをソールビルドしてpargeで管理

結局使わなかったし動作確認したか覚えてないので,メモのみ残す.

1. **ソフトをインストールするディレクトリを作成**

   通常は`/usr/bin`(管理者が`yum`でインストールしたもの)もしくは`/usr/local/bin`(管理者がコンパイルしてインストールしたもの)にインストールするがこのディレクトリはroot権限がないと書き込みできないので,個人用のソフトをインストールディレクトリ`~/local/bin`を作成.(自分で決めてよいがコマンドは適宜読み替えが必要)

   ``` bash
   mkdir -p ~/local/bin
   cd ~/local/bin
   ```

   ソフト管理を行うporgeのインストール

2. **ソースからコンパイルしてインストールしたソフトの管理を行うソフトporgeを最初にインストールする.**
   1. CentOSのバージョン確認

      ``` bash
      $g++ -v
      >COLLECT_GCC=g++
      >COLLECT_LTO_WRAPPER=/usr/libexec/gcc/x86_64-redhat-linux/4.8.5/lto-wrapper
      ```

      ここで, `/usr/libexec/gcc/x86_64_redhat-linux`が存在することを確認する.(以下`x86_64_redhat-linux`は適当なものに読み替える)


   2. **`~/local/bin`にパスを通す**

      `~/.bashrc`に以下を追記

      ``` bash
      #~/local/binにパスを通す 2018/11/10
      export PATH=$HOME/local/bin:$PATH
      ```

   3. 設定を反映させる

      `$sourch ~/.bashrc`

3. **porgeインストール**

   ``` bash
   cd ~/local/bin
   wget http://sourceforge.net/projects/porg/files/porg-0.8.tar.gz
   tar xf porg-0.8.tar.gz
   cd porg-0.8
   nice -n 19 ./configure --host=x86_64-redhat-linux --build=x86_64-redhat-linux --prefix=$HOME/local CFLAGS='-march=core2 -O3' --disable-grop --with-porg-logdir=$HOME/local/root/var/log/porg/
   nice -n 19 make
   nice -n 19 make install
   nice -n 19 make logme
   ```

   [root権限がないサーバーでporgeでインストール](https://qiita.com/Tats_U_/items/9247c53db65ba5d55df9)
