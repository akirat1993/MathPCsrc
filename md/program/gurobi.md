## gurobipy

###事前準備
`~/.bash_profile`に以下を追加(サーバーの場合)


```bash
export LD_LIBRARY_PATH=/opt/gurobi800/linux64/lib:$LD_LIBRARY_PATH
export GRB_LICENSE_FILE=/opt/gurobi800/linux64/gurobi.lic
```

###サンプル

```python
import socket

#add path
#参考資料 Slack>KU>general>2018/5/18
if socket.gethostname() == 'server1':
    if g_ver == "752":
        sys.path.append('/opt/gurobi752/linux64/lib/python3.6_utf32/')
elif socket.gethostname() == 'server2':
    if g_ver == "752":
       sys.path.append('/opt/gurobi752/linux64/lib/python3.6_utf32/')
    elif g_ver == "800":
       sys.path.append('/opt/gurobi800/linux64/lib/python3.6_utf32/')

import gurobipy

#model
m = gurobipy.Model()

#paremeter
#http://www.gurobi.com/documentation/8.0/refman/parameters.html

m.setParam('TimeLimit', 15) 
m.setParam('LogFile', "~/my_gurobi.log") 
m.setParam("Threads",5)

#Variable
x = m.addVar(vtype=gurobipy.GRB.BINARY, name="x")
    #vtype: 変数の属性
        #GRB.CONTINUOUS: 連続変数
        #GRB.INTEGER: 整数変数
        #GRB.BINARY: 01変数

#Constraint1
c1 = 2 * x[1] + x[3]
m.addConstr(c1<=10, "C1")

#Constraint2
m.addConstr(x[1]+x[3]<=10, "C1")等でも可

#変数の総和を取る例
c2 = gurobipy.quicksum([x[i] for i in x])
m.addConstr(c2<=7, "C2")


#Objective value
obj = 3 * x[1] + 4 * x[2] - 2 * x[3]
m.setObjective(obj, gurobipy.GRB.MAXIMIZE)

m.optimize()
print(m.Runtime) # 計算時間(秒)
print(m.ObjVal) #現在の目的関数(計算時間に上限を設けている場合は最適解ではない)
print(m.Status) #結果(2->最適解, 3->実行可能解が存在しない,…,9->計算時間の制約上途中で終わった)
    #gurobipy.Model()の属性  
    #http://www.gurobi.com/documentation/8.0/refman/attributes.html  
    #Statusの意味 http://www.gurobi.com/documentation/8.0/refman/optimization_status_codes.html#sec:StatusCodes 
```



### gurobi8を使ったときのエラーと対処法

pyenv環境でGurobi8を使おうとしたときにエラーメッセージと対処法

1. gurobipyというモジュールがない

   スクリプト+エラーメッセージ

   ```python
   >>> import guribipy
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   ModuleNotFoundError: No module named 'guribipy'
   ```

   原因(pathが通ってない)

   ``` python
   >>> import sys
   >>> sys.path
   ['', '/home/{username}/.pyenv/versions/3.6.3/lib/python36.zip', '/home/{username}/.pyenv/versions/3.6.3/lib/python3.6', '/home/{username}/.pyenv/versions/3.6.3/lib/python3.6/lib-dynload', '/home/{username}/.pyenv/versions/3.6.3/lib/python3.6/site-packages']```
   ```

   sys.path以下にあるモジュールをpythonはimport出来るが,gurobipy(python3.6用)は`(‘/opt/gurobi800/linux64/lib/python3.6_utf32/’`にあるため参照できない

   解決策(pathにgurobipyがある場所を追加する)

   ``` python
   >>> import sys
   >>>sys.path.append('/opt/gurobi800/linux64/lib/python3.6_utf32/')
   >>> import gurobipy
   ```

2. (共有ライブラリのダイナミックライブラリ)libgurobi80.soがない

   **スクリプト+エラー**

   ```python
   >>> import sys
   >>> sys.path.append('/opt/gurobi800/linux64/lib/python3.6_utf32/')
   >>> import gurobipy
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "/opt/gurobi800/linux64/lib/python3.6_utf32/gurobipy/__init__.py", line 1, in <module>
       from .gurobipy import *
   ImportError: libgurobi80.so: cannot open shared object file: No such file or directory
   ```

   **原因と解決策**

   `sys.path`->pythonモジュールを参照する場所

   `LD_LIBRARY_PATH`->ダイナミックライブラリを参照する場所

   みたいなので

   `LD_LIBRARY_PATH`に`libgurobi80.so`がある場所を追加して挙げる.

   つまり`export LD_LIBRARY_PATH=/opt/gurobi800/linux64/lib:$LD_LIBRARY_PATH`
   とターミナルに打てばよい.
   [参考資料](https://stackoverflow.com/questions/1099981/why-cant-python-find-shared-objects-that-are-in-directories-in-sys-path)

3. ライセンスファイル(gurobi.lic)がないと怒られるときの対処法

   スクリプト

   ```python
   >>>import sys
   >>>sys.path.append('/opt/gurobi800/linux64/lib/python3.6_utf32/')
   >>>import gurobipy
   >>>m = gurobipy.Model()
   ```

   エラーメッセージ

   ``` python
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "model.pxi", line 63, in gurobipy.Model.__init__ (../../src/python/gurobipy.c:?????)          
     File "gurobi.pxi", line 17, in gurobipy.gurobi._getdefaultenv (../../src/python/gurobipy.c:??????) 
     File "env.pxi", line 45, in gurobipy.Env.__init__ (../../src/python/gurobipy.c:????)               
   gurobipy.GurobiError: No Gurobi license found (user {username}, host {hostname}, hostid 数字, cores 数字)
   ```

   対処法(gurobiのライセンスファイルの場所を指定してやる)

   `export GRB_LICENSE_FILE=/opt/gurobi800/linux64/gurobi.lic`

   [参考資料](http://www.gurobi.com/documentation/7.5/quickstart_mac/testing_your_license.html)

   ※exportの部分は`~/.bash_profile`に以下を追加しとけば省ける

   ``` bash
   export LD_LIBRARY_PATH=/opt/gurobi800/linux64/lib:$LD_LIBRARY_PATH
   export GRB_LICENSE_FILE=/opt/gurobi800/linux64/gurobi.lic
   ```

   

