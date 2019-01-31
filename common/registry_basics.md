## 注册表基础

---

### 1.注册

```php
Hyperframework\Common\Registry::set('key', $value);
```
### 2.获取值

```php
$value = Hyperframework\Common\Registry::get('key');
```

或:
```.php
$value = Hyperframework\Common\Registry::get('key', function() {
    return new Singleton;
});
```

### 3.移除项

```php
Hyperframework\Common\Registry::remove('key');
```
### 4.查询键是否已经存在

```php
$value = Hyperframework\Common\Registry::has('key');
```
### 5.清空注册表

```php
Hyperframework\Common\Registry::clear();
```
