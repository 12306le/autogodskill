# 全局函数与日志 API

> 全局通用函数（sleep/log/toast/提示等）和日志框架。

## 目录
- [$global - 全局函数](#global---全局函数)
- [$log - 日志框架](#log---日志框架)

---

## $global - 全局函数

- 更新时间:2026-01-30 19:32:52

> 全局函数
> 
> 全局函数，在调用的时候无需使用`$`前缀直接写函数即可




#### sleep(ms)

> 睡眠

- 参数 : ms {int} 毫秒 
- 版本 : 1.0.0


```javascript
//停止1秒钟
sleep(1000);
```


#### tip(info)

> 提示

- 参数 : info {string} 信息 
- 版本 : 1.0.0


```javascript
tip("我是提示");
```


#### alert(title, msg)

> 对话框

- 参数 : title {string} 标题 
- 参数 : msg {string} 内容 
- 版本 : 1.0.0


```javascript
alert("提示对话框","我很好");
```


#### showImg(img)

> 显示图片

- 参数 : img {image|string} 图片路径或图片对象 
- 版本 : 1.0.0


```javascript
//显示图片路径上的图片
let imgPath = "sdcard/Pictures/示例/全局函数/t01.png";
showImg(imgPath);
//显示图片对象(Image)
let img = $img.read(imgPath);
showImg(img);
```


#### closeLog()

> 关闭绘制日志

- 版本 : 1.0.0


```javascript
closeLog();
```


#### closeDraw()

> 关闭绘制
> 
> 关闭绘制悬浮窗

- 版本 : 1.0.0


```javascript
closeDraw();
```


#### clearDraw()

> 清空绘制
> 
> 此方法会清空绘制，但是不会关闭绘制悬浮窗

- 版本 : 1.0.0


```javascript
clearDraw();
```


#### getClip()

> 获取剪切板内容
> 
> 谷歌官方发布表明从安卓13开始将支持应用设置剪切板的内容为敏感信息，这就导致，获取剪切板的内容很可能无法获取，或者获取到的内容为空。
> 
> 因此在实际开发中，如果你发现自己无法获取剪切板的内容，完全属于正常现象，此外，较高版本的安卓系统中，剪切板无法后台获取。

- 返回 : {string} 剪切板内容 
- 版本 : 1.0.0


```javascript
let clip = getClip();
```


#### setClip(text)

> 设置剪切板内容

- 参数 : text {string} 内容 
- 版本 : 1.0.0


```javascript
setClip("我是剪切板内容");
```


#### hasClip()

> 是否有剪切板内容

- 返回 : {boolean} 是否有剪切板内容
- 版本 : 1.0.0


```javascript
if(hasClip()){
    let clip = getClip();
}
```


#### clearClip()

> 清空剪切板内容

- 返回 : {boolean} 是否清空成功
- 版本 : 1.0.0


```javascript
clearClip();
```


#### curPkg()

> 获取无障碍检测到的包名

- 返回 : {string} 活动名称
- 版本 : 1.3.1


```javascript
let pkgName = curPkg();
```


#### curCls()

> 获取无障碍检测到的活动名

- 返回 : {string} 活动名称
- 版本 : 1.3.1


```javascript
let actName = curCls();
```


#### curTime()

> 获取当前时间戳

- 返回 : {long} 时间戳
- 版本 : 1.7.8


```javascript
let stamp = curTime();
log(stamp);
```


#### info(msg)

> 悬浮土司提示
> 
> 悬浮窗土司，可以显示在任何app界面，但是需要悬浮窗权限。

- 参数 : msg {string...} 日志信息  


```javascript
info("提示信息");
```


#### infoLog(msg)

> 悬浮土司加控制台打印

- 参数 : msg {string...} 日志信息 


```javascript
infoLog("提示信息");
```


#### toast(msg)

> 系统土司
> 
> 部分手机需要开启通知权限才允许显示在其他应用上方

- 参数 : msg {string...} 日志信息 


```javascript
toast("提示信息");
```


#### toastLog(msg)

> 系统土司加控制台打印

- 参数 : msg {string...} 日志信息 


```javascript
toastLog("提示信息");
```


#### log(msg)

> 控制台日志

- 参数 : msg {string...} 日志信息 


```javascript
log("信息");
```


#### print(msg)

> 控制台日志

- 参数 : msg {string...} 日志信息 


```javascript
print("信息");
```


#### random()

> 随机数(0-1)

- 返回 : {float} 随机数(0-1)


```javascript
log(random());//0-1之间的随机数
```


#### random(max)

> 随机数(0-max)

- 参数 : max {int} 最大值 


```javascript
log(random(10));//0-10之间的随机数
```


#### random(min, max)

> 随机数(min-max)

- 参数 : min {int} 最小值 
- 参数 : max {int} 最大值 


```javascript
log(random(10,30));//10-30之间的随机数
```


#### require(path)

> 导入模块

- 参数 : path {string} 模块路径或相对路径 
- 返回 : {JsObject} 模块对象


```javascript
let MyClass = require("mCls.js");
let obj = new MyClass();
```

---

## $log - 日志框架

- 更新时间:2026-01-30 19:32:53

> 日志框架




#### i(args)

> 打印信息日志

- 参数 : args {string...} 日志
- 版本 : 1.0.0


```javascript
$log.i("信息");
```


#### info(args)

> 打印信息日志

- 参数 : args {string...} 日志
- 版本 : 1.0.0


```javascript
$log.info("信息");
```


#### d(args)

> 打印调试日志

- 参数 : args {string...} 日志
- 版本 : 1.0.0


```javascript
$log.d("调试");
```


#### debug(args)

> 打印调试日志

- 参数 : args {string...} 日志
- 版本 : 1.2.8


```javascript
$log.debug("调试");
```


#### w(args)

> 打印警告日志

- 参数 : args {string...} 日志
- 版本 : 1.0.0


```javascript
$log.w("警告");
```


#### warn(args)

> 打印警告日志

- 参数 : args {string...} 日志
- 版本 : 1.2.8


```javascript
$log.warn("警告");
```


#### e(args)

> 打印异常日志

- 参数 : args {string...} 日志
- 版本 : 1.0.0


```javascript
$log.e("异常");
```


#### err(args)

> 打印异常日志

- 参数 : args {string...} 日志
- 版本 : 1.2.8


```javascript
$log.err("异常");
```


#### v(args)

> 打印冗余日志

- 参数 : args {string...} 日志
- 版本 : 1.0.0


```javascript
$log.v("冗余");
```


#### log(args)

> 打印日志

- 参数 : args {string...} 日志
- 版本 : 1.0.0


```javascript
$log.log("hello");
```


#### print(args)

> 打印日志

- 参数 : args {string...} 日志
- 版本 : 1.2.0


```javascript
$log.print("hello");
```


#### floaty()

> 打开日志悬浮窗

- 版本 : 1.0.0


```javascript
$log.floaty();
```


#### closeFloaty()

> 关闭日志悬浮窗

- 版本 : 1.8.6


```javascript
$log.closeFloaty();
```


#### activity()

> 打开日志界面

- 版本 : 1.1.2


```javascript
$log.activity();
```


#### delete()

> 删除本地缓存

- 版本 : 1.0.6


```javascript
$log.delete();
```