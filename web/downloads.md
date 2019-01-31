## 下载

---

### 1.通过 Composer 下载

1. 安装 Composer。安装方法参考 Composer 文档。
2. 在项目根目录中新建 composer.json 文件，添加对 Hyperframework 的依赖：

```json
{
    "require": {
        "hyperframework/hyperframework": "*"
    }
}
```
NOTE: 由于目前 Hyperframework 还没有发布正式版，所以需要加入 minimum-stability 字段来获取非正式版本，例如：
```json
{
    "minimum-stability": "alpha",
    "require": {
        "hyperframework/hyperframework": "*"
    }
}
```
3. 在项目根目录中运行：

```
php composer.phar install
```
Hyperframework 会被自动安装到项目根目录的 vendor/hyperframework/hyperframework 文件夹中。 

### 2.通过 Github 下载

项目地址： https://github.com/hyperframework/hyperframework