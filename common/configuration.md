## 配置

---

### 1.设置是否初始化应用配置

名称: hyperframework.initialize_config

类型: bool

默认值: true

### 2.设置是否初始化错误处理器

名称: hyperframework.initialize_error_handler

类型: bool

默认值: true

### 3.设置错误处理器类

名称: hyperframework.error_handler.class

类型: string

默认值: Hyperframework\Common\ErrorHandler，在 web 应用中是 Hyperframework\Web\ErrorHandler

### 4.开启或关闭 PHP 错误日志

名称: hyperframework.error_handler.enable_php_error_logging

类型: bool

默认值: false

### 5.错误处理器生成的最大日志长度


名称: hyperframework.error_handler.max_log_length

类型: int

单位: 字节

默认值: null（不限制）

### 6.错误处理器的错误异常掩码

名称: hyperframework.error_handler.error_exception_bitmask

类型: string

默认值: E_ALL & ~(E_DEPRECATED | E_USER_DEPRECATED)
