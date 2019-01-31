## Web 客户端

---

作者：daydaygo

WebClient 类位于 Hyperframework\Common 命名空间下。

### 1.设计思路

PHP 的 `curl` 扩展是面向过程式的调用，通过 WebClient 封装成面向对象式的调用。封装上尽量贴合 `curl` 的原生函数，学习过 `curl` 用法后可以轻松切换到 WebClient。

### 2.初始化

`$c = new WebClient();`

### 3.get 请求

函数原型：`public function get($url, $options = [])`

使用示例：`$res = $c->get($url, $options = []);`

注意：get 参数需要拼接到 `$url` 参数中

### 4.post 请求

函数原型：`public function post($url, $data = null, $options = [])`

使用示例：`$res = $c->post($url, $data = null, $options = []);`

**注意**: post 请求默认设置 `Content-Type: application/json`, 如果对方服务器不支持, 请设置成相应的格式, 如:

```php
// 推荐: 通过 WebClient const 变量来自定义常用 curl option
$c->post($url, $data = null, [WebClient::OPT_DATA_TYPE => 'application/x-www-form-urlencoded']);

// 不推荐: 简单粗暴设置 http header
$res = $c->post($url, $data = null, [CURLOPT_HTTPHEADER => ['Content-Type: application/x-www-form-urlencoded']]);
```

### 5.异常处理

请求失败时会 `throw new WebClientException`，建议捕获异常并处理

使用示例：

```php
public function get($url, $options = []) {
    // 设置超时，配置项和 curl 保持一致
    if (!isset($options[CURLOPT_TIMEOUT])) {
        $options[CURLOPT_TIMEOUT] = 10;
    }
    // 此处可以日志记录
    Log::log(['url' => $url, 'options' => $options]);

    // 异常处理
    try {
        $result = parent::get($url, $options);
        Log::log(['result' => $result]);
    } catch (Exception $e) {
        // 推荐统一封装异常时的返回值
        $result = json_encode([
            'code'      => '999999',
            'message'   => $e->getMessage(),
        ]);
        // todo：异常处理
    }
    return $result;
}
```

### 6.高级应用 - 发送异步请求

函数原型：`public static function sendAsyncRequests($asyncOptions)`

使用示例：

```php
WebClient::sendAsyncRequests([
    WebClient::OPT_ASYNC_REQUEST_COMPLETE_CALLBACK  => function($client, $response, $error) {
        // 请求完成的回调逻辑
    },
    WebClient::OPT_ASYNC_REQUEST_FETCHING_CALLBACK   => function() {
        // 设置请求，需要考虑请求队列最大容量
    },
    WebClient::OPT_ASYNC_REQUEST_FETCHING_INTERVAL   => 2, // 设置请求时间间隔
    WebClient::OPT_ASYNC_MAX_CONCURRENT_REQUESTS     => 1000 // 请求队列最大容量
]);
```
