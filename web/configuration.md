## 配置

---

### 1.路由类
名称: hyperframework.web.router_class

类型: string

默认值: Hyperframework\Web\Router

### 2.开启/关闭 CSRF 防护
名称: hyperframework.web.csrf_protection.enable

类型: bool

默认值: true

### 3.CSRF 防护引擎类
名称: hyperframework.web.csrf_protection.engine_class

类型: string

默认值: Hyperframework\Web\CsrfProtectionEngine

### 4.CSRF 防护 token 名称
名称: hyperframework.web.csrf_protection.token_name

类型: string

默认值: _csrf_token

### 5.视图文件根路径
名称: hyperframework.web.view.root_path

类型: string

默认值: views

### 6.视图文件名是否包含输出格式
名称:hyperframework.web.view.filename.include_output_format

类型: bool

默认值: true

### 7.视图默认输出格式
名称: hyperframework.web.view.default_output_format

类型: string

默认值: html

### 8.视图文件格式
名称: hyperframework.web.view.format

类型: string

默认值: php

### 9.视图类
名称: hyperframework.web.view.class

类型: string

默认值: Hyperframework\Web\View

### 10.开启/关闭错误视图
名称: hyperframework.web.error_view.enable

类型: bool

默认值: true

### 11.错误视图根路径
名称: hyperframework.web.error_view.root_path

类型: string

默认值: views/_error

### 12.错误视图类
名称: hyperframework.web.error_view.class

类型: string

默认值: Hyperframework\Web\ErrorView

### 13.记录 HTTP 异常日志
名称: hyperframework.web.log_http_exception

类型: bool

默认值: false

### 14.开启/关闭 Debugger
名称: hyperframework.web.debugger.enable

类型: bool

默认值: false

### 15.Debugger 类
名称: hyperframework.web.debugger.class

类型: string

默认值: Hyperframework\Web\Debugger
