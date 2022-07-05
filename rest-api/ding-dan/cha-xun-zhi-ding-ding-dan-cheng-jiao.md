# 查询指定订单成交

权限： 读取

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

####
