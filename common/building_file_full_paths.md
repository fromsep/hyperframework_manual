## 构建文件全路径

---

### 1.基于项目根文件夹的路径

```php
$fullPath = Hyperframework\Common\FileFullPathBuilder::build($relativePath);
```
### 2.基于配置文件夹的路径

```php
$fullPath = Hyperframework\Common\ConfigFileFullPathBuilder::build($relativePath);
```
### 3.基于临时文件夹的路径

```php
$fullPath = Hyperframework\Common\TmpFileFullPathBuilder::build($relativePath);
```
