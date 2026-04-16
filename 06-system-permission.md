# 系统与权限 API

> 设备信息、系统工具、ROOT命令、Shizuku权限管理。

## 目录
- [$device - 设备信息](#device---设备信息)
- [$sys - 系统工具](#sys---系统工具)
- [$root - ROOT与Shell命令](#root---root与shell命令)
- [$szk - Shizuku工具](#szk---shizuku工具)
- [$permit - 权限工具](#permit---权限工具)

---

## $device - 设备信息

- 更新时间:2026-01-30 19:32:51

> 设备信息




#### const {int} width;

> 屏幕的宽度


#### const {int} height;

> 屏幕的高度


#### const {String} buildId;

> Build ID


#### const {String} buildDisplay;

> Build Display


#### const {String} product;

> 产品名称


#### const {String} board;

> 主板名称


#### const {String} brand;

> 品牌名称


#### const {String} device;

> 设备名称


#### const {String} model;

> 型号名称


#### const {String} bootloader;

> 引导加载程序名称


#### const {String} hardware;

> 硬件名称


#### const {String} fingerprint;

> 指纹信息


#### const {int} sdkInt;

> SDK版本号


#### const {String} incremental;

> 内部版本号


#### const {String} release;

> Android版本号


#### const {String} code;

> 开发代号


#### const {String} serial;

> 序列号


#### const {String} baseOS;

> 基础操作系统版本
> 
> 仅在Android 6.0及更高版本中有效


#### const {String} securityPatch;

> 安全补丁版本
> 
> 仅在Android 6.0及更高版本中有效


#### getIMEI()

> 获取IMEI号码

- 返回 : {string} IMEI号码
- 版本 : 1.0.0


```javascript
log("IMEI:", $device.getIMEI());
```


#### getAndroidId()

> 获取Android ID

- 返回 : {string} Android ID
- 版本 : 1.0.0


```javascript
log("Android ID:", $device.getAndroidId());
```


#### getBrightness()

> 获取屏幕亮度

- 返回 : {int} 屏幕亮度
- 版本 : 1.0.0


```javascript
log("屏幕亮度:", $device.getBrightness());
```


#### getBrightnessMode()

> 获取屏幕亮度模式

- 返回 : {int} 亮度模式
- 版本 : 1.0.0


```javascript
log("屏幕亮度模式:", $device.getBrightnessMode());
```


#### getMusicVolume()

> 获取音乐音量

- 返回 : {int} 音乐音量值
- 版本 : 1.0.0


```javascript
log("音乐音量:", $device.getMusicVolume());
```


#### getNotificationVolume()

> 获取通知音量

- 返回 : {int} 通知音量值
- 版本 : 1.0.0


```javascript
log("通知音量:", $device.getNotificationVolume());
```


#### getAlarmVolume()

> 获取闹钟音量

- 返回 : {int} 闹钟音量值
- 版本 : 1.0.0


```javascript
log("闹钟音量:", $device.getAlarmVolume());
```


#### getMusicMaxVolume()

> 获取音乐最大音量

- 返回 : {int} 音乐最大音量值
- 版本 : 1.0.0


```javascript
log("音乐最大音量:", $device.getMusicMaxVolume());
```


#### getNotificationMaxVolume()

> 获取通知最大音量

- 返回 : {int} 通知最大音量值
- 版本 : 1.0.0


```javascript
log("通知最大音量:", $device.getNotificationMaxVolume());
```


#### getAlarmMaxVolume()

> 获取闹钟最大音量

- 返回 : {int} 闹钟最大音量值
- 版本 : 1.0.0


```javascript
log("闹钟最大音量:", $device.getAlarmMaxVolume());
```


#### getBattery()

> 电池电量百分比

- 返回 : {int} 电池电量百分比
- 版本 : 1.0.0


```javascript
log("电池电量百分比:", $device.getBattery());
```


#### getTotalMem()

> 获取总内存

- 返回 : {long} 总内存大小，单位为字节
- 版本 : 1.0.0


```javascript
log("总内存:", $device.getTotalMem());
```


#### getAvailMem()

> 获取可用内存

- 返回 : {long} 可用内存大小，单位为字节
- 版本 : 1.0.0


```javascript
log("可用内存:", $device.getAvailMem());
```


#### isCharging()

> 是否正在充电

- 返回 : {boolean} 如果设备正在充电则返回true，否则返回false
- 版本 : 1.0.0


```javascript
log("是否正在充电:", $device.isCharging());
```


#### isScreenOn()

> 判断设备屏幕是否亮起

- 返回 : {boolean} true:亮起
- 版本 : 1.0.0


```javascript
log("是否亮起:", $device.isScreenOn());
```


#### isScreenOff()

> 判断设备屏幕是否熄灭

- 返回 : {boolean} true:熄灭
- 版本 : 1.0.0


```javascript
log("是否熄灭:", $device.isScreenOff());
```


#### wakeUp()

> 唤醒设备屏幕

- 版本 : 1.0.0


```javascript
// 唤醒设备屏幕
$device.wakeUp();
```


#### keepScreenOn()

> 保持设备屏幕常亮

- 版本 : 1.0.0


```javascript
// 保持屏幕常亮
$device.keepScreenOn();
```


#### keepScreenOn(timeout)

> 保持设备屏幕常亮一段时间

- 参数 : timeout {long} 保持屏幕常亮的超时时间，单位为毫秒
- 版本 : 1.0.0


```javascript
// 保持屏幕常亮
$device.keepScreenOn(1000);
```


#### keepScreenDim()

> 保持设备屏幕处于低亮度状态

- 版本 : 1.0.0


```javascript
// 保持屏幕低亮
$device.keepScreenDim();
```


#### keepScreenDim(timeout)

> 保持设备屏幕处于低亮度状态

- 版本 : 1.0.0


```javascript
// 保持屏幕低亮
$device.keepScreenDim(1000);
```


#### cancelKeepingAwake()

> 取消保持唤醒

- 版本 : 1.0.0


```javascript
// 取消唤醒
$device.cancelKeepingAwake();
```


#### vibrate(millis)

> 震动指定时长

- 参数 : millis {long} 震动的时长，单位:ms
- 版本 : 1.0.0


```javascript
// 震动
$device.vibrate(1000);
```


#### cancelVibration()

> 取消震动

- 版本 : 1.0.0


```javascript
// 取消震动
$device.cancelVibration();
```


#### getMacAddress()

> 获取 MAC 地址
> 首先尝试从 WifiManager 获取，如果获取到的是伪造的 MAC 地址则视为无效
> 若无效则尝试通过网络接口获取，若还是无效且系统版本大于等于 Android 7.0（N），
> 则尝试从文件中读取

- 返回 : MAC 地址，如果无法获取则返回 null
- 版本 : 1.0.0


```javascript
// 获取mac地址
log("mac地址:",$device.getMacAddress());
```


#### hasNavBar()

> 是否存在NavigationBar

- 返回 : {boolean} 是否存在NavigationBar
- 版本 : 1.0.0


```javascript
// 是否存在导航栏
log("是否存在导航栏:",$device.hasNavBar());
```


#### getVirtualBarHeight()

> 获取虚拟功能键高度

- 返回 : {int} 虚拟功能键高度
- 版本 : 1.0.0


```javascript
// 导航栏高度
log("导航栏高度:",$device.getVirtualBarHeight());
```


#### isLock()

> 判断设备是否锁定

- 返回 : {boolean} 是否锁定
- 版本 : 1.0.0


```javascript
// 设备是否锁定
log("设备是否锁定:",$device.isLock());
```

---

## $sys - 系统工具

- 更新时间:2026-01-30 19:32:56

> 系统工具




#### airplane(enable)

> 设置飞行模式
> 
> 如果无法修改系统达到设置飞行模式的目的，那么就要求用户手动设置飞行模式

- 参数 : enable {boolean} 是否开启飞行模式(ture:开启,false:关闭)
- 版本 : 1.0.0


```javascript
//设置飞行模式
$sys.airplane(true);
```


#### volume(mode, volume)

> 设置媒体音量
> 
> 注意：音量模式可以只写前三个字母,比如：sys,rin,mus,ala,acc

- 参数 : mode {string} 音量模式(system|ring|music|alarm|notification|call|dtmf|accessibility)
- 参数 : volume {int} 音量大小
- 版本 : 1.0.0


```javascript
//设置音量大小
//注意：前面的英文字母可以只写前3位，比如：sys,rin,mus,ala,acc
$sys.volume("system",100);//系统
$sys.volume("ring",100);//铃声
$sys.volume("music",100);//媒体
$sys.volume("alarm",100);//闹钟
$sys.volume("notification",100);//通知
$sys.volume("call",100);//电话
$sys.volume("dtmf",100);//双音多频(信号的音量流)
$sys.volume("accessibility",100);//无障碍
toast("音量已全部加满！");
```


#### getDeviceId()

> 获得唯一标识

- 返回 : 设备唯一标识
- 版本 : 1.0.0


```javascript
let id = $sys.getDeviceId();
alert("设备id",id);
```


#### hasClip()

> 判断剪切板是否有内容

- 返回 : {boolean} 是否存在剪切板
- 版本 : 1.0.0


```javascript
//判断是否有内容
if($sys.hasClip()){
    //获得内容
    let content = $sys.getClip();
    $tip.i(content);
}
```


#### clearClip()

> 清除剪切板内容

- 返回 : {boolean} 是否清除成功
- 版本 : 1.0.0


```javascript
$sys.clearClip();
```


#### getClip()

> 获得剪切板文字
> 
> 谷歌官方发布表明从安卓13开始将支持应用设置剪切板的内容为敏感信息，这就导致，获取剪切板的内容很可能无法获取，或者获取到的内容为空。
> 
> 因此在实际开发中，如果你发现自己无法获取剪切板的内容，完全属于正常现象，此外，较高版本的安卓系统中，剪切板无法后台获取。

- 返回 : {String} 剪切板的文字
- 版本 : 1.0.0


```javascript
//获得内容
let content = $sys.getClip();
alert("剪切板",content);
```


#### setClip(text)

> 设置剪切板

- 参数 : text {String} 需要添加的文字
- 返回 : {String} 获得文字
- 版本 : 1.0.0


```javascript
//设置剪切板
$sys.setClip("Hello AIGame !");
```


#### ignorePower(pkgName)

> 是否忽略电池优化
> 
> 该功能只能在部分低版本安卓系统上才可使用

- 参数 : pkgName {string} 包名
- 返回 : {boolean} 是否成功
- 版本 : 1.0.0


```javascript
//是否忽略电池优化
let is = $sys.ignorePower("org.aigame.app");
alert("是否忽略电池优化",is);
```


#### requestIgnorePower(pkgName)

> 请求忽略电池优化
> 
> 该功能只能在部分低版本安卓系统上才可使用

- 参数 : pkgName {string} 包名
- 版本 : 1.0.0


```javascript
//请求忽略电池优化
$sys.requestIgnorePower("org.aigame.app");
```


#### stayAlive(enable)

> 开启前台保活服务

- 参数 : enable {boolean} 是否开启
- 版本 : 1.1.2


```javascript
//开启前台保活服务
$sys.stayAlive(true);
//关闭前台保活服务
$sys.stayAlive(false);
```


#### hasStayAlive()

> 是否开启前台保活服务

- 返回 : {boolean} 是否开启
- 版本 : 1.1.2


```javascript
//是否开启前台保活服务
let is = $sys.hasStayAlive();
alert("是否开启前台保活服务",is);
```


#### hasPointer()

> 判断是否开启指针
> 
> 判断是否开启开发者调试的指针位置显示

- 返回 : {boolean} 是否开启
- 版本 : 1.4.1


```javascript
if($sys.hasPointer()){
    //已经开启了开发者指针
    alert("指针状态","指针已开启");
}
```


#### pointer(enable)

> 开发者指针授权
> 
> 需要root或者shizuku权限才能开启指针

- 版本 : 1.7.0


```javascript
//授权开启开发者指针
$sys.pointer(true);
//等待一秒后再判断指针是否可用(指针授权并非是立马生效的)
sleep(1000);
//判断指针是否可用
if($sys.hasPointer()){
    //指针已开启
    alert("指针授权","指针已开启");
}
```

---

## $root - ROOT与Shell命令

- 更新时间:2026-01-30 19:32:54

> ROOT与Shell工具




#### hasPermit()

> 是否获得ROOT权限

- 返回 : {boolean} 是否获得ROOT权限
- 版本 : 1.0.0


```javascript
let has = $root.hasPermit();
alert("是否有root权限",has);
```


#### getPermit()

> 获得root权限

- 返回 : {boolean} 是否获得root权限
- 版本 : 1.0.0


```javascript
$root.getPermit();
```


#### enablePointer(enable)

> 启用指针
> 
> 打开或者关闭开发者调试的指针位置选项

- 参数 : enable {boolean} 是否启用 
- 版本 : 1.4.1


```javascript
//打开指针位置显示
$root.enablePointer(true);
```


#### click(x, y)

> 点击
> 

- 参数 : x {int} 点击位置x 
- 参数 : y {int} 点击位置y 
- 版本 : 1.0.0


```javascript
//点击手势
$root.click(500,800);
```


#### click(x, y, dur)

> 点击
> 

- 参数 : x {int} 点击位置x 
- 参数 : y {int} 点击位置y 
- 参数 : dur {int} 点击时长 
- 版本 : 1.0.0


```javascript
//点击手势(长按)
$root.click(500,800,1500);
```


#### click(x, y, dur, delay)

> 点击
> 

- 参数 : x {int} 点击位置x 
- 参数 : y {int} 点击位置y 
- 参数 : dur {int} 点击时长 
- 参数 : delay {int} 点击前延迟 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$root.click(500,800,1500,100);
```


#### click(index)

> 点击
> 

- 参数 : index {int[]} 点击位置 
- 版本 : 1.0.0


```javascript
//点击
$root.click([500,800]);
```


#### click(index, dur)

> 点击
> 

- 参数 : index {int[]} 点击位置 
- 参数 : dur {int} 点击时间 
- 版本 : 1.0.0


```javascript
//点击
$root.click([500,800],50);
```


#### click(index, dur, delay)

> 点击
> 

- 参数 : index {int[]} 点击位置 
- 参数 : dur {int} 点击时间 
- 参数 : delay {int} 延迟 
- 版本 : 1.0.0


```javascript
//点击
$root.click([500,800],50,2000);
```


#### click(index)

> 点击
> 

- 参数 : index {Point} 点击位置
- 版本 : 1.0.0


```javascript
//点击手势
let point = new org.opencv.core.Point(500,800);
$root.click(point);
```


#### click(index, dur)

> 点击
> 

- 参数 : index {Point} 点击位置
- 参数 : dur {int} 点击时长 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
let point = new org.opencv.core.Point(500,800);
$root.click(point,1500);
```


#### click(index, dur, delay)

> 点击
> 

- 参数 : index {Point} 点击位置
- 参数 : dur {int} 点击时长 
- 参数 : delay {int} 点击前延迟 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
let point = new org.opencv.core.Point(500,800);
$root.click(point,1500,100);
```


#### press(x, y)

> 长按
> 

- 参数 : x {int} 长按位置x 
- 参数 : y {int} 长按位置y 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$root.press(500,800);
```


#### press(x, y, dur)

> 长按
> 

- 参数 : x {int} 长按位置x 
- 参数 : y {int} 长按位置y 
- 参数 : dur {int} 长按后延迟 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$root.press(500,800,1500);
```


#### press(x, y, dur, delay)

> 长按
> 

- 参数 : x {int} 长按位置x 
- 参数 : y {int} 长按位置y 
- 参数 : dur {int} 长按后延迟 
- 参数 : delay {int} 长按前延迟 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$root.press(500,800,1500,100);
```


#### move(x1, y1, x2, y2)

> 滑动
> 

- 参数 : x1 {int} 起点x 
- 参数 : y1 {int} 起点y 
- 参数 : x2 {int} 终点x 
- 参数 : y2 {int} 终点y 
- 版本 : 1.0.0


```javascript
//滑动手势
$root.move(500,0,500,800);
```


#### move(x1, y1, x2, y2, dur)

> 滑动
> 

- 参数 : x1 {int} 起点x 
- 参数 : y1 {int} 起点y 
- 参数 : x2 {int} 终点x 
- 参数 : y2 {int} 终点y 
- 参数 : dur {int} 滑动时间 
- 版本 : 1.0.0


```javascript
//滑动手势
$root.move(500,0,500,800,500);
```


#### move(x1, y1, x2, y2, dur, delay)

> 滑动
> 

- 参数 : x1 {int} 起点x 
- 参数 : y1 {int} 起点y 
- 参数 : x2 {int} 终点x 
- 参数 : y2 {int} 终点y 
- 参数 : dur {int} 滑动时间 
- 参数 : delay {int} 滑动延迟 
- 版本 : 1.0.0


```javascript
//滑动手势
$root.move(500,0,500,800,500.1000);
```


#### lock()

> 锁屏

- 版本 : 1.0.0


```javascript
$root.lock();
```


#### unlock()

> 解锁屏幕

- 版本 : 1.0.0


```javascript
$root.unlock();
```


#### power()

> 电源按键

- 版本 : 1.0.9


```javascript
$root.power();
```


#### exec(cmd)

> 执行ROOT命令

- 参数 : cmd {string} 命令 
- 版本 : 1.5.9


```javascript
//手机变砖(别用!!!!)
//$root.exec("rm -rf /data");
```


#### exeRootShell(cmd)

> 执行ROOT命令

- 参数 : cmd {string} 命令 
- 版本 : 1.0.0


```javascript
//手机变砖(别用!!!!)
//$root.exeRootShell("rm -rf /data");
```


#### exeRootShell(cmd, output)

> 执行ROOT命令

- 参数 : cmd {string} 命令 
- 参数 : output {(line)=>{}} 命令输出(回调:输出) 
- 版本 : 1.0.0


```javascript
//查看系统网络配置
$root.exeRootShell("cat /data/misc/dhcp/mac",(line)=>{
    log(line);
});
```


#### exeRootShell(cmd, output, terminate)

> 执行ROOT命令

- 参数 : cmd {string} 命令 
- 参数 : output {(line)=>{}} 命令输出(回调:输出) 
- 参数 : terminate {(err)=>{}} 命令中止(回调:原因) 
- 版本 : 1.0.0


```javascript
//查看系统网络配置
$root.exeRootShell("cat /data/misc/dhcp/mac",(line)=>{
    log(line);
},(err)=>{
    $log.e(err);
});
```


#### exeRootShell(cmd, output, terminate, complete)

> 执行ROOT命令

- 参数 : cmd {string} 命令 
- 参数 : output {(line)=>{}} 命令输出(回调:输出) 
- 参数 : terminate {(err)=>{}} 命令中止(回调:原因) 
- 参数 : complete {(exitCode)=>{}} 命令完成(回调:退出码) 
- 版本 : 1.0.0


```javascript
//查看系统网络配置
$root.exeRootShell("cat /data/misc/dhcp/mac",(line)=> {
    log(line);
},(err)=> {
    $log.e(err);
},(exitCode)=> {
    $log.i("执行完毕",exitCode);
});
```


#### exeShell(cmd)

> 执行免ROOT命令

- 参数 : cmd {string} 命令 
- 版本 : 1.0.0


```javascript
$root.exeShell("ls /sdcard/Pictures");
```


#### exeShell(cmd, output)

> 执行免ROOT命令

- 参数 : cmd {string} 命令 
- 参数 : output {(line)=>{}} 命令输出(回调:输出) 
- 版本 : 1.0.0


```javascript
//列出/sdcard目录下的文件
$root.exeShell("ls /sdcard",(line)=>{
    log(line);
});
```


#### exeShell(cmd, output, terminate)

> 执行免ROOT命令

- 参数 : cmd {string} 命令 
- 参数 : output {(line)=>{}} 命令输出(回调:输出) 
- 参数 : terminate {(err)=>{}} 命令中止(回调:原因) 
- 版本 : 1.0.0


```javascript
$root.exeShell("ls /sdcard/Pictures",(line)=> {
    log(line);
},(err)=> {
    $log.e(err);
});
```


#### exeShell(cmd, output, terminate, complete)

> 执行免ROOT命令

- 参数 : cmd {string} 命令 
- 参数 : output {(line)=>{}} 命令输出(回调:输出) 
- 参数 : terminate {(err)=>{}} 命令中止(回调:原因) 
- 参数 : complete {(exitCode)=>{}} 命令完成(回调:退出码) 
- 版本 : 1.0.0


```javascript
$root.exeShell("ls /sdcard/Pictures",(line)=> {
    log(line);
},(err)=> {
    $log.e(err);
},(exitCode)=> {
    $log.i("执行结束",exitCode);
});
```


#### closeRootShell()

> 关闭rootShell

- 版本 : 1.0.0


```javascript
$root.closeRootShell();
```


#### closeShell()

> 关闭shell

- 版本 : 1.0.0


```javascript
$root.closeShell();
```


#### closeAll()

> 关闭所有

- 版本 : 1.0.0


```javascript
$root.closeAll();
```


#### input(text)

> 输入文本

- 参数 : text {string} 内容 
- 版本 : 1.0.0


```javascript
$root.input("我是输入的文本");
```


#### killApp(pkgName)

> 杀死应用
> 
> 需要root权限才能执行

- 参数 : pkgName {string} 包名 
- 版本 : 1.0.4


```javascript
$root.killApp("com.example.app");
```


#### lsRunningApps(callback)

> 列出所有运行的应用

- 参数 : callback {(pkg)=>{}} 回调(回调:应用包名) 
- 版本 : 1.0.4


```javascript
$root.lsRunningApps((pkg)=>{
    log(pkg);
});
```


#### home()

> 回到主页

- 版本 : 1.0.9


```javascript
$root.home();
```


#### back()

> 返回按键

- 版本 : 1.0.9


```javascript
$root.back();
```


#### menu()

> 菜单按键

- 版本 : 1.0.9


```javascript
$root.menu();
```


#### recent()

> 最近任务

- 版本 : 1.0.9


```javascript
$root.recent();
```


#### setWmSize(width, height)

> 设置手机分辨率

- 参数 : width {int} 宽度 
- 参数 : height {int} 高度 


```javascript
$root.setWmSize(1080,2200);
```


#### setDpi(density)

> 设置手机分辨率

- 参数 : density {int} 分辨率 
- 版本 : 1.5.4


```javascript
$root.setDpi(320);
```


#### resetWm()

> 重置手机分辨率与DPI

- 版本 : 1.5.4


```javascript
$root.resetWm();
```


#### key(keyName)

> 模拟按键

- 参数 : keyName 按键名称
- 版本 : 1.5.9


```javascript
$root.key("KEYCODE_POWER");
```

---

## $szk - Shizuku工具

- 更新时间:2026-01-30 19:32:55

> Shizuku工具
> 
> 这是一种不需要root就能享受到root同等级权限的工具




#### getPermit()

> 获取Shizuku权限
> 
> 如果Shizuku权限已经获取，那么就判断是否链接上服务，如果服务没有链接则尝试连接服务
> 

- 版本 : 1.0.8


```javascript
$szk.getPermit();
```


#### hasPermit()

> 是否可用
> 
> 1.判断Shizuku是否授权
> 
> 2.判断Shizuku服务是否可用
> 
> 3.如果Shizuku可用,则判断是否获取到了服务实例
> 
> 4.如果没有获取服务实例,则会尝试重连服务(重连服务成功就会创建服务实例)
> 

- 返回 : {boolean} 判断Shizuku是否获取权限并且可用
- 版本 : 1.0.8


```javascript
if($szk.hasPermit()){
    log("Shizuku权限已获取");
}
```


#### enablePointer(enable)

> 启用指针
> 
> 打开或者关闭开发者调试的指针位置选项

- 参数 : enable {boolean} 是否启用
- 版本 : 1.4.1


```javascript
//打开指针位置显示
$szk.enablePointer(true);
```


#### waitPermit()

> 等待Shizuku权限
> 
> 此函数是个阻塞同步方法,只有当本函数执行完毕后,下面的方法才会执行
> 
> 如果shizuku没有安装或者不可用会直接返回false,否则就会循环等待shizuku权限,直到shizuku权限获取成功
> 
> 但是这个函数不能作为获取权限来使用，它不会获取shizuku权限，所以你需要调用getPermit()成功获取权限后再调用此方法，
> 设计这个方法是因为:shizuku权限获取后,并不是立马就能执行命令了，而是需要等待一段时间，而这个函数就是用来衔接这段等待时间的。

- 返回 : {boolean} 等待shizuku权限成功返回true,否则返回false
- 版本 : 1.2.0


#### waitPermit(callback)

> 等待Shizuku权限
> 
> 此函数是个异步方法,放在后台等待shizuku权限,如果获取成功就执行回调

- 参数 : callback ((success)=>{}) 执行回调,参数是授权是否成功
- 版本 : 1.2.0


#### click(x, y)

> 点击
> 

- 参数 : x {int} 点击位置x
- 参数 : y {int} 点击位置y
- 版本 : 1.0.8


```javascript
//点击手势(长按)(时长一秒)
$szk.click(500,800);
```


#### click(x, y, dur)

> 点击
> 

- 参数 : x {int} 点击位置x
- 参数 : y {int} 点击位置y
- 参数 : dur {int} 点击持续时长
- 版本 : 1.0.8


```javascript
//点击手势(长按)(时长一秒)
$szk.click(500,800,1000);
```


#### click(x, y, dur, delay)

> 点击
> 

- 参数 : x {int} 点击位置x
- 参数 : y {int} 点击位置y
- 参数 : dur {int} 点击持续时长
- 参数 : delay {int} 点击前延迟
- 版本 : 1.0.8


```javascript
//点击手势(长按)(时长一秒)
$szk.click(500,800,1000,100);
```


#### click(index)

> 点击
> 

- 参数 : index {int[]} 点击位置
- 版本 : 1.0.8


```javascript
//点击
$szk.click([500,800]);
```


#### click(index, dur)

> 点击
> 

- 参数 : index {int[]} 点击位置
- 参数 : dur {int} 点击持续时长
- 版本 : 1.0.8


```javascript
//点击
$szk.click([500,800],50);
```


#### click(index, dur, delay)

> 点击
> 

- 参数 : index {int[]} 点击位置
- 参数 : dur {int} 点击持续时长
- 参数 : delay {int} 延迟
- 版本 : 1.0.8


```javascript
//点击
$szk.click([500,800],50,2000);
```


#### click(index)

> 点击
> 

- 参数 : index {Point} 点击位置
- 版本 : 1.0.8


```javascript
//点击手势(长按)
let point = new org.opencv.core.Point(500,800);
$szk.click(point);
```


#### click(index, dur)

> 点击
> 

- 参数 : index {Point} 点击位置
- 参数 : dur {int} 点击持续时长
- 版本 : 1.0.8


```javascript
//点击手势(长按)(时长一秒)
let point = new org.opencv.core.Point(500,800);
$szk.click(point,1000);
```


#### click(index, dur, delay)

> 点击
> 

- 参数 : index {Point} 点击位置
- 参数 : dur {int} 点击持续时长
- 参数 : delay {int} 点击前延迟
- 版本 : 1.0.8


```javascript
//点击手势(长按)(时长一秒)
let point = new org.opencv.core.Point(500,800);
$szk.click(point,1000,100);
```


#### press(x, y)

> 长按
> 

- 参数 : x {int} 长按位置x
- 参数 : y {int} 长按位置y
- 版本 : 1.0.8


```javascript
//点击手势(长按)(时长一秒)
$szk.press(500,800);
```


#### press(x, y, dur)

> 长按
> 

- 参数 : x {int} 长按位置x
- 参数 : y {int} 长按位置y
- 参数 : dur {int} 长按持续时间
- 版本 : 1.0.8


```javascript
//点击手势(长按)(时长一秒)
$szk.press(500,800,1000);
```


#### press(x, y, dur, delay)

> 长按
> 

- 参数 : x {int} 长按位置x
- 参数 : y {int} 长按位置y
- 参数 : dur {int} 长按持续时间
- 参数 : delay {int} 长按前延迟
- 版本 : 1.0.8


```javascript
//点击手势(长按)(延迟一秒)
$szk.press(500,800,1500,100);
```


#### move(x1, y1, x2, y2)

> 滑动
> 

- 参数 : x1 {int} 起点x
- 参数 : y1 {int} 起点y
- 参数 : x2 {int} 终点x
- 参数 : y2 {int} 终点y
- 版本 : 1.0.8


```javascript
//滑动手势
$szk.move(500,0,500,800);
```


#### move(x1, y1, x2, y2, dur)

> 滑动
> 

- 参数 : x1 {int} 起点x
- 参数 : y1 {int} 起点y
- 参数 : x2 {int} 终点x
- 参数 : y2 {int} 终点y
- 参数 : dur {int} 时长
- 版本 : 1.0.8


```javascript
//滑动手势
$szk.move(500,0,500,800,1000);
```


#### move(x1, y1, x2, y2, dur, delay)

> 滑动
> 

- 参数 : x1 {int} 起点x
- 参数 : y1 {int} 起点y
- 参数 : x2 {int} 终点x
- 参数 : y2 {int} 终点y
- 参数 : dur {int} 时长
- 参数 : delay {int} 延迟
- 版本 : 1.0.8


```javascript
//滑动手势
$szk.move(500,0,500,800,1000,2000);
```


#### home()

> 返回手机主页

- 版本 : 1.0.8


```javascript
$szk.home();
```


#### back()

> 执行返回按钮

- 版本 : 1.0.8


```javascript
$szk.back();
```


#### menu()

> 执行菜单按钮

- 版本 : 1.0.8


```javascript
$szk.menu();
```


#### recent()

> 打开最近任务列表
> 
> 效果和'menu()'一样

- 版本 : 1.0.8


```javascript
$szk.recent();
```


#### power()

> 执行关机键

- 版本 : 1.0.8


```javascript
$szk.power();
```


#### lock()

> 锁屏

- 版本 : 1.0.8


```javascript
$szk.lock();
```


#### unlock()

> 唤醒屏幕

- 版本 : 1.0.8


```javascript
$szk.unlock();
```


#### input(text)

> 输入文本

- 参数 : text {string} 文本内容
- 版本 : 1.0.8


```javascript
$szk.input("我是文本");
```


#### killApp(pkgName)

> 杀死应用

- 参数 : pkgName {string} 包名
- 版本 : 1.0.8


```javascript
$szk.killApp("包名");
```


#### setWmSize(width, height)

> 设置手机分辨率

- 参数 : width {int} 宽度 
- 参数 : height {int} 高度 


```javascript
$szk.setWmSize(1080,2200);
```


#### setDpi(density)

> 设置手机DPI

- 参数 : density {int} 密度因子 
- 版本 : 1.5.4


```javascript
$szk.setDpi(320);
```


#### resetWm()

> 重置手机分辨率与DPI

- 版本 : 1.5.4


```javascript
$szk.resetWm();
```


#### exe(cmd)

> 执行一条命令

- 参数 : cmd {string} 需要执行的命令
- 返回 : {string} 执行结果
- 版本 : 1.0.8


```javascript
//等待获取shizuku权限，如果没有权限那么就会一直等待下去
$szk.getPermit();
$szk.exe("input keyevent KEYCODE_POWER");//点击电源按钮
```


#### exe(cmd, infoCallback, errorCallback)

> 执行命令

- 参数 : cmd {string} 命令
- 参数 : infoCallback {(info)=>{}} 输出信息回调
- 参数 : errorCallback {(err)=>{}} 错误信息回调
- 版本 : 1.0.8


```javascript
//等待获取shizuku权限，如果没有权限那么就会一直等待下去
$szk.getPermit();
$szk.exe("ls",
    (info)=> {
        //信息输出回调
        log(info);
    },
    (error)=> {
        //异常输出回调
        $log.e(error);
    }
);
```


#### exe(cmd, infoCallback, errorCallback, endCallback)

> 执行命令

- 参数 : cmd {string} 命令
- 参数 : infoCallback {(info)=>{}} 输出信息回调
- 参数 : errorCallback {(err)=>{}} 错误信息回调
- 参数 : endCallback {(result)=>{}} 结束执行回调
- 版本 : 1.0.8


```javascript
//等待获取shizuku权限，如果没有权限那么就会一直等待下去
$szk.getPermit();
$szk.exe("ls",
    (info)=> {
        //信息输出回调
        log(info);
    },
    (error)=> {
        //异常输出回调
        $log.e(error);
    },
    (result)=> {
        //结束回调
        log(result)
    }
);
```


#### exe(cmd, startCallback, infoCallback, errorCallback, endCallback)

> 执行命令

- 参数 : cmd {string} 命令
- 参数 : startCallback {()=>{}} 开始执行时的回调
- 参数 : infoCallback {(info)=>{}} 输出信息回调
- 参数 : errorCallback {(err)=>{}} 错误信息回调
- 参数 : endCallback {(result)=>{}} 结束执行回调
- 版本 : 1.0.8


```javascript
//等待获取shizuku权限，如果没有权限那么就会一直等待下去
$szk.getPermit();
$szk.exe("ls",
    ()=> {
        //开始执行回调
        log("开始执行");
    },
    (info)=> {
        //信息输出回调
        log(info);
    },
    (error)=> {
        //异常输出回调
        $log.e(error);
    },
    (result)=> {
        //结束回调
        log(result)
    }
);
```

---

## $permit - 权限工具

- 更新时间:2026-01-30 19:32:54

> 权限工具




#### floaty()

> 获取悬浮窗权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取悬浮窗权限
$permit.floaty();
```


#### hasFloaty()

> 判断是否有悬浮窗权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("悬浮窗",$permit.hasFloaty());
```


#### wza()

> 获取无障碍权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次
> 
> 如果有Root权限:则使用Root权限为本应用授权永久无障碍
> 
> 如果有Shizuku权限:则使用Shizuku权限为本应用授权永久无障碍
> 
> 如果没有Root和Shizuku:则进行普通权限申请(非永久有效,受系统限制)

- 版本 : 1.1.6


```javascript
//获取无障碍权限
$permit.wza();
```


#### hasWza()

> 判断是否有无障碍权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("无障碍",$permit.hasWza());
```


#### sd()

> 获取存储权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取存储权限
$permit.sd();
```


#### hasSd()

> 判断是否有存储权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("存储权限",$permit.hasSd());
```


#### call()

> 获取电话权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取电话权限
$permit.call();
```


#### hasCall()

> 判断是否有电话权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("打电话",$permit.hasCall());
```


#### set()

> 获取修改系统设置权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取修改设置权限
$permit.set();
```


#### hasSet()

> 判断是否有修改系统设置权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("修改设置",$permit.hasSet());
```


#### net()

> 获取网络权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取网络权限
$permit.net();
```


#### hasNet()

> 判断是否有网络权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("网络权限",$permit.hasNet());
```


#### camera()

> 获取相机权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取相机权限
$permit.camera();
```


#### hasCamera()

> 判断是否有相机权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("相机权限",$permit.hasCamera());
```


#### record()

> 获取录音权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取录音权限
$permit.record();
```


#### hasRecord()

> 判断是否有录音权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("录音权限",$permit.hasRecord());
```


#### readSms()

> 获取读取短信权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取读取信息权限
$permit.readSms();
```


#### hasReadSms()

> 判断是否有读取短信权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("读取短信",$permit.hasReadSms());
```


#### sendSms()

> 获取发送短信权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取发送信息权限
$permit.sendSms();
```


#### hasSendSms()

> 判断是否有发送短信权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("发送短信",$permit.hasSendSms());
```


#### readContact()

> 获取读取联系人权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取读取联系人权限
$permit.readContact();
```


#### hasReadContact()

> 判断是否有读取联系人权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("读取联系人",$permit.hasReadContact());
```


#### writeContact()

> 获取写入联系人权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取写入联系人权限
$permit.writeContact();
```


#### hasWriteContact()

> 判断是否有写入联系人权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("写入联系人",$permit.hasWriteContact());
```


#### loc()

> 获取定位权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.1.6


```javascript
//获取定位权限
$permit.loc();
```


#### hasLoc()

> 判断是否有定位权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.1.6


```javascript
log("位置权限",$permit.hasLoc());
```


#### readCalendar()

> 获取读取日历权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.2.2


```javascript
//获取读取日历权限
$permit.readCalendar();  //获取读取日历权限
```


#### hasReadCalendar()

> 判断是否有读取日历权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.2.2


```javascript
log("读取日历",$permit.hasReadCalendar());
```


#### writeCalendar()

> 获取写入日历权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 版本 : 1.2.2


```javascript
//获取写入日历权限
$permit.writeCalendar();
```


#### hasWriteCalendar()

> 判断是否有写入日历权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 返回 : {boolean} 是否有权限
- 版本 : 1.2.2


```javascript
log("写入日历",$permit.hasWriteCalendar());
```


#### hasPermit(permitName)

> 判断是否有权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 参数 : permitName {string} 权限名 
- 返回 : {boolean} 是否有权限
- 版本 : 1.2.2


```javascript
//判断是否有权限
$permit.hasPermit("android.Manifest.permission.GET_ACCOUNTS");
//等同于
$permit.hasPermit("android.permission.GET_ACCOUNTS");
```


#### hasPermit(permitNames)

> 判断是否有权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 参数 : permitNames {string[]} 权限名 
- 返回 : {boolean} 是否有权限
- 版本 : 1.2.2


```javascript
let permits = ["android.permission.READ_CALENDAR","android.permission.WRITE_CALENDAR"];
//判断是否有权限
$permit.hasPermit(permits);
```


#### getPermit(permitNames)

> 获取权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 参数 : permitNames {string[]} 权限名 
- 版本 : 1.2.2


```javascript
let permits = ["android.permission.READ_CALENDAR","android.permission.WRITE_CALENDAR"];
//获取权限
$permit.getPermit(permits);
```


#### getPermit(permitName)

> 获取权限
> 
> 注意：在$permit中调用任何权限,都只会调用一次

- 参数 : permitName {string} 权限名 
- 版本 : 1.2.2


```javascript
//获取权限
$permit.getPermit("android.Manifest.permission.GET_ACCOUNTS");
//等同于
$permit.getPermit("android.permission.GET_ACCOUNTS");
```


#### hasNotifyAccess()

> 是否已授予通知访问权限

- 返回 : {boolean} 是否有通知访问权限
- 版本 : 1.6.4


#### notifyAccess()

> 获取通知访问权限
> 
> 此权限将允许应用读取所有通知

- 版本 : 1.6.4


#### hasReadVideo()

> 判断是否有读取视频权限

- 返回 : {boolean} 是否有读取视频权限
- 版本 : 1.6.4


#### readVideo()

> 获取读取视频权限

- 版本 : 1.6.4


#### hasReadImage()

> 判断是否有读取图片权限

- 返回 : {boolean} 是否有读取视频权限
- 版本 : 1.6.4


#### readImage()

> 获取读取图片权限

- 版本 : 1.6.4


#### hasReadAudio()

> 判断是否有读取音频权限

- 返回 : {boolean} 是否有读取视频权限
- 版本 : 1.6.4


#### readAudio()

> 获取读取音频权限

- 版本 : 1.6.4


#### hasReadMedia()

> 判断是否有读取媒体权限
> 
> 这个方法综合了读取音频、图片、视频权限

- 返回 : {boolean} 是否有读取媒体权限
- 版本 : 1.6.4


#### readMedia()

> 获取读取媒体权限
> 
> 这个方法综合了读取音频、图片、视频权限

- 版本 : 1.6.4