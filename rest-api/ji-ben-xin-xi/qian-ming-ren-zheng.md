# 签名认证

### 签名说明

API 请求在通过 internet 传输的过程中极有可能被篡改，为了确保请求未被更改，除公共接口（基础信息，行情数据等）外的私有接口（私有接口均在接口文档中标注了所需要的权限，如果未标注所需权限均为公共接口）均必须使用您的 API Key 做签名认证，以校验参数或参数值在传输途中是否发生了更改。

每一个API Key需要有适当的权限才能访问相应的接口，每个新创建的API Key都需要分配权限。在使用接口前，请查看每个接口的权限类型，并确认你的API Key有相应的权限。

### 签名步骤

1. 获取当前的毫秒时间戳 timestamp
2. 将query参数表示为键值对形式：key=value（参与签名的value值不得做URL Encode）
3. 将键值对按key的ASCII码升序排序并用&拼接 （包括 timestamp ）
4. 将上述结果使用？拼接到 path 后面，生成 path\_url
5. 拼接 method + path\_url（不加其他分隔符，直接拼接）
6. POST和DELETE接口的request body参数，参与签名，接在4后面，若无 body 请求跳过此步
7. 使用SecretKey对拼接后的结果进行HMAC SHA256运算，并将二进制结果进行Base64编码得到结果
8. 将得到的结果赋给signature并添加到Header参数后发出请求



示例：

用户的私钥和请求时间为：

```
Secret： NFqv4MB3hB0SOiEsJNDP9e0jDdKPWbDqS_Z1dbU4

timestamp： 1655896754515
```

查询订单列表的原始请求是：

```
GET /api/v1/trade/allOrders?symbol=BTC_USDT&limit=1
```

第一步，获取当前时间戳

```
timestamp=1655896754515
```

第二步，将 query 参数表示为键值对形式：key=value

```
symbol=BTC_USDT
limit=1
timestamp=1655896754515
```

第三步，将键值对按key的ASCII码升序排序，并使用 & 拼接

```
limit=1&symbol=BTC_USDT&timestamp=1655896754515
```

第四步，将结果拼接到请求 path 后面，生成 path\_url

```
/api/v1/trade/allOrders?limit=1&symbol=BTC_USDT&timestamp=1655896754515
```

第五步，拼接 method + path\_url（不加其他分隔符，直接拼接）

```
GET/api/v1/trade/allOrders?limit=1&symbol=BTC_USDT&timestamp=1655896754515
```

第五步，POST和DELETE跳过的request body参数，参与签名，接在4后面，若无 body 请求跳过此步

```
b'GET/api/v1/trade/allOrders?limit=1&symbol=BTC_USDT&timestamp=1655896754515{"symbol": "BTC_USDT"}'
```

第六步，使用SecretKey对拼接后的结果进行HMAC SHA256运算，并将二进制结果进行Base64编码得到结果

```
b'7IPSHhI3y+fgFy95wOOkdByG9rIBunYvIRSb8ZVRm+E='    //加密结果
```
