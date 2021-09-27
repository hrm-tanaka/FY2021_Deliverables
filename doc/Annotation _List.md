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

