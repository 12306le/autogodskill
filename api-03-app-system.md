# API 03 - 应用管理 & 系统 & 多线程

> 模块：`$app`、`$sys`、`$device`、`$permit`、`$task`、`$thread`、`$bus`、`$event`、`$engine`
> 返回 [README](README.md)

## 目录

- [$app - 应用管理](#app---应用管理)
- [$sys - 系统设置](#sys---系统设置)
- [$device - 设备信息](#device---设备信息)
- [$permit - 权限管理](#permit---权限管理)
- [$task - 任务控制](#task---任务控制)
- [$thread - 多线程](#thread---多线程)
- [$bus - 事件总线](#bus---事件总线)
- [$event - 系统事件监听](#event---系统事件监听)
- [$engine - 脚本引擎](#engine---脚本引擎)

---

## $app - 应用管理

### 启动应用

```javascript
$app.runApp("QQ");                          // 通过应用名启动
$app.runPkg("com.tencent.mobileqq");        // 通过包名启动
$app.run("QQ");                             // 应用名或包名均可
$app.startActivity("QQ", "com.tencent.mobileqq.activity.SplashActivity"); // 启动指定Activity
```

### 应用信息查询

```javascript
// 获取所有应用信息
let apps = $app.ls();
for (let i = 0; i < apps.size(); i++) {
    log(apps.get(i));
}

// 获取最近运行的应用
if ($app.hasUsagePermit()) {
    let pkgList = $app.lsRecent();
    if (pkgList !== null) {
        for (let i = 0; i < pkgList.size(); i++) {
            console.log(pkgList[i]);
        }
    }
} else {
    $app.getUsagePermit(); // 获取使用情况访问权限
}

// 判断应用是否存在
let pkg = "org.aigame.pro";
if ($app.pkgExists(pkg)) {
    alert(pkg, "存在");
} else {
    alert(pkg, "不存在");
}

// 获取包名 / 应用名
let pkg = $app.pkgName("QQ");          // 通过名称获取包名
let name = $app.appName("com.android.settings"); // 通过包名获取名称
```

### 卸载应用

```javascript
$app.uninstallApp("QQ");                        // 通过应用名（部分手机不支持）
$app.uninstallPkg("com.tencent.mobileqq");      // 通过包名（部分手机不支持）
$app.uninstall("QQ");                           // 应用名或包名
```

### 获取应用图标

```javascript
let icon = $app.getIcon("QQ");
$img.show(icon); // 需要悬浮窗权限
```

### 分享 & 通讯

```javascript
$app.openUrl("www.baidu.com");               // 打开网址
$app.shareImg("/sdcard/Pictures/t01.png");   // 分享本地图片
$app.shareText("你好");                      // 分享文本
$app.sendSms("13593749477", "你好我是xxx"); // 发送短信
$app.call("13593749477");                    // 拨打电话
$app.sendMail("email@qq.com", "标题", "内容"); // 发邮件
```

### 文件操作

```javascript
$app.viewFile("/sdcard/Pictures/test.text"); // 打开文件
$app.editFile("/sdcard/Pictures/test.text"); // 编辑文件
$app.appSetting("AIGame Pro");               // 打开应用的权限设置界面
```

### Intent & 广播

```javascript
// 创建 Intent
let intent = $app.newIntent({
    action: "org.aigame.pro.bus.action",
    extras: [{
        name: "mKey",
        value: "哈哈哈"
    }],
    component: {
        cls: "org.aigame.api.bus.receiver.AgBusReceiver",
        pkg: "org.aigame.pro"
    }
});

// 发送广播
$app.sendBroadcast(intent, "org.aigame.pro.bus.permission");
```

### 使用情况权限

```javascript
$app.hasUsagePermit(); // 是否有使用情况访问权限
$app.getUsagePermit(); // 获取权限
```

---

## $sys - 系统设置

### 剪切板

```javascript
$sys.setClip("Hello AIGame !"); // 设置剪切板
let content = $sys.getClip();   // 获取剪切板内容
if ($sys.hasClip()) {           // 判断是否有内容
    $tip.i($sys.getClip());
}
$sys.clearClip();               // 清空剪切板
```

### 音量控制

```javascript
// 音量类型可用前3位缩写：sys, rin, mus, ala, acc
$sys.volume("system", 100);       // 系统音量
$sys.volume("ring", 100);         // 铃声音量
$sys.volume("music", 100);        // 媒体音量
$sys.volume("alarm", 100);        // 闹钟音量
$sys.volume("notification", 100); // 通知音量
$sys.volume("call", 100);         // 电话音量
$sys.volume("dtmf", 100);         // 双音多频
$sys.volume("accessibility", 100);// 无障碍音量
```

### 电话权限

```javascript
$sys.getSetPermit();  // 获取修改系统设置权限

if (!$sys.enableCall()) {
    $sys.getCallPermit(); // 获取电话权限
}

if ($sys.enableCall()) {
    toast("拥有电话权限");
}
```

### 飞行模式

```javascript
$sys.airplane(true);  // 开启飞行模式
$sys.airplane(false); // 关闭飞行模式
```

### 设备 ID

```javascript
let id = $sys.getDeviceId();
alert("设备id", id);
```

### 电池优化

```javascript
let is = $sys.ignorePower("org.aigame.app"); // 是否忽略电池优化
$sys.requestIgnorePower("org.aigame.app");   // 请求忽略电池优化
```

---

## $device - 设备信息

### 基础属性（直接访问）

```javascript
log("屏幕宽度", $device.width);
log("屏幕高度", $device.height);
log("Build ID", $device.buildId);
log("Build Display", $device.buildDisplay);
log("主板名称", $device.broad);
log("品牌名称", $device.brand);
log("设备名称", $device.device);
log("型号名称", $device.model);
log("产品名称", $device.product);
log("引导加载程序", $device.bootloader);
log("硬件名称", $device.hardware);
log("指纹信息", $device.fingerprint);
log("序列号", $device.serial);
log("SDK版本号", $device.sdkInt);
log("内部版本号", $device.incremental);
log("Android版本号", $device.release);
log("基础操作系统版本", $device.baseOS);
log("安全补丁版本", $device.securityPatch);
log("开发代号", $device.code);
```

### 方法调用

```javascript
log("IMEI号码", $device.getIMEI());
log("Android ID", $device.getAndroidId());
log("MAC 地址", $device.getMacAddress());
log("屏幕亮度", $device.getBrightness());
log("亮度模式", $device.getBrightnessMode());
log("音乐音量", $device.getMusicVolume());
log("通知音量", $device.getNotificationVolume());
log("闹钟音量", $device.getAlarmVolume());
log("音乐最大音量", $device.getMusicMaxVolume());
log("通知最大音量", $device.getNotificationMaxVolume());
log("闹钟最大音量", $device.getAlarmMaxVolume());
log("电池电量", $device.getBattery());
log("是否充电", $device.isCharging());
log("总内存", $device.getTotalMem());
log("可用内存", $device.getAvailMem());
log("屏幕是否亮起", $device.isScreenOn());
log("屏幕是否熄灭", $device.isScreenOff());
```

---

## $permit - 权限管理

### 常用权限

```javascript
// 悬浮窗权限
let has = $permit.hasFloaty();
if (!has) { $permit.floaty(); }

// 无障碍权限
let has = $permit.hasWza();
if (!has) { $permit.wza(); }

// 外部存储权限
let has = $permit.hasSd();
if (!has) { $permit.sd(); }

// 相机权限
let has = $permit.hasCamera();
if (!has) { $permit.camera(); }

// 定位权限
let has = $permit.hasLoc();
if (!has) { $permit.loc(); }

// 录音权限
let has = $permit.hasRecord();
if (!has) { $permit.record(); }

// 通知权限
let has = $permit.hasNotifyAccess();
if (!has) { $permit.notifyAccess(); }

// 网络权限
let has = $permit.hasNet();
if (!has) { $permit.net(); }

// 短信权限
let has = $permit.hasSendSms();
if (!has) { $permit.sendSms(); }

// 读取短信权限
let has = $permit.hasReadSms();
if (!has) { $permit.readSms(); }

// 通话权限
let has = $permit.hasCall();
if (!has) { $permit.call(); }

// 系统设置权限
let has = $permit.hasSet();
if (!has) { $permit.set(); }

// 联系人权限
let has = $permit.hasReadContact();
if (!has) { $permit.readContact(); }

let has = $permit.hasWriteContact();
if (!has) { $permit.writeContact(); }

// 日历权限
let has = $permit.hasReadCalendar();
if (!has) { $permit.readCalendar(); }

let has = $permit.hasWriteCalendar();
if (!has) { $permit.writeCalendar(); }
```

### 使用提示框请求权限（推荐方式）

```javascript
if (!$permit.hasFloaty()) {
    $tip.show("获取权限", "是否获取悬浮窗权限?", () => {
        $permit.floaty();
    });
}
```

### 原生权限字符串

```javascript
// 使用 Android 原生权限字符串
let has = $permit.hasPermit(android.Manifest.permission.GET_ACCOUNTS);
$permit.getPermit(android.Manifest.permission.GET_ACCOUNTS);

// 批量权限检查
let permits = [
    "android.permission.READ_PHONE_STATE",
    "android.permission.CALL_PHONE"
];
let has = $permit.hasPermit(permits);
$permit.getPermit(permits);
```

---

## $task - 任务控制

### 路径操作

```javascript
alert("当前任务路径", $task.getPath());

// 相对路径解析
alert("相对路径", $task.getPath("./../../res"));
```

### 任务控制

```javascript
// 停止当前任务
for (let i = 0; i < 10; i++) {
    sleep(1000);
    toast("我还活着");
    if (i == 3) {
        $task.stop(); // 立即停止脚本
    }
}

// 暂停与继续（配合悬浮窗使用）
let ui = $floaty.newAdj(`
<ui>
    <linear dir="v" w="max">
        <button id="bt1" text="暂停" w="max"/>
        <button id="bt2" text="继续" w="max"/>
        <button id="bt3" text="是否活着" w="max"/>
    </linear>
</ui>
`);

ui.id("bt1").click(() => { $task.pause(); });   // 暂停
ui.id("bt2").click(() => { $task.start(); });   // 继续
ui.id("bt3").click(() => {
    info($task.isRunning() ? "我还活着" : "我已经死了");
});

for (let i = 0; i < 20; i++) {
    sleep(1000);
    info("正在运行" + i);
}
```

---

## $thread - 多线程

### 创建并启动线程

```javascript
let t1 = $thread.create(() => {
    for (let i = 0; i < 10; i++) {
        sleep(300);
        log(t1.getName() + "==>" + i);
    }
    log(t1.getName() + "执行完毕");
});

let t2 = $thread.create(() => {
    for (let i = 0; i < 10; i++) {
        sleep(300);
        log(t2.getName() + "==>" + i);
    }
});

t1.start();
t2.start();
```

### 快速在新线程中运行

```javascript
$thread.run(() => {
    sleep(3000);
    toast("延迟3秒后执行");
});
```

### 循环任务（后台定时循环）

```javascript
// 创建并启动循环任务
let t1 = $thread.loop("循环1号", () => {
    sleep(1000);
    log("我还活着！");
});
t1.start();

// 停止循环任务
$thread.stopLoop("循环1号");
// 或停止所有循环
// $thread.stopAllLoop();
```

---

## $bus - 事件总线

> 用于脚本间通信，或接收来自外部应用（如 Tasker）的广播。

### 查看监听器列表

```javascript
let monis = $bus.ls();
log(monis); // 输出: [我的监听器1号]
```

### 注册事件监听器

```javascript
$bus.event("我的监听器1号", (data) => {
    log("获得数据:", data);
    toast(data);
});
```

### 发送事件

```javascript
$bus.post("我的监听器1号", "我是数据");
```

### 关闭监听器

```javascript
$bus.close("我的监听器1号"); // 关闭指定
$bus.clear();                 // 关闭所有（等同于 stopAll()）
$bus.stopAll();               // 关闭所有
```

### 接收全局广播（来自其他 App）

```javascript
// 注册广播接收
$bus.event("broadcast", (intent) => {
    log("接受到了广播:");
    let extras = intent.getExtras();
    let value = extras.get("mKey");
    log("广播数据:" + value);
});
```

### 配合 Tasker 使用

通过 Tasker 向 AIGame 发送广播来触发脚本执行：

```
Tasker 设置：
- 操作(action)：runJs:/sdcard/main.js
- 包名(package)：org.aigame.pro
- 类名(class)：org.aigame.api.bus.receiver.AgBusReceiver
- 目标(type)：(广播)BroadcastReceiver
```

---

## $event - 系统事件监听

### 蓝牙事件

```javascript
$event.on("bluetooth", (data) => {
    log("描述：" + data.desc);
    log("设备别名：" + data.value.alias);
});
```

### 屏幕锁定事件

```javascript
$event.on("lock", (data) => {
    log("描述：" + data.desc);
    log("是否锁屏：" + data.value.lock);
    log("屏幕点亮：" + data.value.screenOn);
    log("屏幕熄灭：" + data.value.screenOff);
});
```

### 存储媒体事件

```javascript
$event.on("media", (data) => {
    log("挂载：" + data.value.mount);
    log("卸载：" + data.value.unmount);
    log("移除：" + data.value.remove);
    log("移除操作不当：" + data.value.badRemove);
});
```

### 按键事件

```javascript
// HOME键/菜单键触发
$event.on("key", (data) => {
    log(data);
});
```

### 通知监听

```javascript
if (!$permit.hasNotifyAccess()) {
    $permit.notifyAccess();
} else {
    $event.on("notify", (data) => {
        log("包名:", data.value.pkg);
        log("标题:", data.value.title);
        log("内容:", data.value.text);
        log("副文本:", data.value.subText);
        log("提示文本:", data.value.tickerText);
        log("大文本:", data.value.bigText);
        log("时间:", data.value.postTime);
        log("是否持续:", data.value.isOngoing);
        log("是否可清除:", data.value.isClearable);
    });
}
```

### 屏幕旋转事件

```javascript
$event.on("screenDir", (data) => {
    log("角度:", data.value.rotation);
    log("是否竖屏:", data.value.isVertical);
});
```

---

## $engine - 脚本引擎

> 用于在不同线程/引擎中运行其他脚本文件。

```javascript
// 在另一个引擎中运行脚本（路径示例）
let path1 = "example/$engine - 脚本引擎/01.不同线程中的路径/脚本1.js";
// 具体 API 参考官方文档
```
