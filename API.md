# 真后端 API 接口说明

## http://host:port/questions POST ![Done](https://img.shields.io/badge/not_ready-green)
**用法**：用于创建一个新的问题，成功时将返回新创建的问题。失败时将返回带有 `"message"` 的 json 字符串以报告问题，错误细节（如有）将在 `"errors"` 中报告。

**头**： Content-Type:application/json

**请求参数**：
+ question: string 类型，必选，放入 payload，是用户输入的问题的内容

*示例*
```payload
{
  "question": "生存还是死亡，这是一个问题。"
}
```

**状态码**：
|状态码|描述|含义|
|:-|:-|:-|
| 201 | Question created. | 成功创建了问题 |
| 400 | Missing argument. | 没有传入 question 参数 |
| 500 | Opps, server not working properly. | 后端出 bug 了 |

**成功时返回示例**：
```result
{
  "id": 22,
  "question": "生存还是死亡，这是一个问题。",
  "create_time": "2023-11-15T04:07:26",
  "answers": []
}
```
**失败时返回示例**：
```result
{
  "errors": {
    "question": "Please tell me your question. Missing required parameter in the JSON body or the post body or the query string"
  },
  "message": "Input payload validation failed"
} # 400
```

## http://host:port/questions/<question_id> GET ![Done](https://img.shields.io/badge/not_ready-green)
**用法**：获取 question_id 指定的问题及其下全部答案，成功时将返回查询到的问题及答案。失败时将返回带有 `"message"` 的 json 字符串以报告问题。

**头**： Content-Type:application/json

**请求参数**：
+ question_id: string 类型，必选，放入 url，是用户希望访问的问题的 id

*示例*
```url-[GET]
http://host:port/questions/23 # 访问 id 为 23 的问题
```

**状态码**：
|状态码|描述|含义|
|:-|:-|:-|
| 200 | Success. | 成功查询并返回了问题 |
| 404 | Question not found. | 没有找到指定 id 的问题 |
| 500 | Opps, server not working properly. | 后端出 bug 了 |

**成功时返回示例**：
```result
{
  "id": 23,
  "question": "生存还是死亡，这是一个问题。",
  "create_time": "2023-11-15T03:54:48.623Z",
  "answers": [
    {
      "id": 19,
      "by": "莎士比亚",
      "answer": "我也不知道。",
      "last_updated": "2023-11-15T03:54:48.623Z",
      "access_token": "7f17f3786af548af4e2abff1f19849a3",
      "question_id": 23
    }
  ]
}
```
**失败时返回示例**：
```result
{
  "message": "Oh, the question fades away. You have requested this URI [/questions/3] but did you mean /questions/<question_id> or /questions ?"
} # 404
```

## http://host:port/questions/<question_id> POST ![Done](https://img.shields.io/badge/not_ready-green)
**用法**：用于创建一个新的回答，成功时以 json 形式返回新创建的问题。失败时将返回带有 `"message"` 的 json 字符串以报告问题，错误细节（如有）将在 `"errors"` 中报告。

**头**： Content-Type:application/json

**请求参数**：
+ question_id: string 类型，必选，放入 url，是用户回答的问题的 id
+ username: string 类型，必选，是用户登陆时输入的用户名，放入 payload，需要进行校验确保不为空
+ password: string 类型，必选，是用户登陆时输入的密码，放入 payload，需要进行校验确保不为空，需要在前端进行 md5 加密后传送
+ anwser_text：string 类型，必选，是用户输入的答案内容，放入 payload，需要进行校验确保不为空

*示例*
```url-[POST]
http://host:port/questions/23 # 回答 id 为 23 的问题
```
```payload
{
  "answer": "我也不知道",
  "username": "神奇用户001",
  "password": "7f17f3786af548af"
}
```

**状态码**：
|状态码|描述|含义|
|:-|:-|:-|
| 201 | Answer created. | 成功创建了答案 |
| 400 | Missing argument. | 没有传入必选参数 |
| 404 | Question not found. | 没有找到指定 id 的问题 |
| 500 | Opps, server not working properly. | 后端出 bug 了 |

**成功时返回示例**：
```result
{
  "id": 30,
  "by": "神奇用户001",
  "answer": "我也不知道",
  "last_updated": "2023-11-15T04:18:38",
  "access_token": "e1cd360fdcb30a521defbfd3f58b8475",
  "question_id": 22
}
```
**失败时返回示例**：
```result
{
  "errors": {
    "answer": "Please tell me your answer. Missing required parameter in the JSON body or the post body or the query string",
    "username": "May I have your name? Missing required parameter in the JSON body or the post body or the query string",
    "password": "Please give me a password encrypted with MD5. Missing required parameter in the JSON body or the post body or the query string"
  },
  "message": "Input payload validation failed"
} # 400
```

## http://host:port/answers/<answers_id> PUT ![Done](https://img.shields.io/badge/not_ready-green)
**用法**：用于更新一个现有的回答，成功时以 json 形式返回修改后的问题。失败时将返回带有 `"message"` 的 json 字符串以报告问题，错误细节（如有）将在 `"errors"` 中报告。

**头**： Content-Type:application/json

**请求参数**：
+ answers_id: string 类型，必选，是用户答案的 id
+ username: string 类型，必选，是用户登陆时输入的用户名，需要进行校验确保不为空
+ password: string 类型，必选，是用户登陆时输入的密码，需要进行校验确保不为空，需要在前端进行 md5 加密后传送
+ anwser_text：string 类型，必选，是用户输入的答案内容，需要进行校验确保不为空

*示例*
```url-[PUT]
http://host:port/answers/30 # 更新 id 为 30 的答案
```
```payload
{
  "answer": "现在我知道了，又要生存，又要死亡。",
  "username": "神奇用户001",
  "password": "7f17f3786af548af"
}
```

**状态码**：
|状态码|描述|含义|
|:-|:-|:-|
| 201 | Answer udpated. | 成功更新了答案 |
| 400 | Missing argument. | 没有传入必选参数 |
| 401 | Unauthorized. | 密码与创建答案时记录的不一致 |
| 404 | Answer is missing. | 没有找到指定 id 的答案 |
| 500 | Opps, server not working properly. | 后端出 bug 了 |

**成功时返回示例**：
```result
{
  "id": 30,
  "by": "神奇用户001",
  "answer": "现在我知道了，又要生存，又要死亡。",
  "last_updated": "2023-11-15T04:24:16",
  "access_token": "e1cd360fdcb30a521defbfd3f58b8475",
  "question_id": 22
}
```
**失败时返回示例**：
```result
{
  "message": "Password mismatch."
} # 401
```
