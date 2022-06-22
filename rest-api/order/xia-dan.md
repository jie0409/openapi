---
description: 下单
---

# 下单

{% swagger method="post" path="" baseUrl="/api/v1/trade/order" summary="下单" %}
{% swagger-description %}
下单

从下单

下单
{% endswagger-description %}

{% swagger-parameter in="body" name="symbol" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="clientOrderId" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="size" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="IOC" type="Boolean" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{ 
  "data": {
    "orderId": 1234567890,
    "clientOrderId":  "9e3d93d6-e9a4-465a-a39c-2e48568fe194"
  },
  "result": true,
  "timestamp": 1566691672311
}
```
{% endswagger-response %}
{% endswagger %}
