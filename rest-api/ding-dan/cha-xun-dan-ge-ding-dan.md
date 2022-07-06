# 查询单个订单

权限： 读取

权重： 1

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
| type          | string  | LIMIT 或 MARKET   |
| side          | string  | BUY 或 SELL       |
| price         | string  | 价格               |
| size          | string  | 订单数量             |
| amount        | string  | 市价买单金额           |
| filledSize    | string  | 已成交数量            |
| filledAmount  | string  | 已成交金额            |
| fee           | string  | 手续费              |
| feeCoin       | string  | 手续费币种            |
| status        | string  | OPEN 或 CLOSED    |
| IOC           | boolean | IOC              |
| clientOrderId | string  | 客户端订单号           |
| source        | string  | 来源， MANUAL 或 API |
| createTime    | number  | 创建订单时的时间戳，毫秒     |
| updateTime    | number  | 最近一次更新时的时间戳，毫秒   |

错误码：

* TRADE\_ORDER\_NOT\_FOUND    未查询到订单
* TRADE\_INVALID\_SYMBOL    无效品种
* TRADE\_PARAMETER\_ERROR   参数错误

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
    "type": "LIMIT",
    "side": "BUY",
    "price": "30000.00",
    "size": "0.1000",
    "filledSize": "0.0500",
    "filledAmount": "1500.00",
    "fee":  "0.15",
    "feeCoin":  "USDT",
    "status": "OPEN",
    "IOC":  false,
    "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194",
    "source": "API",
    "createTime": 1566676132311,
    "updateTime": 1566676132311
  },
  "result": true,
  "timestamp": 1566691672311
}
```
