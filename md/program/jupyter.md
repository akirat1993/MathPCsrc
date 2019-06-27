[TOC]

## 便利機能

* youtubeの動画をjupyter上に貼り付ける

``` python
from IPython.display import YouTubeVideo
YouTubeVideo("cFHHPKp1Tao")
```

​	下記の`cFHHPKp1Tao`の部分は`youtube>SHARE`で出てくるyoutu.be/以下(詳細は下記参照)

<left><img src="../../img/jupytube.png" width="700px" /></left>



## インストール
#### 環境設定

| Mac    | `pyenv>Phothon3.6.3`  <br/>`OS:High Sierra 10.13.3`          |
| ------ | ------------------------------------------------------------ |
| CeotOS | `pyenv 1.2.1-7-gf114557>Phothon3.6.3 virtualenv ` <br/>`CentOS Linux release 7.4.1708 (Core)` |

#### 手順

* ``` bash
    pip install --upgrade pip
    #pip install notebook
    pip --no-cache-dir install -I notebook
    pip install jupyter_contrib_nbextensions #拡張機能が必要な場合
    jupyter contrib nbextension install --user  #拡張機能が必要な場合
    jupyter notebook --generate-config
    ```


#### トラブルシューティング

* [拡張機能(nbextension)が開かない場合の対処法](https://vaaaaaanquish.hatenablog.com/entry/2017/07/15/185832)

* if we come across the error in (line4) like this

  ```bash
  from pysqlite2 import dbapi2 as sqlite
  ImportError: No module named 'pysqlite2'
  ```

  - install sqlite-devel  
    `yum install sqlite-devel`
  - reinstall python

  ```bash
  # uninstall virtualenv-name/ python version
  pyenv uninstall 3.6.3
  # reinstall python
  pyenv install 3.6.3
  # reinstall jupyter notebook
   pip install --no-cache-dir -I notebook
  ```

  - Reference  
    [参考文献1 英語](https://github.com/jupyterhub/jupyterhub/issues/464) 
    [参考文献2 英語](https://stackoverflow.com/questions/1210664/no-module-named-sqlite3)

## 拡張機能
#### 拡張機能をインストール

```bash
pip install jupyter_contrib_nbextensions #拡張機能が必要な場合
jupyter contrib nbextension install --user  #拡張機能が必要な場合
```

[拡張機能(nbextension)が開かない場合の対処法](https://vaaaaaanquish.hatenablog.com/entry/2017/07/15/185832)

#### Vimのキーバインドを入れる

[URL](https://qiita.com/_snow_narcissus/items/80f81926707807ee9bf1)通り(クローン先はコマンド`jupyter --path`で調べる)

```bash
cd /home/{username}/.pyenv/versions/3.6.3/share/jupyter
mkdir nbextensions
git clone https://github.com/lambdalisue/jupyter-vim-binding ./
```
#### 背景色をvim likeにする

[参考資料](https://qiita.com/_snow_narcissus/items/80f81926707807ee9bf1)

```bash
# install jupyterthemes
pip install jupyterthemes

# upgrade to latest version
pip install --upgrade jupyterthemes

jt -t chesterish -f roboto -tfs 10 -nfs 10 -dfs 7 -lineh 130 -ofs 10 -N
    #オプション
    #https://github.com/dunovank/jupyter-themes
```

#### cssの調整(編集画面を暗くする)

`~/.jupyter/custom/custom.css`を編集します。div.cell.edit_mode {という一行がありますので、その直前に下記を挿入します。

```css
/* Jupyter cell is in normal mode when code mirror */
.edit_mode .cell.selected .CodeMirror-focused.cm-fat-cursor {
background-color: #000000 !important;
}
/* Jupyter cell is in insert mode when code mirror */
.edit_mode .cell.selected .CodeMirror-focused:not(.cm-fat-cursor) {
background-color: #000000 !important;
}
```



##### 出力結果(エラー文を含む)が見切れる場合

`~/.jupyter/custom/custom.css`の以下を追記及び編集

```css
div.output_subarea.output_text.output_stream.output_stdout,
div.output_subarea.output_text {
  font-family: "Roboto Mono", monospace, monospace;
  ...
  margin-left: 11.5px;←ここを編集
}
div.output_subarea {
  overflow-x: auto;
  padding: 1.1em !important;←ここを編集
  ...
}
```

:

#### おすすめ拡張機能

| name | Expalain |
|:----|:-----|
|[Table of Contents(2)](http://cartman0.hatenablog.com/entry/2016/03/28/170319#Equation-Auto-Numbering)| 目次を作成作成.反映されない場合は[以下](https://qiita.com/masaru/items/fb2b8ea221278f22c259)を参照 |
|[Collapsible Headings](http://cartman0.hatenablog.com/entry/2016/03/28/170319#Equation-Auto-Numbering) | 目次の項目ごとにCellを閉じることが出来る. |
|[Codefolding](http://cartman0.hatenablog.com/entry/2016/03/28/170319#Equation-Auto-Numbering) | コードをindent毎に閉じることが出来る. |
|Highlight selected word | カーソルがある変数に対して色をつける(文字列の置換時に便利)<br />[ハイライトじゃなく枠線で表示するカスタマイズ方法](#Hightlight-selected-word) |
| [Python Markdown](http://cartman0.hatenablog.com/entry/2016/03/28/170319#Equation-Auto-Numbering) | コード内の変数をMarkdownモードで表示できる.{{variable}}      |
|AutoSaveTime|定期的に自動保存|
|Hinterland|補完機能(多少邪魔)|



#### Hightlight selected word

[カーソル付近の単語と同じ単語をハイライト及び枠で強調するカスタマイズ方法 英語](https://github.com/jcb91/jupyter_highlight_selected_word/issues/14)

ハイライトカラーを変更  
`~/.jupyter/jupyter_notebook_config.py`


```python
from notebook.services.config import ConfigManager
cm = ConfigManager()
cm.update(
    'notebook', 
        {'highlight_selected_word': 
            {
                'delay': 500,
                'code_cells_only':True,
                'highlight_color':'#F0CD59',
                'outlines_only':True
            }
        }
)
```

## Jupyter をリモートサーバーで実行
#### 対応環境
* リモートサーバーにグローバルIPが割り当てられていない
* リモートサーバーにはアクセスするためには経由サーバーが必要な場合.(自宅からdsサーバーにアクセスする場合など)

以下では自宅からjupyterをds上で実行する方法を説明する(pasはnuma経由でないと自宅からログイン出来ない)

####事前準備
[リモートサーバーにjupyterをインストール](#インストール)



#### リモートサーバーでssh接続設定

1. jupyterの設定ファイルを作成 
  
   `$jupyter notebook --generate-config`

   `~/.jupyter/jupyter\_notebook\_config.py`というファイルが作成される.
   
2. certification fileを作成  

   `cd ~/.jupyter/openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mykey.key -out mycert.pem`

3. ハッシュ化されたパスワードを取得  

   (remote サーバー上で以下を順に実行) 

   `$ipython`  

   `from notebook.auth import passwdpasswd()>>Out[2]:'sha1:[ハッシュ化されたログインパスワード]'`  

4. jupyterの設定ファイル(`~/.jupyter/jupyter\_notebook\_config.py`)に以下を設定
   1. 全てのipから接続を許可  
     
      `c.NotebookApp.ip = '0.0.0.0'`
      
   2. IPython notebookのログインパスワードを設定(2.で作成したハッシュ化されたパスワードを使う) 

      `c.NotebookApp.password = 'sha1:[ハッシュ化されたログインパスワード]'`  

   3. certification fileを設定  

      `c.NotebookApp.certfile = u'/home/{useraname}/.jupyter/mycert.pem'`

      `c.NotebookApp.keyfile = u'/home/{username}/.jupyter/mykey.key'`  

   4. サーバーポートのデフォルト設定 

      `c.NotebookApp.port = {port}` 

      {port}は1024~65535の間で指定(9999など)  

#### configの設定
local(Mac)の`~/.ssh/config`に以下を追記  

``` bash
Host host1
    HostName        ???.?.???.?? #host1のIPアドレス ?はセキュリティ上隠した数字
    IdentityFile    ~/.ssh/id_rsa
    User            {username} 
    
Host host2
    HostName        ??.??.??.?? #host2のIPアドレス
    IdentityFile    ~/.ssh/id_rsa
    User            {useraname} 

```


#### bash_profileの設定
Mac(local)の`~/.bash_profile`に以下を追記  

```bash
alias nssh="ssh -oProxyCommand='ssh -CW %h:%p host1' $@"
```

これによりMacで`nssh {remote_host}`と打つとhost1経由で`{remote_host}`にログイン出来る. 

`$@`はnsshコマンド後に打つの全ての引数を表す.

[ProxyCommandについてはの参考サイト](https://qiita.com/tag1216/items/5d06bad7468f731f590e)




####jupyterをリモートサーバー上で実行	
1. サーバー(今回は`{host2}`)にログイン 
  
    ローカル(Mac)上で  
    
    (ネットワーク内からログイン)→`$ssh {host2}` 
    
     (上記以外からログイン)→`$nssh {host2}`

2. サーバー上(ds)で空いているかportを確認 

    `$nmap -p 40100-40200 localhost` 

    (例1)  

    `	>...` 

    `>All 101 scanned ports on localhost (???.?.?.?) are closed` 

    `>...` 

    →40100~40200まで全てのportが開いてる.  

    (例2) 

    `>Not shown: 100 closed ports` 

    `>PORT      STATE SERVICE` 

    `>40100/tcp open  unknown`  

    →40100のportが使用されていて,40101~40200のportは空いている.

3. リモートサーバー上でポートを指定してjupyterを起動 

    以下のコマンドで{port}の部分は**開いてるポート番号を指定**  

    `jupyter notebook --no-browser --port={port}`

4. ローカルの開いてるポート番号を確認(Mac上で以下を実行) 

    {port}が空いているか確認 

    `lsof -i :{port}`  

    何も表示されない場合はそのポートが空いている  

5. ポート転送機能を用いてサーバー(host2)との接続をローカルホストでの接続として確立

  ローカル(Mac)上で  

  **{local\_port}はMac上で開いてるportを指定.**  

  **{remote\_port}はサーバー上でjupyterを開く時に用いたport**  

  {remote\_host}はdsなどconfigで設定してるhostname  
  ネットワーク外からログイン↓↓ 

  `nssh -N -f -L localhost:{local_port}:localhost:{remote_port} {host2}`
  ネットワーク内からログイン↓↓    

  ` ssh -N -f -L localhost:{local_port}:localhost:{remote_port} {host2}`

  `-L`->Local Socket, `-N`->コマンド実行無し(None execution ?). `-f `->バックグラウンドで動作

6. サーバー上のjupyterをブラウザ経由で表示  

    (Chromeなどブラウザを開いてURLに以下を打ち込む)  

    `https://localhost:{local_port}`

#### 関連コマンド

* 自分が開いてるportを確認して必要ないものを削除
    * 想定場面  
    
      サーバー上でscreenやtmuxコマンドを使用して,閉じ忘れたportがある場合.
    
    * 手順
        1. 自分が開いたportを表示  
        
          `$lsof -i`  
        
          `>COMMAND     PID   USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME`
        
          `>jupyter-n 31226 {username}    3u  IPv6 {DEVEICE SIZE}      0t0  TCP *:40100 (LISTEN)`  
        
          `>jupyter-n 31226 {username}    9u  IPv6 {DEVEICE SIZE}     0t0  TCP localhost:40100->localhost:57126 (ESTABLISHED)`
        
          →プロセスID 31226でport40100が使用されている.
        
        2. 必要のないプロセスを削除  
        
          `$kill -9 31226`

#### 参考文献 

[lsof,ss,nmapコマンド](https://www.sejuku.net/blog/57344)  

[port番号の割り振り](https://ja.wikipedia.org/wiki/TCP%E3%82%84UDP%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%83%9D%E3%83%BC%E3%83%88%E7%95%AA%E5%8F%B7%E3%81%AE%E4%B8%80%E8%A6%A7)

[使用が危険なport番号](https://abhp.net/it/IT_Port_No_100000.html)

[jupyterの設定ファイルの書き方](http://hiroto1979.hatenablog.jp/entry/2016/02/01/002136)  

[Config設定方法](http://yetnone.hatenablog.com/entry/2017/07/05/200745)

[ポートの削除コマンド](https://askubuntu.com/questions/447820/ssh-l-error-bind-address-already-in-use)

[ログイン手順(英語)](https://coderwall.com/p/ohk6cg/remote-access-to-ipython-notebooks-via-ssh )



## トラブルシューティング
* jupyter notebookを起動されるとfirbiddenと表示され何も出来なくなる.(ディレクトリ参照、ファイル表示)
  * 対処法  
    
    ブラウザのcaheをcookiesも含めて削除  
    
  * 原因候補  
    
    jupyterのextension追加に失敗  
    
    * 試した手法  
      jupyter, ipythonのアンインストール→失敗  
    * [参考URL](https://goo.gl/jpD9dU  )
