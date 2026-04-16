# API 06 - 截屏 & 图像 & 颜色 & OCR & 绘图

> 模块：`$screen`、`$img`、`$canvas`、`$draw`、`$color`、`$ocr`
> 返回 [README](README.md)

## 目录

- [$screen - 截屏 & 屏幕信息](#screen---截屏--屏幕信息)
- [$img - 图片处理](#img---图片处理)
- [$color - 颜色工具](#color---颜色工具)
- [$ocr - 文字识别](#ocr---文字识别)
- [$canvas - 画布绘图](#canvas---画布绘图)
- [$draw - 屏幕悬浮绘制](#draw---屏幕悬浮绘制)

---

## $screen - 截屏 & 屏幕信息

### 获取截屏权限

```javascript
// 如果没有无障碍权限，则获取录屏权限（阻塞直到获取）
if (!$act.hasPermit()) {
    $screen.getPermit();
}

// 检查是否有录屏权限
$screen.hasPermit();
```

### 截屏

```javascript
// 截屏（优先无障碍，没有则用录屏权限）
let img = $screen.getScreen();
if (img != null) {
    img.show(); // 显示截图
}

// 截屏并保存
let imgPath = "/sdcard/Pictures/截屏.png";
$screen.save(imgPath);
```

### 屏幕信息

```javascript
let w = $screen.getWidth();  // 屏幕宽度
let h = $screen.getHeight(); // 屏幕高度
alert("屏幕宽高", w + "x" + h);

// 详细屏幕信息（包含 w, h, density 等）
let info = $screen.getScreenInfo();
$tip.show("详细信息", info.toString());

// 屏幕密度
let density = $screen.getDensity();
```

### 屏幕状态

```javascript
if ($screen.isScreenOff()) {
    toast("屏幕息屏");
}
if ($screen.isScreenOn()) {
    toast("屏幕亮屏");
}
```

### 屏幕亮度 & 方向

```javascript
// 设置屏幕亮度（0~255）
$screen.bright(100);

// 设置屏幕方向
$screen.dir(0);    // 竖屏
$screen.dir(90);   // 右转横屏
$screen.dir(180);  // 倒置竖屏
$screen.dir(270);  // 左转横屏
$screen.dir(-1);   // 自动旋转
```

---

## $img - 图片处理

### 读取图片

```javascript
let img = $img.read("example/$img - 图片处理/img/t01.png");
img.show(); // 显示图片
```

### 二值化处理

```javascript
let img = $img.read("example/$img - 图片处理/img/t01.png");
let resultImg = $img.threshold(img, 100); // 阈值：100
resultImg.show(); // 显示二值化结果
```

### 获取像素颜色

```javascript
let img = $img.read("path/to/image.png");
let color = img.pixel(x, y); // 获取坐标 (x,y) 的颜色值
log("颜色:" + color);
log("颜色代码:" + $color.str(color));
```

### 多点找色（findMultiColors）

```javascript
let img = $img.read("example/$img - 图片处理/img/t02.png");

// 参数：图片, 查找范围(null=全图), 主色, 相似度, [偏移x, 偏移y, 颜色, 相似度, ...]
let result = $img.findMultiColors(img, null, "#E9AF6D", 5, [
    -10, 1, "#908E8A", 5,
    -4, -8, "#908E8A", 5,
    -18, -4, "#FBFBFB", 5
]);
alert("执行结果", result);
```

---

## $color - 颜色工具

### 找色（单色）

```javascript
// 前提：已有截图 img（$screen.getScreen() 获取）
let img = $screen.getScreen();

// 基础找色
let result = $color.find(img, "#d87d83");
if (result != null) {
    $draw.dot(result); // 绘制找到的位置
    $draw.log(result);
    sleep(3000);
    $draw.closeAll();
}

// 带相似度和范围的找色
// 参数：图片, 颜色, 相似度(0~10,越小越精确), 范围([x,y,w,h] 或 [] 全屏)
let result = $color.find(img, "#d87d83", 5, []);
```

### 找色（全部位置）

```javascript
let img = $screen.getScreen();

// 找出所有匹配位置
let result = $color.findAll(img, "#d28384");
if (result != null) {
    for (let index of result) {
        $draw.dot(index);
        $draw.log(index);
        sleep(300);
    }
    sleep(5000);
    $draw.closeAll();
}

// 带参数版本
let result = $color.findAll(img, "#d28384", 5, []);
```

### 颜色比较

```javascript
// 计算两个颜色的相似度
let result = $color.similar("#1E1F22", "#2B2D30");
alert("相似度", result);

// 判断两个颜色是否相同
let same = $color.equals("#1E1F22", -14803166);
if (same) {
    alert("比较颜色", "颜色相同");
}
```

### 颜色转换

```javascript
// 整数颜色值 → 8位十六进制字符串（#AARRGGBB）
let color1 = $color.toString(-166780);
// 整数颜色值 → 6位十六进制字符串（#RRGGBB）
let color2 = $color.str(-166780);

alert("8位颜色值", color1);
alert("6位颜色值", color2);
```

### 颜色解析

```javascript
// 十六进制字符串 → 整数颜色值
let colorValue1 = $color.parse("#784cde");
// RGB 分量 → 整数颜色值
let colorValue2 = $color.parse(105, 78, 230);
let colorValue3 = $color.rgb(105, 78, 230);
// ARGB → 整数颜色值
let colorValue4 = $color.argb(255, 105, 78, 230);
```

### 提取颜色分量

```javascript
let a = $color.a("#357C94"); // Alpha 通道
let r = $color.r("#357C94"); // Red 通道
let g = $color.g("#357C94"); // Green 通道
let b = $color.b("#357C94"); // Blue 通道

alert("解析通道", `a=${a}\nr=${r}\ng=${g}\nb=${b}`);
```

### 内置颜色常量

```javascript
$color.RED    // 红色
$color.GREEN  // 绿色
$color.BLUE   // 蓝色
$color.BLACK  // 黑色
$color.WHITE  // 白色
// 等等...
```

---

## $ocr - 文字识别

> 支持两种引擎：`mlkit`（无需初始化）和 `ncnn`（需要初始化）。

### 设置 OCR 引擎

```javascript
$ocr.v("mlkit"); // 使用 mlkit 引擎（推荐，无需初始化）
$ocr.v("ncnn");  // 使用 ncnn 引擎（需要先调用 $ocr.init()）
$ocr.init();     // ncnn 引擎初始化（仅 ncnn 需要）
```

> 注意：mlkit 无法计算相似度，`similar` 固定为 0.85。

### 灰度化识别（截屏区域）

```javascript
// 前提：获取截屏权限
$screen.getPermit();
$ocr.v("mlkit");

// 展示要识别的图片
showImg("./example/$ocr - 文字识别/imgs/t01.png");

// 计算识别范围
let si = $screen.getScreenInfo();
let re = [0, si.h / 3, si.w, si.h / 3]; // [x, y, width, height]

// 绘制识别范围（可选，用于调试）
$draw.rect(re[0], re[1], re[2], re[3]);

sleep(1000); // 等待图片显示

// 开始识别
let result = $ocr.detect({
    region: [re[0], re[1], re[2], re[3]],
    gray: true,                      // 开启灰度化
    save: true,                      // 保存处理后的图片（可选）
    savePath: "/sdcard/ocr-gray.png" // 保存路径（可选）
});

alert("识别结果", result);
$draw.closeAll();
```

### 二值化识别（截屏区域）

```javascript
$screen.getPermit();
$ocr.v("mlkit");
showImg("./example/$ocr - 文字识别/imgs/t02.png");

let si = $screen.getScreenInfo();
let re = [0, si.h / 3, si.w, si.h / 3];
$draw.rect(re[0], re[1], re[2], re[3]);
sleep(1000);

let result = $ocr.detect({
    region: [re[0], re[1], re[2], re[3]],
    gray: false,                         // 关闭灰度化（使用二值化）
    color: "#356EFF",                    // 必须：主要颜色（蓝色）
    threshold: 30,                       // 必须：二值化阈值
    save: true,
    savePath: "/sdcard/ocr-thre.png"
});

alert("识别结果", result);

if ($file.exists("/sdcard/ocr-thre.png")) {
    showImg("/sdcard/ocr-thre.png"); // 显示二值化后的图片
}
$draw.closeAll();
```

### 识别本地图片文件

```javascript
$ocr.v("mlkit");
let res = $ocr.detectPath("./example/$ocr - 文字识别/imgs/t01.png");
alert("识别结果", res);
```

### 使用 ncnn 引擎

```javascript
$screen.getPermit();
$ocr.v("ncnn");
$ocr.init(); // ncnn 需要初始化

let si = $screen.getScreenInfo();
let re = [0, si.h / 3, si.w, si.h / 3];
sleep(1000);

// 灰度化识别
let result = $ocr.detect({
    region: [re[0], re[1], re[2], re[3]],
    gray: true
});
alert("识别结果", result);

// 识别本地图片
let res = $ocr.detectPath("./path/to/image.png");
alert("识别结果", res);
```

### 参数说明

| 参数 | 类型 | 说明 |
|------|------|------|
| `region` | `[x, y, w, h]` | 识别区域（相对于屏幕） |
| `gray` | boolean | `true` 灰度化，`false` 二值化 |
| `color` | string | 二值化时必须：主要颜色（十六进制） |
| `threshold` | int | 二值化时必须：阈值（0~255） |
| `save` | boolean | 是否保存处理后的图片 |
| `savePath` | string | 保存路径 |

---

## $canvas - 画布绘图

> 在内存中创建图片，可绘制文字、形状、图表等。

### 创建画布

```javascript
// 创建空白画布（宽, 高）
let canvas = $canvas.create(500, 500);

// 基于已有图片创建画布
let canvas = $canvas.create("path/to/image.jpg");
```

### 创建画笔

```javascript
let paint = $canvas.paint();              // 默认黑色
let paint = $canvas.paint("#FF0000");     // 指定颜色
let paint = $canvas.paint($color.RED);   // 使用颜色常量

// 设置属性
paint.setColor($color.RED);  // 设置颜色
paint.setTextSize(25);       // 设置文字大小
```

### 绘制图形

```javascript
// 绘制矩形（left, top, right, bottom）
canvas.drawRect(30, 30, 400, 400, paint);

// 绘制文字（text, x, y）
canvas.drawText("Hello AIGame", 100, 100, paint);

// 绘制多条线（[x1,y1,x2,y2, x1,y1,x2,y2, ...] 数组）
canvas.drawLines([1,1,500,1, 1,1,1,500], paint);
```

### 显示 / 保存

```javascript
canvas.show();                  // 在悬浮窗中显示（需要悬浮窗权限）
canvas.save("/sdcard/output.jpg"); // 保存到文件

// 转换为图片对象
let img = canvas.toImg();
$img.show(img); // 等同于 canvas.show()

// 获取 Bitmap 对象（用于 UI 显示）
let bitmap = canvas.getBitmap();
ui.id("mImg").setImg(bitmap); // 在布局中显示
```

### 综合示例：填写合同

```javascript
// 基于合同图片创建画布
let canvas = $canvas.create("example/合同.jpg");

// 创建黑色画笔
let paint = $canvas.paint("#000000");
paint.setTextSize(25);

// 在指定坐标填写文字
canvas.drawText("张三丰", 170, 145, paint);
canvas.drawText("420321200006524388", 480, 145, paint);
canvas.drawText("13564962035", 900, 145, paint);
canvas.drawText("翻斗花园2号街A501", 170, 195, paint);

canvas.show();
canvas.save("/sdcard/新合同.jpg");
```

### 综合示例：生成验证码

```javascript
let size = 20;
let canvas = $canvas.create(100, size + 10);

// 生成6位随机验证码
let vcode = random(10) + "" + random(10) + random(10) + random(10) + random(10) + random(10);

let txtPaint = $canvas.paint("#000000");
txtPaint.setTextSize(size);

canvas.drawText(vcode, 0, size, txtPaint);
canvas.show();
```

### 综合示例：绘制表格

```javascript
let aw = 750;  // 表格宽度
let ah = 750;  // 表格高度
let canvas = $canvas.create(aw, ah);

// 绘制表格线条（四条边框 + 分隔线）
let tabs = [
    1, 1, aw - 2, 1,         // 上边框
    1, 1, 1, ah - 2,         // 左边框
    1, ah - 2, aw - 2, ah-2, // 下边框
    aw-2, 1, aw-2, ah-2,     // 右边框
    1, 46, aw - 2, 46,       // 第1行底部横线
];
canvas.drawLines(tabs, $canvas.paint("#000000"));

// 绘制文字
let txtPaint = $canvas.paint("#000000");
txtPaint.setTextSize(20);
canvas.drawText("姓名", 10, 30, txtPaint);
canvas.drawText("身份证号", 160, 30, txtPaint);

canvas.show();
```

---

## $draw - 屏幕悬浮绘制

> 在屏幕上叠加显示图形（悬浮窗方式，需要悬浮窗权限）。

### 基础图形绘制

```javascript
$draw.closeAll(); // 先关闭之前的绘制

// 绘制矩形（x, y, w, h）
$draw.rect(200, 200, 200, 100);
// 向外拓展 50 像素的矩形
$draw.rect(200, 200, 200, 100, 50);

// 绘制圆形（x, y, radius）
$draw.circle(350, 400, 100);
// 向外拓展 50 像素
$draw.circle(350, 400, 100, 50);

// 绘制准心（十字）
$draw.cross(400, 500);

// 绘制点
$draw.dot(400, 500);

// 绘制文字
$draw.text("Hello aigame!", 400, 300);
$draw.text("Hello aigame!", 400, 400, 20); // 文字大小 20px

// 绘制线条（x1, y1, x2, y2）
$draw.line(300, 0, 100, 1000);
```

### 绘制路径（折线/曲线）

```javascript
// 绘制爱心路径
function generateHeartCoordinates(size, offsetX, offsetY) {
    const coordinates = [];
    for (let t = 0; t < 2 * Math.PI; t += 0.01) {
        let x = 16 * Math.pow(Math.sin(t), 3);
        let y = 13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t);
        x = x * size / 32 + size / 2 + offsetX;
        y = -y * size / 32 + size / 2 + offsetY;
        coordinates.push([Math.round(x), Math.round(y)]);
    }
    return coordinates;
}

const heartCoordinates = generateHeartCoordinates(250, 300, 260);
$draw.path(heartCoordinates);
```

### 日志显示

```javascript
$draw.i("信息");  // 信息（蓝色）
$draw.d("调试");  // 调试（灰色）
$draw.w("警告");  // 警告（黄色）
$draw.e("异常");  // 错误（红色）
$draw.v("冗余");  // 冗余（绿色）

// 显示对象的位置（常与找色/找图配合）
$draw.log(result); // result 是包含 x,y 的坐标对象
```

### 动态绘制（清空不销毁）

```javascript
$draw.closeAll(); // 销毁所有悬浮绘制窗
sleep(1000);

let speed = 3;
// 动态的绘制一个移动的点
for (let i = 0; i < $screen.getWidth(); i += speed) {
    $draw.dot(i, 500);
    sleep(10);
    $draw.clear(); // 只清空绘制内容，不销毁悬浮窗
}

sleep(1000);
$draw.closeAll(); // 最终销毁悬浮窗
```

### 关闭绘制

```javascript
$draw.clear();    // 清空绘制内容（悬浮窗保留）
$draw.closeAll(); // 销毁所有悬浮绘制窗
$draw.closeLog(); // 关闭日志显示
```
