## 控制器

---

### 1.主流程

- 1.执行前置过滤逻辑
- 2.执行 action 处理逻辑
  - 执行 action 方法
  - 渲染 action 视图
- 3.执行后置过滤逻辑
- 4.执行 finalize 逻辑

### 2.Action 方法
控制器通过路由器的 getActionMethod 方法获取 action 方法名称。例如，当 action 等于 show 时，默认的 action 方法名称是 onShowAction。

当 Action 方法返回值作为视图模型时，应该返回数组。

### 3.设置视图
控制器的 setView 函数接受一个视图对象或者字符串为参数，字符串表示视图名，例如：

```php
$this->setView('index/show');
```
此时默认加载的视图文件是 views/index/show.html.php。

关于视图文件路径的详细设置参考 [视图]()。

视图对象必须包含 render 方法，该方法允许接受 action 返回值作为参数，例如：

```php
class CustomView {
    public function render($actionResult) {
        /* ... */
    }
}
```

### 4.获取视图

```php
$view = $this->getView();
```
获取通过 setView 设置的值。

当 module 等于 admin，controller 等于 welcome，action 等于 show，则默认值是 admin/welcome/show。

- 禁用视图

```php
$this->disableView();
```

- 激活视图

```php
$this->enableView();
```
- 渲染视图
$this->renderView();
如果视图处于激活状态（默认），此方法会在控制器的 handleAction 方法中被调用（action 方法执行完成之后）。

- 获取输出格式
$format = $this->getOutputFormat();
默认返回 format 路由参数。

### 5.路由参数

- 获取单个路由参数：

```php
$query = $this->getRouteParam('query');
```

- 获取全部路由参数：

```php
$params = $this->getRouteParams();
```

- 查询路由参数是否存在：

```php
$hasQuery = $this->hasRouteParam('query');
```

- 获取 App 对象

```php
$app = $this->getApp();
```

- 重定向

```php
$this->redirect('/path');
```
默认使用 302 重定向，可以重写，例如：

```php
$this->redirect('/path', 301);
```
NOTE: 调用 redirect 程序不会退出。

### 6.过滤器

`前置过滤器` 在 action 处理逻辑之前执行，例如：

```php
$this->addBeforeFilter(function() {
   $this->checkInput();
});
```

addBeforeFilter 函数也接受字符串，表示 filter 类，例如：

```php
$this->addBeforeFilter('MyFilter');
```

Filter 类必须包含 run 方法，该方法包含一个 controller 参数，例如：

```php
class MyFilter {
    public function run($controller) {
        /* filter logic */
    }
}
```
前置过滤器的执行顺序和添加顺序相同。

如果过滤器返回 false，则 controller 的后续 filter 和 action 处理不会被执行。

`后置过滤器` 在 action 处理逻辑之后（包括视图渲染），例如：

```php
$this->addAfterFilter(function() {
   $this->checkStatus();
});
```
addAfterFilter 也接受字符串参数，规则和 addBeforeFilter 函数相同。

后置过滤器的执行顺序和添加顺序相反。

`环绕过滤器` 在 action 处理逻辑之前和之后（包括视图渲染）执行的逻辑，例如：

```php
$this->addAroundFilter(function() {
   $this->begin();
   yield;
   $this->end();
});
```

当 yield 操作被执行，如果没有异常发生，yield 之后的逻辑始终会被执行。

环绕过滤器可以捕获被环绕逻辑中的异常，例如：

```php
$this->addAroundFilter(function() {
   try {
       yield;
   } catch (Exception $e) {
       /* processing the exception */
   }
});
```

addAroundFilter 也接受字符串参数，规则和 addBeforeFilter 函数相同。