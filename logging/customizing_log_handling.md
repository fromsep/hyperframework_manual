## 定制化日志处理

---

### 1.定制默认 Handler

通过配置 hyperframework.logging.handler.class 修改默认 Handler 类。Handler 类必须实现 handle 方法，用于处理 LogRecord，例如：

```php
class MyHandler {
    public function handle($logRecord) {
        //...
    }
}
```
### 2.定制默认 Formatter

通过配置 hyperframework.logging.formatter.class 修改默认 Formatter 类。Formatter 类必须实现 format 方法，用于处理日志记录，此函数返回格式化后的日志字符串，例如：
```php
class MyFormatter {
    public function format($logRecord) {
        //...
        return $result;
    }
}
```
### 3.定制默认 Logger 引擎

通过配置 hyperframework.logging.logger_engine.class 修改默认 Logger 引擎类。

### 4.创建自定义 Logger

```php
use Hyperframework\Logging\Logger;

class MyLogger extends Logger {
    /**
     * @return string
     */
    public static function getName() {
        return 'my_project.my_logger';
    }
}
```

自定义 Logger 配置使用 Logger 名称作为前缀。比如，修改日志等级的配置项为 my_project.my_logger.level。
