## 连接

---

### 1.简介

Hyperframework\Db\DbConnection 继承自 PDO 类。


### 2.连接配置

```php
<?php
return [
    'dsn' => 'mysql:host=localhost;dbname=db',
    'username' => 'test',
    'password' => 'test',
    'options' => [PDO::ATTR_EMULATE_PREPARES => false]
];
```
也可已配置多个连接，例如：
```php
<?php
return [
    'db1' => [
        'dsn' => 'mysql:host=localhost;dbname=db1',
        'username' => 'test',
        'password' => 'test'
    ],
    'db2' => [
        'dsn' => 'mysql:host=localhost;dbname=db2',
        'username' => 'test',
        'password' => 'test'
    ],
];
```

### 3.连接池

自动创建的连接都会被放入连接池，直到脚本运行结束后被回收或者手动移除。


### 4.获取连接

```php
$connection = Hyperframework\Db\DbClient::getConnection();
```


### 5.设置连接

```php
Hyperframework\Db\DbClient::setConnection($connection);
```

### 6.切换连接

```php
$name = 'db1';
$result = Hyperframework\Db\DbClient::useConnection($name, function() {
    $connection = DbClient::getConnection();
    return 'result';
});
```

也可以传入一个 Hyperframework\Db\DbConnection 对象，例如:

```php
$result = Hyperframework\Db\DbClient::useConnection($connection, function() {
    return 'result';
});
```
NOTE: 对象连接不会被放入连接池。切换连接支持嵌套。

### 7.建立连接

```php
$name = 'db1';
Hyperframework\Db\DbClient::connect($name);
```
$name 参数可选，如果没有 $name 参数，则会建立当前连接。

### 8.移除连接

```php
$name = 'db1';
Hyperframework\Db\DbClient::removeConnection($name);
```
$name 参数可选，如果没有 $name 参数，则会移除当前连接。如果移除的连接没有被其他变量引用，则会被回收。


### 9.移除所有连接

```php
Hyperframework\Db\DbClient::removeAllConnections();
```
