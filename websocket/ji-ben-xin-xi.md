# 基本信息

### 连接管理

私有流和公有流分不同地址订阅

订阅私有流地址需要验证，公有流数据不需要验证

#### **验证信息**

在订阅私有流数据时，需要在 query 里携带鉴权参数，格式如下:

* key：用户的api Key
* time：毫秒时间戳
* signature：time + "websocket\_auth" 拼接之后进行HMAC SHA256计算

```
wss://api.pionex.com/ws?key=xxx-xx-xx&time=1566691672311&signature=4F65x5A2bLyMWVQj3Aqp+B4w+ivaA7n5Oi2SuYtCJ9o=
```

### 签名步骤

1. 获取当前的毫秒时间戳 timestamp
2. 将query参数表示为键值对形式：key=value（参与签名的value值不得做URL Encode）
3. 将键值对按key的ASCII码升序排序并用&拼接 （包括 timestamp ）
4. 将上述结果使用？拼接到 path 后面，生成 path\_url
5. 拼接 method + path\_url（不加其他分隔符，直接拼接）
6. POST和DELETE接口的request body参数，参与签名，接在4后面，若无 body 请求跳过此步
7. 使用SecretKey对拼接后的结果进行HMAC SHA256运算，并将将结果转换为16进制
8. 将得到的结果赋给signature并添加到Header参数后发出请求

示例：

用户的私钥和请求时间为：

```
key:  OElNn5D_Frnf5MR0ChjYdG7PunK0AOgHTvevwzWS
secret： NFqv4MB3hB0SOiEsJNDP9e0jDdKPWbDqS_Z1dbU4

timestamp： 1655896754515
```

建立私有数据WebSocket 链接的原始请求是：

```
WSS://api.pionex.com/ws
```

第一步，获取当前时间戳

```
timestamp=1655896754515
```

第二步，将 query 参数表示为键值对形式：key=value

```
key=OElNn5D_Frnf5MR0ChjYdG7PunK0AOgHTvevwzWS
timestamp=1655896754515
```

第三步，将键值对按key的ASCII码升序排序，并使用 & 拼接

```
key=OElNn5D_Frnf5MR0ChjYdG7PunK0AOgHTvevwzWS&timestamp=1655896754515
```

第四步，将结果拼接到请求 path 后面，生成 path\_url

```
/ws?key=OElNn5D_Frnf5MR0ChjYdG7PunK0AOgHTvevwzWS&timestamp=1655896754515
```

第五步，将上述结果后面拼接字符串 websocket\_auth

```
/ws?key=OElNn5D_Frnf5MR0ChjYdG7PunK0AOgHTvevwzWS&timestamp=1655896754515websocket_auth
```

第六步，使用SecretKey对拼接后的结果进行HMAC SHA256运算，并将将结果转换为16进制

```
3e901247350e744353f4a7a479fd67181184a627b119352ec1b7a432925e772c
```

第七步，将得到的结果赋给signature并添加到query参数的后面发起建立链接请求

```
wss://api.pionex.com/ws?key=OElNn5D_Frnf5MR0ChjYdG7PunK0AOgHTvevwzWS&timestamp=1655896754515websocket_auth&signature=3e901247350e744353f4a7a479fd67181184a627b119352ec1b7a432925e772c
```



### **订阅**

发送JSON请求来进行订阅

```
{"op": "SUBSCRIBE", "topic": "ORDER", "symbol": "BTC_USDT"}
```

结果

```
{"type": "SUBSCRIBED", "topic": "ORDER", "symbol": "BTC_USDT"}
```

**取消订阅**

发送JSON请求来进行取消订阅

```
{"op": "UNSUBSCRIBE", "topic": "ORDER", "symbol": "BTC_USDT"}
```

结果

```
{"type": "UNSUBSCRIBED", "topic": "ORDER", "symbol": "BTC_USDT"}
```

### **心跳**

服务器每隔 60 秒会向已建立连接的客户端发送一次PING心跳，格式为：

```
{"op": "PING", "timestamp": 1566691672311}
```

客户端收到服务器心跳后，回复PONG消息，PONG消息的时间戳可以与PING消息不一致，也不必须要一一对应，以文本格式回复（不需要压缩），消息格式如下，其中timestamp 为当前的时间戳，单位毫秒

```
{"op": "PONG", "timestamp": 1566691672311}
```

客户端必须发送最新的时间戳值来保持连接。如果服务器连续3次没有收到对应时间戳的PONG消息，则会在第4次PING消息的时刻断开连接，并向客户端发送断开消息：

```
{"op": "CLOSE", "timestamp": 1566691672311}
```

### 错误码

\_INVALID\_OP

TRADE\_INVALID\_TOPIC

TRADE\_INVALID\_SYMBOL
