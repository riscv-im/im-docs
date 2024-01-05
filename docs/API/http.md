## `/register`

用户注册

### POST

### 请求体

样例1

```json
{
    "name": "alice",
    "password": 123,
    "email": "alice@163.com",
    "security_code": 123456,
    "need_send": False
}
```

样例2

```json
{
    "email": "alice@163.com",
    "need_send" True
}
```

字段含义

| 字段          | 类型    | 含义                                                         |
| ------------- | ------- | ------------------------------------------------------------ |
| name          | string  | 用户名                                                       |
| password      | string  | 密码                                                         |
| email         | email   | 邮箱                                                         |
| security_code | string  | 验证码                                                       |
| need_send     | boolean | 是否需要发送验证码，True对应发送验证码请求，False对应注册请求 |

### 成功响应

状态码：200

样例1（need_send = False）

```json
{
    "code": 0,
    "info": "Succeed",
    "token": generate_jwt_token(alice),
    "ws_url": "ws/user/1/"
}
```

data字段

| 字段   | 类型   | 含义    |
| ------ | ------ | ------- |
| token  | string | token   |
| ws_url | string | 跳转url |



样例2（need_send = True）

```json
{
    "code": 0,
    "info" : "Succeed"
}
```

### 错误响应

| 状态码 | 错误码 | 错误提醒                 |
| ------ | ------ | ------------------------ |
| 400    | -2     | Please verify your email |
| 400    | -1     | Wrong verify code        |
| 400    | -2     | Username duplicate       |
| 400    | -2     | Email already exists     |



## `/login`

用户登录

### POST

### 请求体

样例1（用户名密码登录）

```json
{
    "name": "alice",
    "password": 123
}
```

字段含义

| 字段     | 类型   | 含义   |
| -------- | ------ | ------ |
| name     | string | 用户名 |
| password | string | 密码   |



样例2（邮箱登录）

```json
{
    "email": "alice@163.com",
    “security_code”: 123456,
    "need_send" False
}
```

字段含义

| 字段          | 类型    | 含义                                                         |
| ------------- | ------- | ------------------------------------------------------------ |
| email         | email   | 邮箱                                                         |
| security_code | string  | 验证码                                                       |
| need_send     | boolean | 是否需要发送验证码，True对应发送验证码请求，False对应登录请求 |

### 成功响应

状态码：200

样例

```json
{
    "code": 0,
    "info": "Succeed",
    "token": generate_jwt_token(alice),
    "ws_url": "ws/user/1/"
}
```

data字段

| 字段   | 类型   | 含义    |
| ------ | ------ | ------- |
| token  | string | token   |
| ws_url | string | 跳转url |

### 错误响应

| 状态码 | 错误码 | 错误提醒                 |
| ------ | ------ | ------------------------ |
| 400    | -2     | Username not found       |
| 400    | -2     | Wrong Password           |
| 400    | -2     | Please verify your email |
| 400    | -1     | Wrong verify code        |



## `/change_name`

更改用户名

### POST

### 请求体

样例

```json
{
    "id": 1,
    "new_name": bob
}
```

字段含义

| 字段     | 类型   | 含义                 |
| -------- | ------ | -------------------- |
| id       | int    | 用户id，用于区分用户 |
| new_name | string | 用户名               |

### 成功响应

状态码：200

样例

```json
{
    "code": 0,
    "info": "Succeed"
}
```



### 错误响应

| 状态码 | 错误码 | 错误提醒               |
| ------ | ------ | ---------------------- |
| 400    | -2     | Invalid or expired JWT |
| 400    | -2     | Username duplicate     |



## `/change_password`

更改用户名

### POST

### 请求体

样例

```json
{
    "id": 1,
    "old_password": 123456,
    "new_name": 12345678
}
```

字段含义

| 字段         | 类型   | 含义                 |
| ------------ | ------ | -------------------- |
| id           | int    | 用户id，用于区分用户 |
| old_password | string | 旧密码               |
| new_password | string | 新密码               |

### 成功响应

状态码：200

样例

```json
{
    "code": 0,
    "info": "Succeed"
}
```



### 错误响应

| 状态码 | 错误码 | 错误提醒               |
| ------ | ------ | ---------------------- |
| 400    | -2     | Invalid or expired JWT |
| 400    | -2     | Wrong password         |



## `/change_email`

更改用户名

### POST

### 请求体

样例

```json
{
    "id": 1,
    "new_email": "alice@126.com", 
    "security_code": 123456
}
```

字段含义

| 字段          | 类型   | 含义                 |
| ------------- | ------ | -------------------- |
| id            | int    | 用户id，用于区分用户 |
| new_email     | string | 新邮箱               |
| security_code | string | 验证码               |

### 成功响应

