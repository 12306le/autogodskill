# 示例：应用/系统/多线程


## $app-#U5e94#U7528#U64cd#U4f5c-02.#U8fd0#U884c#U5e94#U7528

```javascript
// AIGame官方示例


$app.runApp("QQ");//应用名




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-03.#U8fd0#U884c#U5305#U540d

```javascript
// AIGame官方示例


$app.runPkg("com.tencent.mobileqq");//传入包名




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-04.#U6253#U5f00#U5e94#U7528

```javascript
// AIGame官方示例


$app.run("QQ");//可传入包名或者应用名




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-05.#U83b7#U5f97#U6240#U6709#U7684#U5e94#U7528#U4fe1#U606f

```javascript
// AIGame官方示例


//获得所有应用信息
let apps = $app.ls();

//打印所应用信息
for(let i = 0 ; i < apps.size() ; i++){
    log(apps.get(i));
}




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-06.#U83b7#U5f97#U6700#U8fd1#U8fd0#U884c#U7684#U5e94#U7528

```javascript
// AIGame官方示例


//获得最进运行的应用
if ($app.hasUsagePermit()) {
    let pkgList = $app.lsRecent();
    if (pkgList !== null) {
        for (let i = 0; i < pkgList.size(); i++) {
            console.log(pkgList[i]);
        }
    }
} else {
    $app.getUsagePermit();
}




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-07.#U542f#U52a8#U6d3b#U52a8

```javascript
// AIGame官方示例


//打开QQ
$app.startActivity("QQ","com.tencent.mobileqq.activity.SplashActivity");




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-08.#U68c0#U67e5#U5305#U662f#U5426#U5b58#U5728

```javascript
// AIGame官方示例


let pkg = "org.aigame.pro";

if ($app.pkgExists(pkg)) {
    alert(pkg,"存在");
} else {
    alert(pkg,"不存在");
}




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-09.#U83b7#U5f97#U5305#U540d#U540d#U79f0

```javascript
// AIGame官方示例


//获得包名
let pkg = $app.pkgName("QQ");


alert("应用包名",pkg);




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-10.#U6839#U636e#U5305#U540d#U62ff#U5e94#U7528#U540d

```javascript
// AIGame官方示例


//获得应用名
let appName = $app.appName("com.android.settings");

alert("应用名称",appName);//设置




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-11.#U5378#U8f7d#U5e94#U7528

```javascript
// AIGame官方示例


//此函数部分手机不支持
//卸载QQ
$app.uninstallApp("QQ");




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-12.#U5378#U8f7d#U5305#U540d

```javascript
// AIGame官方示例


//此函数部分手机不支持
//卸载QQ
$app.uninstallPkg("com.tencent.mobileqq");




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-13.#U5378#U8f7d

```javascript
// AIGame官方示例


//卸载QQ
$app.uninstall("QQ");//应用名或包名




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-14.#U6253#U5f00#U7f51#U9875

```javascript
// AIGame官方示例


//打开网址
let myUrl = "www.baidu.com";

$app.openUrl(myUrl);




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-15.#U5206#U4eab#U56fe#U7247

```javascript
// AIGame官方示例


//分享本地图片
let path = "/sdcard/Pictures/t01.png";
$app.shareImg(path);




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-16.#U5206#U4eab#U6587#U672c

```javascript
// AIGame官方示例


//分享文本
let text = "你好";
$app.shareText(text);




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-17.#U53d1#U9001#U77ed#U4fe1

```javascript
// AIGame官方示例


$app.sendSms("13593749477","你好我是xxx");




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-18.#U62e8#U6253#U7535#U8bdd

```javascript
// AIGame官方示例


$app.call("13593749477");




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-19.#U53d1#U9001#U90ae#U4ef6

```javascript
// AIGame官方示例


$app.sendMail("3502037911@qq.com","标题","内容");




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-20.#U6253#U5f00#U5e94#U7528#U8bbe#U7f6e

