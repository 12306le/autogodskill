# 媒体与工具 API

> 媒体播放、语音朗读、二维码、颜色操作、日期工具。

## 目录
- [$media - 媒体播放](#media---媒体播放)
- [TtsOptions - 语音配置](#ttsoptions---语音配置)
- [$tts - 语音阅读](#tts---语音阅读)
- [QrOptions - 二维码配置](#qroptions---二维码配置)
- [$qr - 二维码工具](#qr---二维码工具)
- [$color - 颜色操作](#color---颜色操作)
- [DateInfo - 日期信息](#dateinfo---日期信息)
- [$date - 日期工具](#date---日期工具)

---

## $media - 媒体播放

- 更新时间:2026-01-30 19:32:54

> 媒体播放




#### play(path)

> 播放音频
> 
> 直接播放音频，播放结束之后我将自动回收音频资源。
> 
> 注意:如果音频资源加载失败会返回null，资源文件已经处于播放状态也会返回null(不过一般不会出现这个情况，因为每次调用play函数的时候都会重新创建新的媒体播放器，因此播放状态也是未播放的)。

- 参数 : path {string} 音频路径(支持相对路径) 
- 返回 : {MediaPlayer} 媒体播放器
- 版本 : 1.5.2


```javascript
$media.play("res/mTip.mp3");
```


#### create()

> 创建媒体播放器
> 
> 当你拿到MediaPlayer对象之后，它的所有方法请参考{android.media.MediaPlayer}类

- 返回 : {MediaPlayer} 媒体播放器
- 版本 : 1.5.2


```javascript
let mediaPlayer = $media.create();
//常用的{MediaPlayer}方法有:其他方法请参考{android.media.MediaPlayer}类
//mediaPlayer.isPlaying();//是否处于播放状态
//mediaPlayer.isLooping();//是否是循环播放
//mediaPlayer.start();//开始播放
//mediaPlayer.stop();//停止播放
//mediaPlayer.getDuration();//总时长
//mediaPlayer.getCurrentPosition();//当前进度
//mediaPlayer.seekTo(long,int);//跳转到进度
//mediaPlayer.seekTo(int);//跳转到进度
//mediaPlayer.prepare();//准备资源
//mediaPlayer.reset();//重置
//mediaPlayer.release();//释放资源
```


#### create(path)

> 创建媒体播放器
> 
> 创建媒体播放器，并且加载音频路径，如果加载成功则返回媒体播放器，如果加载失败则返回null。

- 参数 : path {string} 音频路径(支持相对路径) 
- 返回 : {MediaPlayer} 媒体播放器
- 版本 : 1.5.2


#### setPath(mediaPlayer, path)

> 为媒体播放器设置音频路径
> 
> 如果音频资源没有找到，则会返回false，如果成功设置，则会准备音频，并且返回true。
> 
> 如果此函数被重复调用，可能会抛出异常。

- 参数 : mediaPlayer {MediaPlayer} 媒体播放器 
- 参数 : path {string} 音频路径 
- 返回 : {boolean} 是否设置成功
- 版本 : 1.5.2

---

## TtsOptions - 语音配置

- 更新时间:2026-01-30 19:32:57

> TtsOptions - 语音配置




#### const {float} rate;

> 播放倍速


#### const {float} pitch;

> 音调


#### const {float} volume;

> 音量


#### const {String} language;

> 语言
> 
> 可选值有：zh,en,fr,de,it,ja,ko
> 
> 分别意思：中文,英文,法文,德文,意大利文,日文,韩文


#### const {String} streamType;

> 播放流类型
> 
> 可选值有：alarm,music,notification,ring,system,call,dtmf
> 
> 分别意思：闹钟,音乐,通知,铃声,系统,通话,DTMF

---

## $tts - 语音阅读

- 更新时间:2026-01-30 19:32:57

> 语音阅读




#### read(text, options)

> 播放文本(配置)
> 
> 对于没有TTS引擎的设备而言，此函数执行后无任何效果

- 参数 : text {string} 文本
- 参数 : options {TtsOptions} 配置
- 版本 : 1.0.0


```javascript
let options = {
    rate: 1,//速度
    pitch: 1,//音调
    volume: 1,//音量
    language: "zh",//语言
    streamType: "system"//播放流('system'播放声音最大)
}
$tts.read("你好呀，早安~",options);
```


#### read(text)

> 播放文本
> 
> 对于没有TTS引擎的设备而言，此函数执行后无任何效果

- 参数 : text {string} 文本
- 版本 : 1.0.0


```javascript
$tts.read("你好呀，早安~");
```

---

## QrOptions - 制作二维码配置

- 更新时间:2026-01-30 19:32:54

> 制作二维码配置




#### const {Integer} w;

> 宽度(默认500)


#### const {Integer} h;

> 高度(默认500)


#### const {Integer} margin;

> 边距(默认2)


#### const {String} foreColor;

> 前景颜色(默认#000000)


#### const {String} bgColor;

> 背景颜色(默认#FFFFFF)

---

## $qr - 二维码工具

- 更新时间:2026-01-30 19:32:54

> 二维码工具
> 
> 使用$qr你可以实现制作二维码，或者识别二维码




#### make(content)

> 制作二维码

- 参数 : content {string} 二维码内容 
- 返回 : {Image} 图片对象
- 版本 : 1.2.3


```javascript
//生成二维码
let img = $qr.make("欢迎来到AIGame!");
//显示图片
img.show();//或者调用 showImg(img); 全局函数也可也显示图片
//保存到本地
img.save("/sdcard/qr.png");
```


#### make(content, options)

> 制作二维码

- 参数 : content {string} 二维码内容 
- 参数 : options {QrOptions} 参数 
- 返回 : {Image} 图片对象
- 版本 : 1.2.3


```javascript
//生成二维码
let img = $qr.make("Hello AIGame !", {
    w: 500,//宽度(默认:500)
    h: 500,//高度(默认:500)
    margin: 2,//边距(默认:2)
    foreColor: "#2AACB8",//前景色(默认:#000000)
    bgColor: "#2B2D30",//背景色(默认:#FFFFFF)
});
if (img != null) {
    //显示图片
    img.show(); //或者调用 showImg(img); 全局函数也可也显示图片
    //保存到本地
    img.save("/sdcard/qr.png");
}
```


#### parse(path)

> 解析二维码

- 参数 : path {string} 图片路径 
- 返回 : {string} 二维码内容
- 版本 : 1.2.3


```javascript
let content = $qr.parse("/sdcard/qr.png");
```


#### parse(image)

> 解析二维码

- 参数 : image {Image} 图片对象 
- 返回 : {string} 二维码内容
- 版本 : 1.2.3


```javascript
//获得image对象
let img = $img.read("/sdcard/qr.png");
//识别image对象
let content = $qr.parse(img);
```


#### parse(x, y, w, h)

> 解析屏幕上的二维码
> 
> 根据传入的范围来解析屏幕上的二维码,需要截屏权限

- 参数 : x {int} x坐标 
- 参数 : y {int} y坐标 
- 参数 : w {int} 宽度 
- 参数 : h {int} 高度 
- 返回 : {string} 二维码内容
- 版本 : 1.2.3


```javascript
//截屏后识别指定范围的二维码
let content = $qr.parse(0,400,1080,600);
```


#### parse(region)

> 解析屏幕上的二维码
> 
> 根据传入的范围来解析屏幕上的二维码,需要截屏权限

- 参数 : region {int[]} 范围 
- 返回 : {string} 二维码内容
- 版本 : 1.2.3


```javascript
//截屏后识别指定范围的二维码
let content = $qr.parse([0,400,1080,600]);
```


#### parse(rect)

> 解析屏幕上的二维码
> 
> 根据传入的范围来解析屏幕上的二维码,需要截屏权限

- 参数 : rect {rect} opencv的范围对象
- 返回 : {string} 二维码内容
- 版本 : 1.2.3


```javascript
//使用opencv中的范围对象
let rect = new org.opencv.core.Rect(0, 400, 1080, 600);
//解析截屏范围中的二维码
let content = $qr.parse(rect);
```

---

## $color - 颜色操作

- 更新时间:2026-01-30 19:32:51

> 颜色操作
> 
> 在$color中内置了很多常用的颜色，并且也有依据当前app主题动态获取对应颜色值的函数，尤其是在ui开发的过程中使用较多。
> 
> $color主要用来解析颜色，对比颜色，获取亮色暗色，为颜色设置透明度等等功能。




#### const {int} BLACK;

> 黑色


#### const {int} DGRAY;

> 深灰色


#### const {int} GRAY;

> 灰色


#### const {int} LGRAY;

> 浅灰色


#### const {int} WHITE;

> 白色


#### const {int} RED;

> 红色


#### const {int} GREEN;

> 绿色


#### const {int} BLUE;

> 蓝色


#### const {int} YELLOW;

> 黄色


#### const {int} CYAN;

> 青色


#### const {int} MAGENTA;

> 品红


#### const {int} TRANSPARENT;

> 透明


#### find(img, color, threshold, region)

> 查找颜色的位置

- 参数 : img {Image} 在指定图片中找色 
- 参数 : color {String} 颜色值 
- 参数 : threshold {int} 阈值 
- 参数 : region {double[]} 范围 
- 返回 : {Point} 找到颜色的位置
- 版本 : 1.0.0


```javascript
//(1)截屏
let img = $screen.getScreen();
//(2)在屏幕上找到颜色
let point = $color.find(img, "#a55978", 5, [300,200,500,500]);
if (point != null) {
    //绘制出颜色的位置
    $draw.cross(point);
    sleep(3000);
}
img.close(); //回收截屏图片
$draw.closeAll(); //关闭绘制
```


#### find(img, color, threshold)

> 查找颜色的位置

- 参数 : img {Image} 在指定图片中找色 
- 参数 : color {String} 颜色值 
- 参数 : threshold {int} 阈值 
- 返回 : {Point} 找到颜色的位置
- 版本 : 1.0.0


```javascript
//(1)截屏
let img = $screen.getScreen();
//(2)在屏幕上找到颜色
let point = $color.find(img, "#a55978", 5);
if (point != null) {
    //绘制出颜色的位置
    $draw.cross(point);
    sleep(3000);
}
img.close(); //回收截屏图片
$draw.closeAll(); //关闭绘制
```


#### find(img, color)

> 查找颜色的位置

- 参数 : img {Image} 在指定图片中找色 
- 参数 : color {String} 颜色值 
- 返回 : {Point} 找到颜色的位置
- 版本 : 1.0.0


```javascript
//(1)截屏
let img = $screen.getScreen();
//(2)在屏幕上找到颜色
let point = $color.find(img, "#a55978");
if (point != null) {
    //绘制出颜色的位置
    $draw.cross(point);
    sleep(3000);
}
img.close(); //回收截屏图片
$draw.closeAll(); //关闭绘制
```


#### findAll(img, color, threshold, region)

> 查找颜色所有的位置

- 参数 : img {Image} 在指定图片中找色 
- 参数 : color {String} 颜色值 
- 参数 : threshold {int} 阈值 
- 参数 : region {double[]} 范围 
- 返回 : {Point[]} 找到颜色的位置
- 版本 : 1.0.0


```javascript
let screenImg = $screen.getScreen();
let result = $color.findAll(screenImg,"#d28384",5,[]);
if(result!=null){
    for(let index of result){
        $draw.dot(index);//绘制位置的点
        $draw.log(index);//屏幕显示位置
        sleep(300);
    }
    //3秒后关闭悬浮绘制
    sleep(5000);
    $draw.closeAll();
}
```


#### findAll(img, color, threshold)

> 查找颜色所有的位置

- 参数 : img {} 在指定图片中找色 
- 参数 : color {String} 颜色值 
- 参数 : threshold {int} 阈值 
- 返回 : {Point[]} 找到颜色的位置
- 版本 : 1.0.0


```javascript
let screenImg = $screen.getScreen();
let result = $color.findAll(screenImg,"#d28384",5);
if(result!=null){
    for(let index of result){
        $draw.dot(index);//绘制位置的点
        $draw.log(index);//屏幕显示位置
        sleep(300);
    }
    //3秒后关闭悬浮绘制
    sleep(5000);
    $draw.closeAll();
}
```


#### findAll(img, color)

> 查找颜色所有的位置

- 参数 : img {} 在指定图片中找色 
- 参数 : color {String} 颜色值 
- 返回 : {Point[]} 找到颜色的位置
- 版本 : 1.0.0


```javascript
let screenImg = $screen.getScreen();
let result = $color.findAll(screenImg,"#d28384");
if(result!=null){
    for(let index of result){
        $draw.dot(index);//绘制位置的点
        $draw.log(index);//屏幕显示位置
        sleep(300);
    }
    //3秒后关闭悬浮绘制
    sleep(5000);
    $draw.closeAll();
}
```


#### similar(c1, c2)

> 计算相似度

- 参数 : c1 {string|int} 颜色1 
- 参数 : c2 {string|int} 颜色2 
- 返回 : {double} 相似度
- 版本 : 1.0.0


```javascript
//计算相似度
let result = $color.similar("#1E1F22","#2B2D30");
log("相似度",result);
```


#### similar(c1, c2)

> 计算相似度

- 参数 : c1 {string|int} 颜色1 
- 参数 : c2 {string|int} 颜色2 
- 返回 : {double} 相似度
- 版本 : 1.0.0


```javascript
//计算相似度
let result = $color.similar("#1E1F22","#2B2D30");
log("相似度",result);
```


#### similar(c1, c2)

> 计算相似度

- 参数 : c1 {string|int} 颜色1 
- 参数 : c2 {string|int} 颜色2 
- 返回 : {double} 相似度
- 版本 : 1.0.0


```javascript
//计算相似度
let result = $color.similar("#1E1F22","#2B2D30");
log("相似度",result);
```


#### similar(c1, c2)

> 计算相似度

- 参数 : c1 {string|int} 颜色1 
- 参数 : c2 {string|int} 颜色2 
- 返回 : {double} 相似度
- 版本 : 1.0.0


```javascript
//计算相似度
let result = $color.similar("#1E1F22","#2B2D30");
log("相似度",result);
```


#### toString(color)

> 颜色值转换为8位字符

- 参数 : color {int} 颜色 
- 返回 : {string} 字符串颜色
- 版本 : 1.0.0


```javascript
//转为#00000000
let color = $color.toString(-166780);
```


#### str(color)

> 颜色值转6位字符

- 参数 : color {int} 颜色值 
- 返回 : {string} 颜色
- 版本 : 1.0.0


```javascript
//转为#000000
let color = $color.str(-166780);
```


#### parse(r, g, b)

> 解析rgb的颜色值

- 参数 : r {int} 红 
- 参数 : g {int} 绿 
- 参数 : b {int} 蓝 
- 返回 : {int} 颜色值
- 版本 : 1.0.0


```javascript
let color = $color.parse(105,78,230);
```


#### parse(color)

> 解析颜色值
> 
> 该函数内置了M3风格主题的动态主题颜色，可以通过传入对应的主题字符串来获取对应的颜色值

- 参数 : color {string} 颜色 
- 返回 : {int} 颜色值
- 版本 : 1.0.0


```javascript
//解析颜色值
let colorValue = $color.parse("#1E1F22");
log("颜色值",colorValue);
//除了上面的常规使用方法你也可以用$color动态获取主题颜色
//获取颜色值(返回int类型的颜色值)
let color = $color.parse("white");
let color = $color.parse("black");
let color = $color.parse("null");
let color = $color.parse("none");
let color = $color.parse("green");
let color = $color.parse("red");
let color = $color.parse("blue");
let color = $color.parse("yellow");
//主题颜色值(返回int类型的颜色值)
let color = $color.parse("colorPrimary");//(常用)一般是主题最明显的颜色：蓝色主题一般呈现蓝色
let color = $color.parse("colorSurface");//(常用)一般是背景颜色：亮色主题一般呈现白色，暗色主题一般呈现黑色
let color = $color.parse("colorOnSurface");//(常用)一般是文字颜色：亮色主题一般呈现黑色，暗色主题一般呈现白色
let color = $color.parse("colorOnPrimary");
let color = $color.parse("colorPrimaryContainer");
let color = $color.parse("colorOnPrimaryContainer");
let color = $color.parse("colorSecondary");
let color = $color.parse("colorOnSecondary");
let color = $color.parse("colorSecondaryContainer");
let color = $color.parse("colorOnSecondaryContainer");
let color = $color.parse("colorTertiary");
let color = $color.parse("colorOnTertiary");
let color = $color.parse("colorTertiaryContainer");
let color = $color.parse("colorOnTertiaryContainer");
let color = $color.parse("colorError");
let color = $color.parse("colorErrorContainer");
let color = $color.parse("colorOnErrorContainer");
let color = $color.parse("colorOnBackground");
let color = $color.parse("colorSurfaceVariant");
let color = $color.parse("colorOnSurfaceVariant");
let color = $color.parse("colorOutline");
let color = $color.parse("colorOutlineVariant");
let color = $color.parse("colorPrimaryInverse");
```


#### setAlpha(color, alpha)

> 设置颜色的透明度

- 参数 : color {int} 颜色值 
- 参数 : alpha {int} 透明度(0-255)  
- 返回 : {int} 颜色值
- 版本 : 1.4.3


```javascript
//解析颜色值
let colorValue = $color.parse("#1E1F22");
//设置颜色的透明度
let color = $color.setAlpha(colorValue,100);
```


#### brighter(color)

> 获取较亮颜色

- 参数 : color {int} 颜色值 
- 返回 : {int} 颜色值
- 版本 : 1.4.3


```javascript
//解析颜色值
let colorValue = $color.parse("#1E1F22");
//获取较亮颜色
let color = $color.brighter(colorValue);
```


#### darker(color)

> 获取较暗颜色值

- 参数 : color {int} 颜色值 
- 返回 : {int} 颜色值
- 版本 : 1.4.3


```javascript
//解析颜色值
let colorValue = $color.parse("#1E1F22");
//获取较暗颜色值
let color = $color.darker(colorValue);
```


#### rgb(red, green, blue)

> 通过RGB通道获得颜色值

- 参数 : red {int} R通道 
- 参数 : green {int} G通道 
- 参数 : blue {int} B通道 
- 返回 : {int} 颜色值
- 版本 : 1.0.0


```javascript
let color = $color.rgb(105,78,230);
```


#### argb(alpha, red, green, blue)

> 通过ARGB通道获得颜色值

- 参数 : alpha {int} A通道 
- 参数 : red {int} R通道 
- 参数 : green {int} G通道 
- 参数 : blue {int} B通道 
- 返回 : {int} 颜色值
- 版本 : 1.0.0


```javascript
let color = $color.argb(255,105,78,230);
```


#### a(color)

> 计算[A通道]的值

- 参数 : color {String} 颜色 
- 返回 : {int} 数值
- 版本 : 1.0.0


```javascript
let a = $color.a("#357C94");
```


#### r(color)

> 计算[R通道]的值

- 参数 : color {String} 颜色 
- 返回 : {int} 数值
- 版本 : 1.0.0


```javascript
let r = $color.r("#357C94");
```


#### g(color)

> 计算[G通道]的值

- 参数 : color {String} 颜色 
- 返回 : {int} 数值
- 版本 : 1.0.0


```javascript
let g = $color.g("#357C94");
```


#### b(color)

> 计算[B通道]的值

- 参数 : color {String} 颜色 
- 返回 : {int} 数值
- 版本 : 1.0.0


```javascript
let b = $color.b("#357C94");
```


#### equals(c1, c2)

> 比较两个颜色

- 参数 : c1 {string|int} 颜色1 
- 参数 : c2 {string|int} 颜色2 
- 返回 : {boolean} 是否相等
- 版本 : 1.0.0


```javascript
let color = "#1E1F22";
let colorValue =-14803166;
let same = $color.equals(color,colorValue);
if(same){
    toast("颜色相同");
}else{
    toast("颜色不同");
}
```


#### equals(c1, c2)

> 比较两个颜色

- 参数 : c1 {string|int} 颜色1 
- 参数 : c2 {string|int} 颜色2 
- 返回 : {boolean} 是否相等
- 版本 : 1.0.0


```javascript
let color = "#1E1F22";
let colorValue =-14803166;
let same = $color.equals(color,colorValue);
if(same){
    toast("颜色相同");
}else{
    toast("颜色不同");
}
```


#### equals(c1, c2)

> 比较两个颜色

- 参数 : c1 {string|int} 颜色1 
- 参数 : c2 {string|int} 颜色2 
- 返回 : {boolean} 是否相等
- 版本 : 1.0.0


```javascript
let color = "#1E1F22";
let colorValue =-14803166;
let same = $color.equals(color,colorValue);
if(same){
    toast("颜色相同");
}else{
    toast("颜色不同");
}
```


#### equals(c1, c2)

> 比较两个颜色

- 参数 : c1 {string|int} 颜色1 
- 参数 : c2 {string|int} 颜色2 
- 返回 : {boolean} 是否相等
- 版本 : 1.0.0


```javascript
let color = "#1E1F22";
let colorValue =-14803166;
let same = $color.equals(color,colorValue);
if(same){
    toast("颜色相同");
}else{
    toast("颜色不同");
}
```


#### isDarkTheme()

> 是否是黑暗主题
> 

- 返回 : {boolean} 是否是深色主题


```javascript
let isDark = $color.isDarkTheme();
if(isDark){
    toast("黑暗主题");
}else{
    toast("亮色主题");
}
```


#### isColor(colorStr)

> 判断颜色格式是否正确

- 参数 : colorStr {string} 颜色字符串 
- 返回 : {boolean} 是否是正确的颜色格式
- 版本 : 1.4.3


```javascript
let isColor = $color.isColor("#1E1F22");
if(isColor){
    toast("颜色格式正确");
}else{
    toast("颜色格式错误");
}
```

---

## DateInfo - 日期信息

- 更新时间:2026-01-30 19:32:51

> 日期信息




#### const {long} stamp;

> 时间戳


```javascript
//获取日期信息
let info = $date.info();
log(info.stamp);//时间戳
log(info.year);//年
log(info.month);//月
log(info.day);//日
log(info.week);//星期
log(info.hour);//时
log(info.min);//分
log(info.sec);//秒
log(info.mil);//毫秒
```


#### const {int} year;

> 年


#### const {int} month;

> 月


#### const {int} day;

> 日


#### const {int} week;

> 星期


#### const {int} hour;

> 时


#### const {int} min;

> 分


#### const {int} sec;

> 秒


#### const {int} mil;

> 毫秒


#### getStamp()

> 获得时间戳

- 返回 : {long} 时间戳


```javascript
let info = $date.info("2025/12/08 12-35-24");
log(info.getStamp());
```


#### getYear()

> 获得年

- 返回 : {int} 年


```javascript
let info = $date.info("2025/12/08 12-35-24");
log(info.getYear());
```


#### getMonth()

> 获得月

- 返回 : {int} 月


```javascript
let info = $date.info("2025/12/08 12-35-24");
log(info.getMonth());
```


#### getDay()

> 获得日

- 返回 : {int} 日


```javascript
let info = $date.info("2025/12/08 12-35-24");
log(info.getDay());
```


#### getWeek()

> 获得星期

- 返回 : {int} 星期


```javascript
let info = $date.info("2025/12/08 12-35-24");
log(info.getWeek());
```


#### getHour()

> 获得时

- 返回 : {int} 时


```javascript
let info = $date.info("2025/12/08 12-35-24");
log(info.getHour());
```


#### getMin()

> 获得分

- 返回 : {int} 分


```javascript
let info = $date.info("2025/12/08 12-35-24");
log(info.getMin());
```


#### getSec()

> 获得秒

- 返回 : {int} 秒


```javascript
let info = $date.info("2025/12/08 12-35-24");
log(info.getSec());
```


#### getMil()

> 获得毫秒

- 返回 : {int} 毫秒


```javascript
let info = $date.info("2025/12/08 12-35-24");
log(info.getMil());
```


#### json()

> 转换为JSON字符串

- 返回 : {string} JSON字符串

---

## $date - 日期工具

- 更新时间:2026-01-30 19:32:51

> 日期工具




#### dt()

> 当前日期时间字符串
> 
> 函数名称dt表示dateTime的缩写

- 返回 : {string} 日期时间字符串,格式为:yyyy-MM-dd HH:mm:ss
- 版本 : 1.1.4


```javascript
let dateStr = $date.dt();
alert("日期",dateStr);//2025-10-25 18:32:53
```


#### dt(time)

> 当前日期时间字符串
> 
> 指定时间戳,获得日期和时间的字符串
> 
> 函数名称dt表示dateTime的缩写

- 参数 : time {number} 时间戳
- 返回 : {string} 日期时间字符串,格式为:yyyy-MM-dd HH:mm:ss
- 版本 : 1.1.4


```javascript
let dateStr = $date.dt(1747985594110);
alert("日期",dateStr);
```


#### dt(time)

> 当前日期时间字符串
> 
> 指定时间字符串,获得日期和时间的字符串
> 
> 函数名称dt表示dateTime的缩写

- 参数 : time {string} 时间字符串
- 返回 : {string} 日期时间字符串,格式为:yyyy-MM-dd HH:mm:ss
- 版本 : 1.1.4


```javascript
let dateStr = $date.dt("2025/12/08 12/35/24");
alert("日期",dateStr);//2025-12-08 12:35:24
```


#### d()

> 当前日期字符串
> 
> 函数名称d表示date的缩写

- 返回 : {string} 日期字符串,格式为:yyyy-MM-dd
- 版本 : 1.1.4


```javascript
let dateStr = $date.d();
alert("日期",dateStr);//2025-05-23
```


#### d(time)

> 当前日期字符串
> 
> 指定时间戳,获得日期的字符串
> 
> 函数名称d表示date的缩写

- 参数 : time {number} 时间戳
- 返回 : {string} 日期字符串,格式为:yyyy-MM-dd
- 版本 : 1.1.4


```javascript
let dateStr = $date.d(1747985594110);
alert("日期",dateStr);//2025-05-23
```


#### parse(dateStr, pattern)

> 解析日期

- 参数 : dateStr {string} 日期字符串
- 参数 : pattern {string} 日期格式
- 返回 : {Date} 日期对象
- 版本 : 1.1.4


```javascript
//时间字符串的格式和后面解析模板的格式保持一致
//这样才能解析成功
let date = $date.parse("2025/12/08 12/35/24","yyyy/MM/dd HH/mm/ss");
alert("日期对象",date);//Dec 8, 2025 12:35:24 PM
```


#### parse(dateStr)

> 解析日期
> 
> 内部预制了27种字符串的情况,自动使用这些情况的模板去匹配日期字符串
> 
> 如果解析失败,返回null

- 参数 : dateStr {string} 日期字符串
- 返回 : {Date} 日期对象
- 版本 : 1.1.4


```javascript
//自动解析
let date = $date.parse("2025/12/08 12/35/24");
alert("日期",date);//Mon Dec 08 12:35:24 GMT+08:00 2025
```


#### info()

> 获取日期信息
> 
> 将当前日期的各个字段都分析出来,并且返回

- 返回 : {DateInfo} 日期信息对象
- 版本 : 1.1.4


```javascript
//获取当前日期信息
let info = $date.info();
alert("日期",info);
```


#### info(time)

> 获取指定时间日期信息
> 
> 指定time时间,并且获得这个时间的所有信息

- 返回 : {DateInfo} 日期信息对象
- 版本 : 1.1.4


```javascript
//解析指定时间戳的日期信息
let info = $date.info(1747985594110);
alert("日期",info);
```


#### info(time)

> 获取指定时间日期信息
> 
> 指定字符串时间,并且获得这个时间的所有信息

- 参数 : time {string}  时间字符串
- 返回 : {DateInfo} 日期信息对象
- 版本 : 1.1.4


```javascript
//解析指定时间戳的日期信息
let info = $date.info("2025/12/08 12-35-24");
alert("日期",info);
```


#### format(time, pattern)

> 格式化日期

- 参数 : time {long} 时间戳
- 参数 : pattern {string} 日期格式
- 返回 : {string} 日期字符串
- 版本 : 1.1.4


```javascript
//第一个参数:日期时间戳
//第二个参数:自己想要的格式
let info = $date.format(1747985594110,"yyyy年MM月dd日 HH时mm分ss秒");
alert("日期",info);//2025年05月23日 15时33分14秒
```


#### format(date, pattern)

> 格式化日期

- 参数 : date {Date} 日期
- 参数 : pattern {string} 日期格式
- 返回 : {string} 日期字符串
- 版本 : 1.1.4


```javascript
let date = new java.util.Date();
let info = $date.format(date,"yyyy年MM月dd日 HH时mm分ss秒");
alert("日期",info);//2025年05月23日 15时59分50秒
```


#### format(dateStr, pattern)

> 格式化日期

- 参数 : dateStr {string} 标准日期字符串
- 参数 : pattern {string} 日期格式,自定义的字符串
- 返回 : {string} 日期字符串
- 版本 : 1.1.4


```javascript
//第一个参数:比较乱的日期字符串
//第二个参数:自己想要的格式
let info = $date.format("2025/12/08 12-35-24","yyyy年MM月dd日 HH时mm分ss秒");
alert("日期",info);//2025年12月08日 12时35分24秒
```


#### date()

> 创建日期
> 
> 从当前时间创建一个日期对象

- 返回 : {Date} 当前日期
- 版本 : 1.1.4


```javascript
let info = $date.date();
alert("日期",info);//Fri May 23 15:56:07 GMT+08:00 2025
```


#### date(time)

> 创建日期
> 
> 从指定时间戳中创建日期对象

- 参数 : time {long} 时间戳
- 返回 : {Date} 当前日期
- 版本 : 1.1.4


```javascript
let info = $date.date(1747985594110);
alert("日期",info);//Fri May 23 15:33:14 GMT+08:00 2025
```


#### date(dateStr)

> 创建日期
> 
> 从字符串中创建日期对象，效果和parse(str)一样，内部预制了27种字符串的情况,自动使用这些情况的模板去匹配日期字符串，如果解析失败,返回null

- 参数 : dateStr {string} 日期字符串
- 返回 : {Date} 日期对象
- 版本 : 1.1.4


```javascript
let info = $date.date("2025/12/08 12-35-24");
alert("日期",info);//Mon Dec 08 12:35:24 GMT+08:00 2025
```


#### dur(milliseconds)

> 将毫秒数转换为时间字符串 "x天x时x分x秒"

- 参数 : milliseconds {long}  毫秒数
- 返回 : {string} 格式化的时间字符串
- 版本 : 1.6.1


```javascript
let info = $date.dur(1234567890);
alert("日期",info);//14天6时56分7秒
```


#### curTime()

> 获取当前时间戳

- 返回 : {long} 时间戳
- 版本 : 1.7.8


```javascript
let timestamp = $date.curTime();
alert("时间戳",timestamp);
```