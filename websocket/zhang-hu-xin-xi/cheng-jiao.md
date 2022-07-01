# 成交

当有订单成交时，推送成交记录

订阅：

```
{
  "op": "SUBSCRIBE",  //订阅
  "topic":  "FILL",   //成交
  "symbol": "BTC_USDT"  // 品种
}
```

推送数据

```
{
  "topic":  "FILL",
  "symbol": "BTC_USDT",
  "data": {
    "id": 9876543210,
    "orderId": 1234567890,
    "symbol": "BTC_USDT",
    "side": "BUY",
    "role":  "TAKER",
    "price": "30000.00",
    "size": "0.1000",
    "fee":  "0.15",
    "feeCoin":  "USDT",
    "timestamp": 1566676132311
  },
  "timestamp":1566691672311
}
```