```javascript
// AIGame官方示例


//前往权限设置界面
$app.appSetting("AIGame Pro");




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-21.#U67e5#U770b#U6587#U4ef6

```javascript
// AIGame官方示例


//打开文件
$app.viewFile("/sdcard/Pictures/test.text");




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-22.#U7f16#U8f91#U6587#U4ef6

```javascript
// AIGame官方示例


//编辑文件
$app.editFile("/sdcard/Pictures/test.text");




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-23.#U662f#U5426#U6709#U4f7f#U7528#U60c5#U51b5#U6743#U9650

```javascript
// AIGame官方示例


$app.hasUsagePermit();




// 示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-24.#U4f7f#U7528#U60c5#U51b5

```javascript
// AIGame官方示例


$app.getUsagePermit();




// 示例结束
```


## $bus-#U6d88#U606f#U603b#U7ebf-01.#U5217#U51fa#U6240#U6709#U76d1#U542c#U5668

```javascript
// AIGame官方示例


//获得所有监听器列表
let monis = $bus.ls();

log(monis);//[我的监听器1号]




// 示例结束
```


## $bus-#U6d88#U606f#U603b#U7ebf-01.#U5e7f#U64ad#U4ea4#U4e92-01.#U5f00#U542f#U5e7f#U64ad#U4e8b#U4ef6#U76d1#U542c

```javascript
//


//想要接收全局广播,必须要先注册一个广播事件监听器
//监听器的名称为`broadcast`,回调参数是`Intent`类型

$bus.event("broadcast",(intent)=>{
    log("接受到了广播:");
    let extras = intent.getExtras();
    let value = extras.get("mKey");
    log(`广播数据:${value}`);
});



//
```


## $bus-#U6d88#U606f#U603b#U7ebf-01.#U5e7f#U64ad#U4ea4#U4e92-02.#U53d1#U9001#U5e7f#U64ad

```javascript
//


let intent = $app.newIntent({
    action: "org.aigame.pro.bus.action",
    // 随便写点数据,一会而$bus会接收到广播,在里面获取这个数据
    extras: [{
        name: "mKey",
        value: "哈哈哈"
    } ],
    // 指定接受端的应用(固定写法)
    component: {
        cls: "org.aigame.api.bus.receiver.AgBusReceiver",
        pkg: "org.aigame.pro"
    }
});

//然后发送广播
$app.sendBroadcast(intent,"org.aigame.pro.bus.permission");



//
```


## $bus-#U6d88#U606f#U603b#U7ebf-01.#U5e7f#U64ad#U4ea4#U4e92-04.#U5728autojs#U4e2d#U4e0eAIGame#U5e7f#U64ad#U4ea4#U4e92

```javascript
//以下是auto.js的代码,无法在aigame中执行

app.sendBroadcast({
    packageName: "org.aigame.pro",
    className: "org.aigame.api.bus.receiver.AgBusReceiver",
    extras: {
        mKey: "我是auto.js发送的广播数据",
    } ,
});


//
```


## $bus-#U6d88#U606f#U603b#U7ebf-02.#U53d1#U9001#U4e00#U6761#U4fe1#U606f

```javascript
// AIGame官方示例


$bus.post("我的监听器1号","我是数据");




// 示例结束
```


## $bus-#U6d88#U606f#U603b#U7ebf-03.#U6dfb#U52a0#U76d1#U542c

```javascript
// AIGame官方示例


$bus.event("我的监听器1号",(data)=>{
log("获得数据:",data);
toast(data);
});




// 示例结束
```


## $bus-#U6d88#U606f#U603b#U7ebf-04.#U79fb#U9664#U76d1#U542c#U5668

```javascript
// AIGame官方示例


//指定关闭监听器
$bus.close("我的监听器1号");




// 示例结束
```


## $bus-#U6d88#U606f#U603b#U7ebf-05.#U79fb#U9664#U6240#U6709#U76d1#U542c#U5668

```javascript
// AIGame官方示例


$bus.clear();//关闭所有监听器




// 示例结束
```


