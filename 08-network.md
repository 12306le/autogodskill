# 网络通信 API

> HTTP请求、WebSocket双工通信、网页加载操作。

## 目录
- [$http - 网络请求](#http---网络请求)
- [Ws - WS封装对象](#ws---ws封装对象)
- [$ws - WebSocket双工通信](#ws---websocket双工通信)
- [$html - 网页操作](#html---网页操作)

---

## $http - 网络请求

- 更新时间:2026-01-30 19:32:53

> 网络请求




#### uri(uri)

> 解析Uri字符串
> 
> 如果你想通过文件提供器{FileProvider}来解析文件路径，那么可以使用$file.uri("path");函数

- 参数 : uri {String} Uri字符串
- 返回 : {Uri} Uri对象
- 版本 : 1.3.7


```javascript
let uri = $http.uri("smsto:"+$str.uriEncode("13693749475"));
```


#### get(url)

> 同步请求

- 参数 : url {url} 链接地址
- 返回 : {HttpResponse} 返回结果
- 版本 : 1.2.0


```javascript
//全部配置参数
let opt = {
    url:"",//请求地址
    head:{
        "key":"value",
        "key2":"value2"
    },
    data: "请求数据",//支持file、xml、json、string等类型，会自动判断
    connectTimeout:30, //[可选]连接超时时间(默认30秒)
    readTimeout:30, //[可选]读超时时间(默认30秒)
    writeTimeout:30, //[可选]写超时时间(默认30秒)
    callTimeout:60 //[可选]请求超时时间(默认60秒)
}
//如果要发送文件
let opt = {
    url:"",//请求地址
    head:{ },
    data: "/sdcard/img.png"
}
//如果要发送json
let opt = {
    url:"",//请求地址
    head:{ },
    //直接写json对象，或json字符串也可以
    data: {
        "key":"value",
        "key2":"value2"
    }
}
```


#### get(opts)

> GET请求

- 参数 : opts {HttpOptions} 配置
- 返回 : {HttpResponse} 返回结果
- 版本 : 1.2.0


#### post(opts)

> POST请求

- 参数 : opts {HttpOptions} 配置
- 返回 : {HttpResponse} 返回结果
- 版本 : 1.2.0


#### del(opts)

> DELETE请求

- 参数 : opts {HttpOptions} 配置
- 返回 : {HttpResponse} 返回结果
- 版本 : 1.2.0


#### delete(opts)

> DELETE请求

- 参数 : opts {HttpOptions} 配置
- 返回 : {HttpResponse} 返回结果
- 版本 : 1.2.0


#### put(opts)

> PUT请求

- 参数 : opts {HttpOptions} 配置
- 返回 : {HttpResponse} 返回结果
- 版本 : 1.2.0


#### patch(opts)

> PATCH请求

- 参数 : opts {HttpOptions} 配置
- 返回 : {HttpResponse} 返回结果
- 版本 : 1.2.0


#### download(url, savePath)

> 下载文件

- 参数 : url {string}  url
- 参数 : savePath {string} 保存路径


#### download(url, savePath, completeCallback)

> 下载文件

- 参数 : url {string}  url
- 参数 : savePath {string} 保存路径
- 参数 : completeCallback {()=>{}} 下载完成回调


#### download(url, savePath, completeCallback, onFailure)

> 下载文件

- 参数 : url {string}  url
- 参数 : savePath {string} 保存路径
- 参数 : completeCallback {()=>{}} 下载完成回调
- 参数 : onFailure {(res)=>}  错误回调


#### download(url, savePath, progressListener, completeCallback, onFailure)

> 下载文件

- 参数 : url {string}  url
- 参数 : savePath {string} 保存路径
- 参数 : progressListener {(cur,total,percent)=>{}} 进度监听器
- 参数 : completeCallback {()=>{}} 下载完成回调
- 参数 : onFailure {(res)=>}    错误回调


```javascript
$http.download(
"https://example.com/sample-image.jpeg",
"/sdcard/美女.png",
(cur,total,percent)=>{
    log("下载进度",percent);
},()=>{
    log("下载完毕");
},(res)=>{
    log("下载失败",res);
});
```


#### wifiIp()

> 获取wifi的ip地址
> 
> 如果连接方式不是wifi则返回null

- 返回 : {string} ip地址

---

## Ws - WS封装对象

- 更新时间:2026-01-30 19:32:57

> 双工通信包装对象
> 
> 对okhttp3.WebSocket对象进行封装的对象




#### send(msg)

> 发送字符消息

- 参数 : msg {string} 字符串消息


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//发送字符消息
ws.send("hello");
```


#### send(bytes)

> 发送字节消息

- 参数 : bytes {byte[]} 字节消息


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//发送字节消息
ws.send([10,15,0,1,20]);
```


#### send(byteString)

> 发送消息
> 
> ByteString类型是okhttp提供的一种数据类型，具体函数可以参考okhttp文档

- 参数 : byteString {ByteString} byteString对象消息


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
let byteString = okio.ByteString.encodeUtf8("字符串");
//发送消息
ws.send(byteString);
```


#### sendBase64(base64Str)

> 发送base64消息

- 参数 : base64Str {string} base64 字符串


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//发送base64消息
ws.sendBase64("QXV0by5qcyBQcm8geXlkcw==");
```


#### sendHex(hexStr)

> 发送16进制消息

- 参数 : hexStr {string} 16 进制字符串


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//发送16进制消息
ws.sendHex("621172314F60");
```


#### cancel()

> 关闭
> 
> 效果和 'stop()' 相同


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//立即关闭
ws.cancel();
```


#### stop()

> 关闭
> 
> 效果和 'cancel()' 相同


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//立即关闭
ws.stop();
```


#### close()

> 关闭
> 
> 效果和 stop(),cancel() 相同


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//立即关闭
ws.close();
```


#### close(code)

> 尝试正常关闭

- 参数 : code {number} 关闭码


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//尝试正常关闭(正常关闭退出码一般是1001)
ws.close(1001);
```


#### close(code, reason)

> 尝试正常关闭

- 参数 : code {number} 关闭码
- 参数 : reason {string} 关闭原因


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//尝试正常关闭(正常关闭退出码一般是1001)
ws.close(1001,"close");
```


#### onMsgByte(callback)

> 设置字节字符信息接受回调
> 
> 如果不设置，则使用默认的回调：打印字节数组

- 参数 : callback {(byteString)=>{}}
- 返回 : {Ws} 返回当前对象


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//发送消息
ws.onMsgByte((bs)=> {
    //参数说明：
    // bs: okio.ByteString (参考okhttp3文档)
    //接收到字节数据时回调
    console.log("收到二进制消息：大小 ", bs.size());
    console.log("hex: ", bs.hex());
    console.log("base64: ", bs.base64());
    console.log("md5: ", bs.md5());
    console.log("bytes: ", bs.toByteArray());
});
```


#### onMsgStr(callback)

> 设置字符串信息接受回调
> 
> 如果不设置，则使用默认的回调：打印字符串

- 参数 : callback {(str)=>{}}
- 返回 : {Ws} 返回当前对象


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//设置字符串信息接受回调
ws.onMsgStr((str, ws)=> {
    //参数说明：
    // str: String 字符串数据
    // ws: okhttp3.WebSocket (参考okhttp3文档)
    //接收到字符串信息时回调
    console.log("收到字符串：",str);
});
```


#### onOpen(callback)

> 设置连接成功回调
> 
> 如果不设置，则使用默认的回调：打印连接信息

- 参数 : callback {(res,ws)=>{}} 回调
- 返回 : {Ws} 返回当前对象


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//设置连接成功回调
ws.onOpen((res,ws)=> {
    //参数说明：
    // res: okhttp3.Response (参考okhttp3文档)
    // ws: okhttp3.WebSocket (参考okhttp3文档)
    console.log("链接成功");
});
```


#### onClosed(callback)

> 设置连接关闭回调
> 
> 如果不设置，则使用默认的回调：打印关闭信息

- 参数 : callback {(code,reason,ws)=>{}} 回调
- 返回 : {Ws} 返回当前对象


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//设置连接关闭回调
ws.onClosed((code,reason,ws)=>{
    //参数说明：
    // code:   int    数字
    // reason: String 字符串
    // ws: okhttp3.WebSocket (参考okhttp3文档)
    console.log("正在关闭");
});
```


#### onClosing(callback)

> 设置连接关闭中回调
> 
> 如果不设置，则使用默认的回调：打印关闭信息

- 参数 : callback {(code,reason,ws)=>{}} 回调
- 返回 : {Ws} 返回当前对象


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//设置连接关闭中回调
ws.onClosing((code,reason,ws)=>{
    //参数说明：
    // code:   int    数字
    // reason: String 字符串
    // ws: okhttp3.WebSocket (参考okhttp3文档)
    console.log("正在关闭");
});
```


#### onFail(onFailure)

> 设置连接失败回调
> 
> 如果不设置，则使用默认的回调：打印错误信息

- 参数 : onFailure {(err,res,ws)=>{}} 回调
- 返回 : {Ws} 返回当前对象


```javascript
//创建ws对象
let ws = $ws.create("wss://echo.websocket.org");
//设置连接失败回调
ws.onFail((err,res,ws)=>{
    //参数说明：
    // err: Throwable
    // res: okhttp3.Response (参考okhttp3文档)
    // ws: okhttp3.WebSocket (参考okhttp3文档)
    //打印错误信息
    console.log("出现异常",err);
});
```

---

## $ws - 双工通信:WebSocket

- 更新时间:2026-01-30 19:32:57

> WebSocket工具
> 
> 让客户端和服务器之间建立一条"热线电话"，双方可以随时说话(通信)，不用像以前那样每次都要重新拨号(不用重新建立连接)。




#### create(url)

> 创建一个 WebSocket

- 参数 : url {string} 例如:ws://127.0.0.1:8080
- 返回 : Ws


```javascript
//返回的ws是经过封装的WebSocket对象(不是okhttp3.WebSocket原生对象)
let ws = $ws.create("wss://echo.websocket.org");
//设置监听
ws.onOpen((res,ws)=> {
    //当成功连接时回调(此函数可以不用设置，拥有默认回调:打印信息)
    console.log("链接成功");
    //参数说明：
    // res: okhttp3.Response (参考okhttp3文档)
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onClosed((code,reason,ws)=> {
    //当关闭后回调(此函数可以不用设置，拥有默认回调:打印信息)
    console.log("关闭成功");
    //参数说明：
    // code:   int    数字
    // reason: String 字符串
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onClosing((code,reason,ws)=> {
    //处于关闭时回调(此函数可以不用设置，拥有默认回调:打印信息)
    console.log("正在关闭");
    //参数说明：
    // code:   int    数字
    // reason: String 字符串
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onFail((err,res,ws)=> {
    //出现异常时回调(此函数可以不用设置，拥有默认回调:打印信息)
    console.log("出现异常",err);
    //参数说明：
    // err: Throwable
    // res: okhttp3.Response (参考okhttp3文档)
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onMsgStr((str, ws)=> {
    //接收到字符串信息时回调
    console.log("收到字符串：",str);
    //参数说明：
    // str: String 字符串数据
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onMsgByte((bs)=> {
    //接收到字节数据时回调
    console.log("收到二进制消息：大小 ", bs.size());
    console.log("hex: ", bs.hex());
    console.log("base64: ", bs.base64());
    console.log("md5: ", bs.md5());
    console.log("bytes: ", bs.toByteArray());
    //参数说明：
    // bs: okio.ByteString (参考okhttp3文档)
});
//发送字符串消息
ws.send("Hello AIGame!");
//发送二进制消息
//ws.send([10,15,1,1,0,5]);
```

---

## $html - 网页操作

- 更新时间:2026-01-30 19:32:53

> 网页操作




#### escape(html)

> 转义HTML字符
> 
> 此函数会遍历么一个字符，将特殊字符进行转义。
> 

- 参数 : html 被转义的文本
- 返回 : 转义后的文本


```javascript
let html = "<div>123</div>";
let escapeHtml = $html.escape(html);
```


#### unescape(text)

> 还原被转义的HTML特殊字符

- 参数 : text {string} HTML字符串
- 返回 : {string} 转换后的字符串


#### cleanHtmlTag(text)

> 清除所有HTML标签

- 参数 : text {string} 文本
- 返回 : {string} 清除标签后的文本


#### removeHtmlTag(text, tagNames)

> 删除HTML标签(包括内容)

- 参数 : text {string} 文本
- 参数 : tagNames {string...} 要清除的标签
- 返回 : 去除标签后的文本


#### unwrapHtmlTag(text, tagNames)

> 清除指定HTML标签(不包括内容)

- 参数 : text {string} 文本
- 参数 : tagNames {string...} 要清除的标签
- 返回 : {string} 去除标签后的文本


#### removeHtmlTag(text, withTagContent, tagNames)

> 清除指定HTML标签

- 参数 : text {string} 文本
- 参数 : withTagContent {boolean} 是否去掉被包含在标签中的内容
- 参数 : tagNames {string...}  要清除的标签
- 返回 : {string} 去除标签后的文本


#### removeHtmlAttr(html, attrs)

> 去除HTML标签中的所有属性

- 参数 : html {string} 文本
- 参数 : attrs {string...} 属性名
- 返回 : {string} 处理后的文本


#### removeAllHtmlAttr(html, tagNames)

> 去除指定标签的所有属性

- 参数 : html {string} 内容
- 参数 : tagNames {string...} 指定标签
- 返回 : {string} 处理后的文本


#### filter(html)

> 过滤HTML文本，防止XSS攻击

- 参数 : html {string} HTML内容
- 返回 : {string} 过滤后的内容


#### getWeiYunNote(shortLink)

> 处理腾讯微笔记
> 
> 我们可以在[腾讯微云]->[我的]->[笔记]中创建一个纯文本笔记(切记不要有特殊字符，例如粗体或者改变文本颜色等等特殊处理都不要有)，之后我们点击分享，就可以看到链接最后面的一个字段，我称之为短链接，把短链接放入到这个函数中来，我将解析你的微云笔记，最后把处理好的文本字符串返回给你。
> 
> 这样以来，你可以把腾讯微云当作你的免费云数据库来使用，写一个微云笔记，把自己的数据(例如json字符)存入到笔记中，需要使用的时候使用这个函数拉取后解析成json对象(JSON.parse(str))，就可以使用数据了。

- 参数 : shortLink {string} 短链接 
- 返回 : {string} 处理好的字符串
- 版本 : 1.5.0


```javascript
// 微云笔记链接：https://share.weiyun.com/bnaMAKsa
// 短链接：bnaMAKsa
let noteContent = $html.getWeiYunNote("bnaMAKsa");
// 解析json字符串
let jsonObj = JSON.parse(noteContent);
```