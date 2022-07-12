# 获取交易市场

权重：1

请求路径：

`1GET /api/v1/common/symbols`

请求参数：

| **字段名** | **类型**  | **是否必须** | **描述**        |
| ------- | ------- | -------- | ------------- |
| symbols |  string |  否       | 交易市场，多个用“，”拼接 |

返回参数：

| **字段名** |   | **类型** | **描述** |
| ------- | - | ------ | ------ |

| **字段名** |                 | **类型**  | **描述**                       |
| ------- | --------------- | ------- | ---------------------------- |
| symbols |                 | array   | 按交易市场升序排列                    |
|         | symbol          | string  | 交易市场                         |
|         | type            | string  | SPOT / LEVERAGED             |
|         | baseCurrency    | string  | base币种                       |
|         | quoteCurrency   | string  | quote币种                      |
|         | basePrecision   | number  | base货币交易量精度位数                |
|         | quotePrecision  | number  | quote货币价格精度位数                |
|         | amountPrecision | number  | 市价买额的精度位数                    |
|         | minAmount       | string  | 最小下单金额，price \* size 或者 市价买额 |
|         | minTradeSize    | string  | 最小下单量，限价单限制                  |
|         | maxTradeSize    | string  | 最大下单量，限价单限制                  |
|         | minTradeAmount  | string  | 最小下单金额，市价买单限制                |
|         | maxTradeAmount  | string  | 最大下单金额，市价买单限制                |
|         | minTradeDumping | string  | 最小下单量，市价卖单限制                 |
|         | maxTradeDumping | string  | 最大下单量，市价卖单限制                 |
|         | buyCeiling      | string  | 买价的上限比例，不可高于最新最高买价的倍数，固定为1.1 |
|         | sellFloor       | string  | 卖价的下限比例，不可低于最新最低卖价的倍数，固定为0.9 |
|         | enable          | boolean | 开放交易                         |

注意事项：

错误码：

请求示例：

```
GET https://{site}/api/v1/common/symbols?symbol=BTC_USDT
```

响应示例：

```
{ 
  "data": {
    "symbols":[
      {
        "symbol": "BTC_USDT",
        "type": "SPOT",
        "baseCurrency": "BTC",
        "quoteCurrency": "USDT",
        "basePrecision": 6,
        "quotePrecision": 2,
        "amountPrecision": 8,
        "minAmount": "10",
        "minTradeSize": "0.000001",
        "maxTradeSize": "1000",
        "minTradeAmount": "10",
        "maxTradeAmount": "1000000",
        "minTradeDumping": "0.000001",
        "maxTradeDumping": "100",
        "enable": true,
        "buyCeiling": "1.1",
        "sellFloor": "0.9"
      }
    ]
  },
  "result": true,
  "timestamp": 1566676132311
}
```
