# 订单

{% swagger method="post" path="" baseUrl="/api/v1/trade/order" summary="下单" %}
{% swagger-description %}
权限：交易
{% endswagger-description %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
交易市场
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" type="string" required="true" %}
 BUY or SELL
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}

{% endswagger-parameter %}
{% endswagger %}
