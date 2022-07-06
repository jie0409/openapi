# 订单

**订单**

有订单变化时推送当前订单

订阅：

```
{
  "op": "SUBSCRIBE",  //订阅
  "topic":  "ORDER", //订单
  "symbol": "BTC_USDT"  // 品种
}
```

推送数据

```
{
  "topic": "ORDER",
  "symbol": "BTC_USDT",
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
    "feeCoin": "USDT",
    "IOC":  false,
    "status": "OPEN",
    "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194"
    "createTime": 1566676132311,
    "updateTime": 1566676132311
  },
  "timestamp": 1566691672311
}
```

