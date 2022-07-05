# 撤销指定订单

权限： 交易

权重： 1

请求路径：

```
DELETE /api/v1/trade/order
```

请求参数：

| **字段名** | **类型** | **是否必须** | **描述**     |
| ------- | ------ | -------- | ---------- |
| symbol  | string | 是        | 交易市场       |
| orderId | number | 是        | 需要撤销订单的订单号 |

返回参数：无

错误码：

* TRADE\_INVALID\_SYMBOL 无效品种
* TRADE\_PARAMETER\_ERROR 参数错误
* TRADE\_OPERATION\_DENIED 禁止操作
* TRADE\_SYMBOL\_MAINTAIN 品种维护

请求示例：

```
DELETE https://{site}/api/v1/trade/order
{
  "symbol":         "BTC_USDT",
  "orderId":        1234567890
}
```

响应示例：

```
{ 
  "result": true,
  "timestamp": 1566691672311
}
```
