# 查询余额

权限： 读取

权重： 1

请求路径：

```
GET /api/v1/account/balances
```

请求参数：无

返回参数：

| **字段名**  |        | **类型** | **描述**          |
| -------- | ------ | ------ | --------------- |
| balances |        | array  | 账户余额集合，按照币种升序排列 |
|          | coin   | string | 币种              |
|          | free   | string | 可用余额，8位小数       |
|          | frozen | string | 冻结余额，8位小数       |

注意：余额为直接截取小数点后前8位

错误码：

请求示例：

```
GET https://{site}/api/v1/account/balances
```

响应示例：

```
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

####
