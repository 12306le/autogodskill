---
name: aigame-android
description: AIGame Android 自动化脚本平台 API 文档。当用户需要编写 AIGame / AutoGOD 脚本、使用 AIGame API（如 $act、$screen、$ocr、$http、$floaty、$ui、$file 等）、实现安卓自动化操作、处理图像识别、OCR文字识别、UI界面构建、网络请求、文件操作、多线程等任务时使用本技能。
---

# AIGame Android 自动化脚本 API

AIGame 是 Android 平台上的自动化脚本工具，使用 **JavaScript（Rhino 引擎）** 编写脚本。

- 脚本语言：JavaScript（Rhino，支持 ES5/部分 ES6）
- 运行环境：Android 5.0+
- 核心权限：无障碍权限、悬浮窗权限（可选）、录屏权限（截图/OCR）

---

## 📖 文档导航

本仓库包含两类文档：**API 参考文档**（src-*.md）和**代码示例文档**（src-demo-*.md）。  
**优先查阅代码示例**，需要深入了解某 API 时再查阅详细参考文档。

### 🔍 代码示例文档（src-demo-*）

> 包含可直接运行的官方代码示例，适合快速上手和参考写法

| 文件 | 覆盖模块 | 典型用途 |
|------|----------|----------|
| `src-demo-act.md` | `$act` `$touch` | 点击、滑动、手势、按键、节点查找 |
| `src-demo-ui.md` | `$alert` `$dialog` `$tip` `$floaty` `$arc` `$ui` | 对话框、悬浮窗、界面构建 |
| `src-demo-app-sys.md` | `$app` `$sys` `$device` `$permit` `$task` `$thread` `$bus` `$event` `$engine` | 应用管理、系统设置、多线程 |
| `src-demo-file-net.md` | `$file` `$excel` `$sqlite` `$http` `$ws` `$res` `$ext` | 文件读写、数据库、网络请求 |
| `src-demo-screen-img.md` | `$screen` `$img` `$canvas` `$draw` `$color` `$ocr` | 截屏、找色、OCR、绘图 |
| `src-demo-utils.md` | `$date` `$str` `$crypt` `$log` `$media` `$tts` `$qr` 全局函数 脚本语法 | 工具类：日期、字符串、加密、日志 |
| `src-demo-misc.md` | 拓展示例、综合案例 | 授权、备份、AI对话等完整项目示例 |

### 📚 详细 API 参考文档（src-*）

> 包含完整的 API 定义、参数说明和类型信息，适合查询具体方法签名

| 文件 | 内容 |
|------|------|
| `src-act.md` | `$act` 无障碍手势、Node节点、UiSelector选择器、`$touch` 触摸驱动、`$hid` 键鼠触控、`$adapt` 分辨率适配 |
| `src-app-system.md` | `$app` 应用操作、AppInfo、AppTaskInfo、`$device` 设备信息、`$sys` 系统设置、`$permit` 权限管理、`$root` ROOT执行、`$szk` Shizuku |
| `src-file-data.md` | `$file` 文件系统、`$storage` 存储、`$sqlite` 数据库、`$excel` 表格、`$res` 资源管理、`$fc` 文件选择器、`$ext` 加载扩展、`$plugin` 插件 |
| `src-network.md` | `$http` 网络请求、`$ws` WebSocket、Ws对象、`$html` 网页操作 |
| `src-screen-ocr.md` | `$screen` 截图/屏幕信息、`$ocr` 文字识别（PaddleOCR/MLKit） |
| `src-img-vision.md` | `$img` 图片处理/找色/找图、Image对象、`$draw` 绘图、`$color` 颜色工具、`$yolo` 目标检测（训练/推理） |
| `src-floaty-arc.md` | `$floaty` 悬浮窗（应用级/系统级/可调节）、`$arc` 悬浮球菜单、MenuBody、MenuItem |
| `src-dialogs.md` | `$tip` 阻塞对话框、`$alert` 原生对话框、`$dialog` Material3 对话框 |
| `src-concurrency.md` | `$thread` 多线程、Threadx、CdLock、`$engine` 脚本引擎、`$task` 脚本任务、`$event` 事件监听、`$bus` 消息总线 |
| `src-utils.md` | `$global` 全局函数、`$log` 日志框架、`$date` 日期时间、`$media` 媒体播放、`$tts` 语音播报、`$qr` 二维码 |
| `src-ui-layout.md` | `$ui` 布局系统（linear/frame/relative/grid/scroll/card 等）、布局属性、颜色/gravity常量 |
| `src-ui-controls-a.md` | UI控件：appbar、button/button-group、check、chip/chip-group、drop、edit、fab |
| `src-ui-controls-b.md` | UI控件：img、input、ls（列表）、nav、pager、progress、radio/radio-group、range、seek、slider、statusbar、switch、text、toolbar、video、webview |

