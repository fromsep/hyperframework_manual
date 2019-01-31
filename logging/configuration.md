## 配置

---

### 1.默认 logger 引擎类
名称: hyperframework.logging.logger_engine.class

类型: string

默认值: Hyperframework\Logging\LoggerEngine

### 2.默认日志等级
名称: hyperframework.logging.level

类型: string

默认值: INFO

### 3.默认日志 handler 类
名称: hyperframework.logging.handler.class

类型: string

默认值: Hyperframework\Logging\FileLogHandler

### 4.配置多个默认日志 handler 类
名称: hyperframework.logging.handlers

类型: array

默认值: null

### 5.默认日志 formatter 类
名称: hyperframework.logging.formatter.class

类型: string

默认值: Hyperframework\Logging\LogFormatter

### 6.默认日志时间格式
名称：hyperframework.logging.formatter.time_format

类型：string

默认值：Y-m-d H : i : s

### 7.日志是否包含日志等级标识
名称：hyperframework.logging.formatter.include_level

类型：bool

默认值：true

### 8.日志是否包含进程号
名称：hyperframework.logging.formatter.include_pid

类型：bool

默认值：true

### 9.默认日志文件路径
名称: hyperframework.logging.file_handler.path

类型: string

默认值: log/app.log
