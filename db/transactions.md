## 事务

---

### 1.开始事务

```php
Hyperframework\Db\DbClient::beginTransaction();
```
### 2.递交事务

```php
Hyperframework\Db\DbClient::commit();
```
### 3.回滚事务

```php
Hyperframework\Db\DbClient::rollback();
```
### 4.查询事务状态

```php
$status = Hyperframework\Db\DbClient::inTransaction();
```
### 5.自动化事务处理

可以通过 Hyperframework\Db\DbTransaction 自动处理事务，当没有异常抛出时递交，当有异常抛出时回滚，例如：

```php
$result = Hyperframework\Db\DbTransaction::run(function() {
    return 'result';
});
```

自动化事务处理支持嵌套，事务会在数据库链接对应的最外层回调函数处理完成后递交。
