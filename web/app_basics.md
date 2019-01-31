## App 基础

---

### 1.什么是 App 类
Web 模块中的 App 类继承自 Common 模块的 App 类，并通过 run 静态方法定义了 Web 应用的主流程。应用入口文件（public/index.php）通过调用该类中的 run 静态方法来运行应用。

### 2.Web 应用的主流程

- 1.创建 App 对象

App 类通过调用自身的 createApp 静态方法创建 App 对象。

- 2.创建 Controller 对象

通过 Router 获取 Controller 类，并创建 Controller 对象。

- 3.运行 Controller

通过调用 Controller 对象的 run 方法来运行 Controller。

- 4.结束运行

结束运行时，App 对象的 finalize 方法会被调用。

### 3.获取路由器对象

通过调用 App 对象的 getRouter 方法来获取路由器对象。
可以通过配置修改路由类：

```php
Config::set('hyperframework.web.router_class', 'CustomRouter');
```

### 4.默认的错误处理器
Web 模块的 App 使用 Hyperframework\Web\ErrorHandler 作为默认错误处理器。
关于错误处理器初始化的详细信息，参考 Common 模块文档中的 [ App 基础](common/app_basics.md)。
关于 Web 错误处理的详细信息，参考 [错误处理](web/error_handling.md)。

### 5.其他
由于 Web 模块的 App 类继承自 Common 模块的 App 类，通过 Common 模块文档中的 [App 基础](common/app_basics.md) 获取更多相关信息。