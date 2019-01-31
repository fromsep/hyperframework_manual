## App 基础

---

### 1.App 构造函数
在 App 构造函数中会初始化配置和错误处理器。

**初始化配置**

App 通过自身的 initializeConfig 初始化配置。

应用必须包含初始化配置文件 config/init.php ，它会在此时被导入。

如果环境配置文件 config/env.php 存在，它会在初始化配置导入完成后被导入。

**初始化错误处理器**

App 通过自身的 initializeErrorHandler 初始化错误处理器。

可以通过配置修改错误处理器类：

```php
Hyperframework\Common\Config::set('hyperframework.error_handler.class', 'CustomErrorHandler');
```

默认的错误处理器类是 Hyperframework\Common\ErrorHandler（App 的子类可以定制默认的错误处理器类，例如，Web 模块的 App 默认使用 Hyperframework\Web\ErrorHandler）。
