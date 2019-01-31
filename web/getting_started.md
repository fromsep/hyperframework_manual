## 入门

---

### 1.通过 Composer 安装 Hyperframework
参考 [下载](downloads.md)。

### 2.配置类自动加载
创建 lib 文件夹，同时修改 composer.json，加入 namespace 对应关系：

```json
{
   "require": {
       "hyperframework/hyperframework": "*"
   },
   "autoload": {
        "psr-4": {
            "": "lib"
        }
    }
}
```
NOTE: init.php 必须返回一个数组。

为了更新 composer 类加载逻辑，需要在项目根目录中运行：

```
./composer.phar update
```
### 3.创建应用初始化配置文件
创建 config/init.php，添加配置代码：

```php
<?php
return [];
```

NOTE: init.php 必须返回一个数组。

### 4.创建应用入口文件
创建 public/index.php，添加应用启动代码：

```php
<?php
require dirname(__DIR__) . DIRECTORY_SEPARATOR
    . 'vendor' . DIRECTORY_SEPARATOR . 'autoload.php';
Hyperframework\Web\App::run();
```

### 5.创建路由器
创建 lib/Router.php，添加路由器代码：

```php
<?php
use Hyperframework\Web\Router as Base;

class Router extends Base {
    protected function prepare($routes) {
        $routes->addAll(['/' => 'index/show']);
    }
}
```

### 6.创建控制器

创建 lib/Controllers/IndexController.php，添加控制器代码：

```php
<?php
namespace Controllers;

use Hyperframework\Web\Controller;

class IndexController extends Controller {
    public function onShowAction() {
        return ['message' => 'hello world!'];
    }
}
```

### 7.创建视图
创建 views/index/show.html.php，添加视图代码：

```php
<?php
/* @var $this Hyperframework\Web\View */
echo $this['message'];
```

### 8.创建日志文件夹
创建 log 文件夹。

NOTE: log/app.log 应该可以被 PHP 进程创建和写入。

### 9. 完成

使用浏览器访问网站根目录，将会输出 “hello world!”。