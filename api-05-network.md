# API 05 - 网络请求 & WebSocket

> 模块：`$http`、`$ws`
> 返回 [README](README.md)

## 目录

- [$http - HTTP网络请求](#http---http网络请求)
  - [POST 请求（JSON）](#post-请求json)
  - [POST 请求（字符串）](#post-请求字符串)
  - [GET 请求](#get-请求)
  - [调用 AI API（DeepSeek示例）](#调用-ai-apideepseek示例)
  - [下载文件](#下载文件)
  - [响应处理](#响应处理)
- [$ws - WebSocket](#ws---websocket)

---

## $http - HTTP网络请求

### POST 请求（JSON）

```javascript
let ip = "47.105.110.90";
let port = "8347";

let res = $http.post({
    url: `http://${ip}:${port}/api/endpoint`,
    // 直接传 JSON 对象（自动序列化）或 JSON 字符串
    data: {
        sex: "女"
    },
});

alert("结果", res.str());
```

### POST 请求（字符串）

```javascript
let res = $http.post({
    url: "http://example.com/api",
    data: "本地字符串",
});

alert("结果", res.str());
```

### GET 请求

```javascript
let res = $http.get({
    url: "https://api.example.com/data",
    // 可选：自定义请求头
    head: {
        "Accept": "application/json"
    }
});

alert("结果", res.str());
```

### 自定义请求头

```javascript
let res = $http.post({
    url: "https://api.example.com/endpoint",
    head: {
        "Content-Type": "application/json",
        "Authorization": "Bearer your_token_here",
        "X-Custom-Header": "value"
    },
    data: {
        key: "value"
    }
});
```

### 调用 AI API（DeepSeek示例）

> 原理：将官方 curl 示例翻译成 JavaScript 即可。

```javascript
let url = "https://api.deepseek.com/chat/completions";
let apiKey = ""; // 填写你的 API Key，类似 "sk-xxxx"

let res = $http.post({
    url: url,
    head: {
        "Content-Type": "application/json",
        "Authorization": "Bearer " + apiKey,
    },
    data: {
        model: "deepseek-chat",
        messages: [
            {
                role: "system",
                content: "You are a helpful assistant."
            },
            {
                role: "user",
                content: "Hello!"
            }
        ],
        stream: false
    }
});

alert("请求结果", res.str());

// 如果需要操作 JSON 对象
let json = res.json();
let content = json.choices[0].message.content;
log("AI回复:", content);
```

对应的 curl 命令（参考）：
```bash
curl https://api.deepseek.com/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <API Key>" \
  -d '{"model":"deepseek-chat","messages":[{"role":"user","content":"Hello!"}],"stream":false}'
```

### 下载文件

```javascript
let url = "https://example.com/image.jpg";
let path = "/sdcard/download.jpg";

// 异步下载（带进度回调）
$http.download(
    url,
    path,
    (cur, total, percent) => {
        log("下载进度", percent);
    },
    () => {
        log("下载完毕");
        showImg(path);
    },
    (res) => {
        log("下载失败", res);
    }
);
```

### 响应处理

```javascript
let res = $http.post({ url: "...", data: {} });

res.str();    // 返回响应字符串
res.json();   // 返回响应 JSON 对象（可直接访问属性）
```

---

## $ws - WebSocket

### 完整 WebSocket 示例

```javascript
// 创建 WebSocket（支持 ws:// 和 wss://）
let ws = $ws.create("wss://echo.websocket.org");

// 设置回调监听（链式调用）
ws.onOpen((res, ws) => {
    // 连接成功时回调（有默认回调，可不设置）
    console.log("链接成功");
})
.onClosed((code, reason, ws) => {
    // 关闭后回调（有默认回调，可不设置）
    console.log("关闭成功");
    // code: int, reason: String
})
.onClosing((code, reason, ws) => {
    // 处于关闭中时回调
    console.log("正在关闭");
})
.onFail((err, res, ws) => {
    // 出现异常时回调
    console.log("出现异常", err);
    // err: Throwable, res: okhttp3.Response
})
.onMsgStr((str, ws) => {
    // 接收到字符串消息时回调
    console.log("收到字符串：", str);
})
.onMsgByte((bs) => {
    // 接收到二进制消息时回调
    console.log("收到二进制消息，大小：", bs.size());
    console.log("hex：", bs.hex());
    console.log("base64：", bs.base64());
    console.log("md5：", bs.md5());
    console.log("bytes：", bs.toByteArray());
    // bs: okio.ByteString
});

// 发送字符串消息
ws.send("Hello AIGame!");

// 发送二进制消息
// ws.send([10, 15, 1, 1, 0, 5]);
```

### 说明

| 回调方法 | 参数 | 说明 |
|----------|------|------|
| `onOpen(res, ws)` | okhttp3.Response, okhttp3.WebSocket | 连接建立时触发 |
| `onClosed(code, reason, ws)` | int, String, okhttp3.WebSocket | 连接关闭后触发 |
| `onClosing(code, reason, ws)` | int, String, okhttp3.WebSocket | 正在关闭时触发 |
| `onFail(err, res, ws)` | Throwable, Response, WebSocket | 连接失败时触发 |
| `onMsgStr(str, ws)` | String, okhttp3.WebSocket | 收到字符串消息时触发 |
| `onMsgByte(bs)` | okio.ByteString | 收到二进制消息时触发 |

> 所有回调均有默认实现（打印日志），如不需要自定义可省略设置。
