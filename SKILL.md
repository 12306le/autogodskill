---
name: aigame-android
description: AIGame Android 自动化脚本平台 API 文档。当用户需要编写 AIGame 脚本、使用 AIGame API（如 $act、$screen、$ocr、$http、$floaty、$ui、$file 等）、实现安卓自动化操作、处理图像识别、OCR文字识别、UI界面构建、网络请求、文件操作、多线程等任务时使用本技能。
---

# AIGame Android 自动化脚本 API

AIGame 是 Android 平台上的自动化脚本工具，使用 **JavaScript（Rhino 引擎）** 编写脚本。

- 脚本语言：JavaScript（Rhino，支持 ES5/部分 ES6）
- 运行环境：Android 5.0+
- 核心权限：无障碍权限、悬浮窗权限（可选）、录屏权限（截图/OCR）

---

## 📖 文档导航

本仓库包含两类文档，**优先查阅示例文档**，需要深入了解某 API 时再查阅详细参考文档。

### 🔍 官方示例文档（api-01 ~ api-07）
> 包含可直接运行的代码示例，适合快速上手和参考写法

| 文件 | 覆盖模块 | 典型用途 |
|------|----------|----------|
| [api-01-accessibility.md](api-01-accessibility.md) | `$act` `$touch` | 点击、滑动、手势、按键、节点查找 |
| [api-02-ui-dialog.md](api-02-ui-dialog.md) | `$alert` `$dialog` `$tip` `$floaty` `$arc` `$ui` | 对话框、悬浮窗、界面构建 |
| [api-03-app-system.md](api-03-app-system.md) | `$app` `$sys` `$device` `$permit` `$task` `$thread` `$bus` `$event` `$engine` | 应用管理、系统设置、多线程 |
| [api-04-file-data.md](api-04-file-data.md) | `$file` `$excel` `$sqlite` `$res` `$fc` `$ext` | 文件读写、数据库、Excel |
| [api-05-network.md](api-05-network.md) | `$http` `$ws` | HTTP请求、WebSocket |
| [api-06-screen-image.md](api-06-screen-image.md) | `$screen` `$img` `$canvas` `$draw` `$color` `$ocr` | 截屏、找色、OCR、绘图 |
| [api-07-utils.md](api-07-utils.md) | `$date` `$str` `$crypt` `$log` `$media` `$tts` `$qr` | 工具类：日期、字符串、加密、日志 |

### 📚 详细 API 参考文档（01 ~ 15）
> 包含完整的 API 定义、参数说明和类型信息，适合查询具体方法签名

| 文件 | 内容 |
|------|------|
| [01-getting-started.md](01-getting-started.md) | 环境搭建、链接调试、第一个程序 |
| [02-core-automation.md](02-core-automation.md) | Node节点、UiSelector、`$act`手势、`$adapt`分辨率适配 |
| [03-app-management.md](03-app-management.md) | `$app` 应用操作、AppInfo、AppTaskInfo |
| [04-screen-touch.md](04-screen-touch.md) | `$screen`屏幕、`$touch`触摸驱动、`$hid`键鼠触控 |
| [05-image-vision.md](05-image-vision.md) | Image图片、`$img`、`$ocr`文字识别、`$yolo`目标检测 |
| [06-system-permission.md](06-system-permission.md) | `$device`设备、`$sys`系统、`$root`、`$szk` Shizuku |
| [07-file-storage.md](07-file-storage.md) | `$file`文件系统、`$storage`存储、`$sqlite`数据库 |
| [08-network.md](08-network.md) | `$http`网络请求、`$ws` WebSocket、`$html`网页操作 |
| [09-ui-framework.md](09-ui-framework.md) | `$ui`界面、布局系统、所有UI控件、UI对象 |
| [10-floaty-draw.md](10-floaty-draw.md) | `$floaty`悬浮窗、`$draw`绘制、`$arc`悬浮球 |
| [11-dialogs.md](11-dialogs.md) | `$alert`原生对话框、`$dialog` M3对话框、`$tip`阻塞对话框 |
| [12-media-utils.md](12-media-utils.md) | `$media`媒体、`$tts`语音、`$qr`二维码、`$color`颜色 |
| [13-concurrency-events.md](13-concurrency-events.md) | `$thread`并发、`$task`、`$event`、`$bus`消息总线 |
| [14-extensions.md](14-extensions.md) | `$ext`扩展、`$plugin`插件、`$res`资源、`$excel` |
| [15-global-log.md](15-global-log.md) | `$global`全局函数、`$log`日志框架 |

