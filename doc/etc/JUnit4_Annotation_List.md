## アノテーション一覧

### org.junit
|||
|-----|------|
|[@Test]()|テストメソッド用のアノテーション|
|[@Ignore]()|該当のテストメソッドをスキップする。コメントを付与することもできる|
|[@Before]()|各テストメソッドの実行前に実行される|
|[@BeforeClass]()|テストクラスの実行前に一度だけ実行される|
|[@After]()|各テストメソッドの実行後に実行される|
|[@AfterClass]()|テストクラスの実行後に一度だけ実行される|

### Test

`pubric void`なメソッドに付与することでjUnitにテストメソッドであることを認識させる.  
```php
public class Example {
  @Test
  pubric void method() {
    org.junit.Assert.assertTrue( new ArrayList().isEmpty() );
  }
}  
```
`expected`オプションを付けることで期待された例外が投げられたかテストできる.
```php
  @Test(expected=IndexOutOfBoundsException.class)
  public void outOfBounds() {
    new ArrayList<Object>().get(1);
  }
```
また,`timeout`オプションを付けることでテストに時間制限を設けることができる
```php
  @Test(timeout=100)
  public void infinity() {
    while(true);
  }
```

### Ignore

付与することで，一時的にテストを無視することができる．
```php
  @Ignore
  @Test
  public void something() {
    ...
    }
```

メッセージを付けることも可能
```php
  @Ignore("not redy yet")
  @Test
  public void something() {
    ...
    }
```
また，メソッドだけでなくクラスに付与することも可能．
```php
  @Ignore
  public class IgnoreMe {
      @Test
      public void test1() { ... }
      @Test
      public void test2() { ... }
  }

```
### Before
pubic void なメソッドに付与することで，各テストメソッドを実行する前に都度実行してくれる．いわゆる setup メソッド
```php
public class Example {
    List empty;
    @Before public void initialize() {
       empty= new ArrayList();
    }
    @Test public void size() {
       ...
    }
    @Test public void remove() {
       ...
    }
}
```
### After
pubic void なメソッドに付与することで，各テストメソッドを実行した後に都度実行してくれる．いわゆる teardown メソッド
```php
public class Example {
    File output;
    @Before public void createOutputFile() {
          output= new File(...);
    }
    @Test public void something() {
          ...
    }
    @After public void deleteOutputFile() {
          output.delete();
    }
}
```
### BeforeClass
```php
public class Example {
    DatabaseConnection database;
    @BeforeClass public static void login() {
          database= ...;
    }
    @Test public void something() {
          ...
    }
    @Test public void somethingElse() {
          ...
    }
    @BeforeClass public static void logout() {
          database.logout();
    }
}
```
### AfterClass
```php
public class Example {
    DatabaseConnection database;
    @BeforeClass public static void login() {
          database= ...;
    }
    @Test public void something() {
          ...
    }
    @Test public void somethingElse() {
          ...
    }
    @AfterClass public static void logout() {
          database.logout();
    }
}
```
### org.junit.runnerとorg.junit.runners
|||
|---|---|
|[@RunWith]()|テストランナを指定する|
|[@SuiteClasses]()|テストスイートクラスを指定する|
|[@Parameters]()|パラメータを生成するメソッドを指定する|

### RunWith,SuiteClasses
```php
@RunWith(Suite.class)
@SuiteClasses( { TargetTest1.class, TargetTest2.class})
public class AllTests {
}
```
### Parameters
```php
@RunWith(Parameterized.class)
public class TargetTest1 {
    private int num;
    private String expected;
    
    public TargetTest1(int num, String expected) {
        this.num = num;
        this.expected = expected;
    }
    
    @Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][]{{20, "20"},{100, "100"}});
    }
    @Test
    public void test() throws Exception {
        assertEquals(expected, Integer.toString(num));
    }
}
```
@Parametersアノテーションを付けたCollectionを返すスタティックメソッドを用意すると、テストメソッドの前にコンストラクタ経由で値を設定してくれる。  
上記の例では、numに20,expectedに"20"が設定されたテストと、numに100,expectedに"100"が設定されたテストが、計2回実行されます。
