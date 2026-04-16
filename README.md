# AIGame 开发文档

> **AIGame** 是一个Android自动化框架，支持无障碍、ROOT、Shizuku多种权限方案，提供JavaScript脚本开发能力。  
> 本文档为AI辅助开发使用，覆盖所有API模块。

---

## 📁 文档结构

```
skills/
├── SKILL.md                      # AI 技能入口（AI 读此文件）
├── README.md                     # 本文件
│
├── # 官方示例文档（快速参考）
├── api-01-accessibility.md       # 无障碍操作 & 触控示例
├── api-02-ui-dialog.md           # UI界面 & 对话框 & 悬浮窗示例
├── api-03-app-system.md          # 应用 & 系统 & 多线程示例
├── api-04-file-data.md           # 文件 & 数据库 & Excel示例
├── api-05-network.md             # 网络请求 & WebSocket示例
├── api-06-screen-image.md        # 截屏 & 图像 & OCR & 颜色示例
├── api-07-utils.md               # 工具类示例：加密/日期/字符串/日志
│
└── # 详细 API 参考文档（完整签名）
    ├── 01-getting-started.md
    ├── 02-core-automation.md
    ├── 03-app-management.md
    ├── 04-screen-touch.md
    ├── 05-image-vision.md
    ├── 06-system-permission.md
    ├── 07-file-storage.md
    ├── 08-network.md
    ├── 09-ui-framework.md
    ├── 10-floaty-draw.md
    ├── 11-dialogs.md
    ├── 12-media-utils.md
    ├── 13-concurrency-events.md
    ├── 14-extensions.md
    └── 15-global-log.md
```

---

## 🔍 官方示例文档（api-01 ~ api-07）

包含可直接运行的代码示例，适合快速上手和参考写法。

| 文件 | 覆盖模块 | 典型用途 |
|------|----------|----------|
| [api-01-accessibility.md](api-01-accessibility.md) | `$act` `$touch` | 点击、滑动、手势、按键、节点查找 |
| [api-02-ui-dialog.md](api-02-ui-dialog.md) | `$alert` `$dialog` `$tip` `$floaty` `$arc` `$ui` | 对话框、悬浮窗、界面构建 |
| [api-03-app-system.md](api-03-app-system.md) | `$app` `$sys` `$device` `$permit` `$task` `$thread` `$bus` `$event` `$engine` | 应用管理、系统设置、多线程 |
| [api-04-file-data.md](api-04-file-data.md) | `$file` `$excel` `$sqlite` `$res` `$fc` `$ext` | 文件读写、数据库、Excel |
| [api-05-network.md](api-05-network.md) | `$http` `$ws` | HTTP请求、WebSocket |
| [api-06-screen-image.md](api-06-screen-image.md) | `$screen` `$img` `$canvas` `$draw` `$color` `$ocr` | 截屏、找色、OCR、绘图 |
| [api-07-utils.md](api-07-utils.md) | `$date` `$str` `$crypt` `$log` `$media` `$tts` `$qr` | 工具类：日期、字符串、加密、日志 |

---

## 📚 详细 API 参考文档（01 ~ 15）

包含完整的 API 定义、参数说明和类型信息。

| 文件 | 内容 |
|------|------|
| [01-getting-started.md](01-getting-started.md) | 环境搭建、链接调试、第一个程序、产品优势 |
| [02-core-automation.md](02-core-automation.md) | Node节点、UiSelector选择器、`$act`手势、`$adapt`分辨率适配 |
| [03-app-management.md](03-app-management.md) | `$app`应用操作、AppInfo、AppTaskInfo |
| [04-screen-touch.md](04-screen-touch.md) | `$screen`屏幕、`$touch`触摸驱动、`$hid`键鼠触控、ScreenInfo |
| [05-image-vision.md](05-image-vision.md) | Image图片、`$img`图片操作、`$ocr`文字识别、`$yolo`目标检测 |
| [06-system-permission.md](06-system-permission.md) | `$device`设备、`$sys`系统、`$root` ROOT、`$szk` Shizuku、`$permit`权限 |
| [07-file-storage.md](07-file-storage.md) | `$file`文件系统、`$storage`存储、`$sqlite`数据库 |
| [08-network.md](08-network.md) | `$http`网络请求、`$ws` WebSocket、`$html`网页操作 |
| [09-ui-framework.md](09-ui-framework.md) | `$ui`界面、布局系统、所有UI控件、UI对象 |
| [10-floaty-draw.md](10-floaty-draw.md) | `$floaty`悬浮窗、`$draw`绘制、`$arc`悬浮球、菜单 |
| [11-dialogs.md](11-dialogs.md) | `$alert`原生对话框、`$dialog` M3对话框、`$tip`阻塞对话框 |
| [12-media-utils.md](12-media-utils.md) | `$media`媒体、`$tts`语音、`$qr`二维码、`$color`颜色、`$date`日期 |
| [13-concurrency-events.md](13-concurrency-events.md) | `$thread`并发、`$task`脚本任务、`$event`事件、`$bus`消息总线 |
| [14-extensions.md](14-extensions.md) | `$ext`加载扩展、`$plugin`插件、`$res`资源、`$excel`表格 |
| [15-global-log.md](15-global-log.md) | `$global`全局函数、`$log`日志框架 |

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

## 🔑 核心对象速查

| 对象 | 作用 | 示例 | 详细 |
|------|------|------|------|
| `$act` | 手势动作（点击/滑动/输入） | [api-01](api-01-accessibility.md) | [02](02-core-automation.md) |
| `$app` | 应用启动、包名查询 | [api-03](api-03-app-system.md) | [03](03-app-management.md) |
| `$screen` | 截图、屏幕尺寸 | [api-06](api-06-screen-image.md) | [04](04-screen-touch.md) |
| `$ocr` | 文字识别（离线） | [api-06](api-06-screen-image.md) | [05](05-image-vision.md) |
| `$yolo` | 目标检测（AI识图） | [api-06](api-06-screen-image.md) | [05](05-image-vision.md) |
| `$img` | 图片处理、找色 | [api-06](api-06-screen-image.md) | [05](05-image-vision.md) |
| `$root` | ROOT命令执行 | [api-03](api-03-app-system.md) | [06](06-system-permission.md) |
| `$szk` | Shizuku高级权限 | [api-03](api-03-app-system.md) | [06](06-system-permission.md) |
| `$file` | 文件读写 | [api-04](api-04-file-data.md) | [07](07-file-storage.md) |
| `$http` | HTTP请求 | [api-05](api-05-network.md) | [08](08-network.md) |
| `$ui` | 界面布局构建 | [api-02](api-02-ui-dialog.md) | [09](09-ui-framework.md) |
| `$floaty` | 悬浮窗 | [api-02](api-02-ui-dialog.md) | [10](10-floaty-draw.md) |
| `$thread` | 多线程 | [api-03](api-03-app-system.md) | [13](13-concurrency-events.md) |
| `$log` | 日志输出 | [api-07](api-07-utils.md) | [15](15-global-log.md) |

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

## 📝 语法说明

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
