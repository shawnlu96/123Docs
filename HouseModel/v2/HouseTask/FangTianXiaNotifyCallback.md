﻿功能介绍
========

**注：此接口需要由客户方实现,
发送请求时所有的参数由123生成并发给客户方。**

将3D房源推送给房天下后，回调客户的接口，反馈推送结果。

 

URI
===

**由客户提供**

 

Method
======

POST with form

 

身份认证
========

加固接口的签名验证。\可选\

**注：客户方是否实现此验证不影响接口流程，如果强调安全性，可以实现此验证。**

 

请求头
======

| 参数         | 可空 | 参数类型 | 描述 |
|--------------|------|----------|-----|
| Content-Type | No   | String   | 值应为：application/x-www-form-urlencoded  |
| timestamp    | Yes  | Long     | 10进制unix时间戳。  |
| sign         | Yes  | String   | 根据加固接口的签名验证规则生成出来的签名。 |

 

请求参数
========

| 参数      | 可空 | 参数类型     | 描述                                        |
|-----------|------|--------------|---------------------------------------------|
| houseId   | No   | String (64)  | 客户内网的houseId                           |
| houseType | No   | String (32)  | 客户房源类型，值为客户内网的房源类型的值    |
| packageId | No   | String (128) | 房源数据包ID                                |
| status    | No   | Int          | 1：通知成功，2：通知失败，3：通知时发生错误 |
| payload   | No   | String (max) | 通知时房天下返回的具体内容                  |

 

正确响应
========

HTTP Code返回200即可。