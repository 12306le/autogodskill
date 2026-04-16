# API 01 - 无障碍操作 & 触控

> 模块：`$act`（无障碍）、`$touch`（Root触控）
> 返回 [README](README.md)

## 目录

- [$act - 无障碍操作](#act---无障碍操作)
  - [权限管理](#权限管理)
  - [点击操作](#点击操作)
  - [长按操作](#长按操作)
  - [滑动操作](#滑动操作)
  - [手势操作](#手势操作)
  - [系统按键](#系统按键)
  - [其他操作](#其他操作)
  - [界面监听](#界面监听)
  - [文本输入](#文本输入)
- [$touch - Root触控操作](#touch---root触控操作)

---

## $act - 无障碍操作

> Android 7+ 使用无障碍执行手势，Android 7- 自动切换为 Root 执行手势。

### 权限管理

```javascript
// 判断是否已获取无障碍权限
let has = $act.hasPermit();

if (has) {
    log("已经获得无障碍权限");
} else {
    log("请求获取无障碍权限");
    $act.getPermit(); // 请求权限（会打开设置页面）
}
```

### 点击操作

```javascript
// 点击坐标 (x, y)
$act.click(400, 348);
```

### 长按操作

```javascript
// 长按坐标 (x, y)
$act.press(400, 348);
```

### 滑动操作

```javascript
// 滑动：从 (x1,y1) 到 (x2,y2)，持续 duration 毫秒
// 示例：下拉通知栏（从顶部向下滑）
$act.move(400, 0, 400, 800, 1000);
```

### 手势操作

#### 单指手势（先长按，再滑动）

```javascript
// 注意：不推荐在 Android 7 以下使用多指手势
// Android 7- 的 Root 手势不支持多指

// g1: [startX, startY, endX, endY, startDelay, duration]
let g1 = [504, 583, 504, 583, 0, 1000];    // 先长按（起点=终点）
let g2 = [504, 583, 504, 883, 1000, 1000]; // 再滑动

$act.gesture(g1, g2);
```

#### 多指手势（模拟三指下滑）

```javascript
let g1 = [500, 900, 500, 1500, 0, 1000];
let g2 = [500, 900, 500, 1500, 0, 1000];
let g3 = [500, 900, 500, 1500, 0, 1000];
$act.gesture(g1, g2, g3);
```

### 系统按键

```javascript
sleep(2000);
$act.home();         // HOME 键（返回桌面）

sleep(2000);
$act.menu();         // 菜单键（最近任务，等同于 recent()）

sleep(2000);
$act.back();         // 返回键

sleep(2000);
$act.power();        // 电源键（息屏/亮屏）

sleep(2000);
$act.settings();     // 打开系统设置

sleep(2000);
$act.notifications(); // 打开通知栏
```

### 其他操作

```javascript
// 分屏
$act.splitScreen();

// 截屏
$act.screenshot();

// 息屏（优先用无障碍，不可用时自动切 Root）
$act.lock();
sleep(2000);
$act.unlock(); // 亮屏

// 使用 Root 版本息屏/亮屏（注释掉的示例）
// $root.lock();
// $root.unlock();
```

### 界面监听

```javascript
// 获取当前界面类名（Activity）
let curActivity = $act.activity();
log(curActivity);

// 监听界面切换
$act.activity((name) => {
    log("当前界面:", name);
});

// 20秒后关闭界面变化监听
sleep(20000);
$act.activity(null); // 传入 null 即可关闭监听
```

### 文本输入

```javascript
// 当界面中有文本框获得焦点时，直接设置内容
$act.input("需要设置的内容");
```

---

## $touch - Root触控操作

> Root 专用触控，不需要无障碍权限，但需要 Root。
> 第一次执行大概需要 4 秒，第二次瞬间执行。

### 初始化

```javascript
if ($touch.hasPermit()) {
    $touch.init(); // 初始化（仅需调用一次）
}
```

### 点击

```javascript
if ($touch.hasPermit()) {
    $touch.init();
}
$touch.click(410, 350);
```

### 长按

```javascript
if ($touch.hasPermit()) {
    $touch.init();
}
$touch.press(410, 350);
```

### 滑动

```javascript
if ($touch.hasPermit()) {
    $touch.init();
}
// 从 (400,0) 滑动到 (400,500)
$touch.move(400, 0, 400, 500);
```

---

## 注意事项

| 项目 | 说明 |
|------|------|
| Android 版本 | `$act` Android 7+ 用无障碍，7- 自动切换 Root |
| 多指手势 | 不推荐在 Android 7 以下使用多指 |
| `$touch` 初始化 | 首次需要约 4 秒，后续瞬间 |
| 坐标系 | 以屏幕左上角为原点，x 向右，y 向下 |
