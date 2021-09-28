## Spring アノテーション一覧

|||
|---|---|
|@RequiredArgsConstructor|アノテーションをクラスに指定するとfinalなフィールドを初期化するコンストラクタが生成される|


#### RequiredArgsConstructor

これにより今まで@Autowiredアノテーションでフィールドインジェクションしていたのが不要になる.
```php
@Service
@RequiredArgsConstructor
public class DemoService {
  @NonNull
  private final EmployeeRepository repository;// finalをつけること
  // 省略
```
これでrepositoryがコンストラクタインジェクションされてDIされるようになる
