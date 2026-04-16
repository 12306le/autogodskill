# 并发与事件 API

> 多线程编程、脚本任务、事件监听、消息总线、脚本引擎。

## 目录
- [$thread - 并发编程](#thread---并发编程)
- [CdLock - 倒计时锁](#cdlock---倒计时锁)
- [Threadx - 增强线程](#threadx---增强线程)
- [JsTaskInfo - 脚本任务信息](#jstaskinfo---脚本任务信息)
- [$task - 脚本任务](#task---脚本任务)
- [$engine - 脚本引擎](#engine---脚本引擎)
- [$event - 事件监听](#event---事件监听)
- [$bus - 消息总线](#bus---消息总线)

---

## $thread - 并发编程

- 更新时间:2026-01-30 19:32:56

> 并发编程
> 
> 本平台支持多线程并发编程，并且很多API内部都已经解决了并发问题




#### ui(runnable)

> 在UI线程中执行
> 
> 其实也可以使用$ui.run(()=>{});在ui线程中执行

- 参数 : runnable {()=>{}} 任务
- 版本 : 1.0.0


```javascript
$thread.ui(()=>{
    //这里是UI线程
});
```


#### run(runnable)

> 创建并且运行线程

- 参数 : runnable {()=>{}} 任务
- 返回 : {Threadx} 增强线程
- 版本 : 1.2.0


```javascript
let t1 = $thread.run(()=>{
    //耗时任务
});
//要想停止或者关闭
t1.interrupt();
```


#### create(runnable)

> 创建线程
> 
> 会自动生成线程名称，之后将线程名称和线程对象存储到序列中。

- 参数 : runnable {()=>{}} 线程任务
- 返回 : {Threadx} 增强线程
- 版本 : 1.0.0


```javascript
let t1 = $thread.create(()=> {
    for (let i = 0; i < 10; i++) {
        sleep("300");
        log(t1.getName()+"==>"+i);
    }
    log(t1.getName()+"执行完毕");
});
t1.start();
```


#### create(name, runnable)

> 创建线程
> 
> 优先去序列中查找是否存在这个线程名称，如果存在，会提示名称重复并且返回已经存在的线程对象(threadx)

- 参数 : name {()=>{}} 线程任务
- 返回 : {Threadx} 增强线程
- 版本 : 1.0.0


```javascript
let t1 = $thread.create("线程名称",()=> {
    for (let i = 0; i < 10; i++) {
        sleep("300");
        log(t1.getName()+"==>"+i);
    }
    log(t1.getName()+"执行完毕");
});
t1.start();
```


#### newCdLock(num)

> 创建一个倒计时锁

- 参数 : num {int} 倒计时数量
- 返回 : {CdLock} 倒计时锁
- 版本 : 1.8.3


#### has(name)

> 是否存在线程名称

- 参数 : name {string} 线程名称
- 返回 : {boolean} 是否存在
- 版本 : 1.2.0


```javascript
let has = $thread.has("线程名称");
if(has){
    //存在线程名称
}else{
    //不存在线程名称
}
```


#### get(name)

> 获得已存在的线程

- 参数 : name {string} 线程名称
- 版本 : 1.0.0


```javascript
//获得线程对象
let t1 = $thread.get("线程名称");
if(t1!=null){
    //...
}
```


#### loop(name, runnable)

> 创建一个循环执行器

- 参数 : name {string} 循环器名称
- 参数 : runnable {()=>{}} 循环体
- 返回 : {Threadx} 增强线程
- 版本 : 1.0.0


```javascript
let t1 = $thread.loop("循环1号",()=>{
    sleep(1000);
    log("我还活着！");
});
t1.start();
```


#### hasLoop(name)

> 是否存在循环执行器

- 参数 : name {string} 循环器名称
- 返回 : {boolean} 是否存在
- 版本 : 1.0.0


```javascript
//关闭循环器
let exists = $thread.hasLoop("循环1号");
```


#### stopLoop(name)

> 停止循环执行器

- 参数 : name {string} 循环器名称
- 版本 : 1.0.0


```javascript
//关闭循环器
$thread.stopLoop("循环1号");
```


#### stop(threadx)

> 停止指定线程
> 
> 如果停止线程成功,会将增强线程中的布尔标识(setBool)设置为false

- 参数 : threadx {Threadx} 增强线程
- 版本 : 1.0.0


#### stop(threadName)

> 停止指定线程

- 参数 : threadName {string} 线程名称
- 版本 : 1.0.0


#### stopAll()

> 停止所有线程

- 版本 : 1.0.0


```javascript
//停止所有线程(不包括循环器线程)
$thread.stopAll();
```


#### stopAllLoop()

> 停止所有循环执行器
> 
> 'setInterval'本质上也是通过循环执行器实现的，因此本函数也可以停止'setInterval'的循环执行

- 版本 : 1.0.0


```javascript
//停止所有循环执行器
$thread.stopAllLoop();
```

---

## CdLock - 倒计时锁

- 更新时间:2026-01-30 19:32:56

> 倒计时锁
> 
> 是对CountDownLatch的封装对象，倒计时锁，用于等待多个线程完成。




#### ok()

> 完成一个倒计时

- 版本 : 1.8.3


#### finish()

> 等待所有倒计时完成

- 版本 : 1.8.3


#### finish(timeout)

> 等待所有倒计时完成

- 参数 : timeout {long} 超时时间(ms)
- 返回 : {boolean} 是否完成
- 版本 : 1.8.3


#### getCount()

> 获取倒计时数量

- 返回 : {long} 倒计时数量
- 版本 : 1.8.3

---

## Threadx - 增强线程

- 更新时间:2026-01-30 19:32:56

> 增强线程
> 
> 增强线程名为"Threadx"，它继承自"java.lang.Thread"类，提供了额外的功能和属性，主要允许线程携带一些简单的基础数据。




#### name()

> 获取线程名称

- 返回 : {string} 线程名称
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//获取线程名称
let name = tx.name();
//输出线程名称
alert("线程名称" , name);
```


#### hasRun()

> 判断当前线程是否终止

- 返回 : {boolean} 是否停止运行
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//判断当前线程是否终止
let run = tx.hasRun();
if(run){
     alert("线程正在运行");
}else{
     alert("线程已终止");
}
```


#### setStr(str)

> 设置字符类型的标志

- 参数 : str {string} 字符类型的标志
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//设置字符类型的标志
tx.setStr("携带数据");
```


#### getStr()

> 获得字符类型的标志

- 返回 : {string} 字符类型的标志
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//获得字符类型的标志
let srt = tx.getStr();
```


#### setBool(booFlag)

> 设置布尔类型的标志
> 
> 需要注意:当线程(非循环器)被终止时，布尔类型的标志位会被设置为false;

- 参数 : booFlag {boolean} 布尔类型的标志
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//设置布尔类型的标志
tx.setBool(false);
```


#### getBool()

> 获取布尔类型的标志
> 
> 需要注意:当线程(非循环器)被终止时，布尔类型的标志位会被设置为false;

- 返回 : {boolean} 布尔类型的标志
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//获取布尔类型的标志
let b = tx.getBool();
```


#### getInt()

> 获取整数类型的标志

- 返回 : {int} 整数标志值
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//获取整数类型的标志
let i = tx.getInt();
```


#### setInt(flag)

> 设置整数类型的标志

- 参数 : flag {int} 整数标志值
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//设置整数类型的标志
tx.setInt(0);
```


#### getLong()

> 获取长整数类型的标志

- 返回 : {long} 长整数标志值
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//获取长整数类型的标志
let l = tx.getLong();
```


#### setLong(flag)

> 设置长整数类型的标志

- 参数 : flag {long} 长整数标志值
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//设置长整数类型的标志
tx.setLong(1000);
```


#### getObj()

> 获取对象类型的标志

- 返回 : {Object} 对象标志值
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//获取对象类型的标志
let o = tx.getObj();
```


#### setObj(flag)

> 设置对象类型的标志

- 参数 : flag {Object} 对象标志值
- 版本 : 1.2.0


```javascript
//增强线程对象
let tx = $thread.create(()=>{
    //...
});
//设置对象类型的标志
tx.setObj("我是任意数据");
```


#### kill()

> 终止线程

- 版本 : 1.5.1


```javascript
//由于interrupt不太好记，所以就写了个'kill()'方便中止线程。
//使用kill方法中止线程
tx.kill();//等价于tx.interrupt();
```

---

## JsTaskInfo - 脚本任务信息

- 更新时间:2026-01-30 19:33:08

> 脚本任务信息




#### const {String} ID;

> 任务ID


#### const {String} startTime;

> 开始执行的时间


#### const {String} endTime;

> 执行结束时的时间


#### const {String} runTime;

> 执行时常


#### const {String} name;

> 脚本名称


#### const {String} path;

> 脚本路径


#### getID()

> 任务ID

- 返回 : {string} 任务ID
- 版本 : 1.0.0


#### getStartTime()

> 执行结束时的时间

- 返回 : {string} 执行结束时的时间
- 版本 : 1.0.0


#### getName()

> 执行结束时的时间

- 返回 : {string} 执行结束时的时间
- 版本 : 1.0.0


#### getPath()

> 执行结束时的时间

- 返回 : {string} 执行结束时的时间
- 版本 : 1.0.0

---

## $task - 脚本任务

- 更新时间:2026-01-30 19:33:04

> 脚本任务
> 
> 每个正在执行的代码文件中都会内置一个专属对象：任务对象($task)
> 
> 你可以通过任务对象($task)来控制当前任务的执行
> 
> 你也可以通过任务对象($task)来获取当前任务的信息




#### const {String} ID;

> 任务唯一序列
> 
> 该序列会和当前线程名称保持一致


```javascript
log("当前任务唯一序列:",$task.ID);
```


#### const {long} startTime;

> 当前任务的开始执行时间

- 版本 : 1.3.9


```javascript
log("当前任务的开始执行时间:",$task.startTime);
```


#### const {String} name;

> 当前任务名称
> 
> 有时也指路径或文件名称

- 版本 : 1.3.9


```javascript
log("当前任务名称:",$task.name);
```


#### const {String} threadName;

> 当前任务线程名称
> 
> 线程名称通常与ID相同

- 版本 : 1.3.9


```javascript
log("当前任务线程名称:",$task.threadName);
```


#### const {String} path;

> 当前脚本路径
> 
> 此属性并不重要，取决于执行脚本时传入的路径参数值，如果是临时文件，则路径是随机生成的。

- 版本 : 1.3.9


```javascript
log("当前脚本路径:",$task.path);
```


#### stop()

> 停止任务
> 
> 每个任务($task)都是一条新的线程，如果你的代码中存在死循环，则循环不会停止(因为循环会被当作一条命令执行，表示执行完毕这个命令了)，请处理好脚本逻辑。

- 版本 : 1.0.0


```javascript
$task.stop();
```


#### getInfo()

> 获取脚本任务信息

- 返回 : {JsTaskInfo} 任务信息
- 版本 : 1.0.0


```javascript
let info = $task.getInfo();
alert("任务信息",info.toString());
```


#### isRunning()

> 是否正在运行

- 返回 : {boolean} 返回是否正在运行
- 版本 : 1.0.0


```javascript
let is = $task.isRunning();
if(is){
    alert("任务正在运行");
}else{
    alert("任务已经停止运行");
}
```


#### getID()

> 获取当前任务的ID

- 返回 : {string} 返回当前任务的ID
- 版本 : 1.0.0


```javascript
let id = $task.getID();
alert("任务ID",id);
```


#### getStartTime()

> 获取当前任务的开始时间

- 返回 : {long} 返回当前任务的开始时间
- 版本 : 1.0.0


```javascript
let time = $task.getStartTime();
alert("任务开始时间",time);
```


#### getName()

> 获取当前任务的名称

- 返回 : {string} 返回当前任务的名称
- 版本 : 1.0.0


```javascript
let name = $task.getName();
alert("任务名称",name);
```


#### getThreadName()

> 获取当前任务的线程名称

- 返回 : {string} 返回当前任务的线程名称
- 版本 : 1.0.0


```javascript
let tn = $task.getThreadName();
alert("线程名称",tn);
```


#### getPath()

> 获取当前任务的脚本路径

- 返回 : {string} 返回当前任务的脚本路径
- 版本 : 1.0.0


```javascript
let path = $task.getPath();
alert("脚本路径",path);
```


#### getPath(relativePath)

> 获取相对当前脚本路径的绝对路径

- 参数 : relativePath {string} 相对路径
- 返回 : {string} 返回绝对路径
- 版本 : 1.0.0


```javascript
let path = $task.getPath("../res");
alert("相对路径",path);
```


#### pause()

> 暂停当前任务

- 版本 : 1.3.9


```javascript
//我演示一个错误的用法：
$task.pause();//当暂停以后，下面的代码不会被执行
//...其他代码
$task.start();//这行代码不被执行到，因此这样调用毫无意义
```


#### start()

> 继续运行暂停的任务

- 版本 : 1.3.9


```javascript
$task.start();
```


#### isPause()

> 任务是否暂停

- 返回 : {boolean} 是否暂停
- 版本 : 1.3.9


```javascript
log("是否暂停",$task.isPause());
```


#### isStop()

> 判断任务是否停止
> 
> 只有当调用了'$task.stop()'或者'$engine.stop(ID)'或'$engine.stopAll()'才会返回'true'

- 返回 : {boolean} 是否停止
- 版本 : 1.7.0


```javascript
//因此，在多线程中正确书写死循环的方式：
$thread.run(()=>{
    while(!$task.isStop()){
        log("正在运行...");
        sleep(1000);
    }
    log("脚本停止");
});
```

---

## $engine - 脚本引擎

- 更新时间:2026-01-30 19:32:52



#### runJs(jsPath)

> 执行路径中的脚本

- 参数 : jsPath {String} 脚本路径
- 版本 : 1.8.6


#### stop()

> 停止所有脚本

- 版本 : 1.8.6

---

## $event - 事件监听

- 更新时间:2026-01-30 19:32:51

> 事件监听
> 
> $event主要用来监听一些系统级别的事件,也会处理一些基础的应用事件,这些事件部分会依赖无障碍权限才可以监听得到。
> 
> 此对象是一个线程安全的对象,内部已经处理好了线程并发情况,因此可以在任何线程中调用。




#### on(name, callback)

> 挂载事件监听
> 
> 此函数是[唯一监听器]，全局只会被设置一次(用户调用)，当调用多次该函数时，后者将覆盖前者的数据。
> 
> 如果想要取消[唯一监听器]，只需要将第二个参数设置为null即可，例如：$event.on("lock",null);//取消锁屏事件
> 
> 在$event中，事件分为好几个大类，一般有：(1)系统事件 (2)无障碍事件 (3)软件内部事件
> 
> 一般情况下:(1)系统事件:不需要任何权限，但也有个例(比如：蓝牙需要附近设备权限以及位置权限)，
> 但在(2)无障碍事件中:需要开启无障碍权限，否则无法监听得到。

- 参数 : name {string} 事件类型名称
- 参数 : callback {(data)=>{log(data);};} 回调函数


```javascript
//如果你想监听某些事件，必须要知道这些事件的名称，请参考{EventType}文档
//监听WIFI事件
$event.on("wifi",(data)=>{
    //data中包含着非常详细的描述信息，通过日志就能打印获取
    log(data);
});
```


#### add(name, callback)

> 添加事件监听
> 
> 每次调用该函数，否会增加一个监听器，即使是相同的名称，也会添加到监听器列表中。
> 
> 在$event对象中，存在两种事件触发机制：[唯一监听器]和[监听器列表]
> 
> [唯一监听器]是通过on(name,callback)函数来进行设置的，它是全局唯一的，当事件触发的时候，只会被调用一次。
> 
> [监听器列表]是通过add(name,callback)函数来进行添加的，你可以多次添加多个监听器，甚至允许名称相同，当事件触发时，会调用你添加的所有监听器(软件重启后，监听器列表会被重置清空)。
> 
> 当系统事件触发的时候，会先触发[唯一监听器]，然后再触发[监听器列表]中的所有监听器。

- 参数 : name {string} 事件类型名称
- 参数 : callback {(data)=>{log(data);};} 回调函数


#### ls()

> 获取监听器列表名

- 返回 : {string[]} 监听器列表名


#### clear()

> 清空监听器列表

---

## $bus - 消息总线

- 更新时间:2026-01-30 19:32:51

> 消息总线
> 
> 在全局中发送消息，任意位置获取并且处理消息




#### ls()

> 列出所有监听器

- 返回 : {String[]} 监听器列表
- 版本 : 1.0.0


```javascript
//获得所有监听器列表
let monis = $bus.ls();
log(monis);//[我的监听器1号]
```


#### post(name, object)

> 发送一条信息

- 参数 : name {String} 监听器名称 
- 参数 : object {Object} 信息内容 
- 版本 : 1.0.0


```javascript
$bus.post("我的监听器1号","我是数据");
```


#### event(name, listener)

> 添加监听

- 参数 : name {string} 监听器名称 
- 参数 : listener {(data)=>{}} 监听器 
- 版本 : 1.0.0


```javascript
$bus.event("我的监听器1号",(data)=>{
    log("获得数据:",data);
    toast(data);
});
```


#### close(name)

> 移除监听器

- 参数 : name {string} 名称 
- 版本 : 1.0.0


```javascript
//指定关闭监听器
$bus.close("我的监听器1号");
```


#### clear()

> 移除所有监听器

- 版本 : 1.0.0


```javascript
$bus.clear();//关闭所有监听器
```


#### stopAll()

> 关闭所有监听器

- 版本 : 1.0.0


```javascript
$bus.stopAll();//关闭所有监听器效果和clear()一样
```