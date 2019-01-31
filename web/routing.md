## 路由

---

### 简介

通过实现 Hyperframework\Web\Router 类的 prepare 抽象方法来添加路由。

### 规则匹配

#### 1. 静态路径

```php
$routes->add('my-controller/my-action');
```

匹配规则建议使用相对路径（默认基于根路径）。如需匹配顶层路径，则使用 '/'，例如：

```php
$routes->addAll(['/' => 'index/show']);
```
### 2. 动态段

```php
$routes->add(':segment', ['to' => 'index/show']);
```

如果匹配成功，可以通过 Router 的 getParam 获取对应的值，例如：

```php
$this->getParam('segment');
```

### 3. 可选段

```php
$routes->add('required(/optional)', ['to' => 'index/show']);
```

### 4. 通配符

```php
$routes->add('*wildcard', ['to' => 'index/show']);
```
和动态段不同的是，通配符匹配是贪婪匹配，匹配会跨越 "/"。
如果匹配成功，可以通过 Router 的 getParam 获取对应的值。

### 5. add 选项

* 限制 HTTP 请求方法：

```php
$routes->add('/', [
    'methods' => ['GET'],
    'to' => 'index/show'
]);
```
等价与：
```php
$routes->addGet('/', ['to' => 'index/show']);
```
* 限制多个 HTTP 请求方法：

```php
$routes->add('/', [
    'methods' => ['GET', 'POST'],
    'to' => 'index/show'
]);
```

- 限制文件格式：

```php
$routes->add('path', [
    'format' => 'html',
    'to' => 'index/show'
]);
```

等价与：

```php
$routes->add('path.html', ['to' => 'index/show']);
```
- 匹配多个格式：

```php
$routes->add('path', [
    'formats' => ['html', 'json'],
    'to' => 'index/show'
]);
```

- 匹配任意格式：

```php
$routes->add('path', [
    'has_format' => true,
    'to' => 'index/show'
]);
```
- 设置默认格式：

```php
$routes->add('path', [
    'has_format' => true,
    'default_format' => 'html',
    'to' => 'index/show'
]);
```
- 限制动态段格式：

可以使用正则表达式限制动态段的格式，例如：

```php
$routes->add(':segment', [
    ':segment' => '[a-z]',
    'to' => 'index/show'
]);
```
附加规则：

```php
$routes->add(':segment', [
    'extra' => function($matches) {
        if ($matches['segment'][0] === 'x') {
            return true;
        }
    },
    'to' => 'index/show'
]);
```
附加规则返回 bool 值，true 表示通过匹配。

- 设置多个附加规则：

```php
$routes->add(':segment', [
    'extra' => [$callback1, $callback2],
    'to' => 'index/show'
]);
```
### 6. 资源匹配

```php
$routes->addResource('sitemap');
```

会使用预定义 action 规则：

| HTTP 方法 | 路径 | action |
| --------- | ---- | ------ |
| GET | /sitemap | show |
| GET | /sitemap/new | new |
| GET | /sitemap/edit | edit |
| POST | /sitemap | create |
| PUT/PATCH | /sitemap | update |
| DELETE | /sitemap | delete| 

controller 等于 sitemap。

- 资源匹配选项

设置 action

例如：

```php
$routes->addResource('sitemap', [
    'actions' => ['show']
]);
```

默认值：['show', 'new', 'edit', 'create', 'update', 'delete']

资源匹配选项支持 add 选项，例如：

```php
$routes->addResource('sitemap', [
    'extra' => $callback
]);
```
- 自定义 action

```php
$routes->addResource('sitemap', [
    'actions' => ['preview']
]);
```
等价与：

```php
$routes->addResource('sitemap', [
    'actions' => [
        'preview' => ['GET', 'preview']
    ]
]);
```
第一个元素可以是字符串（定义单个 HTTP 请求方法限制）或数组（定义多个 HTTP 请求方法限制），默认值是 'GET'。

第二个参数是 action 路径，默认和 action 名称相同。action 路径基于资源路径，例如，当资源路径等于 sitemap，action 路径等于 preview，那么请求路径是 sitemap/preview。

action 规则支持 add 选项（methods 选项除外），例如：

```php
$routes->addResource('sitemap', [
    'actions' => [
        'preview' => ['GET', 'preview', 'extra' => $callback]
    ]
]);
```
- 使用预定义 action

