# テストライブラリ学習

## 目的
* テストを自動で実行することができ、エラー個所やエラーの詳細を知ることもできるためテストの負担を減らす
### 1.概要
  JUnitは、テストを自動的に実行してくれるフレームワーク.
つまり、自動テストを行うクラス群と、テストケースを記述するメソッド（API）群.

“自動テスト”と聞くとテストケースを自動的に作ってくれそうなイメージを持つが、実際にはそんな事はなくて、テストケース自体は人間が作る必要がある.
しかし一度テストケースをコーディングしてしまえば実行は何度でも簡単に出来るので、ちょっとした修正をして今までの動作を再確認したいとき等に非常に便利.  
#### 1.1.メソッドベースとシナリオベース
  テストケースには２通りの書き方が考えられる.  
  
  **メソッドベース**  
  > テストするクラスのメソッドをもとにテストメソッドを起こしていく方法.  
  > 例えば,テストするクラスに methodA, methodB という 2つのメソッドがあれば，テストクラスに testMethodA, testMethodB というテストメソッドを用意する.  
  
  **シナリオベース**  
  > テストするクラスのシナリオをもとにテストメソッドを起こしていく方法．
  > 例えば,テストするクラスの使い方として scenarioA, scenarioB という 2つのシナリオがあれば，テストクラスに testScenarioA, testScenarioB というテストメソッドを用意する．  
  
  ## 2.[JUnitテストの実装](doc/2.Implementing_Tests.md)
  ## 3.[Mockitoの使い方](doc/3.Mockito.md)
  ## 4.[Spring Frameworkの使い方](doc/4.Spring_Framework.md)
## 参考

[JUnit API探訪：アノテーション一覧](https://absj31.hatenadiary.com/entry/20120812/1344781770)  
[【java】Mockitoの飲み方(入門)](https://recruit.cct-inc.co.jp/tecblog/java/mockito-primer/)
[Mockitoの最低限な使い方](https://qiita.com/fumu238/items/64c910bc36b051c6b976)
[MockitoとPowerMockの使い分け](https://qiita.com/euledge/items/a224777c15ae7145114a)
