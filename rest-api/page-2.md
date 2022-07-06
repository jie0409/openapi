# API 基本信息

### 请求规范

* 所有 PRIVATE 类型的请求，必须在 query string 中添加 timestamp 参数，在 header 中添加 PIONEX-KEY 和 PIONEX-SIGNATURE 参数

| **参数**           | **类型** | **类型** | **描述**                                                                                                                     |
| ---------------- | ------ | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| timestamp        | query  | number | <p>请求时间戳，毫秒，</p><p>如果是20000毫秒之前，或者“未来”发出的请求，都会被认为无效。</p>                                                                   |
| PIONEX-KEY       | header | string | 账户的 API Key                                                                                                                |
| PIONEX-SIGNATURE | header | string | 签名，GET 请求会由 method + path\_url + query + timestamp生成，POST 和 DELETE请求用 method + path + query + timestamp + body生成，计算方法见验签部分 |

* GET 方法的接口，参数在 query string 中发送
* POST 和 DELETE 方法的接口，参数在 request body 中发送，content-type 为 application/json
* 所有number类型的输入参数，传入0值等同于不传

### 返回格式

* 所有restful接口的响应都是JSON格式，并包含以下字段

| **字段**    | **类型**  | **描述**             |
| --------- | ------- | ------------------ |
| result    | boolean | 请求成功为true，否则为false |
| timestamp | number  | 请求响应的服务器时间戳（毫秒）    |

* 成功的响应会包含业务数据

| **字段** | **类型** | **描述** |
| ------ | ------ | ------ |
| data   | object | 业务数据对象 |

示例：

```
{
  "result": true,
  "data": {
    "orderId":  123456789
  },
  "timestamp":  1566691672311
}
```

* 错误的响应会包含错误码和错误描述

| **字段**  | **类型** | **描述**      |
| ------- | ------ | ----------- |
| code    | string | 错误码（见下文中描述） |
| message | string | 错误描述        |

示例：

```
{
  "result": false,
  "code": "TRADE_INVAILD_SYMBOL",
  "message":  "Invalid symbol",
  "timestamp":  1566691672311
}
```

###
