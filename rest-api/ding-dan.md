# 订单

#### 下单

权限： 交易

请求路径：

```
POST /api/v1/trade/order
```

请求参数：

| **字段名**       | **类型**  | **是否必须** | **描述**                      |
| ------------- | ------- | -------- | --------------------------- |
| symbol        | string  | 是        | 交易市场                        |
| side          | string  | 是        | BUY or SELL                 |
| type          | string  | 是        | LIMIT or MARKET             |
| clientOrderId | string  | 否        | 客户端id，由大小写字母/数字/中横线组成，最大64位 |
| size          | string  | 否        | 数量，限价单和市价卖单必填               |
| price         | string  | 否        | 价格，限价单必填                    |
| amount        | string  | 否        | 市价买单花费,市价必填                 |
| IOC           | boolean | 否        | 默认false                     |

返回参数：

| **字段名**       | **类型** | **描述** |
| ------------- | ------ | ------ |
| orderId       | number | 订单号    |
| clientOrderId | string | 客户端id  |

注意：

错误码：

* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误
* TRADE\_NOT\_ENOUGH\_MONEY 余额不足
* TRADE\_PRICE\_FILTER\_DENIED price非法
* TRADE\_SIZE\_FILTER\_DENIED size非法
* TRADE\_AMOUNT\_FILTER\_DENIED 市价卖金额非法 或 price \* size 非法
* TRADE\_REPEAT\_CLIENT\_ORDER\_ID 重复的client\_order\_id，至少在6小时内判定去重
* TRADE\_OPEN\_ORDER\_EXCEED\_LIMIT open orders 超过最大限制
* TRADE\_SYMBOL\_MAINTAIN 品种维护

请求示例：

```
POST https://{site}/api/v1/trade/order
{
  "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194",
  "symbol":         "BTC_USDT",
  "side":           "BUY",
  "type":           "LIMIT",
  "size":           "0.1",
  "price":          "30000",
  "timeInForce":    "IOC"
}
```

响应示例：

```
{ 
  "data": {
    "orderId": 1234567890,
    "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194"
  },
  "result": true,
  "timestamp": 1566691672311
}
```

#### 查询单个订单

类型：PRIVATE 权限： VIEW

请求路径：

```
GET /api/v1/trade/order
```

请求参数：

| **字段名** | **类型** | **是否必须** | **描述** |
| ------- | ------ | -------- | ------ |
| symbol  | string | 是        | 交易市场   |
| orderId | number | 是        | 订单号    |

返回参数：

| **字段名**       | **类型**  | **描述**           |
| ------------- | ------- | ---------------- |
| orderId       | number  | 订单号              |
| symbol        | string  | 交易市场             |
| type          | string  | LIMIT or MARKET  |
| side          | string  | BUY or SELL      |
| price         | string  | 价格               |
| size          | string  | 订单数量             |
| amount        | string  | 市价买单金额           |
| filledSize    | string  | 已成交数量            |
| filledAmount  | string  | 已成交金额            |
| fee           | string  | 手续费              |
| feeCoin       | string  | 手续费币种            |
| status        | string  | OPEN / CLOSED    |
| IOC           | boolean | IOC              |
| clientOrderId | string  | 客户端订单号           |
| source        | string  | 来源， MANUAL / API |
| createTime    | number  | 创建订单时的时间戳，毫秒     |
| updateTime    | number  | 最近一次更新时的时间戳，毫秒   |

错误码：

* TRADE\_ORDER\_NOT\_FOUND 未查询到订单
* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误

请求示例：

```
GET https://{site}/api/v1/trade/order?symbol=BTC_USDT&orderId=1234567890
```

响应示例：

```
{ 
  "data": {
    "orderId": 1234567890,
    "symbol": "BTC_USDT",
    "orderType": "LIMIT",
    "side": "BUY",
    "price": "30000.00",
    "size": "0.1000",
    "filledSize": "0.0500",
    "filledAmount": "1500.00",
    "fee":  "0.15",
    "feeCoin":  "USDT",
    "IOC":  false,
    "status": "OPEN",
    "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194",
    "source": "API",
    "createdTime": 1566676132311,
    "updatedTime": 1566676132311
  },
  "result": true,
  "timestamp": 1566691672311
}
```

#### 查询订单by幂等id

类型：PRIVATE 权限： VIEW

