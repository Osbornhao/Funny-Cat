# 真后端 API 接口说明

（文档随开发进程更新中...）
本项目中除特殊说明，接口返回时一定携带一个状态码和一个响应体。
状态码为200段（如 200，201，202）时，响应体内容为来自服务端的数据，将以 json 的形式返回；
状态码不为200段时，响应体内容为来自服务端的错误信息，以 string 形式返回。

## http://host:port/create POST ![Not working](https://img.shields.io/badge/not_ready-red)
**用法**：用于创建一个新的问题
**请求参数**：
+ question_text: string 类型，必选，是用户输入的问题的内容
**成功例**：
```
200, {"id":"<question_id>"}
```
**失败例**：
```
500, "The database has run out of space, plz wait for other questions fade away."
```

## http://host:port/<question_id> GET ![Not working](https://img.shields.io/badge/not_ready-red)
**用法**：用于访问指定的问题 id 对应的问题页面
**请求参数**：无
**成功例**：
```
200, {
    "question":"<question_text>",
    "create_time":"<create_time>",
    "anwsers":[
        {
            "by":"<user_name>",
            "anwser":"<anwser_text>",
            "last_updated":"<last_updated_time>",
        }
    ]
}
```
**失败例**：
```
404, "Hey, there's no such question."
```

## http://host:port/<question_id>/anwser POST ![Not working](https://img.shields.io/badge/not_ready-red)
**用法**：用于创建一个新的回答，如果成功执行则需要用重新获取问题页面中的答案以完成显示。
**请求参数**：
+ question_id: string 类型，必选，是用户回答的问题的 id
+ username: string 类型，必选，是用户登陆时输入的用户名，需要进行校验确保不为空
+ password: string 类型，必选，是用户登陆时输入的密码，需要进行校验确保不为空，需要在前端进行 md5 加密后传送
+ anwser_text：string 类型，必选，是用户输入的答案内容，需要进行校验确保不为空
**成功例**：
```
205, {}
```
**失败例**：
```
418, "I'm a teapot." // 只是为了展示失败时的状态码有多种多样的可能性
```

## http://host:port/<question_id>/update PUT ![Not working](https://img.shields.io/badge/not_ready-red)
**用法**：用于更新一个现有的回答，如果成功执行则需要用重新获取问题页面中的答案以完成显示。
**请求参数**：
+ question_id: string 类型，必选，是用户回答的问题的 id
+ username: string 类型，必选，是用户登陆时输入的用户名，需要进行校验确保不为空
+ password: string 类型，必选，是用户登陆时输入的密码，需要进行校验确保不为空，需要在前端进行 md5 加密后传送
+ anwser_text：string 类型，必选，是用户输入的答案内容，需要进行校验确保不为空
**成功例**：
```
205, {}
```
**失败例**：
```
409, "What? A time traveler? Your update has a earlier timestamp than the previous one."
```
