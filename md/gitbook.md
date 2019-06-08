[TOC]

# このページの作り方

## 概要

このサイトは`gitbook`というツールを使って,マークダウン 形式で書いた複数のファイル(拡張子`.md`)からホームページを作成し,`GitHub`の`GitHub Pages`というサービスを用いて公開しています.数式が無いマークダウンファイルを共有する場合は`GitHub`でpublicのrepositoryを作成して,その中にマークダウンファイルを配置すれば共有できます(そっちの方が簡単です).マークダウン に数式がある場合,もしくは目次をキチンと作成したい場合はこのページの作り方を参考にして下さい(**Mac**で作成する前提で書いています)

## 注意点

* `GitBook`で作成したホームページで数式に対して自動で番号を振り分ける機能を導入する方法は分かっていません(知ってる人がいたら教えて下さい)

* 既に共有したい数式を含んだマークダウンファイルが大量にある場合は多少作業が面倒になる可能性があります.以下,私が今のところ把握してるルールです

  * 文章内の数式(inline)は\$数式\$でなく\$\$数式\$\$と書き直す必要がある

    * \$数式\$を\$\$数式\$\$に変換するコマンド(**ファイルが上書きされるのでbackupを初めにとるように**)

      * 成功

        `sed -i '' 's/\$\{1\}[^$]*[^\\]\$\{1\}/$&$/g' /path/to/file`

      * 失敗コマンド1(自分メモ用)

        先頭以外の\$数式\$を\$\$数式\$\$に変換

        `sed -i '' 's/\([^\\]\)\(\$\{1\}.*[^\\\$]\$\{1\}\)/\1$\2$/g' /path/to/file`

      * 失敗コマンド2(自分メモ用)

        先頭の\$数式\$を\$\$数式\$\$に変換

        `sed -i '' 's/^\$\{1\}.*[^\\]\$\{1\}/\$&\$/' /path/to/file`

  * 数式内に日本語は使えない

  * 数式中の通常文字は`{\rm 通常文字}`は使えず,`\text{通常文字}`という風に記入する必要あり

    

## 使用可能な主な機能

