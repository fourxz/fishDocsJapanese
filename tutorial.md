## fish？
fishは、bashやzshなどのコマンドラインシェルです。fishはシンタックスハイライト、オートサジェスト、タブ補完、設定がわかりやすい、などの特徴を持っています。
難解極まりない設定ファイルと格闘せずに、生産的で使いやすくて楽しいコマンドラインを求めているなら、fishは最適です。
## fishを学ぶ
このチュートリアルは、あなたがある程度Unixのコマンドを理解していて、手元でfishが動作していることを前提とします。
fishを起動したら、まず以下の画面を目にすることと思います。
~~~
Welcome to fish, the friendly interactive shell
Type help for instructions on how to use fish
you@hostname ~>
~~~
fishのデフォルトの見た目ではユーザ名、ホスト名、作業ディレクトリを表示します。
デフォルトの見た目を変えるためにはこちら http://fishshell.com/docs/current/tutorial.html#tut_prompt を参照してください。
以下では、場所の節約のため、ユーザ名とホスト名を単に`>`で表現します。
## コマンドを撃つ
他のシェルと同じように、コマンドを実行できます。半角スペースがセパレータです。
~~~
> echo hello world
> hello world
~~~
リテラルの半角スペースはバックスラッシュ\やシングルクオート'、ダブルクオート"を使って入力できます。
~~~
> mkdir My\ Files
> cp ~/Some\ File 'My Files'
> ls "My Files"
Some File
~~~
## ヘルプを見る
`man`コマンドによってターミナルで、`help`コマンドによってブラウザでmanページを開けます。
~~~
> man set
set - handle environment variables
  Synopsis...
~~~
## シンタックスハイライト
## ワイルドカード
## パイプとリダイレクト
## 自動サジェスト
## タブ補完
## 変数
## exit返り値
普通のシェルでは`$?`でexitの返り値を保存していますが、fishでは`$status`です。
~~~
> false
> echo $status
1
~~~
0が成功、0以外が失敗です。
## エクスポート（環境変数）
他のシェルと違い、fishはexportコマンドを持ちません。代わりに、変数が`set`コマンドのオプション`--export`または単に`-x`によってエクスポートされます。
~~~
> set -x MyVariable SomeValue
> env | grep MyVariable
MyVariable=SomeValue
~~~
##リスト
`set`コマンドではMister Noodleが1つの値である必要がありました。

いくつかの変数、$PWDは1つの値を持ちます。
他の、$PATHなんかは、複数の値を持ちます。
~~~
> echo $PATH
/usr/bin /bin /usr/sbin /sbin /usr/local/bin
~~~
リストは再帰的にはできません。
リストの長さを数えるには、`count`を使います
~~~
> count $PATH
5
~~~
リストに値を追加するには、以下のようにします。
以下では、$PATHに大して/usr/local/binを追加しています。
~~~
> set PATH $PATH /usr/local/bin
~~~
個々の値にアクセスするためには、以下のようにします。
1から開始すると先頭から、-1から開始すると末尾からアクセスします。
~~~
> echo $PATH
/usr/bin /bin /usr/sbin /sbin /usr/local/bin
> echo $PATH[1]
/usr/bin
> echo $PATH[-1]
/usr/local/bin
~~~
要素の範囲にアクセスできます。俗に言う"slices：”ですね。
~~~
> echo $PATH[1..2]
/usr/bin /bin
> echo $PATH[-1..2]
/usr/local/bin /sbin /usr/sbin /bin
~~~
リストに対してforループでアクセスできます。
~~~
> for val in $PATH
        echo "entry: $val"
  end
entry: usr/bin/
entry: /bin
entry: /usr/sbin
entry: /sbin
entry: /usr/local/bin
~~~
##コマンド置き換え


