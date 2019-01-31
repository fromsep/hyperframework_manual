## 事件监听

---

### 1.添加事件（Object）

```php
EventEmitter::addListener(Object);
```
Object对象必须具有getEventBindings方法，返回相应的事件用于注册。

使用#示例

```php
class DbOperationEventListener {
    /**
     * @return array
     */
    public function getEventBindings() {
        return [
            'hyperframework.db.transaction_operation_executing'
                => 'onTransactionOperationExecuting',
            'hyperframework.db.transaction_operation_executed'
                => 'onTransactionOperationExecuted',
            'hyperframework.db.sql_statement_executing'
                => 'onSqlStatementExecuting',
            'hyperframework.db.sql_statement_executed'
                => 'onSqlStatementExecuted',
            'hyperframework.db.prepared_statement_executing'
                => 'onPreparedStatementExecuting',
            'hyperframework.db.prepared_statement_executed'
                => 'onPreparedStatementExecuted'
        ];
    }

    /**
     * @param DbConnection $connection
     * @param string $operation
     * @return void
     */
    public function onTransactionOperationExecuting($connection, $operation) {
    }

    /**
     * @param string $status
     * @return void
     */
    public function onTransactionOperationExecuted($status) {
    }

    /**
     * @param DbConnection $connection
     * @param string $sql
     * @return void
     */
    public function onSqlStatementExecuting($connection, $sql) {
    }

    /**
     * @param string $status
     * @return void
     */
    public function onSqlStatementExecuted($status) {
    }

    /**
     * @param DbStatement $statement
     * @param array $params
     * @return void
     */
    public function onPreparedStatementExecuting($statement, $params) {
    }

    /**
     * @param string $status
     * @return void
     */
    public function onPreparedStatementExecuted($status) {
    }
}

EventEmitter::addListener(new DbOperationEventListener());
```

### 2.删除事件（Object）

```php
EventEmitter::removeListener(Object);
```

用于删除Object对象发注册的所有事件

### 3.添加事件（Array）

```php
EventEmitter::bindAll($bindings);
```

使用示例

```php
$bindings = [
	'hyperframework.db.transaction_operation_executing'
		=> 'onTransactionOperationExecuting',
	'hyperframework.db.transaction_operation_executed'
		=> 'onTransactionOperationExecuted',
	'hyperframework.db.sql_statement_executing'
		=> 'onSqlStatementExecuting',
	'hyperframework.db.sql_statement_executed'
		=> 'onSqlStatementExecuted',
	'hyperframework.db.prepared_statement_executing'
		=> 'onPreparedStatementExecuting',
	'hyperframework.db.prepared_statement_executed'
		=> 'onPreparedStatementExecuted'
];

EventEmitter::bindAll($bindings);
```

### 4.删除事件（Array）

```php
EventEmitter::unbindAll($bindings);
```
### 5.添加事件

```php
EventEmitter::bind($name, $callback);
```

### 6.删除事件

```php
EventEmitter::unbind($name, $callback);
```

### 7.触发事件

```php
EventEmitter::emit($name, $arguments);
```
用于触发某个事件



