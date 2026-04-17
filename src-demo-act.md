# 示例：手势操作 ($act / $touch)


## $act-#U52a8#U4f5c#U624b#U52bf-01.#U83b7#U53d6#U6743#U9650

```javascript
//AIGame 官方示例

//(1)判断是否获取无障碍权限
let has = $act.hasPermit();

//(2)如果没有取无障碍，则获取权限
if (has) {
    log("已经获得无障碍权限");
} else {
    log("请求获取无障碍权限");
    $act.getPermit();
}


//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-02.#U70b9#U51fb

```javascript
//AIGame 官方示例

//安卓7以上使用无障碍执行手势
//安卓7以下自动切换成root执行手势

$act.click(400,348);



//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-03.#U957f#U6309

```javascript
//AIGame 官方示例

//安卓7以上使用无障碍执行手势
//安卓7以下自动切换成root执行手势

$act.press(400,348);



//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-04.#U6ed1#U52a8

```javascript
//AIGame 官方示例

//安卓7以上使用无障碍执行手势
//安卓7以下自动切换成root执行手势

//下拉通知
$act.move(400,0,400,800,1000);



//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-05.#U53cc#U6307#U64cd#U4f5c

```javascript
//AIGame 官方示例

//安卓7以上使用无障碍执行手势
//安卓7以下自动切换成root执行手势

//注意:不推荐在android7以下使用多指手势,因为root手势本身就不支持多指
//虽然可以正常运行，但是和无障碍手势的效果有差别

//(1)先长按
let g1 = [504,583,504,583,0,1000];
//(2)再滑动
let g2 = [504,583,504,883,1000,1000];
$act.gesture(g1,g2);



//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-06.#U4e09#U6307#U624b#U52bf

```javascript
//AIGame 官方示例

//安卓7以上使用无障碍执行手势
//安卓7以下自动切换成root执行手势

//注意:不推荐在android7以下使用多指手势,因为root手势本身就不支持多指
//虽然可以正常运行，但是和无障碍手势的效果有差别

//模拟三指下滑
let g1 = [500,900,500,1500,0,1000];
let g2 = [500,900,500,1500,0,1000];
let g3 = [500,900,500,1500,0,1000];
$act.gesture(g1,g2,g3);



//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-07.#U6309#U952e#U64cd#U4f5c

```javascript
//AIGame 官方示例
sleep(2000);
$draw.i("执行操作:$act.home()");
$act.home();

sleep(2000);
$draw.i("执行操作:$act.menu()");
$act.menu();//此函数和recen()t函数效果一致

sleep(2000);
$draw.i("执行操作:$act.back()");
$act.back();

sleep(2000);
$draw.i("执行操作:$act.power()");
$act.power();

sleep(2000);
$draw.i("执行操作:$act.back()");
$act.back();

sleep(2000);
$draw.i("执行操作:$act.settings()");
//打开设置界面
$act.settings();

sleep(2000);
$draw.i("返回主页");
$act.home();

sleep(2000);
$draw.i("执行操作:$act.notifications()");
//打开通知
$act.notifications();

sleep(2000);
$draw.i("返回主页");
$act.home();


sleep(2000);
$draw.closeLog();


//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-08.#U5b89#U53539#U7279#U6b8a#U64cd#U4f5c

```javascript
//AIGame 官方示例

sleep(2000);
//执行分屏操作
$act.splitScreen();

sleep(2000);
//执行截屏操作
$act.screenshot();


//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-09.#U606f#U5c4f#U4e0e#U5524#U9192

```javascript
//AIGame 官方示例

//注意：当无障碍不可用时，自动切换使用root手势执行息屏和亮屏
$act.lock();//息屏
sleep(2000);
$act.unlock();//亮屏



//使用root版本的息屏与亮屏
/*
sleep(2000);
$root.lock();//息屏
sleep(2000);
$root.unlock();//亮屏
*/

//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-10.#U754c#U9762#U76d1#U542c

```javascript
//AIGame 官方示例

let curActivity = $act.activity(); //获得当前界面类名
log(curActivity);

//设置界面变化监听(你可以打开其他软件界面,看看日志信息)
$act.activity((name)=> {
    log("当前界面:",name);
});

//20秒后关闭界面变化监听
sleep(20000);

//关闭界面变化监听
$act.activity(null);

//示例结束
```


## $act-#U52a8#U4f5c#U624b#U52bf-11.#U8f93#U5165#U6587#U672c#U6846

```javascript
//AIGame 官方示例

//当界面中有文本框获得焦点时，可以直接设置内容
$act.input("需要设置的内容");

