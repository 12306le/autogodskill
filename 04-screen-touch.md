# 屏幕与触控 API

> 屏幕截图、触摸驱动、键鼠模拟。

## 目录
- [$screen - 屏幕操作](#screen---屏幕操作)
- [ScreenInfo - 屏幕信息](#screeninfo---屏幕信息)
- [$touch - 触摸驱动](#touch---触摸驱动)
- [$hid - 键鼠触控](#hid---键鼠触控)

---

## $screen - 屏幕操作

- 更新时间:2026-01-30 19:32:55

> 屏幕操作




#### getPermit()

> 获取截屏权限
> 
> 如果系统是安卓11+并且无障碍可以截屏的话就会返回true，否则就判断录屏权限是否可用，如果可用也会返回true，如果这两种截屏方式都不可用，就尝试获取录屏权限。
> 该方法会阻塞线程，直到获取权限成功后，才会结束。
> 
> 需要注意的是：安卓15+的用户在获取录屏权限的时候记得选中整个屏幕选项，而不是单个当前应用截屏。

- 返回 : {boolean} 是否获取成功
- 版本 : 1.0.0


```javascript
//等待获取截屏权限
$screen.getPermit();
```


#### getPermitOnce()

> 获取截屏权限一次
> 
> 本质上只是取消了阻塞线程的行为，然而如果获取不到权限，会继续重新向用户请求权限，直到获取为止。


```javascript
//获取截屏权限一次
$screen.getPermitOnce();
```


#### hasPermit()

> 是否有截屏权限
> 
> 如果支持无障碍截屏的话(安卓11+且无障碍服务可用)，会直接返回true，否则就会判断录屏权限是否可用，如果可用也会返回true。

- 返回 : {boolean} 是否有截屏权限
- 版本 : 1.1.5


```javascript
if($screen.hasPermit()){
    log("有截屏权限");
}
```


#### hasRecord()

> 判断是否有录屏权限
> 
> 这个方法只会判断是否有录屏权限，不会判断无障碍截屏是否可用

- 返回 : {boolean} 是否有录屏权限
- 版本 : 1.7.4


```javascript
if($screen.hasRecord()){
    log("有录屏权限");
}
```


#### onlyRecord(onlyRecord)

> 只用录屏权限
> 
> 默认是false，即默认优先使用无障碍截屏，后用录屏权限截屏。
> 如果设置为true，那么判断是否有权限的函数只会判断录屏权限是否可用，不会判断无障碍截屏是否可用。并且获取截屏的时候只会通过录屏权限获取截屏。

- 参数 : onlyRecord {boolean} 是否只用录屏权限
- 版本 : 1.7.4


```javascript
//设置只使用录屏权限获取截屏
$screen.onlyRecord(true);
```


#### getScreen()

> 获取屏幕截屏
> 
> 此函数将优先使用无障碍截屏(安卓11+)，否则将使用截屏权限来进行截屏。

- 返回 : {Image} 截屏图片
- 版本 : 1.0.0


```javascript
//等待获取截屏权限
$screen.getPermit();
//如果不想用上面的方式，也可以使用 $act.getPermit(); //获取无障碍，也可以截屏(安卓11+以上才行)
let img = $screen.getScreen();//获得屏幕截屏
$img.show(img);//显示截屏
```


#### bright(bright)

> 设置屏幕亮度

- 参数 : bright {int} 亮度值(0-255)
- 版本 : 1.0.0


```javascript
//设置屏幕亮度
$screen.bright(100);
```


#### dir(degree)

> 设置屏幕方向

- 参数 : degree {string} 屏幕旋转度数
- 版本 : 1.0.0


```javascript
//设置屏幕方向
$screen.dir(0);//(强制)竖屏
$screen.dir(90);//(强制)右转横屏
$screen.dir(180);//(强制)倒置竖屏
$screen.dir(270);//(强制)左转横屏
$screen.dir(-1);//(不强制)自动旋转(任何其他数字都是自动旋转)
// 模拟器测试：
// 逍遥     安卓5  : 成功旋转屏幕 会闪退
// 逍遥     安卓7  : 成功旋转屏幕 会闪退
// 逍遥     安卓9  : 成功旋转屏幕 会闪退
// 逍遥     安卓12 : 完美!!!
// 雷电     安卓9  : 毫无反应
//真机测试：
// OPPO    安卓12 : 完美!!!
```


#### getHeight()

> 屏幕高
> 
> 该方法会先获取屏幕的所有信息，之后再反馈屏幕高度。

- 返回 : {int} 屏幕高度
- 版本 : 1.0.0


```javascript
let w = $screen.getWidth();
let h = $screen.getHeight();
alert("屏幕宽高",w+"x"+h);
```


#### getWidth()

> 屏幕宽
> 
> 该方法会先获取屏幕的所有信息，之后再反馈屏幕宽度。

- 返回 : {int} 屏幕宽度
- 版本 : 1.0.0


```javascript
let w = $screen.getWidth();
let h = $screen.getHeight();
alert("屏幕宽高",w+"x"+h);
```


#### getScreenInfo()

> 屏幕信息
> 
> 该方法会获取屏幕的所有信息。

- 返回 : {ScreenInfo} 屏幕宽高信息
- 版本 : 1.0.0


```javascript
let info = $screen.getScreenInfo();//等价于：'$screen.info()'
alert("详细信息",info);
```


#### info()

> 屏幕信息
> 
> 该方法会获取屏幕的所有信息。

- 返回 : {ScreenInfo} 屏幕宽高信息
- 版本 : 1.7.0


```javascript
let info = $screen.info();//等价于：'$screen.getScreenInfo()'
alert("详细信息",info);
```


#### getDensity()

> 获取密度
> 
> 获取屏幕的密度因子

- 返回 : {float} 密度因子
- 版本 : 1.0.0


```javascript
let density = $screen.getDensity();
alert("当前设备的密度",density);
```


#### isScreenOff()

> 判断屏幕是否息屏

- 返回 : {boolean} 是否息屏
- 版本 : 1.0.0


```javascript
if($screen.isScreenOff()){
    toast("屏幕息屏");
}
```


#### isScreenOn()

> 判断屏幕是否亮屏

- 返回 : {boolean} 是否亮屏
- 版本 : 1.0.0


```javascript
if($screen.isScreenOn()){
    toast("屏幕亮屏");
}
```


#### split(tranCut, vertCut, index)

> 屏幕分割
> 
> 将屏幕进行横向和纵向的分割，返回指定索引的范围，该函数对于制作全分辨率脚本非常有用。

- 参数 : tranCut {int} 横向分割数量
- 参数 : vertCut {int} 纵向分割数量
- 参数 : index {int} 块的索引
- 返回 : {Rect} 范围
- 版本 : 1.1.2


```javascript
$draw.closeAll();
//将屏幕分割成9份，找到最后一份的范围
let region = $screen.split(3, 3, 8);
//绘制出这个范围
$draw.rect(region);
```


#### save(path)

> 截屏并保存
> 
> 该函数会直接截屏(需要截屏权限或者无障碍权限)，之后保存截屏到指定的路径。

- 参数 : path {String} 保存路径
- 版本 : 1.0.0


```javascript
//截屏并且保存(支持相对路径写法)
let imgPath = "/sdcard/Pictures/截屏.png";
$screen.save(imgPath);
```


#### mustV()

> 强制竖屏截屏
> 
> 一般情况下用不到该函数，但是确实存在少量设备存在横竖屏异常，此函数就是为了应对特殊情况的。

- 版本 : 1.1.8


```javascript
$screen.mustV();//强制竖屏截屏
```


#### mustH()

> 强制横屏截屏
> 
> 一般情况下用不到该函数，但是确实存在少量设备存在横竖屏异常，此函数就是为了应对特殊情况的。

- 版本 : 1.1.8


```javascript
$screen.mustH();//强制横屏截屏
```


#### cancelMust()

> 取消强制横竖屏
> 
> 默认情况下,$screen会根据当前屏幕状态自动检测截屏是横屏还是竖屏,所以一般情况下mustV、mustH、cancelMust这三个函数没必要调用。
> 之所以设计这三个函数,是为了更好的适配更多的设备,正常情况下手机的宽度都是小于高度的,但是也有那种宽度大于高度的情况,例如：平板设备，此时就可以使用强制横屏或竖屏来截屏了。

- 版本 : 1.1.8


```javascript
$screen.cancelMust();//取消强制横竖屏(默认是:自动检测)
```

---

## ScreenInfo - 屏幕信息

- 更新时间:2026-01-30 19:32:48

> 屏幕信息




#### const {int} w;

> 屏幕宽度


#### const {int} h;

> 屏幕高度


#### const {int} dpi;

> 屏幕密度


#### const {float} xdpi;

> 屏幕水平分辨率


#### const {float} ydpi;

> 屏幕垂直密度


#### const {float} density;

> 屏幕密度因子


#### const {float} scaledDensity;

> 屏幕缩放密度


#### const {Boolean} isVertical;

> 是否为垂直方向


#### const {Boolean} navShow;

> 是否显示导航栏


#### const {int} navH;

> 导航栏高度


#### const {Boolean} barShow;

> 是否显示状态栏


#### const {int} barH;

> 状态栏高度


#### getW()

> 获取屏幕宽度

- 返回 : {int} 屏幕宽度


```javascript
let screenInfo = $screen.info();
//获取屏幕宽度
log(screenInfo.getW());
```


#### getH()

> 获取屏幕高度

- 返回 : {int} 屏幕高度


```javascript
let screenInfo = $screen.info();
//获取屏幕高度
log(screenInfo.getH());
```


#### getDpi()

> 获取屏幕密度

- 返回 : {int} 屏幕密度


```javascript
let screenInfo = $screen.info();
//获取屏幕密度
log(screenInfo.getDpi());
```


#### isVertical()

> 是否为垂直方向

- 返回 : {boolean} 是否为垂直方向


```javascript
let screenInfo = $screen.info();
//判断:是否为垂直方向
log(screenInfo.isVertical());
```


#### getDensity()

> 获取屏幕密度因子

- 返回 : {float} 屏幕密度因子


```javascript
let screenInfo = $screen.info();
//获取屏幕密度因子
log(screenInfo.getDensity());
```


#### isNavShow()

> 是否显示导航栏

- 返回 : {boolean} 是否显示导航栏


```javascript
let screenInfo = $screen.info();
//判断：是否显示导航栏
log(screenInfo.isNavShow());
```


#### getNavH()

> 获取导航栏高度

- 返回 : {int} 导航栏高度


```javascript
let screenInfo = $screen.info();
//获取导航栏高度
log(screenInfo.getNavH());
```


#### isBarShow()

> 是否显示状态栏

- 返回 : {boolean} 是否显示状态栏


```javascript
let screenInfo = $screen.info();
//判断：是否显示状态栏
log(screenInfo.isBarShow());
```


#### getBarH()

> 获取状态栏高度

- 返回 : {int} 状态栏高度


```javascript
let screenInfo = $screen.info();
//获取状态栏高度
log(screenInfo.getBarH());
```


#### getXdpi()

> 获取水平密度

- 返回 : {float} 水平密度


```javascript
let screenInfo = $screen.info();
//获取水平密度
log(screenInfo.getXdpi());
```


#### getYdpi()

> 获取垂直密度

- 返回 : {float} 垂直密度


```javascript
let screenInfo = $screen.info();
//获取垂直密度
log(screenInfo.getYdpi());
```


#### getScaledDensity()

> 获取缩放密度

- 返回 : {float} 缩放密度


```javascript
let screenInfo = $screen.info();
//获取缩放密度
log(screenInfo.getScaledDensity());
```

---

## $touch - 触摸驱动

- 更新时间:2026-01-30 19:32:57

> 触摸驱动
> 
> 需要ROOT权限，部分手机不会与手指触摸冲突。




#### hasPermit()

> 是否可用
> 
> 一般如果有root权限，就是可用的状态，本质上这个函数是用来判断设备是否有root权限的。这个函数性能很高，一旦初始化成功了，就会直接返回true，并不会每次都检查root权限。

- 返回 : {boolean} 是否可用
- 版本 : 1.5.2


```javascript
//初始化
if($touch.hasPermit()){
    $touch.init();
}
//之后再操作，否则无效果
```


#### init()

> 初始化
> 
> $touch需要初始化才可以使用，初始化大概需要5秒时间，但如果已经初始化过了，就会直接返回true。

- 返回 : {boolean} 是否已经初始化成功


```javascript
//开始初始化
$touch.init();
```


#### touchDown(fingerId, x, y)

> 按下手指

- 参数 : fingerId {int} 手指ID 
- 参数 : x {int}  坐标X 
- 参数 : y {int}  坐标Y 
- 版本 : 1.5.2


```javascript
$touch.touchDown(1, 100, 100);
```


#### touchMove(fingerId, x, y)

> 移动手指

- 参数 : fingerId {int} 手指ID 
- 参数 : x {int}  坐标X 
- 参数 : y {int}  坐标Y 
- 版本 : 1.5.2


```javascript
$touch.touchMove(1, 300, 500);
```


#### touchUp(fingerId)

> 抬起手指

- 参数 : fingerId {int} 手指ID 
- 版本 : 1.5.2


```javascript
$touch.touchUp(1);
```


#### click(x, y)

> 点击
> 
> 原理是在C/C++层执行系统命令进行事件注入，因此效率较高

- 参数 : x {int} 坐标X 
- 参数 : y {int} 坐标Y 
- 版本 : 1.5.4


```javascript
$touch.click(300, 500);
```


#### click(pointerId, x, y)

> 点击
> 
> 默认按压时长为1毫秒，该函数的本质是touchDown和touchUp的组合，因此效率较慢

- 参数 : pointerId {int} 指针ID 
- 参数 : x {int}  坐标X 
- 参数 : y {int}  坐标Y 
- 版本 : 1.5.2


```javascript
$touch.click(1, 300, 500);
```


#### click(pointerId, x, y, dur)

> 点击
> 
> 原理是touchDown和touchUp的组合

- 参数 : pointerId {int} 指针ID 
- 参数 : x {int}  坐标X 
- 参数 : y {int}  坐标Y 
- 参数 : dur {int}  按压时长 
- 版本 : 1.5.2


```javascript
$touch.click(1, 300, 500, 50);
```


#### press(x, y)

> 长按
> 
> 原理是touchDown和touchUp的组合，默认按压时间是750毫秒

- 参数 : x {int}  坐标X 
- 参数 : y {int}  坐标Y 
- 版本 : 1.5.2


```javascript
$touch.press(300, 500);
```


#### press(pointerId, x, y)

> 长按
> 
> 原理是touchDown和touchUp的组合，默认按压时间是750毫秒

- 参数 : pointerId {int} 指针ID 
- 参数 : x {int}  坐标X 
- 参数 : y {int}  坐标Y 
- 版本 : 1.5.2


```javascript
$touch.press(1, 300, 500);
```


#### press(pointerId, x, y, dur)

> 长按
> 
> 原理是touchDown和touchUp的组合

- 参数 : pointerId {int} 指针ID 
- 参数 : x {int}  坐标X 
- 参数 : y {int}  坐标Y 
- 参数 : dur {int}  长按时间 
- 版本 : 1.5.2


```javascript
$touch.press(1, 300, 500, 2000);
```


#### move(x, y, x2, y2)

> 滑动
> 
> 默认的滑动时间是1秒

- 参数 : x {int}  起点X 
- 参数 : y {int}  起点Y 
- 参数 : x2 {int}  终点X 
- 参数 : y2 {int}  终点Y 
- 版本 : 1.5.2


```javascript
$touch.move(100, 100, 300, 500);
```


#### move(x, y, x2, y2, dur)

> 滑动

- 参数 : x {int}  起点X 
- 参数 : y {int}  起点Y 
- 参数 : x2 {int}  终点X 
- 参数 : y2 {int}  终点Y 
- 参数 : dur {int}  移动时间 
- 版本 : 1.5.2


```javascript
$touch.move(100, 100, 300, 500, 1000);
```


#### move(pointerId, x, y, x2, y2, dur)

> 滑动
> 
> 滑动的时间是根据CPU数量来进行计算的，因此并不一定就完全准确，不同手机执行的滑动时间可能有一点误差，但这并没有太大影响。

- 参数 : pointerId {int} 指针ID 
- 参数 : x {int}  起点X 
- 参数 : y {int}  起点Y 
- 参数 : x2 {int}  终点X 
- 参数 : y2 {int}  终点Y 
- 参数 : dur {int}  移动时间 
- 版本 : 1.5.2


```javascript
$touch.move(1, 100, 100, 300, 500, 1000);
```


#### swipe(x, y, x2, y2, dur)

> 模拟滑动
> 
> 原理是C/C++层系统调用命令来实现注入滑动

- 参数 : x {int} 起点X 
- 参数 : y {int}  起点Y 
- 参数 : x2 {int} 终点X 
- 参数 : y2 {int} 终点Y 
- 参数 : dur {int} 滑动时间 
- 版本 : 1.5.4


```javascript
$touch.swipe(100,200,600,1200,2000);
```


#### key(keyCode)

> 模拟按键
> 
> 原理是C/C++层系统调用命令来实现注入按键事件

- 参数 : keyCode {int} 键值 
- 版本 : 1.5.4


```javascript
$touch.key(4);//返回按钮
```

---

## $hid - 键鼠触控

- 更新时间:2026-01-30 19:32:53

> 键鼠触控
> 
> 无需任何权限，连接键鼠硬件即可完成自动化触控功能。




#### init()

> 初始化HID

- 返回 : {String} 初始化成功返回true，否则就是失败原因
- 版本 : 1.8.9


```javascript
let res = $hid.init();
if(res=="true"){
    log("初始化成功");
}else{
    log("初始化失败:",res);
}
```


#### isOn()

> 判断是否开启
> 
> 判断是否链接了硬件

- 返回 : {boolean} 是否开启
- 版本 : 1.8.9


```javascript
if($hid.isOn()){
    log("处于开启状态");
}
```


#### dexBeat()

> 获取版本号
> 
> 获取插件版本号

- 返回 : {float} 版本号
- 版本 : 1.8.9


```javascript
log("HID版本:",$hid.dexBeat());
```


#### getBatteryLevel()

> 获取电量
> 
> 获取手机当前电量

- 返回 : {int} 电量
- 版本 : 1.8.9


```javascript
log("电池电量:",$hid.getBatteryLevel());
```


#### isCharging()

> 是否处于充电状态
> 
> 判断当前手机是否在供电

- 返回 : {boolean} 是否处于充电状态
- 版本 : 1.8.9


```javascript
if($hid.isCharging()){
    log("正在充电...");
}
```


#### setPowerOff()

> 关闭供电

- 版本 : 1.8.9


```javascript
$hid.setPowerOff();
```


#### setPowerOn()

> 开启供电

- 版本 : 1.8.9


```javascript
$hid.setPowerOn();
```


#### click(x, y)

> 点击

- 参数 : x {int} 坐标x
- 参数 : y {int} 坐标y
- 返回 : {boolean} 是否点击成功
- 版本 : 1.8.9


```javascript
$hid.click(100,100);
```


#### click(index)

> 点击

- 参数 : index {int[]} 坐标
- 返回 : {boolean} 是否点击成功
- 版本 : 1.8.9


```javascript
$hid.click([100,100]);
```


#### longClick(x, y, dur)

> 长按

- 参数 : x {int} 坐标x
- 参数 : y {int} 坐标y
- 参数 : dur {int} 长按时间
- 返回 : {boolean} 是否点击成功
- 版本 : 1.8.9


```javascript
$hid.longClick(100,100,1500);
```


#### longClick(index)

> 长按

- 参数 : index {int[]} 坐标
- 返回 : {boolean} 是否点击成功
- 版本 : 1.8.9


```javascript
$hid.longClick([100,100,1500]);
```


#### swipEx(x1, y1, x2, y2)

> 增强滑动

- 参数 : x1 {int} 起点坐标x
- 参数 : y1 {int} 起点坐标y
- 参数 : x2 {int} 终点坐标x
- 参数 : y2 {int} 终点坐标y
- 返回 : {boolean} 是否滑动成功
- 版本 : 1.8.9


```javascript
$hid.swipEx(100,100,200,200);
```


#### swipEx(x1, y1, x2, y2, press, time, delay)

> 增强滑动

- 参数 : x1 {int} 起点坐标x
- 参数 : y1 {int} 起点坐标y
- 参数 : x2 {int} 终点坐标x
- 参数 : y2 {int} 终点坐标y
- 参数 : press {int} 按下时长(默认:300)
- 参数 : time {int} 滑动时长(默认:1000)
- 参数 : delay {int} 延迟时长(默认:0)
- 返回 : {boolean} 是否滑动成功
- 版本 : 1.8.9


```javascript
$hid.swipEx(100,100,200,200,300,1000,0);
```


#### touchDown(id, x, y)

> 按下

- 参数 : id {int} 手指id
- 参数 : x {int} 坐标x
- 参数 : y {int} 坐标y
- 返回 : {boolean} 是否按下成功
- 版本 : 1.8.9


```javascript
$hid.touchDown(0,100,100);
```


#### touchMove(id, x, y)

> 移动

- 参数 : id {int} 手指id
- 参数 : x {int} 坐标x
- 参数 : y {int} 坐标y
- 返回 : {boolean} 是否移动成功
- 版本 : 1.8.9


```javascript
$hid.touchMove(0,100,100);
```


#### touchUp(id)

> 抬起

- 参数 : id {int} 手指id
- 返回 : {boolean} 是否抬起成功
- 版本 : 1.8.9


```javascript
$hid.touchUp(0);
```


#### keyPress(keyCode)

> 按键

- 参数 : keyCode {int} 按键码
- 返回 : {boolean} 是否按下成功
- 版本 : 1.8.9


```javascript
$hid.keyPress(40);
```


#### keyPress(modify, keyCode)

> 按键

- 参数 : modify {int} 组合按键码
- 参数 : keyCode {int} 按键码
- 返回 : {boolean} 是否按下成功
- 版本 : 1.8.9


```javascript
$hid.keyPress(0,40);
```


#### home()

> 主页
> 
> 按下手机主页键

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.home();
```


#### back()

> 返回
> 
> 按下手机返回键

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.back();
```


#### recents()

> 最近
> 
> 按下手机后台键

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.recents();
```


#### recentsV2()

> 最近任务增强版
> 
> 按下手机后台键 第二种方法,特殊机型使用

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.recentsV2();
```


#### selectAll()

> 全选
> 
> 按下手机全选键 选择输入框 全部文本内容

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.selectAll();
```


#### cut()

> 剪切
> 
> 按下手机剪切键 剪切输入框 全部文本内容到剪切板

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.cut();
```


#### copy()

> 复制
> 
> 按下手机后台键 复制输入框 全部文本内容到剪切板

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.copy();
```


#### paste()

> 粘贴
> 
> 按下手机粘贴键 剪切板内容粘贴到输入框内 可以配合写入剪切板命令

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
//先设置剪切板
$sys.setClip("我是来自剪切板的内容");
//再粘贴内容
$hid.paste();
```


#### paste(text)

> 粘贴文本
> 
> 按下手机粘贴键 剪切板内容粘贴到输入框内 可以配合写入剪切板命令

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.paste("我是来自剪切板内容");
//等价于下面的写法
//1.先设置剪切板
$sys.setClip("我是来自剪切板的内容");
//2.再粘贴内容
$hid.paste();
```


#### inputSimple(text)

> 输入
> 
> 按下手机键盘键 在输入框输入英文字母+数字
> 
> 注意:标点符号和中文不能输入

- 参数 : text {String} 文本
- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.inputSimple("abcd1234");
```


#### delete()

> 删除
> 
> 按下手机删除键 删除输入框文本内容 特殊机型用回退键

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.delete();
```


#### delete(len)

> 删除
> 
> 按下手机删除键 删除输入框文本内容 特殊机型用回退键

- 参数 : len {int} 删除长度
- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.delete(2);
```


#### backspace()

> 回退
> 
> 按下手机回退键 回退输入框文本内容 特殊机型用回退键

- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.backspace();
```


#### backspace(len)

> 回退
> 
> 按下手机回退键 回退输入框文本内容 特殊机型用回退键

- 参数 : len {int} 回退长度
- 返回 : {boolean} 是否成功
- 版本 : 1.8.9


```javascript
$hid.backspace(2);
```