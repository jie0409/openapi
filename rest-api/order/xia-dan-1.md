---
description: 下单
---

# 下单1

类型：PRIVATE

权限：TRADE

{% swagger method="post" path="" baseUrl="/api/v1/trade/order" summary="Create a new order" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" name="symbol" required="true" type="string" %}
交易市场
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" required="true" type="string" %}
方向：BUY or SELL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" required="true" type="string" %}
类型：LIMIT or MARKET
{% endswagger-parameter %}

{% swagger-parameter in="body" name="clientOrderId" type="string" %}
客户端id，由大小写字母、数字、中横线组成，最大64位
{% endswagger-parameter %}

{% swagger-parameter in="body" name="size" type="string" %}
数量，限价单和市价卖单必填
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="string" %}
价格，限价单必填
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" %}
市价买单花费,市价必填
{% endswagger-parameter %}

{% swagger-parameter in="body" name="IOC" type="boolean" %}

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


{% swagger-parameter in="body" name="symbol" required="true" type="string" %} 交易市场 {% endswagger-parameter %}

{% swagger-parameter in="body" name="side" required="true" type="string" %} 方向：BUY or SELL {% endswagger-parameter %}

{% swagger-parameter in="body" name="type" required="true" type="string" %} 类型：LIMIT or MARKET {% endswagger-parameter %}

{% swagger-parameter in="body" name="clientOrderId" type="string" %} 客户端id，由大小写字母、数字、中横线组成，最大64位 {% endswagger-parameter %}