请求路径：

```
GET /api/v1/trade/orderByClientOrderId
```

请求参数：

| **字段名**       | **类型** | **是否必须** | **描述**                                             |
| ------------- | ------ | -------- | -------------------------------------------------- |
| symbol        | string | 是        | 交易市场                                               |
| clientOrderId | number | 是        | 客户端订单号，一定时间内的订单可以通过此接口查询，正常查询请尽量使用 /v1/trade/order |

返回参数：

| **字段名**       | **类型**  | **描述**           |
| ------------- | ------- | ---------------- |
| orderId       | number  | 订单号              |
| symbol        | string  | 交易市场             |
| type          | string  | LIMIT or MARKET  |
| side          | string  | BUY or SELL      |
| price         | string  | 价格               |
| size          | string  | 订单数量             |
| amount        | string  | 市价买单金额           |
| filledSize    | string  | 已成交数量            |
| filledAmount  | string  | 已成交金额            |
| fee           | string  | 手续费              |
| feeCoin       | string  | 手续费币种            |
| status        | string  | OPEN / CLOSED    |
| IOC           | boolean | IOC              |
| clientOrderId | string  | 客户端订单号           |
| source        | string  | 来源， MANUAL / API |
| createTime    | number  | 创建订单时的时间戳，毫秒     |
| updateTime    | number  | 最近一次更新时的时间戳，毫秒   |

错误码：

* TRADE\_ORDER\_NOT\_FOUND 未查询到订单
* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误

请求示例：

```
GET https://{site}/api/v1/trade/orderByClientOrderId?symbol=BTC_USDT&clientOrderId=9e3d93d6-e9a4-465a-a39c-2e48568fe194
```

响应示例：

```
{ 
  "data": {
    "orderId": 1234567890,
    "symbol": "BTC_USDT",
    "orderType": "LIMIT",
    "side": "BUY",
    "price": "30000.00",
    "size": "0.1000",
    "filledSize": "0.0500",
    "filledAmount": "1500.00",
    "fee":  "0.15",
    "feeCoin":  "USDT",
    "IOC":  false,
    "status": "OPEN",
    "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194",
    "source": "API",
    "createdTime": 1566676132311,
    "updatedTime": 1566676132311
  },
  "result": true,
  "timestamp": 1566691672311
}
```

#### 撤销订单（异步）

类型：PRIVATE 权限： TRADE

请求路径：

```
DELETE /api/v1/trade/order
```

请求参数：

| **字段名** | **类型** | **是否必须** | **描述**     |
| ------- | ------ | -------- | ---------- |
| symbol  | string | 是        | 交易市场       |
| orderId | number | 是        | 需要撤销订单的订单号 |

返回参数：无

错误码：

* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误
* TRADE\_OPERATION\_DENIED 禁止操作
* TRADE\_SYMBOL\_MAINTAIN 品种维护

请求示例：

```
DELETE https://{site}/api/v1/trade/order
{
  "symbol":         "BTC_USDT",
  "orderId":        1234567890
}
```

响应示例：

```
{ 
  "result": true,
  "timestamp": 1566691672311
}
```

#### 查询活跃订单

类型：PRIVATE 权限： VIEW

请求路径：

```
GET /api/v1/trade/openOrders?symbol=BTC_USDT
```

请求参数：

| **字段名** | **类型** | **是否必须** | **描述** |
| ------- | ------ | -------- | ------ |
| symbol  | string | 是        | 交易市场   |

返回参数：

| **字段名** |               | **类型**  | **描述**               |
| ------- | ------------- | ------- | -------------------- |
| orders  |               | array   | createTime 时间倒序排列    |
|         | orderId       | number  | 订单号                  |
|         | symbol        | string  | 交易市场                 |
|         | type          | string  | LIMIT or MARKET      |
|         | side          | string  | BUY or SELL          |
|         | price         | string  | 价格                   |
|         | size          | string  | 订单数量                 |
|         | amount        | string  | 市价买单，买额              |
|         | filledSize    | string  | 已成交数量                |
|         | filledAmount  | string  | 已成交金额                |
|         | fee           | string  | 手续费                  |
|         | feeCoin       | string  | 手续费币种                |
|         | status        | string  | OPEN / CLOSED        |
|         | IOC           | boolean | 是否IOC                |
|         | clientOrderId | string  | 客户端订单号               |
|         | source        | string  | 来源， MANUAL / OPENAPI |
|         | createTime    | number  | 创建订单时的时间戳，毫秒，时间倒序    |
|         | updateTime    | number  | 最近一次更新时的时间戳，毫秒       |

