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
    "mathjax-commonhtml",←数式対応(mathjaxでは上手くいかない場合があった)
    "-lunr", "-search", "search-pro-kui",←日本語検索対応
    "page-toc",←ページ毎に目次を表示
    "expandable-chapters",←chapterの畳み込み
    "navigator",←ページの目次を常に右に表示(イカリのアイコン)
    "git-author",←編集日時をつける
    "copy-code-button",←コードにコピーボタンをつける
  	"-shareing",←SNSのシェアボタン
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