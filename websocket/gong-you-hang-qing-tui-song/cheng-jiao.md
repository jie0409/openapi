# 成交

只推送主动成交方，即TAKER方数据

订阅：

```
{
  "op": "SUBSCRIBE",  //订阅
  "topic":  "TRADES",   //深度
  "symbol": "BTC_USDT"  // 品种
}
```

推送数据(每次最多100条)

```
{
  "topic": "TRADES",
  "symbol": "BTC_USDT"
  "data": [
    {
      "symbol": "BTC_USDT",
      "tradeId": "600848671",
      "price": "7962.62",
      "size": "0.0122",
      "direction": "BUY",
      "timestamp": 1566691672311
    },
    {
      "symbol": "BTC_USDT",
      "tradeId": "600848672",
      "price": "7962.62",
      "size": "0.0322",
      "direction": "BUY",
      "timestamp": 1566691672311
    },
    {
      "symbol": "BTC_USDT",
      "tradeId": "600848673",
      "price": "7962.62",
      "size": "0.0132",
      "direction": "BUY",
      "timestamp": 1566691672311
    }
  ]
  "timestamp":1566691672311
}
```

###
