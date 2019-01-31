## 文件加载器

---

### 1.加载 PHP 文件

```php
$result = Hyperframework\Common\FileLoader::loadPhp($path);
```
如果加载文件是相对路径，那么会基于项目根路径。

### 2.加载数据文件

```php
$result = Hyperframework\Common\FileLoader::loadData($path);
```
如果加载文件是相对路径，那么会基于项目根路径。

### 3.加载 PHP 配置文件

```php
$result = Hyperframework\Common\ConfigFileLoader::loadPhp($path);
```
如果加载文件是相对路径，那么会基于项目根路径的 config 文件夹。

### 4.加载配置数据文件

```php
$result = Hyperframework\Common\ConfigFileLoader::loadData($path);
```
如果加载文件是相对路径，那么会基于项目根路径的 config 文件夹。

### 5.加载 PHP 临时文件

```php
$result = Hyperframework\Common\TmpFileLoader::loadPhp($path);
```
如果加载文件是相对路径，那么会基于项目根路径的 tmp 文件夹。

### 6.加载临时数据文件

```php
$result = Hyperframework\Common\TmpFileLoader::loadData($path);
```
如果加载文件是相对路径，那么会基于项目根路径的 tmp 文件夹。