//示例结束
```


## $color-#U989c#U8272#U5de5#U5177-01.#U56fe#U7247#U627e#U8272-01.#U627e#U51fa#U4e00#U4e2a#U4f4d#U7f6e

```javascript
//如果没有无障碍权限，则会获取录屏权限
if(!$act.hasPermit()){
    //阻塞方法:直到获取录屏权限为止，才会继续向下执行代码
    $screen.getPermit();
}

//获取悬浮窗权限
$floaty.getPermit();
//把图片显示在屏幕上
$img.show("example/$color - 颜色工具/01.图片找色/p01.png")
//截屏并且找颜色
sleep(1000);//显示图片需要时间,所以延迟一秒
let screenImg = $screen.getScreen();//如果有无障碍就会使用无障碍来截屏
//第4个参数因为我不知到具体的范围所以就空着(默认全屏查找)
let result = $color.find(screenImg,"#d87d83");
if(result!=null){
    $draw.dot(result);//绘制结果位置
    $draw.log(result);//屏幕显示位置
    sleep(3000);
    $draw.closeAll();//关闭绘制
}
```


## $color-#U989c#U8272#U5de5#U5177-01.#U56fe#U7247#U627e#U8272-02.#U627e#U51fa#U4e00#U4e2a#U4f4d#U7f6e(#U5b8c#U6574#U53c2#U6570)

```javascript
//如果没有无障碍权限，则会获取录屏权限
if(!$act.hasPermit()){
    //阻塞方法:直到获取录屏权限为止，才会继续向下执行代码
    $screen.getPermit();
}

//获取悬浮窗权限
$floaty.getPermit();
//把图片显示在屏幕上
$img.show("example/$color - 颜色工具/01.图片找色/p01.png")
//截屏并且找颜色
sleep(1000);//显示图片需要时间,所以延迟一秒
let screenImg = $screen.getScreen();//如果有无障碍就会使用无障碍来截屏
//第4个参数因为我不知到具体的范围所以就空着(默认全屏查找)
let result = $color.find(screenImg,"#d87d83",5,[]);
if(result!=null){
    $draw.dot(result);//绘制结果位置
    $draw.log(result);//屏幕显示位置
    sleep(3000);
    $draw.closeAll();//关闭绘制
}
```


## $color-#U989c#U8272#U5de5#U5177-01.#U56fe#U7247#U627e#U8272-03.#U627e#U51fa#U591a#U4e2a#U4f4d#U7f6e

```javascript
//如果没有无障碍权限，则会获取录屏权限
if(!$act.hasPermit()){
    //阻塞方法:直到获取录屏权限为止，才会继续向下执行代码
    $screen.getPermit();
}

//获取悬浮窗权限
$floaty.getPermit();
//把图片显示在屏幕上
$img.show("example/$color - 颜色工具/01.图片找色/p02.png")
//截屏并且找颜色
sleep(1000);//显示图片需要时间,所以延迟一秒
let screenImg = $screen.getScreen();//如果有无障碍就会使用无障碍来截屏
//只用两个参数其他的默认
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


## $color-#U989c#U8272#U5de5#U5177-01.#U56fe#U7247#U627e#U8272-04.#U627e#U51fa#U591a#U4e2a#U4f4d#U7f6e(#U5b8c#U6574#U53c2#U6570)

```javascript
//如果没有无障碍权限，则会获取录屏权限
if(!$act.hasPermit()){
    //阻塞方法:直到获取录屏权限为止，才会继续向下执行代码
    $screen.getPermit();
}

//获取悬浮窗权限
$floaty.getPermit();
//把图片显示在屏幕上
$img.show("example/$color - 颜色工具/01.图片找色/p02.png")
//截屏并且找颜色
sleep(1000);//显示图片需要时间,所以延迟一秒
let screenImg = $screen.getScreen();//如果有无障碍就会使用无障碍来截屏
//第4个参数因为我不知到具体的范围所以就空着(默认全屏查找)
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


## $touch-#U89e6#U6478#U9a71#U52a8-01.#U70b9#U51fb

```javascript
//官方示例

//第一次执行大概需要4秒，第二次瞬间就能执行触摸操作
if($touch.hasPermit()){
    $touch.init();
}

$touch.click(410,350);



//示例结束
```


## $touch-#U89e6#U6478#U9a71#U52a8-02.#U957f#U6309

```javascript
//官方示例

//第一次执行大概需要4秒，第二次瞬间就能执行触摸操作
if($touch.hasPermit()){
    $touch.init();
}

$touch.press(410,350);



//示例结束
```


## $touch-#U89e6#U6478#U9a71#U52a8-03.#U6ed1#U52a8

```javascript
//官方示例

//第一次执行大概需要4秒，第二次瞬间就能执行触摸操作
if($touch.hasPermit()){
    $touch.init();
}

$touch.move(400,0,400,500);



//示例结束
```
