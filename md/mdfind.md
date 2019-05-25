### 詳細なファイル検索をする方法
+ 想定場面  
以前xxについてのパワーポインの資料を作成したけど,ファイル名覚えていないしどうしよう...去年の12月頃作ったことは覚えているんだが...  
+ 手順  
    1. terminal上で`mdfind`のコマンドを使ってファイルを検索  
        * コマンド  
        `mdfind 'kMDItemDisplayName == *.pptx && kMDItemTextContent == *LSTM* && kMDItemTextContent == *リーマン*'`  
        * コマンド解説  
        ファイル名の末尾が`.pptx`であり`LSTM`と`リーマン`という文字列を含むファイルパスを表示
    2. 検索結果をFinderで表示  
        * 手法概要  
        一時的なディレクトリを作成し,`mdfind`で取得したファイルのシンボリックリンクをその一時ディレクトリに貼る  
        * コマンド例  
            * 一時ディレクトリを作成  
            `mkdir -p ~/tmp/mdfind`   
            * シンボリックを貼る  
            `mdfind 'kMDItemDisplayName == *.pptx && kMDItemTextContent == *LSTM*' | xargs -I% ln % ~/tmp/mdfind`  
            (`xargs`以下はパイプ`|`で渡された引数を%として保持し, `%`のシンボリックリンクを`~/tmp/mdfind`に貼るというコマンド)  
            * マックのプレビュー(Finder上でファイルを選択してスペースキー)などを使って目的の資料を探す.  
            `open ~/tmp/mdfind`  
            * 探し終えたらシンボリックリンクを削除  
            `cd ~/tmp/mdfind`  
            `ls | xargs -I% unlink %`  
    3. その他mdfind検索で便利な機能      
        + ファイル作成日時で検索  
        2018/11/01以降に作成したパワポを検索    
        `mdfind 'kMDItemFSCreationDate > $time.iso(2018-11-01) && kMDItemDisplayName == *.pptx'`  
        + ディレクトリを指定(`-onlyin`)   
        `mdfind -onlyin /path/to/directory 'kMDItemDisplayName == *.pptx'`  
        + `&&` = and, `|` = or  
        + その他検索したい属性(`kMDItemDisplayName`など)は以下のように確認できる.  
        `mdls CANデータ年度末資料.pptx`
+ 参考資料    
    + [mdfindの属性検索(ex `kMDItemDisplayName`)ついて(**一番参考にした記事**)](http://baqamore.hatenablog.com/entry/2013/02/20/193924)
    + [日付を検索対象に入れる方法`kMDItemFSCreationDate`](https://apple.stackexchange.com/questions/247298/use-mdfind-for-a-date-range-on-os-x)
    + [spotlight検索の便利機能GUI](https://ferret-plus.com/8073)