注意：同一品种，openOrders 最多只允许200个

错误码：

* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误

请求示例：

```
GET https://{site}/api/v1/trade/openOrders?symbol=BTC_USDT
```

响应示例：

```
{ 
  "data": {
    "orders":[
      {
        "orderId": 1234567890,
        "symbol": "BTC_USDT",
        "orderType": "LIMIT",
        "side": "BUY",
        "price": "30000.00",
        "size": "0.1000",
        "filledSize": "0.0500",
        "filledAmount": "1500.00",
        "fee":  "0.15",
        "feeCoin":  "USDT",
        "IOC": false,
        "state": "OPEN",
        "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194",
        "source": "API",
        "createdTime": 1566676132311,
        "updatedTime": 1566676132311
      }
    ]
  },
  "result": true,
  "timestamp": 1566676132311
}
```

#### 查询所有订单

类型：PRIVATE 权限： VIEW

请求路径：

```
GET /api/v1/trade/allOrders?symbol=BTC_USDT
```

请求参数：

| **字段名**   | **类型** | **是否必须** | **描述**                                              |
| --------- | ------ | -------- | --------------------------------------------------- |
| symbol    | string | 是        | 交易市场                                                |
| startTime | number | 否        | 开始时间                                                |
| endTime   | number | 否        | 结束时间，默认当前时间                                         |
| limit     | number | 否        | <p>默认50， 1 - 200</p><p>当时间范围内超出limit时，返回前limit条</p> |

返回参数：

| **字段名** |               | **类型**  | **描述**               |
| ------- | ------------- | ------- | -------------------- |
| orders  |               | array   | createTime 时间倒序排列    |
|         | orderId       | number  | 订单号                  |
|         | symbol        | string  | 交易市场                 |
|         | orderType     | string  | LIMIT or MARKET      |
|         | side          | string  | BUY or SELL          |
|         | price         | string  | 价格                   |
|         | size          | string  | 订单数量                 |
|         | amount        | string  | 市价买单额                |
|         | filledSize    | string  | 已成交数量                |
|         | filledAmount  | string  | 已成交金额                |
|         | fee           | string  | 手续费                  |
|         | feeCoin       | string  | 手续费币种                |
|         | status        | string  | OPEN / CLOSED        |
|         | IOC           | boolean | 是否IOC                |
|         | clientOrderId | string  | 客户端订单号               |
|         | source        | string  | 来源， MANUAL / OPENAPI |
|         | createTime    | number  | 创建订单时的时间戳，毫秒，时间倒序    |
|         | updateTime    | number  | 最近一次更新时的时间戳，毫秒       |

错误码：

* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误

请求示例：

```
GET https://{site}/api/v1/trade/allOrders?symbol=BTC_USDT&limit=1
```

响应示例：

```
{ 
  "data": {
    "orders":[
      {
        "orderId": 1234567890,
        "symbol": "BTC_USDT",
        "orderType": "LIMIT",
        "side": "BUY",
        "price": "30000.00",
        "size": "0.1000",
        "filledSize": "0.0500",
        "filledAmount": "1500.00",
        "fee":  "0.15",
        "feeCoin":  "USDT",
        "IOC": false,
        "state": "OPEN",
        "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194",
        "source": "API",
        "createdTime": 1566676132311,
        "updatedTime": 1566676132311
      }
    ]
  },
  "result": true,
  "timestamp": 1566691672311
}
```

#### 查询成交

类型：PRIVATE 权限： VIEW

请求路径：

```
GET /api/v1/trade/fills
```

请求参数：

| **字段名**   | **类型** | **是否必须** | **描述** |
| --------- | ------ | -------- | ------ |
| symbol    | string | 是        | 交易市场   |
| startTime | number | 否        | 开始时间   |
| endTime   | number | 否        | 结束时间   |

返回参数：

