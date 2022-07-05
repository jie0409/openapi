# 查询成交

权限： 读取

权重： 10

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

| **字段名** |           | **类型** | **描述**        |
| ------- | --------- | ------ | ------------- |
| fills   |           | array  | 成交集合，时间倒序排列   |
|         | id        | number | 成交id          |
|         | orderId   | number | 订单号           |
|         | symbol    | string | 交易市场          |
|         | side      | string | BUY 或 SELL    |
|         | role      | string | TAKER 或 MAKER |
|         | price     | string | 价格            |
|         | size      | string | 订单数量          |
|         | fee       | string | 手续费           |
|         | feeCoin   | string | 手续费币种         |
|         | timestamp | number | 成交时间戳，毫秒      |

注意：当时间范围内超出100时，返回前100条

错误码：

* TRADE\_INVALID\_SYMBOL    无效品种
* TRADE\_PARAMETER\_ERROR    参数错误

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
