## Kotlin とは

kotlinは、Java言語をもっと簡潔かつ安全になるように改良した産業利用向け汎用言語として開発されたもの。
型推論のある静的型付けのオブジェクト指向プログラミング言語であり、Scalaの関数型プログラミング言語や、C#のジェネリクスの要素などを取り入れている。
Java言語と同様に、Javaバイトコードにコンパイルされて、Java仮想マシン上で動作する。
Java言語との連携が言語仕様として組み込まれているため、Java言語のプロジェクトにKotlinのソースを段階的に追加したり、KotlinからJava言語のクラスやメソッドを呼び出することもできる。

## Jetbrains とは

Androidの開発言語としてKotilnが正式に採用されたため、Kotlinという開発言語とセットでGoogle社の名前が目立つが、Kotlinを開発しているのはJetbrains社である。
Jetbrains社は、IntelliJ IDEAというJavaの統合開発環境（IDE）の開発や販売を行っている企業である。
過去にAndroidアプリを開発していたころは、EclipseとADT Pluginの組み合わせが主流でしたが、現在はAndroid Studioが主流となってる。
このAndroid Studioも、Jetbrains社がIntelliJ IDEAをAndroid開発用にカスタマイズしたもの。
ちなみに、Jetbrains社はPythonの統合開発環境であるPyCharmを開発していることでも有名ですね。

## Kotlin学習メモ

### 変数

* var 変数名 : 型
* Kotlin には参照型しかない（プリミティブ型は用意されていない）
* 行末のセミコロンはいらない（あってもよい）
```
var a : Long = 1000L
var b : Int = 100
var c : Short = 10
var d : Byte = 1
var e : Float = 1.1F
var f : Double = 3.14
var g : String = "Hello!"
var h : Char = 'X'
var i : Boolean = true
```

#### 型推論
```
var str = "test"
```

#### 読取専用変数
```
val num : Int = 20
```

* 宣言と初期化を分けることも可能
```
val num : Int
num = 20
```

### 定数
