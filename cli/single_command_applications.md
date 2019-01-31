## 单命令应用

---

### 1.什么是 App 类
Cli 模块中的 App 类继承自 Common 模块的 App 类，并通过 run 静态方法定义了单命令行应用的主流程。应用启动文件（run）通过调用该类中的 run 静态方法来运行应用。

### 2.主流程
**1. App 对象创建**

App 类通过调用自身的 createApp 静态方法创建 App 对象。对象创建过程中会执行父类的构造函数，同时解析命令行输入（选项，参数），如果包含 help 选项，则调用 renderHelp 方法输出帮助信息，如果包含 version 选项，则调用 renderVersion 方法输出版本信息。

**2. 执行命令**

根据命令类配置，创建 command 对象。然后，调用 command 对象的 execute 方法（输入参数等于传入 execute 方法参数）。

**3. 结束运行**

结束运行时，app 对象的 finalize 方法会被调用。

### 3.命令配置
**配置文件**

配置文件 config/command.php。

**名称**

```php
return [
    'name' => 'my-command'
];
```
必须设置命令名称。

**版本**

```php
[
    'version' => '1.0.0'
];
```

**描述**
```php
[
    'description' => 'content'
];
```

**类**
```php
[
    'class' => 'CustomCommand'
];
```
默认值是应用根命名空间的 command 类。比如，当应用的根命名空间是 MyApp 时，默认的 command 类就是 MyApp\Command。

**参数**
```php
[
    'arguments' => [
        [
            'name' => 'arg-1',
            'required' => false,
            'repeatable' => true
        ]
    ]
];
```
单个 argument 配置必须有 name 字段，字段值的类型必须是字符串，字段值必须值包含一个以上的字母，数字或中划线，并且不能以中划线开始。

required 字段：配置参数是否是必选的，必须是一个 bool 值，默认值是 true。

repeatable 字段：配置参数是否是可重复的，必须是一个 bool 值，默认值是 false。

如果参数配置不存在，那么，将通过使用 command 对象的 execute 方法的参数列表信息作为默认配置，比如：
```php
class Command {
    public function execute($arg1, $arg2 = null) {
    }
}
```
等价与：
```php
[
    'arguments' => [
        [
            'name' => 'arg1'
        ], [
            'name' => 'arg2',
            'required' => false,
        ]
    ]
];
```
```php
class Command {
    public function execute(...$args) {
    }
}
```
等价与：
```php
[
    'arguments' => [
        [
            'name' => 'arg',
            'required' => false,
            'is_repeatable' => true,
        ]
    ]
];
```

NOTE: 可重复参数必须是最后一个，必选参数之后的参数必须都是必选的。

**选项**
```php
[
    'options' => [
        'name' => 'option1',
        'short_name' => 'o',
        'required' => true,
        'repeatable' => true,
        'description' => 'content'
    ]
];
```

Option 配置必须有 name 字段，name 字段值的类型必须是字符串，字段值必须值包含一个以上的字母，数字或中划线，并且不能以中划线开始。

short_name 字段值的类型必须是字符串，字段值必须值必须是字母或数字，并且不能是 W（大写）。

required 字段必须是一个 bool 值，默认值是 false。

repeatable 字段必须是一个 bool 值，默认值是 false。

**互斥选项分组**
```php
[
    'mutually_exclusive_option_groups' => [
        ['option1', 'option2', 'required' => true]
    ]
];
```

required 字段必须是一个 bool 值，默认值是 false。

### 4.获取命令配置对象
```php
$app->getCommandConfig();
```

### 5.命令参数
设置命令参数：
```php
$app->setArguments($arguments);
```
$arguments 是一个数组，包含所有用户输入的参数值。setArguments 是 protected 方法。

获取命令参数：
```php
$app->getArguments();
```
### 6.命令选项
设置命令选项：
```php
$app->setOptions($options);
```
参数 $options 是一个数组，包含所有用户输入的选项值，字段名表示 option 的名称，如果 option 没有参数，默认值是 true。setOptions 是 protected 方法。

获取所有命令选项：
```php
$options = $app->getOptions();
```
获取单个命令选项：
```php
$value = $app->getOption($name);
```
查询命令选项是否存在：
```php
$hasOption = $app->hasOption($name);
```
### 7.魔术选项
**--help**

当命令中包含 help 选项时，在应用的构造函数中会自动调用 renderHelp 方法渲染帮助信息。 

**--version**

当命令中包含 version 选项时，在应用的构造函数中会自动调用 renderVersion 方法版本信息。

**--**

用于分割选项和参数（如果参数需要以 - 开始）

### 8.其他
由于 Cli 模块的 App 类继承自 Common 模块的 App 类，通过 Common 模块文档中的 [App 基础](/cn/manual/common/app_basics) 获取更多相关信息。
