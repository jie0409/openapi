# 查询成交



请求路径：

```
GET /api/v1/market/trades
```

请求参数：

| **字段名** | **类型** | **是否必须** | **描述**         |
| ------- | ------ | -------- | -------------- |
| symbol  | string | 是        | 交易市场           |
| limit   | number | 否        | 默认100；10 - 500 |

返回参数：

| **字段名** |           | **类型** | **描述**          |
| ------- | --------- | ------ | --------------- |
| trades  |           | array  | 最新实时成交集合，时间倒序排列 |
|         | symbol    | string | 交易市场            |
|         | tradeId   | string | 品种              |
|         | price     | string | 最新买价            |
|         | size      | string | 最新卖家            |
|         | side      | string | BUY 或 SELL      |
|         | timestamp | string | 成交时间戳，毫秒        |

注意: 查询到的结果为主动成交的记录，即taker 方产生的trades

错误码：

* MARKET\_INVALID\_SYMBOL 无效品种
* MARKET\_PARAMETER\_ERROR 参数错误

请求示例：

```
GET https://{site}/api/v1/market/trades
```

响应示例：

```
{ 
  "data": {
    "trades": [
      {
        "symbol": "BTC_USDT",
        "tradeId": "600848671",
        "price": "7962.62",
        "size": "0.0122",
        "side": "BUY",
        "timestamp": 1566691672311
      },
      {
        "symbol": "BTC_USDT",
        "tradeId": "600848670",
        "price": "7960.12",
        "size": "0.0198",
        "side": "BUY",
        "timestamp": 1566691672311
      }
    ]
  },
  "result": true,
  "timestamp": 1566691672311
}
```
