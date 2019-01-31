## 错误处理

---

### 1.错误转异常

错误处理器默认会把除了 E_DEPRECATED 和 E_USER_DEPRECATED 以外可被错误处理回调函数捕获的所有错误都转换成 ErrorException 后抛出。

可以通过配置修改需要转换的错误类型，例如：

```php
Hyperframework\Common\Config::set('hyperframework.error_handler.error_exception_bitmask', E_ALL);
```

NOTE: 此功能只对可被错误处理回调函数捕获的错误类型有效。

### 2.写日志

错误处理器使用 Hyperframework\Common\ErrorLogger 记录日志，可以通过 hyperframework.error_logger.* 来配置。

NOTE: PHP 错误日志默认被关闭，可以通过配置 hyperframework.error_handler.enable_php_error_logging 开启。

错误码和日志级别的关系：
```php
[
    E_DEPRECATED        => LogLevel::NOTICE,
    E_USER_DEPRECATED   => LogLevel::NOTICE,
    E_STRICT            => LogLevel::NOTICE,
    E_NOTICE            => LogLevel::NOTICE,
    E_USER_NOTICE       => LogLevel::NOTICE,
    E_WARNING           => LogLevel::WARNING,
    E_USER_WARNING      => LogLevel::WARNING,
    E_COMPILE_WARNING   => LogLevel::WARNING,
    E_CORE_WARNING      => LogLevel::WARNING,
    E_RECOVERABLE_ERROR => LogLevel::FATAL,
    E_USER_ERROR        => LogLevel::FATAL,
    E_ERROR             => LogLevel::FATAL,
    E_PARSE             => LogLevel::FATAL,
    E_COMPILE_ERROR     => LogLevel::FATAL,
    E_CORE_ERROR        => LogLevel::FATAL
]
```
### 3.获取错误对象

```php
$this->getError();
```

getError 是 protected 方法。
