# Funny-Cat

Funny Cat is a project for collecting answers from folks of your choice. Create a question and share it with your family, friends, chatgroup or whoever you want. Everyone with the link could join the discussion! However, like every topic in the real world, people will shift their focus away after some time. The data server will delete your question **FOREVER** after 14 days. So, be sure to check the topic before it fades away.

---
## Usecase
#### Create A Question
+ A user can create a question.

#### Access A Question
+ A user can use a search bar on the webpage to navigate to a certain question
+ Alternatively, the webpage will navigate the user to the question if they first created the question
+ Anyone who knows the question link can see all the answers 

#### Answer A Question
+ Anyone who knows the question link can answer it.
+ The user will need to set a username and password for themselves if they want to add an answer
+ The website will store the username and password locally once the user logged in.

#### Update Your Answer
+ Once a user has submitted their answer, they can use the same username and password to update their previous answer

---
##### 模拟后端接口说明
**Read [The README file in ./data](./data/README.md)**

##### 真后端接口说明
**Read [The API file in ./](./API.md)**

##### 创建问题
> 1. 用户点击 Ask question 按钮，弹出弹窗
> 2. 用户在弹窗中填写问题
> 3. 用户点击 Ask 按钮
> 4. 前端向后端发送用户的问题（可能发生：ERROR_1）
> 5. 后端接收到用户的问题后返回数据
> 6. 前端在接收到后端返回的数据之后跳转到问题页面
> 7. 前端根据后端返回的数据渲染问题页面的内容（可能发生： ALT_1, ERROR_2）

##### 访问问题
> 1. 用户在搜索栏中输入问题 id
> 2. 用户点击搜索按钮或者在搜索栏中按下回车键
> 3. 前端校验用户的输入是否为能够转换为 int 的数字
> 4. 前端向后端发送用户输入的数字拉取问题内容（可能发生：ERROR_1）
> 5. 前端在接收到后端返回的数据之后跳转到问题页面
> 6. 前端根据后端返回的数据渲染问题页面的内容（可能发生： ALT_1, ERROR_2）

##### login 组件预备
> 1. 在初始化 login 组件时尝试获取 localStorage 中的用户名和密码 <br>
> 2a. 如果获取到数据，将 login 组件更新为登陆后的状态 <br>
> 2b. 如果没有获取到数据，将 login 组件展示为登陆前的状态

##### 登录
> 1. 用户在用户名栏输入用户名
> 2. 用户在用户名栏按下回车时，网页焦点移动到密码栏
> 3. 用户在密码栏输入密码 <br>
> 4a. 用户在密码栏中按下回车时开始验证登录 <br>
> 4b. 用户点击登录按钮时开始验证登录
> 5. 前端将用户输入的密码使用 md5 加密
> 6. 前端将加密后的 md5 密码和用户名一起保存在本地 localStorage 中
> 7. 前端将用户的用户名和经过 md5 加密的密码进行字符串拼接后使用 md5 进行二次加密
> 8. 前端遍历当前问题下所有的问题答案的 access_token 属性比对 <br>
> 9a. 若存在匹配，证明当前用户回答过问题，登陆后的按钮提示更新答案 <br>
> 9b. 若不存在匹配，证明当前用户为新用户，登陆后的按钮提示回答问题
> 10. 将 login 组件更新为登陆后的状态

##### 登出
> 1. 用户点击登出按钮
> 2. 清空保存在本地的 localStorage 中的用户名和密码
> 3. 将 login 组件更新为登陆前的状态

##### 回答问题
> 1. 用户在登陆状态点击回答问题的按钮
> 2. 前端弹出输入窗口
> 3. 用户在输入窗口中完成答案输入
> 4. 用户点击提交答案的按钮
> 5. 前端取出保存在 localStorage 中的用户名和密码
> 6. 前端将当前问题的 id、 用户名、密码和问题的答案发送给后端（可能发生：ERROR_1）
> 7. 后端返回添加成功的问题的信息（可能发生： ALT_1, ERROR_2）
> 8. 前端根据后端返回的数据，将添加成功的答案渲染在页面上 

##### 更新答案
> 1. 用户在登陆状态点击更新问题的按钮
> 2. 前端弹出输入窗口
> 3. 前端在输入窗口中提前填充用户上次的问题答案
> 4. 用户在输入窗口中完成答案修改
> 5. 用户点击提交答案的按钮
> 6. 前端取出保存在 localStorage 中的用户名和密码
> 7. 前端将当前问题的 id、 用户名、密码和问题的答案发送给后端（可能发生：ERROR_1）
> 8. 后端返回修改后的问题的信息（可能发生： ALT_1, ERROR_2）
> 9. 前端根据后端返回的数据，将添加成功的答案渲染在页面上 

##### ERROR_1
前端向后端请求数据时因网络问题无法获得反馈
> 1. 弹出窗口提示用户网络暂不可达，请稍后再试
> 2. 停止在当前页面

##### ERROR_2
后端发来的数据和文档记录的不一致，前端无法正确解析并显示
> 1. 弹出窗口提示用户服务遇到错误
> 2. 停止在当前页面

##### ALT_1
后端返回了 200 段以外的状态码
> 1. 弹出窗口向用户展示状态码以及报错信息