例如：
```php
$routes->addResource('sitemap', [
    'actions' => ['show']
]);
```
等价与：
```php
$routes->addResource('sitemap', [
    'actions' => [
         'show' => [['GET'], '/']
    ]
]);
```
- 修改预定义 action 规则

```php
$routes->addResource('sitemap', [
    'actions' => [
        'delete' => ['DELETE', 'remove']
    ]
]);
```

### 7.资源集合匹配

```php
$routes->addResources('documents');
```
会使用预定义集合 action 规则：

| HTTP 方法 | 路径 | action |
| --------- | ---- | ------ |
| GET | /documents  | index |
| GET | /documents/new | new |
| POST |  /documents | create |

和预定义元素 action 规则：

| HTTP 方法 | 路径 | action |
| --------- | ---- | ------ |
| GET | /documents/:id |  show |
| GET | /documents/:id/edit | edit |
| PUT/PATCH | /documents/:id | update |
| DELETE | /documents/:id | delete | 

controller 等于 document。

### 8.资源集合匹配选项

- collection_actions

设置集合 action，例如：

```php
$routes->addResources('documents', [
    'collection_actions' => ['index']
]);
```

默认值：['index', 'new', 'create']

- element_actions

设置元素 action，例如：

```php
$routes->addResource('documents', [
    'element_actions' => ['show']
]);
```

默认值：['show', 'edit', 'update', 'delete']

- id

通过正则表达式定义元素 id 匹配规则，例如：

```php
$routes->addResources('documents', [
    'id' => '[a-z]+'
]);
```
默认值：\d+

- 更多选项

资源集合匹配选项支持 add 选项（methods 选项除外），例如：

```php
$routes->addResources('documents', [
    'extra' => $callback
]);
```
### 8.Scope 匹配

Scope 匹配用于限制和修改根域名和路径，域名和根路径只能是静态的。

路径匹配：

```php
$routes->addScope('admin', function($routes) {
    $routes->addAll(['settings' => 'setting/index']);
});
```
等价与：

```php
$routes->add(['admin/settings' => 'admin/setting/index']);
```
- 域名匹配：

```php
$routes->addScope(['domain' => 'subdomain.hyperframework.com'] , function($routes) {
    $routes->addAll(['settings' => 'setting/index']);
});
```
NOTE: 在 scope 回调方法内调用 $this->getPath() 和 $this->getDomain() 返回的是相对路径和域名。

- 设置 module：

```php
$routes->addScope(['path' => 'admin', 'module' => 'console'], function($routes) {
    $routes->addAll(['settings' => 'setting/index']);
});
```
- 设置顶层 module：

```php
$routes->addScope(['path' => 'admin', 'module' => '/'], function($routes) {
    $routes->addAll(['settings' => 'setting/index']);
});
```

### 10.获取 app 对象

```php
$app = $this->getApp();
```

### 11. 获取路径

```php
$path = $this->getPath();
```

### 12. 设置/获取 action

- 设置：

```php
$this->setAction('preview');
```

- 获取：

```php
$action = $this->getAction();
```

### 13. 设置/获取 action 方法

- 设置：

```php
$this->setActionMethod('onPreviewAction');
```

- 获取：

```php
$method = $this->getActionMethod();
```

### 14. 设置/获取 controller

- 设置：

```php
$this->setController('documents');
```

- 获取：

```php
$controller = $this->getController();
```

### 15.设置/获取 controller 类

- 设置：

```php
$this->setControllerClass('DocumentsController');
```

- 获取：

```php
$class = $this->getControllerClass();
```

### 16.设置/获取 module

- 设置：

```php
$this->setModule('admin');
```

- 获取：

```php
$this= $routes->getModule();
```

### 17. 路由参数

- 设置：

```php
$this->setParam('query', 'hyperframework');
```

- 删除：

```php
$this->removeParam('query');
```

- 获取单个路由参数：

```php
$query = $this->getParam('query');
```

- 获取全部路由参数：

```php
$params = $this->getParams();
```

- 查询路由参数是否存在：

```php
$hasQuery = $this->hasParam('query');
```

- 重定向

```php
$routes->add(':segment', ['redirect_to' => '/books']);
```

等价于：

```php
$routes->add(':segment', ['redirect_to' => ['location': '/books', 'status_code' => 301]]);
```

- 使用闭包函数：

```php
$routes->add(':segment', ['redirect_to' => function() {
    return '/books/' . $this->getParam('segment');
}]);
```