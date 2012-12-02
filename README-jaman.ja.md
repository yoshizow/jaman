jaman - javadoc検索スクリプト
============================

これは何か？
-----------

Java の API リファレンス (javadoc) を、クラス名やメンバ名を指定
するだけでブラウズできるシェルスクリプトです。

以下のような特徴があります。

* ヒューリスティックマッチングで、最小の入力文字数で最適な結果
* 複数の javadoc を串刺し検索できる
* 予めインデックスを作っておく必要がない (自動生成される)

要求環境
--------

一般的な UNIX コマンド (grep, sed, gawk(nawk), gzip 等) が存在する UNIX 環境。
Cygwin 環境でも動きます。

HTML ファイルをブラウズするときに、`browse`
という名前のプログラムを URL を引数にして呼び出すので、
予め用意しておく必要があります。

インストール方法
---------------

1. `grep, sed, gawk` 等が特別な場所にある場合は、
   ファイル `jaman` の先頭に書いてある、これらのパスを書き換えます。
2. ファイル `jaman` と `browse` とを、パスの通ったディレクトリに置きます。
3. 環境変数 `JAMANPATH` に、検索したい javadoc
   の置いてあるディレクトリを ':' で区切って指定します。
   ここで指定するディレクトリは、`allclasses-frame.html`
   等が置いてあるディレクトリです。例:

   <pre>
export JAMANPATH=/usr/local/jdk1.4/docs/ja/api:$HOME/doc/jdom/apidocs:/usr/local/junit3.7/javadoc:/usr/local/bcel-5.0/docs/api
</pre>

   順番は重要です。先にあるもののほうが何かと優先されます。
4. これで準備は完了です。
   最初の検索実行時には、インデックスファイルを作成するので
   少々時間がかかります。
   インデックスファイルはホームディレクトリの下の
   `.jaman.cache/` 以下に作られます。

使い方
------

### 基本的な使い方

`jaman2` はコマンドラインから起動します。

クラス名やメンバ名の一部を表す文字列を渡すと、
その文字列にマッチするクラス/メンバの javadoc ファイルをブラウザに表示します。
例:

<pre>
$ jaman String        => java.lang.String
$ jaman mkdirs        => java.io.File#mkdirs()
$ jaman awt.List      => java.awt.List
$ jaman List.size     => java.util.List#size()
$ jaman List#size     => java.util.List#size()
$ jaman lang.Object   => java.lang.Object
$ jaman g.Object      => java.lang.Object
</pre>

jaman の検索は、最小の入力で最良の結果を得ることを目指しており、
与えられたパターンを元に、なるべく適切なエントリを表示しようとします。
例えば、"`io.InputStream`" を検索した場合、

* `java.io.InputStream`
* `java.io.InputStreamReader`

の2つがマッチしますが、`java.io.InputStream` のほうが
より適切 [1] なので、こちらを表示します。
そして、他に `java.io.InputStreamReader` という候補がある旨を、
標準出力に出力します。[2]

適切と思われるエントリが複数見つかった場合には、
候補のリストをリンク付きでブラウザに表示します。
例えば、"`List`" を検索すると、

* `java.awt.List`
* `java.util.List`

の2つから選ぶような HTML ファイルを生成して、ブラウザ画面に表示します。
なお、候補数が多すぎるとき (デフォルトでは 20 を超えたとき) には、
件数のみが表示され、候補リストのブラウズは行われません。

マッチしてブラウズが行なわれたり、候補のリストが表示された場合でも、
他に可能性のある候補があれば、その旨が標準出力に出力されます。
候補数が多すぎるとき (デフォルトでは 20 を超えたとき) には、
件数のみ表示します。

### その他

* 内部クラスにも対応しています。

  <pre>
$ jaman Arc2D.D       => java.awt.geom.Arc2D.Double
$ jaman Entry         => java.util.Map.Entry
</pre>

* 複数のパターンを指定することができます (AND 検索)。
  複数のパターンを指定すると、その並び順に従って、
  全てのパターンにマッチするエントリが検索されます。

  <pre>
$ jaman util setValue    => java.util.Map.Entry#setValue()
$ jaman Out Writer       => java.io.OutputStreamWriter
</pre>

* 検索の際の大小文字の区別について
  jaman は、大小文字の区別について、
  デフォルトでは Emacs ライクな方法を使います。
  つまり、パターン指定が全て小文字なら、
  大小文字を無視して検索します。
  パターンの中にひとつでも大文字が混じっていたら、
  大小文字を区別した検索を行ないます。

  <pre>
$ jaman method     => java.lang.reflect.Method,
                      java.net.HttpURLConnection#method,
                      javax.swing.text.html.HTML.Attribute#METHOD
$ jaman Method     => java.lang.reflect.Method
</pre>

コマンドラインオプション
-----------------------

`usage: jaman [option...] <pattern>...`

オプション:

<table>
 <tr><td><code>-path <var>&lt;path&gt;</var></code></td><td>APIリファレンスの検索パスを指定する。パスは ':' で区切られる。</td></tr>
 <tr><td><code>-i</code></td><td>大小文字を無視した検索を行なう。</td></tr>
 <tr><td><code>-c</code></td><td>大小文字を区別した検索を行なう。</td></tr>
 <tr><td><code>-s</code>&nbsp;<var>&lt;n&gt;</var>, <code>-show-candidates-max</code>&nbsp;<var>&lt;n&gt;</var>&nbsp;&nbsp;</td><td>n 件以下の候補があった場合、省略せずに全部表示する。'all' を指定した場合には上限を設けない。n のデフォルトは 20。</td></tr>
</table>

ライセンス
----------

jaman は MIT ライセンスの下で配布されます。
詳しくは `jaman` スクリプトファイルの先頭にある記述を参照してください。

---

<dl>
 <dt>*1:</dt>
 <dd><p>「適切」かどうかの判断は、パターンが単語単位でマッチするか、
     substring としてマッチするか、によってなされます。
     単語単位でマッチするもののほうが、より「適切」であるとみなされ、
     substring としてマッチするものより優先されます。</p></dd>
 <dt>*2:</dt>
 <dd><p>逆に、<code>InputStreamReader</code> を表示したい場合には、
     <code>jaman InputStreamR</code> 等と実行して下さい。</p>
     <p>一般に、最悪の場合でも、他と区別できるユニークな
      最短の文字列を指定すれば、目的のクラス又はメンバが
      一発でブラウズできます。
     </p>
<pre>
% jaman l.List      =&gt; java.util.List
% jaman g.Obj       =&gt; java.lang.Object
% jaman r#substr    =&gt; java.lang.StringBuffer#substring()
</pre>
 </dd>
</dl>