* [ページ内/外へリンクを貼ることができる(ページ内の場合はheaderまで指定可能)](https://www.garyng.xyz/gtil-gitbook/GitBook/relative-internal-links-in-gitbook.html)
* mathjax-commonhtmlのpluginを用いて数式を埋め込むことができる
* 検索をかけれる
* 画像を埋め込むことができる(動画については動作未確認)



## 作成方法詳細

* [簡易的なサイトの作成手順をこちら](https://akirat1993.github.io/ToyGitBook/)



## オススメプラグイン

このページの`book.json`はこんな感じ

``` json
{
  "plugins": [
    "mathjax",←embed-pdfのプラグインを入れる時のみ必要
    "mathjax-commonhtml",←数式対応(mathjaxでは上手くいかない場合があった)
    "-lunr", "-search", "search-pro-kui",←日本語検索対応
    "page-toc",←ページ毎に目次を表示
    "expandable-chapters",←chapterの畳み込み
    "navigator",←ページの目次を常に右に表示(イカリのアイコン)
    "git-author",←編集日時をつける
    "copy-code-button",←コードにコピーボタンをつける
  	"-shareing",←SNSのシェアボタン
  	"embed-pdf",←pdfの埋め込み
		"include-html",←htmlの埋め込み
 	],
  "pluginsConfig": {
    "page-toc": {
      "selector": ".markdown-section h1, .markdown-section h2, .markdown-section h3, .markdown-section h4, .markdown-section h5",
      "position": "top",
      "showByDefault": true
    },
    "git-author":{
      "position": "bottom",
      "modifyTpl": "Last modified by {user} {timeStamp}",
      "createTpl": "Created by {user} {timeStamp}",
      "timeStampFormat": "YYYY-MM-DD HH:mm:ss"
    },
    "sharing":{
      "facebook": true,
      "twitter": true,
      "google": false,
      "weibo": false,
      "instapaper": false,
      "vk": false,
      "all": [
        "facebook", "google", "twitter",
        "weibo", "instapaper"
      ]
    }
}
```

※`-lunr`と`-search`はデフォルトの検索エンジンを無効化する

※[page-toc 公式](https://www.npmjs.com/package/gitbook-plugin-page-toc)



## GitBookについて

### 基本的な使い方

#### GitBookをローカルブラウザで表示させる方法

##### 概要

GitBookをブラウザで表示させるための方法.

GitHubのprivateリポジトリでgitbookを共有して各自がlocalでブラウザに表示させることを想定.

##### GitBook環境設定(Mac)

1. [Node.jsをインストール](https://qiita.com/kyosuke5_20/items/c5f68fc9d89b84c0df09)

   GitBookを使うのに必要なNode.jsをインストールします.手順は上記サイトを参考にしてください.

2. Gitbookが使ってるnpmを初期化(要らないかも)

   `$npm init`

3. Gitbookをインストール

   `$npm install -g gitbook-cli`

[参考資料](https://qiita.com/kannkyo/items/7ad6a7ebaf8622e4d8d6)



##### GitHub環境設定

1. [GitHubアカウント作成](https://qiita.com/okumurakengo/items/848f7177765cf25fcde0)

   アカウントを持ってない場合は上記を参考にしてアカウント作成してください

   ※学生だとprivateリポジトリで多人数の共同編集が可能なProが無料で使えたと記憶してるので,登録後に学生登録することを推奨します.ちなみに無料プランだとprivateリポジトリで3人のみ共同編集可能

2. GitHubアカウントをリポジトリの所有者に教える

   登録メールアドレス,もしくはユーザー名をリポジトリの管理者に教える

※基本的にpush権限が与えられているので注意



##### GitBookをブラウザで表示

1. GitBookがあるレポジトリをcloneで持ってくる.

   リポジトリの所有者から招待メールが来ていることを確認した後で`git clone`する.

   `$git clone https://github.com...`

   GitBookがあるディレクトリが作成される

2. Gitbookをブラウザで表示させる

   1. clone先のディレクトリに移動

      `$cd /path/to/directory`

   2. ファイルの自動更新

      `$git pull`

   3. (初回もしくは新しい拡張機能が必要の時のみ必要)

      Gitbook作成元ファイルがある`src`に移動

      `$cd src`

   4. (初回もしくは新しい拡張機能が必要の時のみ必要)

      必要なplugin(拡張機能をインストール)

      `$gitbook install`

      →`node_modules`というディレクトリが作成できていればOK

   5. `src`があるディレクトリに移動

      `$cd ../`

   6. Gitbookを作成+表示

      `$gitbook serve src docs`

      `>Serving book on http://localhost:4000`

      と表示されるのでSafariやChoromeなど適当なブラウザを開いてURLに`http://localhost:4000`をコピペしてエンターキーを押す.

      ※コマンドは`gitbook serve [book] [output]`であり,`[book]`は`SUMMARY.md`が存在するディレクトリ,`[output]`は出力先を表す



### トラブルシューティング

#### no_such_file_or_directory

* 概要

  Gitbookで`gitbook serve`コマンド時に以下のエラーが発生したのでその対処法

  `Error: ENOENT: no such file or directory, stat '/Users/../fontsettings.js`

* 対処法

  `/Users/{username}/.gitbook/versions/3.2.3/lib/output/website/copyPluginAssets.js`の以下の2つのメソッドを修正

  `copyAssets(output, plugin),copyResources(output, plugin)`

  関数の中の`confirm:true`を`confirm:false`に修正

* [参考資料](http://kuttsun.blogspot.com/2018/06/gitbook-no-such-file-or-directory.html)

### 便利機能

#### GitHub Pagesにすぐに反映

* 概要

  GitHub Pagesでファイルを更新してもすぐに反映されない時があるので,一時的に更新ページを表示させる方法

* 対処法

  末尾に`?version=[コミットID]`をつける.下記は例.

  `https://example.github.io/index.html?version=a1b2c3d`

#### 複数serveする

* 概要

  同時に複数`serve`するとエラーになるので対処する方法

* 解決策

  ポートを例えば以下のようにして指定してあげる.デフォルトport等は`$gitbook help`で確認できる.

  `gitbook serve src docs --port 4001 --lrport 35730`