| **字段名** |           | **类型** | **描述**         |
| ------- | --------- | ------ | -------------- |
| fills   |           | array  | 时间倒序排列         |
|         | id        | number | 成交id           |
|         | orderId   | number | 订单号            |
|         | symbol    | string | 交易市场           |
|         | side      | string | BUY or SELL    |
|         | role      | string | TAKER or MAKER |
|         | price     | string | 价格             |
|         | size      | string | 订单数量           |
|         | fee       | string | 手续费            |
|         | feeCoin   | string | 手续费币种          |
|         | timestamp | number | 时间戳，毫秒，时间倒序    |

注意：当时间范围内超出100时，返回前100条

错误码：

* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误

请求示例：

```
GET https://{site}/api/v1/trade/fills?symbol=BTC_USDT
```

响应示例：

```
{ 
  "data": {
    "fills":[
      {
        "id": 9876543210,
        "symbol": "BTC_USDT",
        "side": "BUY",
        "role":  "TAKER",
        "price": "30000.00",
        "size": "0.1000",
        "fee":  "0.15",
        "feeCoin":  "USDT",
        "timestamp": 1566676132311
      },
      {
        "id": 9876543200
        "symbol": "BTC_USDT",
        "side": "BUY",
        "role":  "TAKER",
        "price": "29000.00",
        "size": "0.1200",
        "fee":  "0.145",
        "feeCoin":  "USDT",
        "timestamp": 1566676132311
      }
    ]
  },
  "result": true,
  "timestamp": 1566691672311
}
```

#### 根据orderId查询成交

类型：PRIVATE 权限： VIEW

请求路径：

```
GET /api/v1/trade/fillsByOrderId
```

请求参数：

| **字段名** | **类型** | **是否必须** | **描述**                                                                  |
| ------- | ------ | -------- | ----------------------------------------------------------------------- |
| symbol  | string | 是        | 交易市场                                                                    |
| orderId | number | 是        | 订单ID，不存在时返回空列表                                                          |
| fromId  | number | 否        | <p>返回此id 之前100条记录（更旧的记录），不足100条返回所有</p><p>不指定则返回最新的</p><p>不包含此id的成交</p> |

返回参数：

| **字段名** |           | **类型** | **描述**         |
| ------- | --------- | ------ | -------------- |
| fills   |           | array  | 时间倒序排列         |
|         | id        | number | 成交id           |
|         | orderId   | number | 订单号            |
|         | symbol    | string | 交易市场           |
|         | side      | string | BUY or SELL    |
|         | role      | string | TAKER or MAKER |
|         | price     | string | 价格             |
|         | size      | string | 订单数量           |
|         | fee       | string | 手续费            |
|         | feeCoin   | string | 手续费币种          |
|         | timestamp | number | 时间戳，毫秒，时间倒序    |

错误码：

* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误

请求示例：

```
GET https://{site}/api/v1/trade/fillsByOrderId?symbol=BTC_USDT&orderId=22334455
```

响应示例：

```
{ 
  "data": {
    "fills":[
      {
        "id": 9876543210,
        "orderId": 22334455,
        "symbol": "BTC_USDT",
        "side": "BUY",
        "role":  "TAKER",
        "price": "30000.00",
        "size": "0.1000",
        "fee":  "0.15",
        "feeCoin":  "USDT",
        "timestamp": 1566676132311
      },
      {
        "id": 9876543200,
        "orderId": 22334455,
        "symbol": "BTC_USDT",
        "side": "BUY",
        "role":  "TAKER",
        "price": "29000.00",
        "size": "0.1200",
        "fee":  "0.145",
        "feeCoin":  "USDT",
        "timestamp": 1566676132311
      }
    ]
  },
  "result": true,
  "timestamp": 1566691672311
}
```

#### 撤销市场所有订单 （异步）

类型：PRIVATE 权限： TRADE

请求路径：

```
DELETE /api/v1/trade/allOrders
```

请求参数：

| **字段名** | **类型** | **是否必须** | **描述** |
| ------- | ------ | -------- | ------ |
| symbol  | string | 是        | 交易市场   |

返回参数：无

错误码：

* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误
* TRADE\_OPERATION\_DENIED 禁止操作
* TRADE\_SYMBOL\_MAINTAIN 品种维护

请求示例：

```
DELETE https://{site}/api/v1/trade/allOrders
{
  "symbol":         "BTC_USDT"
}
```

响应示例：

```
{ 
  "result": true,
  "timestamp": 1566691672311
}
```

###
