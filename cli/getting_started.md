## 入门

---

### 1.通过 Composer 安装 Hyperframework
参考 [下载](/web/downloads.md)。

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

为了更新 composer 类加载逻辑，需要在项目根目录中运行：

```bash
./composer.phar update
```

### 3.创建应用初始化配置文件
创建 config/init.php，添加配置代码：

```php
<?php
return [];
```

NOTE: init.php 必须返回一个数组。

### 4.创建应用启动文件
创建 run，添加应用启动代码：

```php
#!/usr/bin/env php
<?php
require __DIR__ . DIRECTORY_SEPARATOR
    . 'vendor' . DIRECTORY_SEPARATOR . 'autoload.php';
Hyperframework\Cli\App::run(__DIR__);
```

### 5.赋予 run 可执行权限：

```bash
chmod 755 run
```

### 6.添加命令配置
创建 config/command.php，添加命令配置代码：
```php
<?php
return [
    'name' => 'demo',
    'version' => '1.0.0',
    'options' => [
        ['name' => 'opt'],
        ['name' => 'help'],
        ['name' => 'version']
    ]
];
```
### 7.添加命令
创建 lib/Command.php，添加命令代码：

```php
<?php
use Hyperframework\Cli\Command as Base;

class Command extends Base {
    public function execute($arg) {
        if ($this->hasOption('opt')) {
            echo 'opt: true', PHP_EOL;
        }
        echo 'arg: ', $arg, PHP_EOL;
    }
}
```

### 8.显示帮助
在项目根目录，输入：
```.bash
./run --help
```
默认帮助信息将会被输出：
```.nohighlight
Usage: demo [--opt] [--help] [--version] <arg>
```

### 9.执行命令
在项目根目录，输入：
```.bash
./run --opt content
```
输出：
```.nohighlight
opt: true
arg: content
```
