## 操作剖析

---

Hyperframework\Db\DbOperationProfiler 是一个数据库操作事件监听器，需要作为 listener 添加到 Hyperframework\Common\EventEmitter：

```php
EventEmitter::addListener(new DbOperationProfiler);
```
NOTE: 同时需要把 hyperframework.db.operation_profiler.enable 设置成 true 来激活操作剖析器（默认 false）。

### 1.记录日志
当日志剖析器被开启时，会通过 Hyperframework\Db\DbLogger 输出操作日志, 可以通过 hyperframework.db.logger.* 来配置。

### 2.定制化剖析数据处理
可以通过配置 hyperframework.db.operation_profiler.profile_handler_class 或 hyperframework.db.operation_profiler.profile_handler_classes 设置剖析数据处理器类，剖析数据处理器类必须实现 handle 方法来接收数据，例如：
```php
class ProfileHandler {
    public function handle($profile) {
        //...
    }
}
```
