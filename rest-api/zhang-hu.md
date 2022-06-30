# 账户

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

####
