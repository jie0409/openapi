# 查询所有订单

权限： 读取

请求路径：

```
GET /api/v1/trade/allOrders
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
