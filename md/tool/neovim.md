

[TOC]

##  Neovimの紹介

`vi->vim->neovim(イマココ)`の順に開発されており最新のものがneovim

##### 

## インストール(終了後にnvimコマンドが使用可)

### MacOS上にインストール(Mac環境)

`pyenv`を使用している人向け.`brew`で`neovim`をインストール

[主な参考資料](https://poyo.hatenablog.jp/entry/2017/09/03/233350),[neovim公式](https://github.com/neovim/neovim/wiki/Installing-Neovim)

1. `neovim`をインストール

   ``` bash
   #brew tap neovim/neovim
   brew install neovim
   #brew install --HEAD neovim 
   ```

2. 設定ファイルを作成

   ``` bash
   mkdir -p ~/.config/nvim
   touch ~/.config/nvim/init.vim #初期設定ファイル
   ```

### CentOS上にインストール(local環境)

1. **事前に必要なパッケージは管理者権限がある人にインストールしてもらう**

   `sudo yum -y install libtool autoconf automake cmake gcc gcc-c++ make pkgconfig unzip`

2. **~/local/binにインストール**

   ``` bash
   #実行ファイルを置く場所を作成
   mkdir -p ~/local/bin
   cd ~/local/bin
   
   # パッケージをgit clone
   git clone https://github.com/neovim/neovim
   cd neovim
   
   #buildファイルがあったら削除
   #rm -r build
   #makec
   make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX:PATH=$HOME/local"
   make install
   ```

3. **パスを通す**

   `~/.bashrc`に以下を追加

   ``` bash
   #~/local/binにパスを通す(/usr/bin/,/usr/local/binより優先) 2018/11/14
   export PATH=$HOME/local/bin:$PATH
   ```

   

4. **設定ファイルを作成**

   ``` bash
   mkdir -p ~/.config/nvim
   touch ~/.config/nvim/init.vim #初期設定ファイル
   ```

   [ソースからビルド(local環境ではない)](https://wonderwall.hatenablog.com/entry/2016/03/12/225800)

   [localにインストール](https://qiita.com/py0n/items/8d2ec775522086779967)



## 環境設定

### 基本的な設定

1. 拡張機能でpythonを使うものがあるので`pip`でインストールしておく

   `pip install neovim`

2. `~/.config/nvim/init.vim`に設定を記述(必要な部分だけ真似すること)

   ``` bash
   "----------------------------------
   "一般設定  
   "----------------------------------
   set number             "行番号を表示 2018/11/10
   set tabstop=4          "タブを何文字の空白に変換するか 2018/11/10
   set shiftwidth=4       "自動インデント時に入力する空白の数 2018/11/10
   set foldmethod=indent "(インデントで折りたたみを自動作成してくれる) 2018/11/13
   set smartindent "前の行のインデントを継承してくれる 2018/11/14
   ```

### dein.vim(パッケージ管理ツール)を用いたプラグイン設定

#### プラグイン管理ツールdein.vimをインストール

1. インストール

   [dein.vimのインストール設定ファイルの書き方](https://qiita.com/tamago3keran/items/cdfd66b627b3686846d2)

   ``` bash
   mkdir -p ~/.cache/dein
   cd ~/.cache/dein
   wget https://raw.githubusercontent.com/Shougo/dein.vim/master/bin/installer.sh
   sh ./installer.sh ~/.cache/dein/
   ```

2. 設定ファイルを置く場所を指定

   `~/.bashrc`に以下を記載

   ```bash
   #neovimの設定ファイルを置く場所を指定 2018/11/14
   export XDG_CONFIG_HOME=$HOME/.config
   ```

#### オススメplugin

[pluginまとめ](https://qiita.com/lighttiger2505/items/e0ada17634516c081ee7)

| pluin         | 機能                                                         |
| ------------- | ------------------------------------------------------------ |
| vimproc       | 非同期処理を実現するためのプラグイン.時間のかかる処理を実行した時に,vimが一見応答不能な状態に見えたり,処理中で何もできなくなってしまうことがあります.重たい処理を非同期実行にすることにより,ユーザーが作業をブロックされることを防ぐことができる.[参考](http://kaworu.jpn.org/vim/vimproc) |
| deoplete      | Neovim用の補完機能[ページの中段(動画で使用例が見れる)](https://github.com/Shougo/deoplete.nvim) |
| denite        | ファイルランチャー.`denite起動→絞り込み→開く`を実現[参考資料](https://qiita.com/okamos/items/4e1665ecd416ef77df7c) [ソース 英語](https://github.com/Shougo/denite.nvim/blob/master/doc/denite.txt) |
| deoplete-jedi | Python用の補完機能 [詳しい解説](https://wonderwall.hatenablog.com/entry/2017/01/29/213052) |
| neomru        | Most Recently Used 最近開いたファイルをdeniteで表示するために使用[設定の仕方の参考](http://takkii.hatenablog.com/entry/2016/09/06/095820) |

#### pluginをインストール

1. 導入するプラグインを記述

   [オプションの参考資料](https://qiita.com/okamos/items/2259d5c770d51b88d75b)

   `~/.config/nvim/dein.toml`に以下を記述(Neovim起動時に読み込み)

   ```toml
   [[plugins]]
   repo = 'Shougo/dein.vim'
   
   [[plugins]]
   #非同期処理を実現するためのプラグイン 2018/11/14
   #http://kaworu.jpn.org/vim/vimproc
   repo = 'Shougo/vimproc.vim'
   
   [[plugins]]
   #色指定
   repo = 'romainl/Apprentice'
   
   [[plugins]]
   #file luncher 2018/11/14
   #https://qiita.com/okamos/items/4e1665ecd416ef77df7cn
   repo = 'Shougo/denite.nvim'
   
   [[plugins]] # インデントを見やすく 2018/11/14
   repo = 'Yggdroot/indentLine'
   ```

   `~/.config/nvim/dein_lazy.toml`に以下を記述

   ```toml
   [[plugins]]
   #補完機能 2018/11/14
   repo = 'Shougo/deoplete.nvim'
   on_event = 'InsertEnter'
   hook_add = ' #←実際はシングルクオテーションを3つだけど表示が失敗するので1つで表記
     let g:deoplete#enable_at_startup = 1
     let g:deoplete#auto_complete_delay = 0
   '#←実際はシングルクオテーションを3つだけど表示が失敗するので1つで表記
   
   [[plugins]]
   #pythonの補完機能 2018/11/14
   #https://blog.515hikaru.net/entry/2017/06/25/043035
   repo = 'zchee/deoplete-jedi'
   on_i = 1 #on_i 1を指定すると、インサートモードに入った時に読み込まれます
   on_ft = 'python' #on_ft 指定したファイルタイプの時に読み込まれます
   
   [[plugins]]
   #最近開いたファイルをdeniteで表示するために使用 2018/11/14
   #設定の仕方の参考
   #http://takkii.hatenablog.com/entry/2016/09/06/095820
   repo      = 'Shougo/neomru.vim'
   on_source = ['denite.vim']
   on_path = '.*'
   
   ```
   
2. 確認作業

   ```bash
   $ pyenv which python
   #$HOME/.pyenv以下が出力されていることを確認
   /Users/akirat/.pyenv/versions/3.6.3/bin/python
   $ which pip
   #$HOME/.pyenv以下が出力されていることを確認
   /Users/akirat/.pyenv/shims/pip
   ```

3. 設定ファイルを作成

   `~/.config/nvim/init.vim`に以下を書き込む

   python_host_progのところは現在使用しているpythonにする

   ```bash
   "--------------------------------------------------
   "deinによるパッケージ管理
   "--------------------------------------------------
   "Mac等でneovimをbrewで入れたがpyenvで使用しているpythonを参照させたいとき 2018/11/14
   if has("mac")
       let g:python_host_prog = "$(pyenv root)/versions/$(pyenv global)/bin/python"
   endif
   
   " 2018/11/14
   if &compatible
     set nocompatible
   endif
   
   "2018/11/14
   set runtimepath+=~/.cache/dein/repos/github.com/Shougo/dein.vim
   
   " プラグインを読み込む 2018/11/14
   if dein#load_state('~/.cache/dein')
     call dein#begin('~/.cache/dein')
   
     "TOMLを読み込み(lazy:0->Neovim起動時に読み込み,lazy:1->遅延読み込み)
     call dein#load_toml('~/.config/nvim/dein.toml', {'lazy': 0})
     call dein#load_toml('~/.config/nvim/dein_lazy.toml', {'lazy': 1})
     
     call dein#end()
     call dein#save_state()
   endif
   " プラグインの追加・削除やtomlファイルの設定を変更した後は
   " 適宜 call dein#update や call dein#clear_state を呼んでください。
   " そもそもキャッシュしなくて良いならload_state/save_stateを呼ばないようにしてください。
   
   " その他インストールしていないものはこちらに入れる
   if dein#check_install()
     call dein#install()
   endif
   
   "よくわからない 2018/11/14
   filetype plugin indent on
   syntax enable
   
   "カラースキームを使えるように変更
   "http://www.maruc.net/2016/07/11/dein-vimのcolorscheme/
   colorscheme Apprentice     " ←コイツと
   syntax on              " ←コイツをかいとく
   
   "----------------------------------
   "一般設定  
   "----------------------------------
   "--------------
   set number             "行番号を表示 2018/11/14
   set tabstop=2          "タブを何文字の空白に変換するか 2018/11/14
   set shiftwidth=2       "自動インデント時に入力する空白の数 2018/11/14
   set cursorcolumn       "列のハイライト 2018/11/14
   set foldmethod=indent "(インデントで折りたたみを自動作成してくれる) 2018/11/14
   set smartindent "前の行のインデントを継承してくれる 2018/11/14
   
   colorscheme apprentice "colorscheme 2018/11/14
   ```



## Plugin

### Plugin詳細

#### denite

[参考資料](https://qiita.com/okamos/items/4e1665ecd416ef77df7c),[ソース 英語](https://github.com/Shougo/denite.nvim/blob/master/doc/denite.txt)

| 用法                                     | コマンド                |
| ---------------------------------------- | ----------------------- |
| カレントディレクトリを表示/再帰的に表示  | `:Denite file/file_rec` |
| 前回のdeniteバッファを再表示             | `:Denite -resume`       |
| 最近使ったファイルを表示                 | `:Denite file_mru`      |
| 前回のdeniteバッファを再表示             | `:Denite neoyank`       |
| Deniteのbufferを閉じる                   | `<C-c>`                 |
| ノーマルモードに切り替え                 | `<C-o>`                 |
| 挿入モードに切り替え                     | `i`                     |
| アクションを選択(アクションを選択します) | `<Tab>`                 |
| 親ディレクトリに移動(ノーマルモード)     | `U`                     |
| パスを指定                               | `P`                     |
| 次の行に移動(insertモード)               | `<C-g>`                 |
| 前の行に移動(insertモード)               | `<C-t>`                 |



### pluginを追加した場合の処理(dein.toml, dein_lazy.toml)

```bash
:call dein#update()
:call dein#clear_state()
```



## 便利機能

### ctag(関数ジャンプ)

#### 事前準備

1. `ctag`コマンドをダウンロード
   * Macの場合
     1. インストール:`brew install ctag`
     2. エイリアスを通す
        `~/.bash_profile`に以下を追記``alias ctags="`brew --prefix`/bin/ctags"``
     3. 設定を反映
        `source ~/.bash_profile`
2. ctagファイルを作成
   ソーツツリーのトップで`ctag -R`を実行(ctagというファイルが作成される)
3. `nvim`を開いた後にtagのパスを通す
   `:set tags=<tags_path>`

| コマンド                                                  | 意味                           |
| --------------------------------------------------------- | ------------------------------ |
| `g C-]` (gキー入力後にControlキーを押しながら]キーを押す) | 定義に複数候補がある場合に選択 |
| `C-t`                                                     | 直前のタグに戻る               |

[vimでtag jamp参考資料](http://archiva.jp/web/tool/vim_ctags.html)



##使用方法

### コマンド備忘録

#### コマンド一般

| 用途                                                         | コマンド                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| コマンド履歴の表示                                           | `q:`                                                         |
| 前方検索履歴, 後方検索                                       | `q/`,`q?`                                                    |
| Yank[複数yank](http://cohama.hateblo.jp/entry/20130108/1357664352) | `"{character}`                                               |
| Pate                                                         | `"{character}p`/`"0y`                                        |
| インサートモードでの貼り付け                                 | `<C-R>"`                                                     |
| レジスタ表示                                                 | `:reg`                                                       |
| 置換(範囲指定後)                                             | `'<,'>s/置換文字/置換後文字/オプション`<br />オプション:g->マッチした全ての文字を置換,c->マッチするたびに |
| 置換行数指定                                                 | `開始行,終了行s/置換文字/置換後文字/オプション`              |
| 検索文字列を置換                                             | `/`で文字列を検索した後で<br />`%s//<replace word>/cg`       |

#### コードの折りたたみ

設定ファイル`~/.config/nvim/init.vim`などに以下を追記しておく

 `set foldmethod=indent "(インデントで折りたたみを自動作成してくれる) 2018/11/13`

| 説明                                   | ショートカット |
| -------------------------------------- | -------------- |
| 全ての折り畳みを開く                   | `zR`           |
| カーソルの下の折畳を一段階閉じる       | `zc`           |
| 全ての折りたたみを閉じる               | `zM`           |
| カーソルの下の折畳を再帰的に全て閉じる | `zC`           |
| カーソルの下の折畳を一段階開く         | `zo`           |
| カーソルの下の折畳を再帰的に全て開く   | `zO`           |



