# 账户

{% swagger method="get" path="" baseUrl="/api/v1/account/balances" summary="查询账户资产" %}
{% swagger-description %}
权限：读取
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{ 
  "data": {
    "balances": [
      {
        "coin": "BTC",
        "free": "0.9000000",
        "frozen": "0.00000000"
      },
      {
        "coin": "USDT",
        "free": "100.00000000",
        "frozen": "900.00000000"
      }
    ]
  },
  "result": true,
  "timestamp": 1566691672311
}
```
{% endswagger-response %}
{% endswagger %}