## $bus-#U6d88#U606f#U603b#U7ebf-06.#U5173#U95ed#U6240#U6709#U76d1#U542c#U5668

```javascript
// AIGame官方示例


$bus.stopAll();//关闭所有监听器效果和clear()一样




// 示例结束
```


## $device-#U8bbe#U5907#U4fe1#U606f-01.#U83b7#U53d6#U8bbe#U5907#U4fe1#U606f

```javascript
//AIGame 官方示例


log("屏幕的宽度",$device.width);
log("屏幕的高度",$device.height);
log("Build ID",$device.buildId);
log("Build Display",$device.buildDisplay);
log("主板名称",$device.broad);
log("品牌名称",$device.brand);
log("设备名称",$device.device);
log("型号名称",$device.model);
log("产品名称",$device.product);
log("引导加载程序名称",$device.bootloader);
log("硬件名称",$device.hardware);
log("指纹信息",$device.fingerprint);
log("序列号",$device.serial);
log("SDK版本号",$device.sdkInt);
log("内部版本号",$device.incremental);
log("Android版本号",$device.release);
log("基础操作系统版本",$device.baseOS);
log("安全补丁版本",$device.securityPatch);
log("开发代号",$device.code);

//获取其他信息

log("IMEI号码",$device.getIMEI());
log("Android ID",$device.getAndroidId());
log("MAC 地址",$device.getMacAddress());
log("屏幕亮度",$device.getBrightness());
log("屏幕亮度模式",$device.getBrightnessMode());
log("音乐音量",$device.getMusicVolume());
log("通知音量",$device.getNotificationVolume());
log("闹钟音量",$device.getAlarmVolume());
log("音乐最大音量",$device.getMusicMaxVolume());
log("通知最大音量",$device.getNotificationMaxVolume());
log("闹钟最大音量",$device.getAlarmMaxVolume());
log("电池电量百分比",$device.getBattery());
log("是否正在充电",$device.isCharging());
log("总内存",$device.getTotalMem());
log("可用内存",$device.getAvailMem());
log("屏幕是否亮起",$device.isScreenOn());
log("屏幕是否熄灭",$device.isScreenOff());



//示例结束
```


## $engine-#U811a#U672c#U5f15#U64ce-01.#U4e0d#U540c#U7ebf#U7a0b#U4e2d#U7684#U8def#U5f84-#U811a#U672c1

```javascript
//在AIGame中，每个被执行的脚本都被看作成一个任务($task)
//每个被执行的脚本都含有一个属于自己的($task)任务对象
//我们可以根据每个脚本专有的($task)任务对象获取数据

for(let i = 0 ; i < 5; i++){
    sleep(1000);
    //获取当前脚本路径
    log("脚本1:"+$task.getPath());
}
```


## $engine-#U811a#U672c#U5f15#U64ce-01.#U4e0d#U540c#U7ebf#U7a0b#U4e2d#U7684#U8def#U5f84-#U811a#U672c2

```javascript
//在AIGame中，每个被执行的脚本都被看作成一个任务($task)
//每个被执行的脚本都含有一个属于自己的($task)任务对象
//我们可以根据每个脚本专有的($task)任务对象获取数据

for(let i = 0 ; i < 5; i++){
    sleep(1000);
    //获取当前脚本路径
    log("脚本2:"+$task.getPath());
}
```


## $engine-#U811a#U672c#U5f15#U64ce-01.#U4e0d#U540c#U7ebf#U7a0b#U4e2d#U7684#U8def#U5f84-01.#U542f#U52a8#U591a#U4e2a#U811a#U672c

```javascript
//AIGame 官方示例

let path1 = "example/$engine - 脚本引擎/01.不同线程中的路径/脚本1.js";
let path2 = "example/$engine - 脚本引擎/01.不同线程中的路径/脚本2.js";

$engine.run(path1);
$engine.run(path2);


//示例结束
```


## $engine-#U811a#U672c#U5f15#U64ce-01.#U6267#U884c#U811a#U672c

```javascript
//官方示例

$engine.run("/example/$engine - 脚本引擎/test/run.js");


//示例结束
```


