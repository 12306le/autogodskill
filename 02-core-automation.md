# 核心自动化 API

> 涵盖节点查找、UI选择器、手势操作、分辨率适配等核心模块。

## 目录
- [$act - 手势动作](#act---手势动作)
- [UiSelector - UI选择器](#uiselector---ui选择器)
- [Node - 节点信息](#node---节点信息)
- [$adapt - 分辨率适配](#adapt---分辨率适配)

---

## $act - 手势动作

- 更新时间:2026-01-30 19:32:49

> 手势动作
> 
> $act是一个高度封装的框架，其中集成了无障碍、$root、$szk触摸方案，优先级为：$root>$szk>无障碍
> 
> $act中所有click、press、move函数都会优先判断是否有ROOT权限，如果有，则使用$root进行点击；之后判断是否有Shizuku权限，如果有，则使用$szk进行手势操作；之后判断是否有无障碍权限，如果有，则使用无障碍执行。




#### hasPermit()

> 无障碍服务是否开启
> 
> 判断无障碍服务是否开启，如果开启了则返回true，否则返回false。

- 返回 : {boolean} 是否开启
- 版本 : 1.0.0


```javascript
//判断是否有权限
let hasPermit = $act.hasPermit();
$tip.show("是否获得无障碍",hasPermit);
```


#### getPermit()

> 获得无障碍服务
> 
> 如果有Root权限:则使用Root权限为本应用授权永久无障碍
> 
> 如果有Shizuku权限:则使用Shizuku权限为本应用授权永久无障碍
> 
> 如果没有Root和Shizuku:则进行普通权限申请(非永久有效,受系统限制)
> 
> 该函数是一个阻塞式函数，请勿放在ui线程当中操作，如果你想在ui状态下申请无障碍，建议使用$permit.wza()函数。
> 
> 注意：永久无障碍其实是每次启动软件时，会自动自我授权无障碍，它不会立即获得无障碍权限，一般需要等待1-5秒的时间，不过这些操作都会在应用后台进行操作，因此用户并不会感知到这一操作，只会莫名其妙的觉得自己开启的无障碍权限从未关闭过一样。
> 在授权无障碍期间，你最好还是使用 $act.hasPermit() 判断无障碍权限是否可用。

- 返回 : {boolean} 是否获得
- 版本 : 1.0.0


```javascript
$act.getPermit();//获得权限
```


#### click(x, y)

> 点击
> 
> 如果Root可用，优先使用Root执行手势；
> 如果Shizuku可用，优先使用Shizuku执行手势；
> 如果无障碍可用，使用无障碍执行手势；
> 如果以上都不可用，将无任何效果；

- 参数 : x {int} 点击位置x 
- 参数 : y {int} 点击位置y 
- 版本 : 1.0.0


```javascript
//点击手势
$act.click(500,800);
```


#### click(x, y, dur)

> 点击
> 
> 如果Root可用，优先使用Root执行手势
> 如果Shizuku可用，优先使用Shizuku执行手势
> 如果无障碍可用，使用无障碍执行手势
> 如果以上都不可用，将无任何效果

- 参数 : x {int} 点击位置x 
- 参数 : y {int} 点击位置y 
- 参数 : dur {int} 点击后延迟 
- 版本 : 1.0.0


```javascript
//设置点击时常(长按效果)
sleep(1000);
$act.click(135,344,1500);
```


#### click(x, y, dur, delay)

> 点击
> 
> 如果Root可用，优先使用Root执行手势
> 如果Shizuku可用，优先使用Shizuku执行手势
> 如果无障碍可用，使用无障碍执行手势
> 如果以上都不可用，将无任何效果

- 参数 : x {int} 点击位置x 
- 参数 : y {int} 点击位置y 
- 参数 : dur {int} 点击后延迟 
- 参数 : delay {int} 点击前延迟 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$act.click(500,800,1500,100);
```


#### click(index)

> 点击
> 
> 如果Root可用，优先使用Root执行手势
> 如果Shizuku可用，优先使用Shizuku执行手势
> 如果无障碍可用，使用无障碍执行手势
> 如果以上都不可用，将无任何效果

- 参数 : index {int[]} 点击位置 
- 版本 : 1.0.0


```javascript
//点击
$act.click([500,800]);
```


#### click(index, dur)

> 点击
> 
> 如果Root可用，优先使用Root执行手势
> 如果Shizuku可用，优先使用Shizuku执行手势
> 如果无障碍可用，使用无障碍执行手势
> 如果以上都不可用，将无任何效果

- 参数 : index {int[]} 点击位置  
- 参数 : dur {int} 点击后延迟 
- 版本 : 1.0.0


```javascript
//点击手势(长按)
$act.click([135,347],1500);
```


#### click(index, dur, delay)

> 点击
> 
> 如果Root可用，优先使用Root执行手势
> 如果Shizuku可用，优先使用Shizuku执行手势
> 如果无障碍可用，使用无障碍执行手势
> 如果以上都不可用，将无任何效果

- 参数 : index {int[]} 点击位置 
- 参数 : dur {int} 点击后延迟 
- 参数 : delay {int} 点击前延迟 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$act.click([136,347],1500,100);
```


#### click(index)

> 点击
> 
> 如果Root可用，优先使用Root执行手势
> 如果Shizuku可用，优先使用Shizuku执行手势
> 如果无障碍可用，使用无障碍执行手势
> 如果以上都不可用，将无任何效果

- 参数 : index {Point} 点击位置
- 版本 : 1.0.0


```javascript
//点击手势(点击opencv返参)
let point = new org.opencv.core.Point(136,347);
$act.click(point);
```


#### click(index, dur)

> 点击
> 
> 如果Root可用，优先使用Root执行手势
> 如果Shizuku可用，优先使用Shizuku执行手势
> 如果无障碍可用，使用无障碍执行手势
> 如果以上都不可用，将无任何效果

- 参数 : index {Point} 点击位置
- 参数 : dur {int} 点击后延迟  
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
let point = new org.opencv.core.Point(136,347);
$act.click(point,1500);
```


#### click(index, dur, delay)

> 点击
> 
> 如果Root可用，优先使用Root执行手势
> 如果Shizuku可用，优先使用Shizuku执行手势
> 如果无障碍可用，使用无障碍执行手势
> 如果以上都不可用，将无任何效果

- 参数 : index {Point} 点击位置
- 参数 : dur {int} 点击后延迟 
- 参数 : delay {int} 点击前延迟 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
let point = new org.opencv.core.Point(136,347);
$act.click(point,1500,100);
```


#### click(node)

> 点击节点
> 
> 如果节点支持点击，就是用节点本身的点击行为进行点击，如果不支持，则通过$act的坐标方式来点击节点的坐标位置。

- 参数 : node {Node} 点击位置  
- 版本 : 1.0.0


```javascript
//如果你通过选择器找到了节点，也可以通过这种方式来点击节点
let node = $act.selector()
.pkg("org.aigame.pro")
.cls("android.widget.FrameLayout")
.waitFirst();
if(node!=null){
     // 绘制节点位置
     node.draw();
     // 可以这样点击
     node.click();
     // 也可以这样点击
     $act.click(node);
}
```


#### click(node, useAct)

> 点击节点
> 
> 如果节点支持点击，就是用节点本身的点击行为进行点击，如果不支持，则通过$act的坐标方式来点击节点的坐标位置。

- 参数 : node {Node} 点击位置 
- 参数 : useAct {boolean} 是否使用无障碍点击 
- 版本 : 1.0.0


```javascript
//如果你通过选择器找到了节点，也可以通过这种方式来点击节点
let node = $act.selector()
.pkg("org.aigame.pro")
.cls("android.widget.FrameLayout")
.waitFirst();
if(node!=null){
     // 绘制节点位置
     node.draw();
     // 可以这样点击
     node.click();
     // 也可以这样点击
     $act.click(node,true);//true表示直接使用$act的点击坐标方式进行点击
}
```


#### press(node)

> 长按节点
> 
> 如果节点支持点击，就是用节点本身的点击行为进行长按，如果不支持，则通过$act的坐标方式来点击节点的坐标位置。

- 参数 : node {Node} 节点 
- 版本 : 1.0.0


```javascript
//如果你通过选择器找到了节点，也可以通过这种方式来点击节点
let node = $act.selector()
.pkg("org.aigame.pro")
.cls("android.widget.FrameLayout")
.waitFirst();
if(node!=null){
     // 绘制节点位置
     node.draw();
     // 长按节点 或者也可以直接调用 node.press();
     $act.press(node);
}
```


#### press(node, useAct)

> 长按节点
> 
> 如果设备获得了root，将优先使用root来执行手势,如果没有root,则使用无障碍来执行手势

- 参数 : node {Node} 节点 
- 参数 : useAct {boolean} 是否使用act点击 
- 版本 : 1.0.0


#### press(x, y)

> 长按
> 

- 参数 : x {int} 长按位置x 
- 参数 : y {int} 长按位置y 
- 版本 : 1.0.0


```javascript
//点击手势(长按)(延迟一秒)
$act.press(136,347);
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
$act.press(136,347,1500);
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
$act.press(136,347,1500,100);
```


#### slide(startX, startY, endX, endY, duration)

> 模拟人手滑动

- 参数 : startX {int} 起点x(必填) 
- 参数 : startY {int} 起点y(必填) 
- 参数 : endX {int} 终点x(必填) 
- 参数 : endY {int} 终点y(必填) 
- 参数 : duration {int} 持续时间(可为空:默认:1秒) 
- 版本 : 1.7.8


```javascript
//随机模拟真人滑动(推荐)
$act.slide(189,244,733,1440,3000);
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
$act.move(500,0,500,800);
```


#### move(x1, y1, x2, y2, dur)

> 滑动
> 

- 参数 : x1 {int} 起点x 
- 参数 : y1 {int} 起点y 
- 参数 : x2 {int} 终点x 
- 参数 : y2 {int} 终点y 
- 参数 : dur {int} 滑动延迟 
- 版本 : 1.0.0


```javascript
//滑动手势
$act.move(500,0,500,800,500);
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
$act.move(500,0,500,800,500.1000);
```


#### move(node, dir)

> 滑动节点
> 
> 仅无障碍可用

- 参数 : node {Node} 节点 
- 参数 : dir {String} 方向(up|down|left|right)
- 版本 : 1.0.0


#### move(node, x2, y2, dur)

> 滑动
> 

- 参数 : node {Node} 节点 
- 参数 : x2 {int} 终点x 
- 参数 : y2 {int} 终点y 
- 参数 : dur {int} 滑动时间 
- 版本 : 1.0.0


```javascript
//滑动手势
$act.move(node,800,500,1000);
```


#### move(node, x2, y2, dur, delay)

> 滑动
> 

- 参数 : node {Node} 节点 
- 参数 : x2 {int} 终点x 
- 参数 : y2 {int} 终点y 
- 参数 : dur {int} 滑动时间 
- 参数 : delay {int} 滑动延迟 
- 版本 : 1.0.0


```javascript
//滑动手势
$act.move(node,800,500,1000,100);
```


#### gesture(gesture)

> 多指手势

- 参数 : gesture {int[]} 动作数据数组[起点x,起点y,终点x,终点y,开始时间,时长]
- 版本 : 1.0.0


```javascript
// 手势模拟向下滑动
$act.gesture([500,0,500,800,0,500]);
```


#### gesture(gesture1, gesture2)

> 双指手势
> 

- 参数 : gesture1 {int[]} 动作数据数组[起点x,起点y,终点x,终点y,开始时间,时长]
- 参数 : gesture2 {int[]} 动作数据数组[起点x,起点y,终点x,终点y,开始时间,时长]
- 版本 : 1.0.0


```javascript
// 双指放大
let centerX = 500;
let centerY = 800;
$act.gesture(
    [centerX,centerY,centerX-400,centerY-400,0,500],
    [centerX,centerY,centerX+400,centerY+400,0,500]
);
```


#### gesture(gesture1, gesture2, gesture3)

> 三指动作
> 

- 参数 : gesture1 {int[]} 动作数据数组
- 参数 : gesture2 {int[]} 动作数据数组
- 参数 : gesture3 {int[]} 动作数据数组
- 版本 : 1.0.0


```javascript
//三指滑动动作
$act.gesture( [500,0,500,800,500,0] ,
[550,0,550,800,500,0] ,
[600,0,600,800,500,0]
);
```


#### gesture(gesture1, gesture2, gesture3, gesture4)

> 四指动作
> 

- 参数 : gesture1 {int[]} 动作数据数组
- 参数 : gesture2 {int[]} 动作数据数组
- 参数 : gesture3 {int[]} 动作数据数组
- 版本 : 1.0.0


```javascript
//四指滑动动作
$act.gesture( [500,0,500,800,500,0] ,
[550,0,550,800,500,0] ,
[600,0,600,800,500,0] ,
[650,0,650,800,500,0]
);
```


#### createPath(paths)

> 通过路径来构建path对象(默认持续时间为1秒)

- 参数 : paths {[][]} 动作数据数组
- 返回 : {Path}
- 版本 : 1.0.0


#### createPath(paths, dur)

> 通过路径来构建path对象

- 参数 : paths {[][]} 动作数据数组
- 参数 : dur {int} 持续
- 返回 : {AgPath} 路径对象
- 版本 : 1.0.0


#### createPath(paths, delay, dur)

> 通过路径来构建path对象

- 参数 : paths {[][]} 动作数据数组
- 参数 : delay {int} 开始时间 
- 参数 : dur {int} 延迟 
- 返回 : {Path}
- 版本 : 1.0.0


#### path(paths)

> 执行路径

- 参数 : paths {AgPath...} 多路径
- 版本 : 1.0.0


#### path(paths)

> 构建一个路径并且执行(默认时间为1秒)

- 参数 : paths {int[][]} 动作数据数组
- 版本 : 1.0.0


#### path(paths, dur)

> 构建一个路径并且执行

- 参数 : paths {int[][]} 动作数据数组
- 参数 : dur {int} 延迟 
- 版本 : 1.0.0


#### path(paths, startTime, dur)

> 构建一个路径并且执行

- 参数 : paths {int[][]} 动作数据数组
- 参数 : startTime {int} 开始时间 
- 参数 : dur {int} 延迟 
- 版本 : 1.0.0


#### home()

> 点击home键
> 
> 如果有root则优先使用root执行
> 如果有Shizuku则优先使用shizuku执行
> 如果有无障碍则优先使用无障碍执行
> 如果以上都没有，则无效果

- 版本 : 1.0.0


```javascript
$act.home();
```


#### back()

> 返回
> 
> 如果有root则优先使用root执行
> 如果有Shizuku则优先使用shizuku执行
> 如果有无障碍则优先使用无障碍执行
> 如果以上都没有，则无效果

- 版本 : 1.0.0


```javascript
$act.back();
```


#### menu()

> 返回
> 
> 如果有root则优先使用root执行
> 如果有Shizuku则优先使用shizuku执行
> 如果有无障碍则优先使用无障碍执行
> 如果以上都没有，则无效果

- 版本 : 1.0.0


```javascript
$act.menu();
```


#### recent()

> 近期任务
> 
> 如果有root则优先使用root执行
> 如果有Shizuku则优先使用shizuku执行
> 如果有无障碍则优先使用无障碍执行
> 如果以上都没有，则无效果

- 版本 : 1.0.0


```javascript
$act.recent();
```


#### power()

> 长按电源
> 
> 如果有root则优先使用root执行
> 如果有Shizuku则优先使用shizuku执行
> 如果有无障碍则优先使用无障碍执行
> 如果以上都没有，则无效果

- 版本 : 1.0.0


```javascript
$act.power();
```


#### lock()

> 锁屏
> 
> 如果有root则优先使用root执行
> 如果有Shizuku则优先使用shizuku执行
> 如果有无障碍则优先使用无障碍执行
> 如果以上都没有，则无效果

- 版本 : 1.0.0


```javascript
$act.lock();
```


#### unlock()

> 唤醒屏幕
> 
> 如果有root则优先使用root执行
> 如果有Shizuku则优先使用shizuku执行
> 如果有无障碍则优先使用无障碍执行
> 如果以上都没有，则无效果

- 版本 : 1.0.0


```javascript
$act.unlock();
```


#### splitScreen()

> 分屏

- 版本 : 1.0.0


```javascript
$act.splitScreen();
```


#### settings()

> 设置

- 版本 : 1.0.0


```javascript
$act.settings();
```


#### notifications()

> 通知

- 版本 : 1.0.0


```javascript
$act.notifications();
```


#### screenshot()

> 截屏
> 
> 唤起手机自带的截屏操作

- 版本 : 1.0.0


```javascript
$act.screenshot();
```


#### input(text)

> 粘贴到文本框
> 
> 如果有root则优先使用root执行
> 如果有Shizuku则优先使用shizuku执行
> 如果有无障碍则优先使用无障碍执行
> 如果以上都没有，则无效果

- 参数 : text {String} 需要输入的文字 
- 版本 : 1.0.0


```javascript
$act.input("我是要粘贴的内容");
```


#### input(node, text)

> 粘贴到文本框
> 
> 无障碍专属的函数

- 参数 : node {AccessibilityNodeInfo} 指定节点
- 参数 : text {String} 需要输入的文字 
- 版本 : 1.0.0


```javascript
$act.input("我是要粘贴的内容");
```


#### input(node, text)

> 粘贴到文本框
> 
> 无障碍专属的函数

- 参数 : node {Node} 指定节点 
- 参数 : text {String} 需要输入的文字 
- 版本 : 1.0.0


```javascript
$act.input("我是要粘贴的内容");
```


#### activity()

> 获得activity类名

- 返回 : activity类名
- 版本 : 1.0.0


```javascript
let name = $act.activity();
log("当前类名:"+name);
```


#### activity(callback)

> 设置窗口变化监听

- 参数 : callback {(name)=>{}} 回调 
- 版本 : 1.0.0


```javascript
//设置监听:
$act.activity((name)=> {
    log("当前界面==>"+name);
});
```


#### selector()

> 创建一个ui选择器
> 

- 返回 : {UiSelector} UI选择器
- 版本 : 1.0.0


#### setDevDensity(density)

> 设置开发环境的密度
> 
> 注意：此函数用于全分辨率适配，需要配合 $act.setAdapt(true) 来使用。
> 
> 测试API:此方法后续可能会被删除

- 参数 : density {float} 密度因子 
- 版本 : 1.0.0


#### setAdapt(usable)

> 是否启动分辨率适配
> 
> 我将根据屏幕密度来等比例计算出坐标的位置。
> 
> 测试API:此方法后续可能会被删除

- 参数 : usable {boolean} 启用分辨率适配 
- 版本 : 1.0.0


#### isOnlyAcc()

> 判断$act是否只使用无障碍服务

- 返回 : {boolean} 是否只使用无障碍服务


#### setOnlyAcc(onlyAcc)

> 设置$act只使用无障碍服务
> 
> 在本应用中$act是一个高度封装的框架，很多动作都会优先判断是否有$root和$szk，如果有root则优先使用root来执行手势，如果有szk(Shizuku)则优先使用Shizuku执行手势，如果$touch可用，则使用$touch执行手势。
> 
> 正因为$act是一个高度封装的框架，导致运行速度会比较慢，毕竟内部的执行逻辑稍微复杂一些。
> 
> 然而有时候我们不需要用到$root、$szk、$touch来执行操作，故设计了这个函数，用来配置$act是否只使用无障碍来进行操作，以加快运行速度。

- 参数 : onlyAcc {boolean} 是否只使用无障碍进行操作 
- 版本 : 1.4.3


#### setJitter(jitter)

> 设置抖动值
> 
> $act允许用户配置抖动值(默认是0)，以实现随机点击，而抖动值其实就是随机值的范围，例如：点击坐标 X=10，抖动值为5时，实际上点击的位置将可能是 X=5到15之间。
> 假设：点击 X=5，抖动值设置为10，则实际上 X抖动之后在0-15之间(而不是-5到15之间)，我要告诉你：抖动之后的坐标不会小于0。
> 
> 不过我需要提醒:我并不会判断你的坐标在抖动之后是否处于屏幕的外部，因此，你需要合理的设置抖动值。

- 参数 : jitter {int} 抖动值  
- 版本 : 1.4.3


#### enableRoot(enableRoot)

> 启用$root
> 
> $act是一个高度封装的框架，很多动作都会判断是否有$root，如果有$root则优先使用$root来执行手势。
> 
> 默认情况下，$root是启用的，你可以通过此函数来禁用$root。

- 参数 : enableRoot {boolean} 是否启用$root 
- 版本 : 1.4.7


#### isEnableRoot()

> 判断$root是否启用

- 返回 : {boolean} 是否启用$root
- 版本 : 1.4.7


#### enableSzk(enableSzk)

> 启用$szk
> 
> $act是一个高度封装的框架，很多动作都会判断是否有$szk，如果有$szk则优先使用$szk来执行手势。
> 
> 默认情况下，$szk是启用的，你可以通过此函数来禁用$szk。

- 参数 : enableSzk {boolean} 是否启用$szk 


#### isEnableSzk()

> 判断$szk是否启用

- 返回 : {boolean} 是否启用$szk
- 版本 : 1.4.7

---

## UiSelector - UI选择器

- 更新时间:2026-01-30 19:32:50

> UI选择器
> 
> 界面的元素有很多，但不一定都是我们要找的那个节点，因此我们需要一些筛选条件过滤掉这些节点。
> 
> UI选择器主要用来过滤界面元素，并且选中我们想要的元素。所以在使用的时候我们需要两类方法：(1).筛选元素;(2).选中元素;



```javascript
//(1)筛选元素
let selector = $act.selector() // 创建UI选择器
     .text("登录") //筛选文本是"登录"的元素
     .cls("android.widget.Button") //筛选类名为"android.widget.Button"的元素
     .pkg("org.aigame.pro") //筛选包名为"org.aigame.pro"的元素
     .desc("点击登录"); //筛选描述是"点击登录"的元素
//(2)选中节点
let node = selector.findFirst(); // 查找一个节点
//其实上面的代码可以直接写成：
let node = $act.selector()
     .text("登录") //筛选文本是"登录"的元素
     .cls("android.widget.Button") //筛选类名为"android.widget.Button"的元素
     .pkg("org.aigame.pro") //筛选包名为"org.aigame.pro"的元素
     .desc("点击登录") //筛选描述是"点击登录"的元素
     .findFirst(); // 查找一个节点
```




#### screen(transCut, vertCut, index)

> 屏幕区域
> 
> 按照屏幕进行切割,在切割的范围中查找元素

- 参数 : transCut {int} 横向切割数
- 参数 : vertCut {int} 纵向切割数
- 参数 : index {int} 第几个区域
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


```javascript
//你可以提前使用下面的方式找到自己想要的范围(查看$screen的文档)
$draw.closeAll();
//将屏幕分割成9份，找到最后一份的范围
let region = $screen.split(3, 3, 8);
//绘制出这个范围
$draw.rect(region);
//用上面这种方式可以快速的定位一个自己想要的范围，而且如果需要找的控件就在范围内，基本上就是全分辨率的。
//如果位置不合适，再调整参数，尽量提高容错，保证自己的脚本支持全分辨率。
//如果位置合适，再把这三个参数传入进来
let nodes = $act.selector()
.screen(3, 3, 8) //我们想要的三个参数
.findAll();
```


#### clickable(able)

> 可点击的

- 参数 : able {boolean} 是否可点击
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### visible(able)

> 是否可见

- 参数 : able {boolean} 是否可见
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.6.1


#### longClickable(able)

> 可长按的

- 参数 : able {boolean} 是否可长按
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### enabled(able)

> 可用的

- 参数 : able {boolean} 是否可用
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### selected(able)

> 选中的

- 参数 : able {boolean} 是否选中
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### scrollable(able)

> 可滚动的

- 参数 : able {boolean} 是否可滚动
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### checkable(able)

> 可勾选的

- 参数 : able {boolean} 是否可勾选
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### checked(able)

> 勾选的

- 参数 : able {boolean} 是否勾选
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### region(x, y, w, h)

> 范围

- 参数 : x {int} x坐标
- 参数 : y {int} y坐标
- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### regionHas(x, y, w, h)

> 输入的范围包含了控件范围

- 参数 : x {int} x坐标
- 参数 : y {int} y坐标
- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### regionInside(x, y, w, h)

> 输入的范围在控件范围的里面

- 参数 : x {int} x坐标
- 参数 : y {int} y坐标
- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### multiLine(able)

> 多行的

- 参数 : able {boolean} 是否多行
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### drawOrder(order)

> 绘制顺序

- 参数 : order {int} 绘制顺序
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### desc(desc)

> 描述

- 参数 : desc {String} 描述
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### descNotNull(notNull)

> 描述不能为空
> 
> 如规定描述不能为空，当遇到描述为空的节点时会自动过滤这个节点

- 参数 : notNull {boolean} 是否不能为空
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.7.6


#### descHas(desc)

> 描述包含

- 参数 : desc {String} 描述
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### descStart(desc)

> 描述开头

- 参数 : desc {String} 描述
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### descEnd(desc)

> 描述结尾

- 参数 : desc {String} 描述
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### descMatch(regex)

> 描述匹配正则表达式

- 参数 : regex {String} 正则表达式
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.6.8


#### windowId(id)

> 窗口id

- 参数 : id {String} id
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### id(id)

> 资源id

- 参数 : id {String} id
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### idNotNull(notNull)

> 资源id不能为空
> 
> 如规定资源id不能为空，当遇到id为空的节点时会自动过滤这个节点

- 参数 : notNull {boolean} 是否不能为空
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.7.6


#### idHas(id)

> 资源id包含

- 参数 : id {String} id
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### idStart(id)

> 资源id开头

- 参数 : id {String} id
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### idEnd(id)

> 资源id结尾

- 参数 : id {String} id
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### idMatch(regex)

> 资源id匹配正则表达式

- 参数 : regex {String} 正则表达式
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.6.8


#### tip(tip)

> 提示信息

- 参数 : tip {String} tip
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### tipNotNull(notNull)

> 提示信息不能为空
> 
> 如规定提示信息不能为空，当遇到提示信息为空的节点时会自动过滤这个节点

- 参数 : notNull {boolean} 是否不能为空
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.7.6


#### tipHas(tip)

> 提示信息包含

- 参数 : tip {String} tip
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### tipStart(tip)

> 提示信息开头

- 参数 : tip {String} tip
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### tipEnd(tip)

> 提示信息结尾

- 参数 : tip {String} tip
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### tipMatch(regex)

> 提示信息匹配正则表达式

- 参数 : regex {String} 正则表达式
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.6.8


#### pkg(packageName)

> 包名

- 参数 : packageName {String} 包名
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### pkgNotNull(notNull)

> 包名不能为空
> 
> 如规定包名不能为空，当遇到提包名为空的节点时会自动过滤这个节点

- 参数 : notNull {boolean} 是否不能为空
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.7.6


#### pkgHas(packageName)

> 包名包含

- 参数 : packageName {String} 包名
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### pkgStart(packageName)

> 包名开头

- 参数 : packageName {String} 包名
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### pkgEnd(packageName)

> 包名结尾

- 参数 : packageName {String} 包名
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### pkgMatch(regex)

> 包名匹配正则

- 参数 : regex {String} 正则表达式
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.6.8


#### cls(className)

> 类名

- 参数 : className {String} 类名
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### clsNotNull(notNull)

> 类名不能为空
> 
> 如规定类名不能为空，当遇到提类名为空的节点时会自动过滤这个节点

- 参数 : notNull {boolean} 是否不能为空
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.7.6


#### clsHas(className)

> 类名包含

- 参数 : className {String} 类名
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### clsStart(className)

> 类名开头

- 参数 : className {String} 类名
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### clsEnd(className)

> 类名结尾

- 参数 : className {String} 类名
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### clsMatch(regex)

> 类名匹配正则表达式

- 参数 : regex {String} 正则表达式
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.6.8


#### text(text)

> 文本

- 参数 : text {String} 文本
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### textNotNull(notNull)

> 文本不能为空
> 
> 如规定文本不能为空，当遇到文本为空的节点时会自动过滤这个节点

- 参数 : notNull {boolean} 是否不能为空
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.7.6


#### textHas(text)

> 文本包含

- 参数 : text {String} 文本
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### textStart(text)

> 文本开头

- 参数 : text {String} 文本
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### textEnd(text)

> 文本结尾

- 参数 : text {String} 文本
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.0.0


#### textMatch(regex)

> 文本匹配正则

- 参数 : regex {String} 正则表达式
- 返回 : {UiSelector} 节点选择器
- 版本 : 1.6.8


#### or()

> 构建或者过滤器
> 
> 创建新的过滤器，并且与之前的过滤器处于或者的关系，当选择当前界面元素的时候，如果存在多个过滤器，只要有一个过滤器满足条件，即可返回结果节点。

- 返回 : {UiSelector} 节点选择器
- 版本 : 1.7.8


```javascript
//这里我封装好了一个强制停止应用的示例
let killApp = function (APP) {
    //先打开指定app的设置界面
    $app.openAppSetting(APP);
    sleep(1000);
    //找到强制停止的按钮
    let node = $act.selector()
        //这里相当于构建了第1个过滤器
        .cls("android.widget.Button")
        .textMatch("强行停止|结束运行|停止|结束")
        .or() //调用 or 函数的时候，可以继续构建下一个过滤器
        //这里相当于构建了第2个过滤器
        .cls("android.widget.TextView")
        .textMatch("强行停止|结束运行|停止|结束")
        //其实你还可以继续用 or 构建更多的情况
        .waitFirst();
    if (node != null) {
        // 绘制节点位置
        node.draw();
        //点击这个节点
        node.click();
        //找到确定按钮
        let node_ensure = $act.selector()
            .cls("android.widget.Button")
            .text("确定")
            .waitFirst();
        if (node_ensure != null) {
            // 绘制节点位置
            node_ensure.draw();
            // 点击
            node_ensure.click();
            //关闭所有悬浮窗
            $draw.closeAll();
            //回到主程序
            $app.openSelf();
        }
    }
}
//先打开这个软件，让它存在运行的状态才能够出现强制停止
$app.run("抖音");
sleep(5000);
// 强制停止app
killApp("抖音");
```


#### findAll()

> 查找全部

- 返回 : {Node[]} 找到的集合
- 版本 : 1.0.0


#### find(index)

> 查找指定

- 参数 : index {int} 第几个，如果index在集合的范围内，就返回index对应的控件，否则返回第一个
- 返回 : {Node} 找到的控件
- 版本 : 1.0.0


#### findFirst()

> 查找第一个

- 返回 : {Node} 找到的控件
- 版本 : 1.0.0


#### findLast()

> 查找最后一个

- 返回 : {Node} 找到的控件
- 版本 : 1.0.0


#### waitAll()

> 等待出现任意一个

- 返回 : {Node[]} 找到的控件集合
- 版本 : 1.0.0


#### waitAll(failCallback)

> 等待出现任意一个
> 
> 会按照默认的等待次数来等待控件出现，当然你可以通过setWaitDur()和setWaitTime()来配置这些参数

- 返回 : {Node[]} 找到的控件列表
- 版本 : 1.0.0


```javascript
let nodes = $act.selector().text("登录").waitAll();
```


#### wait(index, failCallback)

> 等待出现

- 参数 : index {int} 第几个，如果index在集合的范围内，就返回index对应的控件，否则返回第一个
- 参数 : failCallback {()=>{}} 失败回调:连一个控件也没有找到时会回调
- 返回 : {Node} 找到的控件
- 版本 : 1.0.0


#### wait(index)

> 等待出现

- 参数 : index {int} 第几个，如果index在集合的范围内，就返回index对应的控件，否则返回第一个
- 返回 : {Node} 找到的控件
- 版本 : 1.0.0


#### waitFirst()

> 等待出现第一个

- 返回 : {Node} 找到的控件
- 版本 : 1.0.0


#### waitFirst(failCallback)

> 等待出现第一个

- 参数 : failCallback {()=>{}} 失败回调:连一个控件也没有找到时会回调
- 返回 : {Node} 找到的控件
- 版本 : 1.0.0


#### waitLast()

> 等待出现最后一个

- 返回 : {Node} 找到的控件
- 版本 : 1.0.0


#### waitLast(failCallback)

> 等待出现最后一个

- 参数 : failCallback {()=>{}} 失败回调:连一个控件也没有找到时会回调
- 返回 : {Node} 找到的控件
- 版本 : 1.0.0


#### setWaitTime(times)

> 设置等待次数

- 参数 : times {int} 等待次数(默认:120)
- 版本 : 1.0.0


#### setWaitDur(times)

> 设置等待延迟
> 
> 每次等待中会有一定的间隔

- 参数 : times {int} 等待延迟(默认:500[毫秒])
- 版本 : 1.0.0


#### setMainWindow(yes)

> 设置是否只搜索主窗口
> 
> 默认情况下搜索所有的窗口，不过有时候应对一些复杂的UI可能会出现窗口过多(导致元素过多)导致栈溢出的异常，
> 部分app的创建界面如果构建的很复杂，也会导致节点元素不能被及时找出来，因此这个函数就是设置当前选择器只在主窗口中查找元素。
> 
> 举个比较奇葩的例子：有些软件只有当分析主窗口的时候才能找到节点，但是如果分析全部窗口反而找不到节点了，非常奇葩。

- 参数 : yes {boolean} true:只搜索主窗口，false:搜索所有窗口
- 返回 : 1.7.8

---

## Node - 节点信息

- 更新时间:2026-01-30 19:32:50

> 节点信息
> 
> 该节点信息由本应用进行封装，提供了大量便捷的操作，例如可以直接绘制出节点在屏幕上的位置、可以直接调用点击、滑动、输入文字等操作。



```javascript
//首先创建节点选择器
let selector = $act.selector();
//接下来可以通过selector进行界面ui的选择，不过要先进行条件筛选和过滤，因此可以先调用一些筛选类的方法：
selector = selector
.text("登录") //筛选控件文本必须是"登录"的节点
.cls("android.widget.Button");//筛选控件类必须是"android.widget.Button"的节点
//接下来可以调用一些选择类的方法选择节点
let node = selector.waitLast();//在筛选完毕的列表中选择最后一个节点
//接下来就可以使用{Node}中封装的函数了，例如绘制出节点在屏幕的位置：
if(node!=null){
    node.draw();
}
```




#### const {Integer} x;

> x坐标


#### const {Integer} y;

> y坐标


#### const {Integer} w;

> 宽度


#### const {Integer} h;

> 高度


#### const {Integer} cx;

> 中心点x坐标


#### const {Integer} cy;

> 中心点y坐标


#### const {Boolean} clickable;

> 是否可点击


#### const {Boolean} longClickable;

> 是否可长按


#### const {Boolean} enabled;

> 是否可用


#### const {Boolean} selected;

> 是否选中


#### const {Boolean} scrollable;

> 是否可滚动


#### const {Boolean} checkable;

> 是否可勾选


#### const {Boolean} checked;

> 是否勾选


#### const {Boolean} visible;

> 是否可见


#### const {int[]} region;

> 区域
> 格式为[left, top, width, height]


#### const {Boolean} multiLine;

> 是否多行


#### const {Integer} drawOrder;

> 绘制顺序


#### const {String} desc;

> 描述信息


#### const {String} tip;

> 提示信息
> 仅Android 9.0+支持


#### const {String} id;

> 资源id


#### const {String} pkg;

> 包名


#### const {String} cls;

> 类名


#### const {String} text;

> 文本


#### const {Integer} windowId;

> 窗口id


#### const {AccessibilityNodeInfo} node;

> 安卓原生节点信息
> 
> 类名：android.view.accessibility.AccessibilityNodeInfo


#### parent()

> 获取父节点

- 返回 : {Node} 父节点
- 版本 : 1.3.6


#### childNum()

> 获取子节点数

- 返回 : {int} 子节点数量
- 版本 : 1.4.3


#### childs()

> 获取所有子节点

- 返回 : {Node[]} 子节点列表
- 版本 : 1.4.3


#### child(index)

> 获取子节点

- 参数 : index {int} 下标
- 返回 : {Node} 子节点
- 版本 : 1.4.3


#### getX()

> 获取x坐标

- 返回 : {int} x坐标
- 版本 : 1.3.6


#### getY()

> 获取y坐标

- 返回 : {int} y坐标
- 版本 : 1.3.6


#### getW()

> 获取宽度

- 返回 : {int} 宽度
- 版本 : 1.3.6


#### getH()

> 获取高度

- 返回 : {int} 高度
- 版本 : 1.3.6


#### getCx()

> 获取中心点x坐标

- 返回 : {int} 中心点x坐标
- 版本 : 1.3.6


#### getCy()

> 获取中心点y坐标

- 返回 : {int} 中心点y坐标
- 版本 : 1.3.6


#### getClickable()

> 获取是否可点击

- 返回 : {boolean} 是否可点击
- 版本 : 1.3.6


#### getLongClickable()

> 获取是否可长按

- 返回 : {boolean} 是否可长按
- 版本 : 1.3.6


#### getEnabled()

> 获取是否可用

- 返回 : {boolean} 是否可用
- 版本 : 1.3.6


#### getSelected()

> 获取是否选中

- 返回 : {boolean} 是否选中
- 版本 : 1.3.6


#### getScrollable()

> 获取是否可滚动

- 返回 : {boolean} 是否可滚动
- 版本 : 1.3.6


#### getCheckable()

> 获取是否可勾选

- 返回 : {boolean} 是否可勾选
- 版本 : 1.3.6


#### getChecked()

> 获取是否勾选

- 返回 : {boolean} 是否勾选
- 版本 : 1.3.6


#### getRegion()

> 获取区域

- 返回 : {int[]} 区域
- 版本 : 1.3.6


#### getMultiLine()

> 获取是否多行

- 返回 : {boolean} 是否多行
- 版本 : 1.3.6


#### getDrawOrder()

> 获取绘制顺序

- 返回 : {int} 绘制顺序
- 版本 : 1.3.6


#### getTip()

> 获取提示信息

- 返回 : {String} 提示信息
- 版本 : 1.3.6


#### getDesc()

> 获取描述信息

- 返回 : {String} 描述信息
- 版本 : 1.3.6


#### getId()

> 获取资源id

- 返回 : {String} 资源id
- 版本 : 1.3.6


#### getPkg()

> 获取包名

- 返回 : {String} 包名
- 版本 : 1.3.6


#### getCls()

> 获取类名

- 返回 : {String} 类名
- 版本 : 1.3.6


#### getText()

> 获取文本

- 返回 : {String} 文本
- 版本 : 1.3.6


#### getWindowId()

> 获取窗口id

- 返回 : {int} 窗口id
- 版本 : 1.3.6


#### getNode()

> 获取安卓原生节点信息
> 
> 获取安卓原本的对象{AccessibilityNodeInfo}之后就可以调用它本身就具有的API了

- 返回 : {AccessibilityNodeInfo} 安卓原生节点信息
- 版本 : 1.3.6


```javascript
//获得安卓原生类
let andNodeInfo = node.getNode();
//调用安卓API:获取子节点个数
let count = andNodeInfo.getChildCount();//参考{AccessibilityNodeInfo}类中的方法
alert("子节点个数",""+count);
```


#### click()

> 点击
> 
> 默认不使用坐标手势:click(false)，而是使用节点手势执行点击动作。

- 版本 : 1.3.6


#### click(useAct)

> 点击
> 
> 节点执行的手势有时候没有效果，此时可以使用坐标来进行点击:click(true);

- 参数 : useAct {boolean} 是否使用act点击
- 版本 : 1.3.6


#### click(px, py)

> 点击
> 
> 偏移点击，会相对于当前节点的坐标进行偏移x或y的距离，可传入正负数。

- 参数 : px {int} x的偏移量
- 参数 : py {int} y的偏移量
- 版本 : 1.3.6


#### press()

> 长按
> 
> 默认不使用坐标手势:press(false)，而是使用节点手势执行长按动作。

- 版本 : 1.3.6


#### press(dur)

> 长按

- 参数 : dur {int} 长按时间
- 版本 : 1.3.6


#### press(px, py)

> 长按

- 参数 : px {int} x的偏移量
- 参数 : py {int} y的偏移量
- 版本 : 1.3.6


#### press(px, py, dur)

> 长按

- 参数 : px {int} x的偏移量
- 参数 : py {int} y的偏移量
- 参数 : dur {int} 长按时间
- 版本 : 1.3.6


#### press(useAct)

> 长按
> 
> 节点执行的手势有时候没有效果，此时可以使用坐标来进行长按:press(true);

- 参数 : useAct {boolean} 是否使用坐标长按
- 版本 : 1.3.6


#### move(dir)

> 滑动

- 参数 : dir {string} 方向:up,down,left,right
- 版本 : 1.3.6


#### move(x2, y2, dur)

> 滑动

- 参数 : x2 {int} 目标x坐标
- 参数 : y2 {int} 目标y坐标
- 参数 : dur {int} 滑动时间
- 版本 : 1.3.6


#### move(x2, y2, dur, delay)

> 滑动

- 参数 : x2 {int} 目标x坐标
- 参数 : y2 {int} 目标y坐标
- 参数 : dur {int} 滑动时间
- 参数 : delay {int} 滑动延迟
- 版本 : 1.3.6


#### move(px, py, x2, y2, dur, delay)

> 滑动

- 参数 : px {int} x的偏移量
- 参数 : py {int} y的偏移量
- 参数 : x2 {int} 目标x坐标
- 参数 : y2 {int} 目标y坐标
- 参数 : dur {int} 滑动时间
- 参数 : delay {int} 滑动延迟
- 版本 : 1.3.6


#### draw()

> 全屏绘制节点方框
> 
> 需要悬浮窗权限

- 版本 : 1.3.6


#### input(text)

> 输入内容
> 
> 对于使用网页开发的输入框，需要指定本应用的输入法才可以输入文字，此函数可以判断输入法是否可用，如果可用就优先使用输入法输入，否则就用无障碍输入。

- 版本 : 1.3.6


#### input(text, useAcc)

> 输入内容
> 
> 对于使用网页开发的输入框，需要指定本应用的输入法才可以输入文字

- 参数 : text {boolean} 是否只用无障碍输入，为true时，只会使用无障碍输入，如果为false则会判断输入法是否可用,可用就用输入法输入，否则就用无障碍输入
- 版本 : 1.3.6


#### findFirst(selector)

> 查找子孙节点

- 参数 : selector {uiSelector} 筛选器 
- 返回 : {node} 符合条件的节点


```javascript
let node = $act.selector() //创建选择器
.pkg("com.taobao.idlefish") //为选择器添加过滤条件
.cls("android.view.View") //为选择器添加过滤条件
.desc("看对眼就留言，问问更多细节~") //为选择器添加过滤条件
.waitFirst(); //通过过滤条件找到符合要求的节点
if (node != null) {
    //如果想要查找node的子孙节点，也可以通过选择器来查找
    let mSelector = $act.selector() //创建选择器
    .pkg("com.taobao.idlefish") //为选择器添加过滤条件
    .cls("android.view.Button"); //为选择器添加过滤条件
    //然后把选择器传入进去即可过滤找到node的子孙节点
    let childNode = node.findFirst(mSelector);
    if(childNode!=null){
        log("找到子孙节点了");
        childNode.draw();//绘制位置
    }
}
```


#### findLast(selector)

> 查找子孙节点

- 参数 : selector {uiSelector} 筛选器 
- 返回 : {node} 符合条件的节点


#### find(selector, index)

> 查找子孙节点
> 
> 指定过滤器以及子孙节点的下标，当下标超过列表范围的时候，会返回列表最后一个node节点

- 参数 : selector {uiSelector} 筛选器 
- 参数 : index {num} 下标
- 返回 : {node} 符合条件的节点


#### findAll(selector)

> 查找子孙节点

- 参数 : selector {uiSelector} 筛选器 
- 返回 : {node[]} 符合条件的节点列表

---

*# # - 内容未找到*