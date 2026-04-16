# API 02 - UI界面 & 对话框 & 悬浮窗

> 模块：`$alert`、`$dialog`、`$tip`、`$floaty`、`$arc`、`$ui`
> 返回 [README](README.md)

## 目录

- [$alert - 警告对话框（非阻塞）](#alert---警告对话框非阻塞)
- [$dialog - 普通对话框](#dialog---普通对话框)
- [$tip - 阻塞式对话框 & 输入](#tip---阻塞式对话框--输入)
- [$floaty - 悬浮窗](#floaty---悬浮窗)
- [$arc - 悬浮菜单球](#arc---悬浮菜单球)
- [$ui - 交互界面构建](#ui---交互界面构建)

---

## $alert - 警告对话框（非阻塞）

> `$alert` 比 `$dialog` 更适合显示较大的视图，为非阻塞式对话框。

### 基础用法

```javascript
$alert.create()
    .title("标题")
    .msg("我是信息内容")
    .but1("按钮1")
    .but2("按钮2")
    .but3("按钮3")
    .show();
```

### 禁止外部点击关闭

```javascript
$alert.create()
    .title("禁止自动关闭")
    .msg("不允许通过点击外部自动关闭对话框")
    .but3("取消")
    .cancelable(false)
    .show();
```

### 列表单选（items）

```javascript
// 注意：使用了 items 就不能再使用 msg
$alert.create()
    .title("单选")
    .items(["选项1", "选项2", "选项3"], (di, which) => {
        info("选中了:" + which);
    })
    .but3("取消")
    .cancelable(false)
    .show();
```

### 单选按钮（oneItems，有默认选中）

```javascript
$alert.create()
    .title("单选")
    .oneItems(
        ["选项1", "选项2", "选项3"],
        0,  // 默认选中第一个
        (di, which) => {
            info("选中了:" + which);
        })
    .but3("取消")
    .cancelable(false)
    .show();
```

### 多选（moreItems）

```javascript
// 基础多选
$alert.create()
    .title("多选")
    .moreItems(
        ["选项1", "选项2", "选项3"],
        (di, which) => {
            info("选中了:" + which);
        })
    .but3("取消")
    .cancelable(false)
    .show();

// 带默认选中状态的多选
$alert.create()
    .title("多选（有默认值）")
    .moreItems(
        ["选项1", "选项2", "选项3"],
        [true, true, false], // 默认选中前两个
        (di, which) => {
            info("选中了:" + which);
        })
    .but3("取消")
    .cancelable(false)
    .show();
```

### 设置图标

```javascript
$alert.create()
    .title("设置图标")
    .icon("logo_ag")       // 图标名称
    .msg("看看我的图标")
    .but3("取消")
    .cancelable(false)
    .show();
```

### 自定义视图

```javascript
let mAlert = $alert.create();

let ui = $ui.layout(`
<ui w="max">
    <button id="mButton1" style="text" text="点我试试" w="max"/>
    <button id="mButton2" text="关闭对话框" style="text" w="max" />
</ui>
`);

ui.id("mButton1").click(() => {
    info("我被点击了");
});

ui.id("mButton2").click(() => {
    mAlert.close(); // 关闭对话框
});

let mView = ui.getView();

mAlert
    .cancelable(false)  // 禁止外部点击关闭（务必提供关闭方式）
    .view(mView)        // 设置自定义布局
    .show();
```

---

## $dialog - 普通对话框

> 与 `$alert` 用法基本相同，适合普通大小的对话框。

### 基础用法

```javascript
$dialog.create()
    .title("标题")
    .msg("我是信息内容")
    .but1("按钮1")
    .but2("按钮2")
    .but3("按钮3")
    .show();
```

### 单选 / 多选 / 禁止关闭

> 与 `$alert` 完全相同，将 `$alert` 替换为 `$dialog` 即可。

```javascript
$dialog.create()
    .title("单选")
    .items(["选项1", "选项2", "选项3"], (di, which) => {
        info("选中了:" + which);
    })
    .but3("取消")
    .cancelable(false)
    .show();
```

### 自定义视图

```javascript
let dialog = $dialog.create();

let ui = $ui.layout(`
<ui w="max">
    <button id="mButton1" style="text" text="点我试试" w="max"/>
    <button id="mButton2" text="关闭对话框" style="text" w="max" />
</ui>
`);

ui.id("mButton2").click(() => {
    dialog.close();
});

dialog
    .cancelable(false)
    .view(ui.getView())
    .show();
```

---

## $tip - 阻塞式对话框 & 输入

> `$tip` 是阻塞式的，调用后脚本会暂停直到用户操作完成。

### 信息显示

```javascript
$tip.i("信息");    // 信息级别
$tip.d("调试");    // 调试级别
$tip.w("警告");    // 警告级别
$tip.e("异常");    // 错误级别
$tip.v("冗余");    // 冗余级别
```

### 简单对话框

```javascript
// 无按钮（只显示内容）
$tip.show("标题", "我是你的AIGame助手");

// 有确认按钮
$tip.show("标题", "我是你的AIGame助手", () => {
    toast("你点了确认");
});
```

### 输入框

```javascript
// 无默认值
$tip.input("请输入你的名字", (value) => {
    toast("输入的内容:" + value);
});

// 有默认值
$tip.input("请输入你的名字", "张三", (value) => {
    toast("输入的内容:" + value);
});
```

### 单选列表

```javascript
let arr = ["小狗", "小猫", "小猪"];
$tip.one("请选择", arr, (value) => {
    toast("你选择了:" + value);
});
```

### 多选列表

```javascript
let arr = ["小狗", "小猫", "小猪"];
$tip.more("请选择", arr, (values) => {
    toast("你选择了:" + values);
});
```

### 日期选择

```javascript
// 日历选择器
$tip.calendar((info) => {
    let year = info.year;   // 或 info.y
    let month = info.month; // 或 info.m
    let day = info.day;     // 或 info.d
    alert("日期", year + "-" + month + "-" + day);
});

// 日期选择（同 calendar）
$tip.date((info) => {
    alert("日期", info.y + "-" + info.m + "-" + info.d);
});
```

### 时间选择

```javascript
// 24小时制
$tip.clock((info) => {
    let hour = info.hour;     // 或 info.h
    let minute = info.minute; // 或 info.m
    alert("时间", hour + ":" + minute);
});

// 同 clock
$tip.time((info) => {
    alert("时间", info.h + ":" + info.m);
});
```

### 自定义视图

```javascript
let ui = $ui.layout("path/to/ui.xml");
let view = ui.getView();

// 显示自定义视图（有确认按钮）
$tip.show("自定义对话框", view, () => {
    toast("保存成功");
});

// 显示自定义视图（无按钮）
$tip.show("自定义对话框", view);
```

---

## $floaty - 悬浮窗

> 需要悬浮窗权限：`$floaty.getPermit()`

### 获取权限

```javascript
$floaty.getPermit();
```

### 可调节悬浮窗（newAdj）

> 用户可以拖动调整位置。

```javascript
let floaty = $floaty.newAdj(`
<ui>
    <linear dir="v" w="max">
        <button text="按钮1" w="max"/>
        <button text="按钮2" w="max"/>
        <button id="closeButton" text="关闭" w="max"/>
    </linear>
</ui>
`);

floaty.id("closeButton").click(() => {
    floaty.close();
});
```

### 应用悬浮窗（newApp）

```javascript
$floaty.closeAll(); // 先关闭之前的悬浮窗

let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max" bg="#33FF0000">
        <button id="mButton" text="关闭" ripper="#FFFFFF" />
        <button id="mBut1" text="全屏" ripper="#FFFFFF" />
        <button id="mBut2" text="非全屏" ripper="#FFFFFF" />
        <button id="mBut3" text="取消触摸" ripper="#FFFFFF" />
        <button id="mBut4" text="修改位置" ripper="#FFFFFF" />
    </linear>
</ui>
`);

floaty.id("mButton").click(() => floaty.close());
floaty.id("mBut1").click(() => floaty.fill(true));   // 全屏
floaty.id("mBut2").click(() => floaty.fill(false));  // 非全屏
floaty.id("mBut3").click(() => {
    floaty.touch(false); // 取消触摸（3秒后恢复）
    $thread.run(() => {
        sleep(3000);
        floaty.touch(true);
        toast("开启触摸啦");
    });
});
floaty.id("mBut4").click(() => floaty.setXY(300, 400)); // 修改位置
```

### 全屏触摸坐标获取器（实用示例）

```javascript
$floaty.closeAll();
alert("提示", "触摸屏幕，获取坐标，点击关闭后复制到剪切板");

let floaty = $floaty.newApp(`
<ui>
    <linear id="mLinear" w="max" h="max" gravity="center">
        <text id="mText"/>
        <button id="mButton" text="关闭" ripper="#FFFFFF" />
        <img id="mImg" src="ic_record" tint="colorPrimary" />
    </linear>
</ui>
`);

let x = 0;
let y = 0;

floaty.fill(true);
floaty.id("mLinear").getView().setOnTouchListener((view, event) => {
    x = Math.round(event.getRawX());
    y = Math.round(event.getRawY());
    floaty.id("mText").setText(x + "," + y);
    let img = floaty.id("mImg");
    img.setX(x - img.getW() / 2);
    img.setY(y - img.getH() / 2);
    return true;
});

floaty.id("mButton").click(() => {
    floaty.close();
    setClip(x + "," + y);
    toast("坐标复制完成");
});
```

### 系统级悬浮窗（newSys）

> 用法与 `newApp` 完全相同，权限级别更高。

```javascript
$floaty.closeAll();
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max" bg="#33FF0000">
        <button id="mButton" text="关闭" ripper="#FFFFFF" />
    </linear>
</ui>
`);
floaty.id("mButton").click(() => floaty.close());
```

### 区域选择悬浮窗

```javascript
$floaty.newSelect((rect) => {
    log("用户选择范围:", rect);
});
```

### 关闭悬浮窗

```javascript
floaty.close();      // 关闭指定悬浮窗
$floaty.closeAll();  // 关闭所有悬浮窗
```

---

## $arc - 悬浮菜单球

> 圆形悬浮菜单，可添加多个小按钮。

### 基础用法

```javascript
let myName = "悬浮球1号";

if (!$arc.has(myName)) { // 避免重复创建
    let menuBody = $arc.body(myName); // 创建容器（指定名称）

    // 创建小按钮（参数为图标名称）
    let menu1 = $arc.item("logo").bg("#55FFFFFF");
    let menu2 = $arc.item("ic_color_lens_outline").bg("#FAFDFA");
    let menu3 = $arc.item("ic_play_arrow_outline");
    let menu4 = $arc.item("ic_cloud_upload_outline").bg("#C7DFD9");
    let menu5 = $arc.item("ic_clear_outline").style("outline").iconTint("#FF0000");

    // 设置样式（方法2：链式调用）
    menu3.radius(15).iconSize(80).iconPadding(0).iconTint("#57965C").bg("#55FFFFFF");

    // 绑定点击事件（切换图标）
    let play = false;
    menu3.click(() => {
        if (play) {
            menu3.icon("ic_play_arrow_outline").iconTint("#57965C");
            play = false;
        } else {
            menu3.icon("ic_stop_fill").iconTint("#FF0000");
            play = true;
        }
    });

    // 关闭按钮
    menu5.click(() => {
        $arc.closeAll(); // 关闭所有悬浮菜单
    });

    // 向容器添加按钮并显示
    menuBody
        .add(menu1)
        .add(menu2)
        .add(menu3)
        .add(menu4.iconTint("#F2C55C")) // 方法3：添加时设置样式
        .add(menu5)
        .show();
} else {
    log(myName + "已存在");
}
```

### 关闭悬浮菜单球

```javascript
$arc.close("悬浮球1号"); // 关闭指定名称
$arc.closeAll();          // 关闭全部
```

---

## $ui - 交互界面构建

> 使用 XML 构建 Android 原生界面。

### 基本结构

```javascript
let ui = $ui.layout(`
<ui>
    <statusbar/>
    <appbar back="true" id="mAppbar" title="我的界面" w="max"/>
    <linear dir="v" w="max" h="max" gravity="center">
        <button id="mBtn" text="点击我" w="max"/>
        <text id="mText" text="Hello AIGame" />
    </linear>
</ui>
`);

// 绑定事件
ui.id("mBtn").click(() => {
    ui.id("mText").setText("被点击了！");
});

// 返回按钮
ui.id("mAppbar").back(() => {
    ui.finish();
});

ui.show();
```

### 从 XML 文件加载

```javascript
let ui = $ui.layout("path/to/ui.xml");
ui.id("mAppbar").back(() => { ui.finish(); });
ui.show();
```

### 动态添加/删除视图

```javascript
let mainUi = $ui.layout(`
<ui>
    <statusbar/>
    <nested w="max">
        <linear w="max" id="mLayout" />
    </nested>
</ui>
`);
let mLayout = mainUi.id("mLayout");

$thread.create(() => {
    for (let i = 0; i < 10; i++) {
        sleep(1000);
        let itemUi = $ui.layout(`
            <ui>
                <card w="max" id="mCard" margin="3">
                    <text text="我是卡片" margin="15" />
                </card>
            </ui>
        `);
        mLayout.addView(itemUi.id("mCard")); // 动态添加
    }
    mLayout.removeAll(); // 移除所有子视图
    mainUi.finish();
}).start();

mainUi.show();
```

### 列表控件（ls）

```javascript
let ui = $ui.layout("path/to/list_ui.xml");
ui.id("mAppbar").back(() => { ui.finish(); });
ui.show();

let ls = ui.id("mLs");

// 绑定数据适配器（优先调用）
ls.bindHolder((holder, data, position) => {
    holder.id("mText").setText(data);

    // 删除按钮
    holder.id("delBut").click(() => {
        $tip.show("删除", "确定删除：" + data + "吗?", () => {
            ls.del(position);
        });
    });

    // 修改按钮
    holder.id("edtBut").click(() => {
        $tip.input("修改名称", data, (value) => {
            ls.flush(value, position);
        });
    });
});

// 设置数据
ls.flush(["张三", "李四", "王五"]);

// 动态添加
ls.add("数据新增");
ls.add("数据", 1); // 添加到指定位置

// 滚动控制
ls.scrollBottom(); // 滚动到底部
ls.scrollTop();    // 滚动到顶部
ls.scroll(2);      // 滚动到指定位置
```

### 滑动页面（pager + tab）

```javascript
let ui = $ui.layout("path/to/pager_ui.xml");
let mPager = ui.id("mPager");
let mTab = ui.id("mTab");

// 联动绑定
if (mPager != null && mTab != null) {
    mPager.bind(mTab);
}
ui.show();
```

### $ui 支持的 XML 组件列表

| 组件标签 | 说明 |
|----------|------|
| `appbar` | 顶部应用栏 |
| `button` | 按钮 |
| `button-group` | 按钮组 |
| `card` | 卡片 |
| `check` | 多选框 |
| `chip` | 小片 |
| `chip-group` | 小片组 |
| `drop` | 下拉框 |
| `edit` | 编辑器 |
| `fab` | 悬浮按钮 |
| `hr` | 分割线 |
| `img` | 图片 |
| `input` | 输入框 |
| `ls` | 列表 |
| `nav` | 导航栏 |
| `pager` | 滑动页面 |
| `progress` | 进度条 |
| `radio` | 单选按钮 |
| `radio-group` | 单选按钮组 |
| `rail` | 轨道工具栏 |
| `range` | 范围条 |
| `slider` | 拖拽条 |
| `statusbar` | 状态栏 |
| `switch` | 开关 |
| `toolbar` | 工具栏 |
| `webview` | 网页控件 |
| `log` | 日志显示控件 |
| `video` | 视频 |
| `nested` | 可嵌套滚动容器 |
| `linear` | 线性布局（dir="v"\|"h"） |