---

## 🔑 核心对象速查

| 对象 | 作用 | 示例文档 | API文档 |
|------|------|----------|---------|
| `$act` | 手势动作（点击/滑动/输入），集成ROOT/Shizuku/无障碍 | `src-demo-act.md` | `src-act.md` |
| `$app` | 应用启动、包名查询、应用列表 | `src-demo-app-sys.md` | `src-app-system.md` |
| `$screen` | 截图、屏幕尺寸、录屏 | `src-demo-screen-img.md` | `src-screen-ocr.md` |
| `$ocr` | 文字识别（离线，PaddleOCR/MLKit） | `src-demo-screen-img.md` | `src-screen-ocr.md` |
| `$yolo` | 目标检测（AI识图，YoloV5~V13） | `src-demo-screen-img.md` | `src-img-vision.md` |
| `$img` | 图片处理、找色、找图 | `src-demo-screen-img.md` | `src-img-vision.md` |
| `$root` | ROOT命令执行 | `src-demo-app-sys.md` | `src-app-system.md` |
| `$szk` | Shizuku高级权限 | `src-demo-app-sys.md` | `src-app-system.md` |
| `$file` | 文件读写 | `src-demo-file-net.md` | `src-file-data.md` |
| `$http` | HTTP请求 | `src-demo-file-net.md` | `src-network.md` |
| `$ui` | 界面布局构建 | `src-demo-ui.md` | `src-ui-layout.md` |
| `$floaty` | 悬浮窗 | `src-demo-ui.md` | `src-floaty-arc.md` |
| `$thread` | 多线程 | `src-demo-app-sys.md` | `src-concurrency.md` |
| `$log` | 日志输出 | `src-demo-utils.md` | `src-utils.md` |

---

## 🚀 快速开始

```javascript
// 1. 获取无障碍权限
if (!$act.hasPermit()) {
    $act.getPermit();
}

// 2. 点击屏幕上的"登录"按钮
let node = $act.selector().text("登录").findFirst();
if (node != null) {
    node.click();
}

// 3. 截图并识别文字
let img = $screen.capture();
let results = $ocr.recognize(img);
results.forEach(r => log(r.label));

// 4. 运行应用并等待界面
$app.run("QQ");
$act.selector().text("首页").waitFirst(5000);
```

---

## ⚙️ 权限体系说明

AIGame支持三种权限方案，优先级：**ROOT > Shizuku > 无障碍**

| 方案 | 条件 | 速度 | 能力 |
|------|------|------|------|
| 无障碍（Accessibility） | 开启无障碍服务 | 一般 | 基础操作 |
| Shizuku（`$szk`） | 安装Shizuku应用 | 较快 | 更多系统操作 |
| ROOT（`$root`） | 已root设备 | 最快 | 最高权限 |

`$act` 对象会自动按优先级选择可用方案。

---

## 📝 编写脚本的通用规范

1. **优先使用无障碍**：大多数操作需要无障碍权限，脚本开头检查并获取
2. **sleep 控制节奏**：UI 操作后加 `sleep()` 等待界面响应
3. **坐标系**：以屏幕左上角为原点，x 向右，y 向下
4. **Rhino JS 限制**：不支持 async/await；多线程用 `$thread`；无原生 Promise 支持
5. **分辨率适配**：跨设备脚本使用 `$adapt` 进行坐标换算

## 支持的中文关键字

AIGame使用自定义JavaScript方言，支持中文关键字：

| 中文关键字 | 对应JS | 说明 |
|-----------|--------|------|
| `定义` | `let/var` | 变量声明 |
| `如果` | `if` | 条件判断 |
| `否则` | `else` | 否则 |
| `循环` | `for` | 循环 |
| `关于` | `of` | for...of |
| `空` | `null` | 空值 |
| `真` | `true` | 布尔真 |
| `假` | `false` | 布尔假 |
| `打印` | `log()` | 输出日志 |
| `提示` | `toast()` | Toast提示 |
