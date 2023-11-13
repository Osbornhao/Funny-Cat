# 关于 data 这个文件夹的 FAQ

## 这是什么？
这是一个伪装成后端的 json 文件，需要配合 json-server 使用。这可以让前端开发可以和后端一起开始工作，不必等待真正的后端上线。这种使用假后端的方式可以极大的提升开发速度。但是代价是开发流程上的变更，前端开发需要和后端开发在开始工作之前沟通并确定数据的传递形式，**以文档形式记录，并同步给整个开发组**（悲剧常在这一步开端），在开发结束之后，前端和后端需要联合调试，确保数据能准确的从后端发出并被前端正确接收（悲剧常在这一步进入高潮）。

## json 是什么？
Json 是一种轻量级资料交换格式。其内容由属性和值所组成，因此也有易于阅读和处理的优势。
Json 类似于 JavaScript 中的 object，是由 `{}` 包裹的一组键值对（key-value pair）。
键是一个 string，值支持 object，array，value 三种数据类型，键和值中间使用 `:` 分割，键值对中间使用 `,` 分割。
object: 是由 `{}` 包裹的一组键值对，类似 python 的 dictionary 和 JavaScript 的 object
array: 是由 `[]` 包裹的一组 value，类似 python 中的 list 和 JavaScript 的 array
string: 是由 `""` 包裹的字符串，如: "woo-foo", "woo", " foo"
value: 是以下一种 object，array，string，True，False，数字 或 null，如: "good", False, 123, \[123\]
[官方文档](https://www.json.org/json-zh.html)

## 什么是 json-server？
是一个根据 json 文件的结构生成 url 并且相应请求的 npm 应用，能够用来支持数据源很少改变的网站应用。
请参考[官方文档](https://www.npmjs.com/package/json-server)

## 在开始向 server 发送请求之前我应该了解什么？
为了更好的完成这次的项目，除了 Vue、 JavaScript html、 css 之外，你还应该了解 HTTP 的相关知识。
作为前端开发人员，网络相关的知识同样是不可或缺的，你可以搜索 Youtube 获得大量 HTTP 相关的教程，或者访问[这个文档](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)查看相关内容。
你应该了解基础的 HTTP 请求方法（如：GET POST SET DELETE）、 HTTP 响应状态码（如：403，404，433，500）。同时，你应该对 HTTP 访问控制（CORS）有一定了解，我们大概率会遇到它。

## 如何使用这个假后端？
首先使用命令行安装 json-server，运行
```shell
npm install json-server
```
安装完成后，启动 json-server 并且 watch 用作数据源的 json 文件
```shell
json-server --watch <your_data_path>
```
之后我们可以对 json-server 显示出的 url 发送 HTTP 请求并获得返回的数据了。

## 这个文件夹一定要叫做 data 吗？
不一定，它也可以被叫做 dog，foo，“新建文件夹” 或者其他的什么东西，叫做 data 为了方便理解其中的内容是用作测试的数据。
同理，fake_data.json 也不一定要叫做 “fake_data”。
只要 json-server 能 watch 一个 json 文件就好。

## 我们的数据如何传递？
参见 [API.md](./api.md)
