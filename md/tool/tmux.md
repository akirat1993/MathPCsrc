[TOC]

## tmuxコマンド

### インストール

[このサイトの通り](https://qiita.com/makisyu/items/d6b32d88cdd97b01a00f)にして`~/.bashrc`に以下を記載

```
# User specific aliases and functions
#~/local/binにパスを通す(/usr/bin/,/usr/local/binより優先) 2018/11/14                                                      
export PATH=$HOME/local/bin:$PATH     
export LD_LIBRARY_PATH=${HOME}/local/lib:$LD_LIBRARY_PATH
```

### 便利機能

##### 履歴を残す

* 動機

  tmuxはdefaultで履歴(`history-limit`)が2,000行までしか保存されないためスクリプトの標準出力を確認出来ない場合がある.それを避ける方法

* コマンド

  1. `$PREFIX`

  2. **今後**同じsession内で作成されるpaneは15000行まで履歴を残すように設定.(**違うsettion内やtmuxを終了した際は**defaultの2,000行に戻る)

     `:set-option history-limit 15000 `

* 豆知識

  defaultの`history-limit`も指定出来るが,大きな値にしてしまうと,RAMを消費してしまう.[参考資料 英語](https://stackoverflow.com/questions/18760281/how-to-increase-scrollback-buffer-size-in-tmux)

  設定方法は`~/.tmux.cof` に以下を書き込む

  `set-option -g history-limit 5000`

  `-g`はglobal settion or windowを表す.[参考文献  英語](https://superuser.com/questions/929430/what-does-the-set-g-command-do-in-tmux)

##### 複数の端末間で履歴を共有

* `~/.bashrc`に以下を書き込む([参考文献](https://qiita.com/piroor/items/7c9380e408d07fd83bfc))

  ```bash
  #複数の仮想端末で履歴を共有(同じコマンドは残さない) 181107
  #https://qiita.com/piroor/items/7c9380e408d07fd83bfc
  function share_history {
    history -a
    # ここから追記
    tac ~/.bash_history | awk '!a[$0]++' | tac > ~/.bash_history.tmp
    mv ~/.bash_history{.tmp,}
    # ここまで追記
    history -c
    history -r
  }
  PROMPT_COMMAND='share_history'
  ```


### Windowに関するコマンド

| window位置の交換 | `swap-window -s window1 -t window2` |
| ---------------- | ----------------------------------- |
|                  |                                     |

### ペイン操作

| ペインの分割(横/縦)                                          | `"`/`%`               |
| ------------------------------------------------------------ | --------------------- |
| ペインの切り替え                                             | `o`                   |
| 現在のペインを新規ウインドウにする                           | `:break-pane`         |
| 現在のペインを既存のウインドウの新規ペインとして追加         | `joinp -t :window_no` |
| [ペインを大きさ変更(縦分割から横分割など)](https://superuser.com/questions/493048/how-to-convert-2-horizontal-panes-to-vertical-panes-in-tmux) | `space`               |
| ペインの入れ替え                                             | `}`/`{`               |
| ウインドウ名を変更                                           | Prefix+.              |
|                                                              |                       |

### マニアックコマンド

| [tmuxのコマンド一覧表示 英語](https://gist.github.com/kennyng/816c29eb75e8eb022108) | `$tmux list-commands`                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| optionの値を確認                                             | globalの履歴の保存行数(history-limit)<br />`show-options -g history-limit` |

## 設定ファイル

*181106編集*

`~/.tmux.conf`(Mac)

``` bash
#vimの表示がおかしいのを対処(256色表示) 180125
#https://goo.gl/5pJf7s
set-option -g default-terminal screen-256color
set -g terminal-overrides 'xterm:colors=256'

#tmuxのwinodow nameが変わらないようにする方法 180125
#http://blog.tmtk.net/post/2015-09-19-tmux-allow-rename-off/
set-option -g allow-rename off

# vim-like key-bind 180127
setw -g mode-keys vi

#set scrollback buffer size (default) #181106
#https://stackoverflow.com/questions/18760281/how-to-increase-scrollback-buffer-size-in-tmux
set-option -g history-limit 5000 #default 2000

#--------------------
#サーバー上で必要
#--------------------
# change prefix-key to C-t                                                                
#set -g prefix C-t

#-------------------
##必要ない可能性あり
#-------------------
# rで設定読み込み 180125
bind r source-file ~/.tmux.conf \; display "Config reloaded."


#---------------------
#必要ない可能性あり
#---------------------
# begin-selection key-bind(tmux2.6 180127)
#    Reference(Long Example):
#    https://github.com/tmux/tmux/issues/754
unbind-key -T copy-mode-vi Space
bind-key -T copy-mode-vi v send-keys -X begin-selection

#---------------------
#必要ない可能性あり
#---------------------
#begin-selection key-bind(tmux2.6 180127) 
#$ brew install reattach-to-user-namespace 
#    Reference(Long Example):
#    https://github.com/tmux/tmux/issues/754
#    https://github.com/tmux/tmux/issues/543
unbind-key -T copy-mode-vi Enter
bind-key -T copy-mode-vi y send-keys -X copy-pipe-and-cancel "reattach-to-user-namespace pbcopy"



```