---

## 🔑 核心对象速查

| 对象 | 作用 | 示例文档 | 详细文档 |
|------|------|----------|----------|
| `$act` | 手势动作（点击/滑动/输入），集成ROOT/Shizuku/无障碍 | [api-01](api-01-accessibility.md) | [02](02-core-automation.md) |
| `$app` | 应用启动、包名查询、应用列表 | [api-03](api-03-app-system.md) | [03](03-app-management.md) |
| `$screen` | 截图、屏幕尺寸、录屏 | [api-06](api-06-screen-image.md) | [04](04-screen-touch.md) |
| `$ocr` | 文字识别（离线） | [api-06](api-06-screen-image.md) | [05](05-image-vision.md) |
| `$yolo` | 目标检测（AI识图） | [api-06](api-06-screen-image.md) | [05](05-image-vision.md) |
| `$img` | 图片处理、找色、找图 | [api-06](api-06-screen-image.md) | [05](05-image-vision.md) |
| `$root` | ROOT命令执行 | [api-03](api-03-app-system.md) | [06](06-system-permission.md) |
| `$szk` | Shizuku高级权限 | [api-03](api-03-app-system.md) | [06](06-system-permission.md) |
| `$file` | 文件读写 | [api-04](api-04-file-data.md) | [07](07-file-storage.md) |
| `$http` | HTTP请求 | [api-05](api-05-network.md) | [08](08-network.md) |
| `$ui` | 界面布局构建 | [api-02](api-02-ui-dialog.md) | [09](09-ui-framework.md) |
| `$floaty` | 悬浮窗 | [api-02](api-02-ui-dialog.md) | [10](10-floaty-draw.md) |
| `$thread` | 多线程 | [api-03](api-03-app-system.md) | [13](13-concurrency-events.md) |
| `$log` | 日志输出 | [api-07](api-07-utils.md) | [15](15-global-log.md) |

---

## 全局函数（无需模块前缀）

```javascript
sleep(2000);          // 延迟毫秒
toast("提示内容");    // Toast 提示
log("日志内容");      // 日志输出
info("信息内容");     // 信息框
alert("标题", "内容"); // 阻塞弹窗
setClip("内容");      // 设置剪贴板
let n = random(10);   // 随机整数 0~9
showImg("路径或图片对象"); // 显示图片
```

---

## ⚙️ 权限体系说明

AIGame支持三种权限方案，优先级：**ROOT > Shizuku > 无障碍**

- **无障碍（Accessibility）**：最基础，无需特殊权限，但速度较慢
- **Shizuku（`$szk`）**：需要安装Shizuku应用，支持更多系统操作
- **ROOT（`$root`）**：最高权限，速度最快，需要已root设备

`$act` 对象自动按优先级选择可用方案。

---

## 编写脚本的通用规范

1. **优先使用无障碍**：大多数操作需要无障碍权限，脚本开头检查并获取
2. **sleep 控制节奏**：UI 操作后加 `sleep()` 等待界面响应
3. **坐标系**：以屏幕左上角为原点，x 向右，y 向下
4. **Rhino JS 限制**：不支持 async/await；多线程用 `$thread`；无原生 Promise 支持
5. **分辨率适配**：跨设备脚本使用 `$adapt` 进行坐标换算
