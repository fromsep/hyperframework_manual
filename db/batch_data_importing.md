## 批量数据导入

---

```php
$options = [];
$table = 'Article';
$rows = [
    [
        'title' => 'title 1',
        'content' => 'content 1'
    ],
    [
        'title' => 'title 2',
        'content' => 'content 2'
    ]
];
Hyperframework\Db\DbClient::insertAll($table, $rows, $options);
```
$rows 参数是一个二维数组，包含要导入的行。

$options 参数是可选的，有两个选项：

**batch_size**

用于设定一条 sql 语句最多导入多少行（默认使用一条 sql 语句导入所有行），例如：

```php
$options = ['batch_size' => 2];
$table = 'Article';
$rows = [
    [
        'title' => 'title 1',
        'content' => 'content 1'
    ],
    [
        'title' => 'title 2',
        'content' => 'content 2'
    ],
    [
        'title' => 'title 3',
        'content' => 'content 3'
    ]
];
Hyperframework\Db\DbClient::insertAll($table, $rows, $options);
```

**column_names**

用于指定列名，这样 $rows 参数中包含的行就可以省去列名。

例如：
```php
$options = ['column_names' => ['title', 'content']];
$table = 'Article';
$rows = [
    [
        'title 1',
        'content 1'
    ],
    [
        'title 2',
        'content 2'
    ]
];
Hyperframework\Db\DbClient::insertAll($table, $rows, $options);
```