## $engine-#U811a#U672c#U5f15#U64ce-02.#U8fd0#U884c#U4ee3#U7801

```javascript
//官方示例

//读取脚本文件
let code = $file.read("/example/$engine - 脚本引擎/test/run.js");
//执行脚本代码
$engine.runCode(code);


//示例结束
```


## $engine-#U811a#U672c#U5f15#U64ce-03.#U8fd0#U884c#U4ee3#U7801-#U5168#U53c2

```javascript
//官方示例

//定义脚本路径
let path = "/example/$engine - 脚本引擎/test/run.js";
//读取脚本文件
let code = $file.read(path);
//执行脚本代码
$engine.runCode(path, code);


//示例结束
```


## $engine-#U811a#U672c#U5f15#U64ce-05.#U7f57#U5217#U4efb#U52a1#U4fe1#U606f

```javascript
//官方示例


let list = $engine.lsTask();

for (let item of list) {
    log(item);
}



//示例结束
```


## $engine-#U811a#U672c#U5f15#U64ce-06.#U505c#U6b62#U6240#U6709

```javascript
//官方示例



$engine.stopAll();



//示例结束
```


## $engine-#U811a#U672c#U5f15#U64ce-test-delay

```javascript
//这里模拟一个延迟任务
//主要是为了演示脚本的运行与暂停
//由于脚本引擎是解释执行的
//因此暂停脚本的时候：会从当前执行的语句暂停

for (let i = 0; i < 15; i++) {
    sleep(1000);
    info("我还活着:" + (i + 1) + "秒");
}
```


## $engine-#U811a#U672c#U5f15#U64ce-test-run

```javascript
alert("提示", "我是被执行的脚本");
```


## $event-#U4e8b#U4ef6#U76d1#U542c-01.#U97f3#U91cf#U76d1#U542c

```javascript
//官方示例

//运行此代码之后，尝试自己手动加减音量，然后回来看日志
$event.on("volume",(data)=>{
    log("描述："+data.desc);
    log("音量类型："+data.value.type);
    log("当前音量："+data.value.curVolume);
    log("最大音量："+data.value.maxVolume);
    log("");//打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-02.#U5c4f#U5e55#U76d1#U542c

```javascript
//官方示例

