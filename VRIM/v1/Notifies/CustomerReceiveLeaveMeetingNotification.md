# 功能介绍

**客户提供接口接收参与者离开会议的消息，用于释放对某用户的锁定来继续接单以及记录信息**

该接口会在有人离开会议时被调用。通过isFirstOne来区分该用户是否为会议的发起者，在这里即为消费者。isTimeOut来区分是主动断开还是因心跳超时断开

# URI

**由客户方提供**


# Method

**Post with Form**


# 身份认证

[加固接口的签名验证](../Agreement/StrongValidation.md)


# 请求头

| 参数         | 可空 | 参数类型 | 描述                                                         |
| ------------ | ---- | -------- | ------------------------------------------------------------ |
| Content-Type | No   | String   | x-www-form-urlencoded                                        |
| sign         | Yes  | String   | 根据[加固接口的签名验证](../Agreement/StrongValidation.md)规则生成出来的签名。 |


# 请求参数

| 字段名     | 可空 | 数据类型    | 描述                       |
| ---------- | ---- | ----------- | -------------------------- |
| packageId  | No   | string(128) | 数据包id                   |
| meetingId  | No   | int         | 123定义的会议id            |
| exitTime   | No   | DateTime    | 参与者的离开时间           |
| user       | No   | string(max) | 该参与者的用户id           |
| isTimeOut  | No   | bool        | 是否因为心跳超时导致的退出 |
| isFirstOne | No   | bool        | 加入的是否是第一个用户     |
| noResponse | Yes   | bool       | 呼叫方是否等等60秒后仍无人接听 |
| meetingStatus | No   | int      | 0:会议未开始；1：进行中；2：已结束；3：无人接听；4：呼叫方主动取消 |


# 正确响应

| 字段名  | 可空 | 数据类型 | 描述                                         |
| ------- | ---- | -------- | -------------------------------------------- |
| state   | No   | Int      | [返回状态](../Agreement/APIResponseState.md) |
| payload | No   | String   | 客户方想返回的msg，如果没有可为空            |

## Schema

```json
{
    "state": 200,
    "payload":  "Success"
}
```

# 错误响应

| 字段名  | 可空 | 数据类型 | 描述                                         |
| ------- | ---- | -------- | -------------------------------------------- |
| state   | No   | Int      | [返回状态](../Agreement/APIResponseState.md) |
| payload | No   | String   | 错误代码或Message                            |

## Schema 

``` json
{
    "state": 401,
    "payload": "Unauthorized"
}
```

``` json
{
    "state": 403,
    "payload": "InvalidXXXXXX"
}
```

``` json
{
    "state": 500,
    "payload": "InnerServerError -> detail xxxxxx"
}
```
