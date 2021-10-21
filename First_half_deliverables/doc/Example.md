## テストコードの基本構造  
  
```php
public class Foo {

    public void method1() {
    ...
    }
    public void method2() {
    ...
    }
}
```
上記クラスに関するテストケース例
```php
@RunWith(JUnit4.class) // テストランナーを指定
public class FooTest { // TestCaseのサブクラスである必要はない

    @Before // setUpのオーバーライドではなく、任意のメソッドにアノテーションをつける
    protected void setUp() {
        // セットアップ処理
    }

    @After // tearDownのオーバーライドではなく、任意のメソッドにアノテーションをつける
    protected void tearDown() {
        // 後処理
    }

    // テストケースとなるメソッドにTestアノテーションをつける。名前は自由。
    @Test
    public void method1DoSomething() { 

    }

    @Test
    public void testMethod2() {

    }

```