//运行此代码之后，尝试自己手动关闭屏幕，然后回来看日志
$event.on("screen",(data)=>{
    //除了监听，你也可以使用 $screen.isScreenOn() 函数判断屏幕是否点亮
    log("描述："+data.desc);
    log("是否点亮："+data.value.screenOn);
    log("是否关闭："+data.value.screenOff);
    log("");//打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-03.#U7528#U6237#U89e3#U9501#U76d1#U542c

```javascript
//官方示例


//运行此代码之后，尝试自己手动解锁屏幕，然后回来看日志
$event.on("screenUnlock",(data)=>{
    log("描述："+data.desc);
    log("是否解锁："+data.value.screenUnlock);
    log("");//打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-04.#U7f51#U7edc#U76d1#U542c

```javascript
//官方示例


//运行此代码之后，尝试自己手动联网或关闭网络，然后回来看日志
$event.on("net",(data)=>{
    //此方法不是专门针对wifi做的监听，所以wifi关闭时未必会回调这里
    //如果想专门监听wifi请移步到下一个示例[05.WIFI监听.js]
    log("描述："+data.desc);
    log("网络类型："+data.value.type);//常用
    log("链接状态："+data.value.connect);//常用
    log("原因："+data.value.type);
    log("附属类型："+data.value.subtype);
    log("信息："+data.value.info);
    log("");//打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-05.WIFI#U76d1#U542c

```javascript
//官方示例


//运行此代码之后，尝试自己手动链接wifi或断开wifi，然后回来看日志
$event.on("wifi",(data)=>{
    log("描述："+data.desc);
    log("是否启用："+data.value.enable);
    log("正在启用："+data.value.enabling);
    log("是否禁用："+data.value.disable);
    log("正在禁用："+data.value.disabling);
    log("");//打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-06.WIFI#U72b6#U6001#U76d1#U542c

```javascript
//官方示例


//运行此代码之后，尝试自己手动链接wifi或断开wifi，然后回来看日志
$event.on("wifiState",(data)=>{
    log("描述："+data.desc);
    log("类型："+data.value.type);
    log("原因："+data.value.reason);
    log("信息："+data.value.info);
    log("附属类型："+data.value.subtype);
    log("");//打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-07.#U7535#U6c60#U76d1#U542c

```javascript
//官方示例

//主要监听电池电量相关的事件：充电器链接、电量低、电量恢复等事件
$event.on("power",(data)=>{
    log("描述："+data.desc);
    log("充电器链接："+data.value.connect);
    log("电量过低："+data.value.low);
    log("电量恢复："+data.value.okay);
    log("");//打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-08.#U7535#U91cf#U76d1#U542c

```javascript
//官方示例

//主要监听电池电量:电量百分比等等
$event.on("battery",(data)=>{
    log("描述："+data.desc);
    log("电量百分比："+data.value.percent);
    log("是否充电："+data.value.isCharge);
    log("充电方式："+data.value.chargeType);
    log("");//打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-09.#U84dd#U7259#U8fde#U63a5#U76d1#U542c

```javascript
//官方示例

//安卓6-11要位置权限 安卓12要蓝牙权限
let ps = ["android.permission.ACCESS_FINE_LOCATION","android.permission.BLUETOOTH_CONNECT"];

if ($permit.hasPermit(ps)) {
    log("权限满足");
} else {
    $permit.getPermit(ps);
}


//可以尝试连接蓝牙耳机，观察日志信息
$event.on("bluetooth",(data)=> {
    log("描述："+data.desc);
    log("是否连接："+data.value.connect);
    log("是否开启："+data.value.on);
    log("是否关闭："+data.value.off);
    log("正在开启："+data.value.starting);
    log("正在关闭："+data.value.closing);

    if (data.value.address != null) {
        log("连接MAC地址: "+data.value.address);
    }

    //需要蓝牙权限:如果没有就是null
    if (data.value.name != null) {
        log("设备名称: "+data.value.name);
    }

    //需要蓝牙权限并且安卓11+:如果没有就是null
    if (data.value.alias != null) {
        log("设备别名: "+data.value.alias);
    }

    log(""); //打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-10.#U9501#U5c4f#U76d1#U542c

```javascript
//官方示例

//手动锁屏再解锁，最后观察日志
$event.on("lock",(data)=> {
    //lock事件并非是一个专门监听屏幕事件的监听器
    //如果你想监听屏幕事件，请移步[02.屏幕监听.js]
    //除了监听，你也可以使用 $device.isLock() 来判断设备是否锁定
    log("描述："+data.desc);
    log("是否锁屏："+data.value.lock);
    log("屏幕点亮："+data.value.screenOn);
    log("屏幕熄灭："+data.value.screenOff);
    log(""); //打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-11.#U78c1#U76d8#U76d1#U542c

```javascript
//官方示例

//主要用来监听磁盘挂载、移除等事件，不算常用
$event.on("media",(data)=> {
    log("描述："+data.desc);
    log("挂载："+data.value.mount);
    log("卸载："+data.value.unmount);
    log("移除："+data.value.remove);
    log("移除操作不当："+data.value.badRemove);
    log(""); //打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-12.#U6309#U952e#U76d1#U542c

```javascript
//官方示例

//运行此代码之后，尝试自己手动HOME按键或者菜单RECENT按键，然后回来看日志
$event.on("key",(data)=>{
    log(data);
    log("");//打印一行分割
});




//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-13.#U901a#U77e5#U76d1#U542c

```javascript
//官方示例

//获取应用访问权限
if (!$permit.hasNotifyAccess()) {
    $permit.notifyAccess();
} else {
    //通知监听 需要授予通知访问权限才能监听到通知
    $event.on("notify",(data)=> {
        log("包名:",data.value.pkg);
        log("标题:",data.value.title);
        log("内容:",data.value.text);
        log("副文本:",data.value.subText);
        log("提示文本:",data.value.tickerText);
        log("大文本:",data.value.bigText);
        log("时间:",data.value.postTime);
        log("是否为持续通知:",data.value.isOngoing);
        log("是否可清除:",data.value.isClearable);
        log(""); //用来分隔
    });
}



//示例结束
```


## $event-#U4e8b#U4ef6#U76d1#U542c-14.#U5c4f#U5e55#U65cb#U8f6c#U76d1#U542c

```javascript
//官方示例

//当屏幕旋转时触发
$event.on("screenDir",(data)=> {
    log("角度:",data.value.rotation);
    log("是否竖屏:",data.value.isVertical);
    log(""); //用来分隔
});


//示例结束
```


## $permit-#U6743#U9650#U5de5#U5177-03.#U5355#U72ec#U5224#U65ad#U67d0#U4e2a#U6743#U9650

```javascript
//使用安卓原生类中定义的权限字符串
let has = $permit.hasPermit(android.Manifest.permission.GET_ACCOUNTS);

if (has) {
    toast("有权限");
} else {
    toast("无权限");
}




//测试记录:
/*
【1】：模拟器
雷电    安卓9   完美
雷电    安卓7   完美


【2】：真机
OPPO A92S     安卓12     完美






*/
```


## $permit-#U6743#U9650#U5de5#U5177-04.#U5355#U72ec#U83b7#U53d6#U67d0#U4e2a#U6743#U9650

```javascript
//使用安卓原生类中定义的权限字符串

$permit.getPermit(android.Manifest.permission.GET_ACCOUNTS);





//测试记录:
/*
【1】：模拟器
雷电    安卓9   完美
雷电    安卓7   完美


【2】：真机
OPPO A92S     安卓12     完美






*/
```


## $permit-#U6743#U9650#U5de5#U5177-11.#U6743#U9650#U7ec4#U5224#U65ad#U6743#U9650

```javascript
// 电话权限组

let permits = [
    "android.permission.READ_PHONE_STATE",
    "android.permission.CALL_PHONE"
];


let has = $permit.hasPermit(permits);

if (has) {
    toast("有权限");
} else {
    toast("无权限");
}






//测试记录:
/*
【1】：模拟器
雷电    安卓9   完美
雷电    安卓7   完美


【2】：真机
OPPO A92S     安卓12     完美






*/
```


## $permit-#U6743#U9650#U5de5#U5177-12.#U6743#U9650#U7ec4#U83b7#U53d6#U6743#U9650

```javascript
// 电话权限组

let permits = [
    "android.permission.READ_PHONE_STATE",
    "android.permission.CALL_PHONE"
];


$permit.getPermit(permits);






//测试记录:
/*
【1】：模拟器
雷电    安卓9   完美
雷电    安卓7   完美


【2】：真机
OPPO A92S     安卓12     完美






*/
```


## $sys-#U7cfb#U7edf#U5de5#U5177-01.#U83b7#U53d6#U4fee#U6539#U8bbe#U7f6e#U6743#U9650

```javascript
// AIGame官方示例


//获取修改系统设置权限
$sys.getSetPermit();




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-02.#U83b7#U53d6#U7535#U8bdd#U6743#U9650

```javascript
// AIGame官方示例


//获得电话权限
if (!$sys.enableCall()) {
    $sys.getCallPermit();
}

//拨打电话
//$app.call("13593749477");




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-03.#U662f#U5426#U62e5#U6709#U7535#U8bdd#U6743#U9650

```javascript
// AIGame官方示例


//判断是否获得电话权限
if ($sys.enableCall()) {
    toast("拥有权限");
}else{
    toast("无电话权限");
}




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-04.#U8bbe#U7f6e#U98de#U884c#U6a21#U5f0f

```javascript
// AIGame官方示例


//设置飞行模式
$sys.airplane(true);




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-05.#U8bbe#U7f6e#U5a92#U4f53#U97f3#U91cf

```javascript
// AIGame官方示例


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




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-06.#U83b7#U5f97#U552f#U4e00#U6807#U8bc6

```javascript
// AIGame官方示例


let id = $sys.getDeviceId();

alert("设备id",id);




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-08.#U6e05#U9664#U526a#U5207#U677f#U5185#U5bb9

```javascript
// AIGame官方示例


$sys.clearClip();




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-09.#U83b7#U5f97#U526a#U5207#U677f#U6587#U5b57

```javascript
// AIGame官方示例


//获得内容
let content = $sys.getClip();
alert("剪切板",content);




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-10.#U8bbe#U7f6e#U526a#U5207#U677f

```javascript
// AIGame官方示例


//设置剪切板
$sys.setClip("Hello AIGame !");




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-11.#U662f#U5426#U5ffd#U7565#U7535#U6c60#U4f18#U5316

```javascript
// AIGame官方示例


//是否忽略电池优化
let is = $sys.ignorePower("org.aigame.app");
alert("是否忽略电池优化",is);




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-12.#U8bf7#U6c42#U5ffd#U7565#U7535#U6c60#U4f18#U5316

```javascript
// AIGame官方示例


//请求忽略电池优化
$sys.requestIgnorePower("org.aigame.app");




// 示例结束
```


## $task-#U811a#U672c#U4efb#U52a1-01.#U83b7#U5f97#U5f53#U524d#U811a#U672c#U7684#U8def#U5f84

```javascript
//AIGame 官方示例


alert("当前任务路径",$task.getPath());



//示例结束
```


## $task-#U811a#U672c#U4efb#U52a1-02.#U76f8#U5bf9#U5f53#U524d#U811a#U672c#U7684#U8def#U5f84

```javascript
//AIGame 官方示例


alert("相对路径",$task.getPath("./../../res"));



//示例结束
```


## $task-#U811a#U672c#U4efb#U52a1-03.#U81ea#U8eab#U505c#U6b62

```javascript
//AIGame 官方示例


for (let i = 0; i < 10; i++) {
    sleep(1000);
    toast("我还活着");
    if (i == 3) {
        //每个脚本都会内置一个独属于自己的$task对象，代表当前脚本任务
        $task.stop();
    }
}



//示例结束
```


## $thread-#U591a#U7ebf#U7a0b-01.#U591a#U7ebf#U7a0b

```javascript
//AIGame 官方示例

let t1 = $thread.create(()=> {
    for (let i = 0; i < 10; i++) {
        sleep("300");
        log(t1.getName()+"==>"+i);
    }
    log(t1.getName()+"执行完毕");
});

let t2 = $thread.create(()=> {
    for (let i = 0; i < 10; i++) {
        sleep("300");
        log(t2.getName()+"==>"+i);
    }
    log(t1.getName()+"执行完毕");
});

let t3 = $thread.create(()=> {
    for (let i = 0; i < 10; i++) {
        sleep("300");
        log(t3.getName()+"==>"+i);
    }
    log(t1.getName()+"执行完毕");
});



t1.start();
t2.start();
t3.start();



//示例结束
```


## $thread-#U591a#U7ebf#U7a0b-01.#U5faa#U73af#U6267#U884c#U5668-01.#U521b#U5efa#U5faa#U73af#U6267#U884c#U5668

```javascript
//AIGame 官方示例

//执行完这个脚本后再执行[02.停止循环任务.js]可见效果

let t1 = $thread.loop("循环1号",()=>{
    sleep(1000);
    log("我还活着！");
});


t1.start();




//示例结束
```


## $thread-#U591a#U7ebf#U7a0b-01.#U5faa#U73af#U6267#U884c#U5668-02.#U505c#U6b62#U5faa#U73af#U4efb#U52a1

```javascript
//AIGame 官方示例

//关闭循环器
$thread.stopLoop("循环1号");
//或者直接停止全部
//$thread.stopAllLoop();



//示例结束
```
