# 应用管理 API

> 管理Android应用：启动、查询、列表等操作。

## 目录
- [$app - 应用操作](#app---应用操作)
- [AppInfo - 应用信息](#appinfo---应用信息)
- [AppTaskInfo - 任务信息](#apptaskinfo---任务信息)

---

## $app - 应用操作

- 更新时间:2026-01-30 19:32:51

> 应用操作
> 
> 这里包含了一写常用的应用操作、意图操作、或者一些拓展操作：发送短信等等。




这里我给个我自己经常使用的工具函数，就是添加QQ群函数。


```xml
//[工具] 可以用来添加QQ群
let joinQQGroup = function (qqNum) {
    $app.startActivity({
        data: `mqqapi://card/show_pslcard?src_type=internal&version=1&uin=${qqNum}&card_type=group&from=qrcode`,
        pkg: "com.tencent.mobileqq"
    });
}
//使用方式
joinQQGroup(661266412);
```


#### getIcon(name)

> 获取应用图标

- 参数 : name {string} 应用名称或包名 
- 返回 : {Image} 图标
- 版本 : 1.0.0


```javascript
//获取悬浮窗权限
$floaty.getPermit();
//获取图标
let icon = $app.getIcon("QQ");//应用名称或者包名
//显示图片
$img.show(icon);//(需要用悬浮窗权限) 也可以直接调用 icon.show(); //icon是{Image}类对象，因此可以世界调用show()方法。
```


#### runApp(appName)

> 运行应用

- 参数 : appName {String} 应用名 
- 返回 : {boolean} 是否运行成功
- 版本 : 1.0.0


```javascript
$app.runApp("QQ");//应用名
```


#### launchApp(appName)

> 运行应用
> 
> 这个函数的效果和$app.runApp("应用");相同

- 参数 : appName {String} 应用名称 
- 返回 : {boolean} 是否运行成功
- 版本 : 1.0.0


```javascript
$app.launchApp("QQ");//应用名
```


#### launch(appName)

> 运行应用
> 
> 这个函数的效果和$app.runApp("应用");相同

- 参数 : appName {String} 应用名称 
- 返回 : {boolean} 是否运行成功
- 版本 : 1.0.0


```javascript
$app.launch("QQ");//应用名或包名
```


#### launchPkg(packageName)

> 运行包名
> 
> 此函数和$app.runPkg("包名");效果相同

- 参数 : packageName {String} 程序包名 
- 返回 : {boolean} 是否跳转成功
- 版本 : 1.0.0


```javascript
$app.launchPkg("com.tencent.mobileqq");//传入包名
```


#### runPkg(packageName)

> 运行包名

- 参数 : packageName {String} 程序包名 
- 返回 : {boolean} 是否跳转成功
- 版本 : 1.0.0


```javascript
$app.runPkg("com.tencent.mobileqq");//传入包名
```


#### run(name)

> 打开应用(推荐)
> 
> 最简洁的启动应用函数，推荐使用

- 参数 : name {string} 包名或程序名称 
- 返回 : {boolean} 是否打开成功
- 版本 : 1.0.0


```javascript
$app.run("QQ");//可传入包名或者应用名
```


#### ls()

> 获得应用列表

- 返回 : {AppInfo[]} 应用信息列表
- 版本 : 1.0.0


```javascript
//获得所有应用信息
let apps = $app.ls();//返回一个AppInfo的列表
//打印所应用信息
for(let i = 0 ; i < apps.size() ; i++){
    let appInfo = apps.get(i);//获得{AppInfo}对象(注意{AppInfo}是由本平台封装的对象)
    //一些常用属性
    let appName = appInfo.appName;//应用名称{string}
    let pkgName = appInfo.pkgName;//包名{string}
    let icon = appInfo.icon;//图标{Image} 可以直接调用 icon.show(); 显示出来(注意{Image}是由本平台封装的对象)
    let info = appInfo.info;//安卓原生应用信息{android.content.pm.ApplicationInfo}
    //{ApplicationInfo}常用属性(安卓自带的对象)
    let sourceDir = info.sourceDir; // {string}应用APK文件的路径
    let className = info.className; // {string}应用的主Application类名
    let packageName = info.packageName; // {string}应用的包名
    let componentFactory = info.appComponentFactory; // {string}应用组件工厂类，用于创建Activity、Service等组件
    let sdkVersion = info.compileSdkVersion; // {int}应用编译时使用的SDK版本号
    let sdkName = info.compileSdkVersionCodename; // {string}应用编译时使用的SDK版本代号，如"Q"、"R"等
    let dataDir = info.dataDir; // {string}应用的数据目录，一般为/data/data/包名
    let dpDataDir = info.deviceProtectedDataDir; // {string}设备受保护存储中的应用数据目录
}
```


#### lsUserApp()

> 获得用户应用列表

- 返回 : {AppInfo[]} 应用列表
- 版本 : 1.3.2


```javascript
//获得用户应用列表
let apps = $app.lsUserApp();
//打印所应用信息
for(let i = 0 ; i < apps.size() ; i++){
    log(apps.get(i));
}
```


#### lsSysApp()

> 获得系统应用列表

- 返回 : {AppInfo[]} 应用列表
- 版本 : 1.3.2


```javascript
//获得系统应用列表
let apps = $app.lsSysApp();
//打印所应用信息
for(let i = 0 ; i < apps.size() ; i++){
    log(apps.get(i));
}
```


#### lsRecent()

> 获得最近运行的应用

- 返回 : {AppTaskInfo[]} 应用信息列表
- 版本 : 1.0.1


```javascript
//获得最近运行的应用(需要用到查询应用使用情况的权限)
if ($app.hasUsagePermit()) {
    let pkgList = $app.lsRecent();
    if (pkgList !== null) {
        for (let i = 0; i < pkgList.size(); i++) {
            let taskInfo = pkgList.get(i);//获得{AppTaskInfo}对象(由本平台封装的对象)
            //常用属性：(可参考AppTaskInfo文档)
            let appName = taskInfo.appName;//{string}应用名称
            let pkgName = taskInfo.pkgName;//{string}包名
            let lastUseTime = taskInfo.lastUseTime;//{string}最后使用时间 对lastUsedTime进行格式化日期的字符串
            let lastUsedTime = taskInfo.lastUsedTime;//{long}最后使用时间
            let info = taskInfo.info;//{android.content.pm.ApplicationInfo}应用信息(安卓类对象)
        }
    }
} else {
    //获取查询应用使用情况的权限
    $app.getUsagePermit();
}
```


#### startActivity(name)

> 打开AIGame中的界面
> 
> 允许用户打开本应用中集成的各种调试界面：Log日志、Device设备信息、Ocr文字识别、Yolo目标检测、Shizuku高级权限等。

- 参数 : name {string} 界面名称 
- 版本 : 1.6.9


```javascript
//打开日志界面
$app.startActivity("log");//推荐写法
$app.startActivity("console");//兼容auto.js写法
//打开设备信息界面
$app.startActivity("device");
//打开OCR调试界面
$app.startActivity("ocr");
//打开Yolo调试界面
$app.startActivity("yolo");
//打开Shizuku调试界面
$app.startActivity("shizuku");
```


#### startActivity(name, activityName)

> 启动活动

- 参数 : name {String} 包名或应用名 
- 参数 : activityName {String} activity地址 
- 返回 : {boolean} 是否跳转成功
- 版本 : 1.0.0


```javascript
//打开QQ
$app.startActivity("QQ","com.tencent.mobileqq.activity.SplashActivity");
```


#### pkgExists(pkgName)

> 包名是否存在

- 参数 : pkgName {String} 包名 
- 返回 : {boolean} 是否存在
- 版本 : 1.0.0


```javascript
let pkg = "org.aigame.pro";
if ($app.pkgExists(pkg)) {
    alert(pkg,"存在");
} else {
    alert(pkg,"不存在");
}
```


#### getPackageName(appName)

> 获得包名名称
> 
> 效果和$app.pkgName("QQ");相同

- 参数 : appName {String} app名称 
- 返回 : {String} 包名
- 版本 : 1.0.0


```javascript
//获得包名
let pkg = $app.getPackageName("QQ");
alert("应用包名",pkg);
```


#### pkgName(appName)

> 获得包名名称

- 参数 : appName {String} app名称 
- 返回 : {String} 包名
- 版本 : 1.0.0


```javascript
//获得包名
let pkg = $app.pkgName("QQ");
alert("应用包名",pkg);
```


#### appName(packageName)

> 根据包名拿应用名

- 参数 : packageName {String} 包名 
- 返回 : {String} app名称
- 版本 : 1.0.0


```javascript
//获得应用名
let appName = $app.appName("com.android.settings");
alert("应用名称",appName);//设置
```


#### installApk(apkPath)

> 安装apk文件
> 
> 此函数会获取系统的安装意图，然后尝试安装apk文件，前提是apk文件必须存在

- 参数 : apkPath {string} 路径(支持相对路径) 
- 返回 : {boolean} 是否成功获取安装意图
- 版本 : 1.3.3


```javascript
//安装本地apk文件
$app.installApk("./apk/qq.apk");
```


#### uninstallApp(name)

> 卸载应用

- 参数 : name {string} 应用名称 
- 版本 : 1.0.0


```javascript
//此函数部分手机不支持
//卸载QQ
$app.uninstallApp("QQ");
```


#### uninstallPkg(name)

> 卸载包名
> 
> 部分手机不支持

- 参数 : name {string} 应用名称或包名 
- 版本 : 1.0.0


```javascript
//此函数部分手机不支持
//卸载QQ
$app.uninstallPkg("com.tencent.mobileqq");
```


#### uninstall(name)

> 卸载

- 参数 : name {string} 应用名称或包名 
- 版本 : 1.0.0


```javascript
//此函数部分手机不支持
//卸载QQ
$app.uninstall("QQ");//应用名或包名
```


#### openUrl(url)

> 打开链接
> 
> 如果传入的网址不是以"http"开头的，则默认追加"http://"到连接前面

- 参数 : url {string} 网页链接 
- 版本 : 1.0.0


```javascript
//打开网址
let myUrl = "www.baidu.com";
$app.openUrl(myUrl);//http://www.baidu.com
```


#### shareImg(imgPath)

> 分享图片

- 参数 : imgPath {string} 图片路径 
- 版本 : 1.0.0


```javascript
//分享本地图片
let path = "/sdcard/Pictures/t01.png";
$app.shareImg(path);
```


#### shareText(content)

> 分享文本

- 参数 : content {string} 内容 
- 版本 : 1.0.0


```javascript
//分享文本
let text = "你好";
$app.shareText(text);
```


#### sendSms(phone, message)

> 发送短信
> 
> 跳转到发送短信的界面

- 参数 : phone {string} 电话号码 
- 参数 : message {string} 短信内容 
- 版本 : 1.0.0


```javascript
$app.sendSms("13593749477","你好我是xxx");
```


#### call(phoneNumber)

> 拨打电话
> 
> 如果拥有电话权限会直接拨通电话

- 参数 : phoneNumber {string} 电话号码 
- 版本 : 1.0.0


```javascript
$app.call("13593749477");
```


#### sendMail(mail, title, content)

> 发送邮件
> 
> 需要手机有自带的邮箱功能或应用

- 参数 : mail {string} 收件邮箱 
- 参数 : title {string} 标题 
- 参数 : content {string} 内容 
- 返回 : {boolean} 是否发送成功
- 版本 : 1.0.0


```javascript
$app.sendMail("3502037911@qq.com","标题","内容");
```


#### openAppSetting(name)

> 打开应用设置
> 
> 和$app.appSetting("AIGame Pro");效果相同
> 
> 会打开应用详情设置界面

- 参数 : name {string} 应用名称或包名 
- 返回 : {boolean} 是否打开成功
- 版本 : 1.0.0


```javascript
//前往权限设置界面
$app.openAppSetting("AIGame");
```


#### appSetting(name)

> 打开应用设置
> 
> 会打开应用详情设置界面

- 参数 : name {string} 应用名称或包名 
- 返回 : {boolean} 是否打开成功
- 版本 : 1.0.0


```javascript
//前往权限设置界面
$app.appSetting("AIGame");
```


#### viewFile(path)

> 查看文件

- 参数 : path {string} 文件路径 
- 返回 : {boolean} 是否打开成功
- 版本 : 1.0.0


```javascript
//打开文件
$app.viewFile("/sdcard/Pictures/test.text");
```


#### editFile(path)

> 编辑文件

- 参数 : path {string} 文件路径 
- 返回 : {boolean} 是否打开成功
- 版本 : 1.0.0


```javascript
//编辑文件
$app.editFile("/sdcard/Pictures/test.text");
```


#### hasUsagePermit()

> 是否有使用情况权限

- 返回 : {boolean} 是否有使用情况权限
- 版本 : 1.0.1


```javascript
$app.hasUsagePermit();
```


#### getUsagePermit()

> 获取使用情况权限

- 返回 : {boolean} 是否打开成功
- 版本 : 1.0.1


```javascript
$app.getUsagePermit();
```


#### intent(options)

> 创建意图

- 参数 : options {Object} 配置参数 
- 返回 : {Intent} 意图
- 版本 : 1.0.1


```javascript
//写必要的参数
let options = {
    action: "android.intent.action.VIEW",//只写VIEW也可以(自动追加前缀:"android.intent.action.")
    data: "https://www.baidu.com",//数据内容
    pkg: "com.baidu.BaiduMap",//包名
    type: "text/plain",//数据类型
    flags: ["FLAG_ACTIVITY_NEW_TASK","..."],//标志
    component: {
        cls: "org.aigame.pro.ActivityMain",
        pkg: "org.aigame.pro"
    },//组件
    categories: ["CATEGORY_DEFAULT","..."],//类别
    extras:[{
        name:"",
        value:""
    },{
        name:"",
        value:""
    }]//额外内容
}
//创建意图
let intent = $app.intent(options);
```


#### sendBroadcast(intent)

> 发送异步广播

- 参数 : intent {Intent} 意图 
- 版本 : 1.0.1


#### sendBroadcast(intent, permis)

> 发送异步广播(含权限)

- 参数 : intent {Intent} 意图 
- 参数 : permis {string} 权限 
- 版本 : 1.0.1


#### sendOrderedBroadcast(intent, permis)

> 发送同步广播

- 参数 : intent {Intent} 意图 
- 参数 : permis {string} 权限 
- 版本 : 1.0.1


#### startActivity(intent)

> 用意图启动Activity

- 参数 : intent {Intent} 意图 
- 版本 : 1.0.1


#### startActivity(options)

> 启动Activity

- 参数 : options {Object} 意图配置 
- 版本 : 1.1.1


#### getForeApps()

> 获取前台应用
> 
> 此方法只在低版本安卓中有明显效果，建议使用 $root.lsRunningApps((pkg)=>{}); 来获取前台应用

- 返回 : {String[]} 前台应用包名列表
- 版本 : 1.0.4


#### kill(name)

> 杀死应用
> 
> 如果有root权限，优先使用root权限来杀死应用,如果有shizuku则使用shizuku来杀死应用
> 
> 在低版本的安卓中，直接就可以通过活动管理器杀死应用，但是在较高版本的安卓中(安卓9+)很可能无法直接杀死应用进程。

- 参数 : name {string} 应用名或包名 
- 版本 : 1.0.4


```javascript
//结束应用
$app.kill("QQ");
$app.kill("MT管理器");
```


#### sendMms(phone, title, message, imgPath)

> 发送彩信

- 参数 : phone {string} 电话号码
- 参数 : title {string} 主题(可为null)
- 参数 : message {string} 短信内容
- 参数 : imgPath {string} 图片全路径(无法支持相对路径)
- 版本 : 1.4.9


```javascript
//发送彩信
$app.sendMms("13800000000", "测试彩信", "这是一条彩信", "/sdcard/DCIM/100ANDRO/IMG_20230801_100000.jpg");
```


#### openSelf()

> 打开自身
> 
> 打开自身的主活动（通常是启动器图标点击后的活动）。
> 
> 此方法尝试使用启动器意图来打开应用。如果失败（例如，应用未安装），则会创建一个新的意图来启动主活动。
> 
> 如果是打包后的apk则会打开打包后的apk主界面

- 版本 : 1.6.2


```javascript
//打开自身应用
$app.openSelf();
```

---

## AppInfo - 应用信息

- 更新时间:2026-01-30 19:32:51

> 应用信息
> 
> 通过 $app.ls(); 方法返回的列表元素类型




#### const {String} appName;

> 应用名称


#### const {String} pkgName;

> 包名


#### const {Image} icon;

> 图标


#### const {ApplicationInfo} info;

> 安卓原生应用信息
> 
> 类名：android.content.pm.ApplicationInfo


#### getAppName()

> 获取应用名称

- 返回 : {string} 应用名称


#### getPkgName()

> 获取包名

- 返回 : {string} 包名


#### getIcon()

> 获取图标

- 返回 : {Image} 图标


#### getInfo()

> 获取安卓原生应用信息

- 返回 : {ApplicationInfo} 安卓原生应用信息


#### json()

> 转成json字符串

- 返回 : {string} json字符串
- 版本 : 1.7.0

---

## AppTaskInfo - 任务信息

- 更新时间:2026-01-30 19:32:51

> 应用任务信息
> 
> 通过 $app.lsRecent(); 方法返回的列表元素类型




#### const {String} appName;

> 应用名称


#### const {String} pkgName;

> 包名


#### const {String} lastUseTime;

> 最后使用时间


#### const {long} lastUsedTime;

> 最后使用时间


#### const {ApplicationInfo} info;

> 安卓原生应用信息
> 
> 类型：{android.content.pm.ApplicationInfo}


#### getLastUsedTime()

> 最后使用时间

- 返回 : {long} 最后使用时间


#### getAppName()

> 获取应用名称

- 返回 : {string} 应用名称


#### getPkgName()

> 获得包名

- 返回 : {string} 包名


#### getLastUseTime()

> 获得最后时间格式化字符串

- 返回 : {string} 最后使用时间


#### json()

> 将当信息对象转为json字符串

- 返回 : {String} json字符串
- 版本 : 1.7.0