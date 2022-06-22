# 查询单个订单

{% swagger method="get" path="" baseUrl="/api/v1/trade/order" summary="查询订单" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="symbol" required="true" %}
交易市场
{% endswagger-parameter %}

{% swagger-parameter in="query" required="true" name="orderId" type="Number" %}
订单号
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "data": {
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
    "IOC":  false,
    "status": "OPEN",
    "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194",
    "source": "API",
    "createdTime": 1566676132311,
    "updatedTime": 1566676132311
  },
  "result": true,
  "timestamp": 1566691672311
}
```
{% endswagger-response %}
{% endswagger %}
