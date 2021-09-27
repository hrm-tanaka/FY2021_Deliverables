## アノテーション一覧

### org.junit

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
