# "If I have a common lisp in the browser."

[Resarch notes **NOT A SOLUTION**]

A process of research and reflection on the following:

1. Organize useful use cases.
2. Explore some ways to use Common Lisp from a web browser.

# Use Cases

- Common Lisp で作った関数やアプリケーションをJavaScript に変換し、ブラウザ上で実行できる
	- as a Portable way.

- Common Lisp のREPL 環境をブラウザから使う
	- Debugger
	- Condition System
	- Inspector
	- IDE
		- Editor
			- Paredit
		- Code Complete
		- Tags
		- Ref. Hyperspec
		- Language Server Protocol - https://microsoft.github.io/language-server-protocol/

- ブラウザを仮想マシン(Lisp マシン)とみなす。そのホスト言語としてJavaScript の代わりにCommon Lisp で書けるようにする。ブラウザをOS とみなしAPI を駆使する。

- Common Lisp のライブラリが使える

- JavaScript のライブラリが使える
	- https://threejs.org/
	- https://js.cytoscape.org/
	- https://github.com/processing-js/processing-js

- Bidirectional evaluation(双方向評価) by Baku Hashimoto
	https://baku89.com/2020/06/26/c-activity
	https://github.com/baku89/glisp/

- ブラウザからCommon Lisp がどのように見えるべきか？
	- 陰に
		- 必要な時にREPL やエディタを立ち上げることができる
		- JavaScript のConsole のように
			- JavaScript のConsole からCommon Lisp が使える
	- 陽に
		- ブラウザーがまるごとREPL 環境となり、JavaScript の開発環境となる

- Web サービス開発
	- SPA etc.
	- React etc.
	- From Backend to Frontend.
		- バックエンド側のCommon Lisp コードと、フロントエンド側のJavaScript にコンパイルされるコード開発はすべてサーバー上で行う
			- →今回はブラウザーでCommon Lisp を動かす環境の話題だからこの利用例ではない

- ブラウザーからサーバー側Common Lisp のREPL でSBCL として使え、SBCL で作ったJavaScript がブラウザー側にもってこれて動く。こういうユースケースが自然じゃないだろうか？
	- すべてのCommon Lisp がJS に変換できなくてもよいと思う
	- であればJupyter でこれが実現できているかな？
		- デバッガーはどうだ？

- もし、Common Lisp がJavaScript にコンパイルされるというとき、それは処理系まるごとがJavaScript 上で動くことも意味する
	- この場合、Emscripten によるWebAssembly 書き出しということになるが、現在実現されていない他、デメリットも考えられる
		- SBCL のイメージをダウンロードするのに時間がかかる
		- それはCommon Lisp そのものであり、JavaScript やJavaScript で叩くWebAPI が使えない
			- したがってそのSBCL 上でParenscript を読み込んでJavaScript コード書き出しを行い、それをなにかの方法でブラウザー側に渡し実行する手段が必要となる
		- ホストOSがないのでファイル保存などもできないのではないか?

- ポイント
	- ニーズの観点
		1. Common Lisp でJavaScript のコーディングができること
			- Common Lisp で(サーバー実装は当然できるが) Web のフロントエンド開発もできる
		2. ブラウザー上でCommon Lisp 処理系(更に開発環境)を持てる
	- 技術の観点
		- サーバーとクライアント側の役割分担をどうするか
		- JavaScript にコンパイルする内容に、Common Lisp そのものを含めるのかどうか(ex: デバッガー, GC, スペシャル変数, etc.)


# How to use Common Lisp in a web browser

## Project Jupyter

- common lisp jupyter - https://github.com/yitzchak/common-lisp-jupyter

## Subset of Common Lisps

### JSCL

- https://github.com/jscl-project/jscl
	- https://github.com/jscl-project/Moren-IDE

### Parenscript

- https://common-lisp.net/project/parenscript/
- https://github.com/BnMcGn/sigil

## Using with WebSocket?

- Like a https://replit.com/languages/elisp
- SLYME/SLY のWebSocket クライアント実装はある？

## FullSpec Common Lisp by WebAssembly

- Not at now
- (Scheme is Here: http://feeley.github.io/gambit-in-the-browser/)

## Common Lisp to JavaScript Compiler

- valtan[alpha version] - https://github.com/cxxxr/valtan
	Common Lisp to JavaScript compiler
- jacl - https://tailrecursion.com/JACL/
	JACL: A Common Lisp for Developing Single-Page Web Applications.

## 👎 CPU Emulator by JavaScript

SBCL ではx86_64(多分x86も) のネイティブコードにコンパイルされる。
そのバイナリーをJavaScript 側で受け取り、x86 として実行できればいいのか？と考えた。
	- 👎 この考え方は筋が悪い。OSのシステムコールやDynamic Link Library 等も用意せねばならないのではないか。

### x86 Emulator

- https://github.com/copy/v86
	- ex) http://copy.sh/v86/

この場合OS のイメージ読み込みから必要であり、読み込みに時間がかかる。
更に、仮想マシン側からホスト(ブラウザー)側で実行するJavaScript コードが書き出せればよいのだが、そこまでの仕組みがあるかどうか。
なければただの仮想マシンでしかない。

## Other Lisps in the Browser (**NOT A COMMON LISP**)

- https://clojurescript.org/
- https://lisperator.net/slip/
- https://glisp.app/docs/
- http://feeley.github.io/gambit-in-the-browser/
- https://bitbucket.org/ktg/parenjs/src/master/
- http://smihica.github.io/arc-js/
- http://nhiro.org/learn_language/LISP-on-browser.html

# Refs
- https://project-awesome.org/CodyReichert/awesome-cl#javascript
- https://lisp-journey.gitlab.io/blog/state-of-the-common-lisp-ecosystem-2020/