状态码：200

样例

```json
{
    "code": 0,
    "info": "Succeed"
}
```



### 错误响应

| 状态码 | 错误码 | 错误提醒                 |
| ------ | ------ | ------------------------ |
| 400    | -2     | Invalid or expired JWT   |
| 400    | -2     | Please verify your email |
| 400    | -1     | Wrong verify code        |



## `/change_image`

更改用户名

### POST

### 请求体

样例

```json
{
    "id": 1,
    "avatar": avatar
}
```

字段含义

| 字段   | 类型 | 含义                 |
| ------ | ---- | -------------------- |
| id     | int  | 用户id，用于区分用户 |
| avatar | 图片 | 更改后的头像         |

### 成功响应

状态码：200

样例

```json
{
    "code": 0,
    "info": "Succeed"
    "url": user.image.url
}
```

data字段

| 字段 | 类型   | 含义    |
| ---- | ------ | ------- |
| url  | string | 图片url |



### 错误响应

| 状态码 | 错误码 | 错误提醒                         |
| ------ | ------ | -------------------------------- |
| 400    | -2     | Invalid or expired JWT           |
| 400    | -1     | Missing or error type of [image] |
| 400    | -1     | Invalid type of [image]          |





## `/upload_image`

群聊上传图片

### POST

### 请求体

样例

```json
{
    "id": 1,
    "avatar": avatar
}
```

字段含义

| 字段   | 类型 | 含义                     |
| ------ | ---- | ------------------------ |
| id     | int  | 群聊id，用于区分不同群聊 |
| avatar | 图片 | 群聊中发送的图片消息     |

### 成功响应

状态码：200

样例

```json
{
    "code": 0,
    "info": "Succeed"
    "url": user.image.url
}
```

data字段

| 字段 | 类型   | 含义    |
| ---- | ------ | ------- |
| url  | string | 图片url |



### 错误响应

| 状态码 | 错误码 | 错误提醒                         |
| ------ | ------ | -------------------------------- |
| 400    | -2     | Invalid or expired JWT           |
| 400    | -1     | Missing or error type of [image] |
| 400    | -1     | Invalid type of [image]          |



## `/upload_expression`

群聊上传表情

### POST

### 请求体

样例

```json
{
    "id": 1,
    "expression": avatar
}
```

字段含义

| 字段   | 类型 | 含义                     |
| ------ | ---- | ------------------------ |
| id     | int  | 群聊id，用于区分不同群聊 |
| avatar | 表情 | 群聊中发送的表情消息     |

### 成功响应

状态码：200

样例

```json
{
    "code": 0,
    "info": "Succeed"
    "url": user.image.url
}
```

data字段

| 字段 | 类型   | 含义    |
| ---- | ------ | ------- |
| url  | string | 表情url |



### 错误响应

| 状态码 | 错误码 | 错误提醒                              |
| ------ | ------ | ------------------------------------- |
| 400    | -2     | Invalid or expired JWT                |
| 400    | -1     | Missing or error type of [expression] |
| 400    | -1     | Invalid type of [expression]          |



## `/upload_file`

群聊上传文件

### POST

### 请求体

样例

```json
{
    "id": 1,
    "file": file
}
```

字段含义

| 字段 | 类型 | 含义                     |
| ---- | ---- | ------------------------ |
| id   | int  | 群聊id，用于区分不同群聊 |
| file | 文件 | 群聊中发送的文件消息     |

### 成功响应

状态码：200

样例

```json
{
    "code": 0,
    "info": "Succeed"
    "url": user.image.url
}
```

data字段

| 字段 | 类型   | 含义    |
| ---- | ------ | ------- |
| url  | string | 文件url |



### 错误响应

| 状态码 | 错误码 | 错误提醒                        |
| ------ | ------ | ------------------------------- |
| 400    | -2     | Invalid or expired JWT          |
| 400    | -1     | Missing or error type of [file] |





## `/upload_voice`

群聊上传表情

### POST

### 请求体

样例

```json
{
    "id": 1,
    "voice": voice
}
```

字段含义

| 字段  | 类型 | 含义                     |
| ----- | ---- | ------------------------ |
| id    | int  | 群聊id，用于区分不同群聊 |
| voice | 语音 | 群聊中发送的语音消息     |

### 成功响应

状态码：200

样例

```json
{
    "code": 0,
    "info": "Succeed"
    "url": user.image.url
}
```

data字段

| 字段 | 类型   | 含义    |
| ---- | ------ | ------- |
| url  | string | 语音url |



### 错误响应

| 状态码 | 错误码 | 错误提醒                         |
| ------ | ------ | -------------------------------- |
| 400    | -2     | Invalid or expired JWT           |
| 400    | -1     | Missing or error type of [voice] |