[TOC]

##pyenvの利点
* ユーザー間でデフォルトで指定しているpythonのバージョン(python2.6やpython3.6)が異なる.
* モジュール(Networkx)等のバージョンが異なる.
* pythonのバージョン1つにつき環境を複数用意したい.(例えばpython3.6.3の環境の1つ目ではNetworkxのバージョンは2だが、環境の2つ目ではバージョン3を持ち内場合など) 

## モジュール管理
### pip
* Install another module version  
`pip install --no-cache-dir -I module(for example numpy)`
    * `--no-cache-dir`:Clear out its download cache and downloat from the scratch. use the specific version


## インストール

### CentOS
#### pyenvの環境構築
* pyenvのインストーラの取得  
`git clone https://github.com/pyenv/pyenv.git ~/.pyenv`  
* pyenveにパスを通す(~/.bash_profileに以下を追加)  
`export PYENV_ROOT="${HOME}/.pyenv"`    
`export PATH="${PYENV_ROOT}/bin:$PATH"`
`eval "$(pyenv init -)"`

* pyenvのバージョンを確認  
 `pyenv -v`  
* pyenvのバージョンをあげるplugin
    * インストール  
    `git clone git://github.com/yyuu/pyenv-update.git ~/.pyenv/plugins/pyenv-update`    
    * pyenvをアップデート  
    `pyenv update`  
    * [参考資料](https://qiita.com/moroku0519/items/1c029659de4f169cd09a)
* pyenvでインストール出来るpythonのバージョンを確認  
`pyenv install -l`  
* pyenvでpython のバージョンのインストール  
 `pyenv install 3.6.3`  
* pyenvで使用するpythonのバージョンを指定  
 `pyenv global 3.6.3`  
* pyenvで使用している(使用可能な)pythonのバージョンを確認 
`pyenv version(s)`

#### pyenv-virtualenvの環境構築
* virtualenvのインストール  
`git clone https://github.com/yyuu/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv`  
* virtualenvにパスを通す.  
`eval "$(pyenv virtualenv-init -)"`  
* 使用可能なバージョンを確認  
`pyenv versions`  
* 使用可能なバージョン(3.6.3)から仮想環境(3.6.3_v1)を作成.  
`pyenv virtualenv 3.6.3 3.6.3_v1`  
* pip等でインストールしたモジュールを継承して仮想環境(3.6.3_v1cp)構築  
`pyenv virtualenv 3.6.3_v1 3.6.3_v1cp`  
※仮想環境`3.6.3_v1`のモジュールを継承するとする.  
* pyenvで使用するpythonのバージョンを指定(virtualenv-name).  
 `pyenv global virtualenv-name`  
* pyenvの仮想環境(virtual-name)を削除  
` pyenv uninstall virtual-name `  
* モジュールのリストをインストール  
`pip freeze > pyp_list.txt`  
* まとめてモジュールをインストール  
`pip install -r pyp_list.txt`  

#### 参考文献

[CentOSにインストール](https://qiita.com/micheleno13/items/bd19dca20da97f3f056e),[virtualenv基本コマンド](https://qiita.com/ryskiwt/items/eb39bca9762043601675),[virtualenv環境設定](https://qiita.com/Kodaira_/items/feadfef9add468e3a85b)