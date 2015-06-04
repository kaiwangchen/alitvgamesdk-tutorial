## HTTP API

若启用服务端附加流程，平台服务端会向商店/游戏服务端发送 HTTP 回调通知。

* 通知参数 (HTTP GET 请求的 query string 参数)

| 参数名 | 类型 | 可选性 | 含义
|--------|------|----------------|----------------
| app_order_id | String | 必选 | 透传的流水号，即 payFromServer 的 orderId 参数 |
| coin_order_id	| long  | 必选 | 数娱宝点的消费流水号
| consume_amount | long | 必选 | 总消费金额（单位 人民币分），包含信用消费金额
| credit_amount | long | 若玩家使用信用消费（又称“先玩后附”），则必有此字段 | 信用消费金额（单位 人民币分）
| ts | long | 必选 | 时间戳(按毫秒)
| is_success | String | 必选 | 消费成功失败
| error_code | String | 若 is_success 为 F，则必有此字段 | 失败原因
| sign | String | 必选 | 宝点签名，详见附录[签名算法](../appendix/sign.md)

* 响应参数 (HTTP 响应 body 中的 json 字段）

| 参数名 | 类型 | 可选性 | 含义
|--------|------|----------------|----------------
| is_success | String | 必选 | 是(`T`)否(`F`)受理该请求
| app_order_id | String | 必选 | 从通知参数中复制过来 |
| coin_order_id	| long  | 必选 | 从通知参数中复制过来
| error_code | String | is_success 为 F 时必选此字段 | 错误码
| msg | String | is_success 为 F 时必选此字段 | 错误描述
