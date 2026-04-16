# 悬浮窗与绘制 API

> 系统悬浮窗、应用级悬浮窗、全屏绘制、悬浮球菜单。

## 目录
- [$floaty - 悬浮窗](#floaty---悬浮窗)
- [SysFloaty - 系统级悬浮窗](#sysfloaty---系统级悬浮窗)
- [AppFloaty - 应用级悬浮窗](#appfloaty---应用级悬浮窗)
- [AdjFloaty - 可调节悬浮窗](#adjfloaty---可调节悬浮窗)
- [SelectFloaty - 选择悬浮窗](#selectfloaty---选择悬浮窗)
- [$draw - 全屏绘制](#draw---全屏绘制)
- [$arc - 悬浮球](#arc---悬浮球)
- [MenuBody - 按钮容器](#menybody---按钮容器)
- [MenuItem - 悬浮按钮](#menuitem---悬浮按钮)

---

## $floaty - 悬浮窗

- 更新时间:2026-01-30 19:32:53

> 悬浮窗




#### getPermit()

> 获取悬浮窗权限
> 
> 这个方法是个阻塞方法，如果没有获取到悬浮窗权限，则每隔30秒会请求一次权限，那么后面的代码不会被执行，并且会一直等待悬浮窗权限，直到获取到为止。
> 
> 如果你希望只获取一次悬浮窗权限，可以调用$permit.floaty();来获取权限

- 返回 : {boolean} 是否有权限
- 版本 : 1.0.0


```javascript
//获取悬浮窗权限
let hasPermit = $floaty.getPermit();
if(hasPermit){
    log("获取到悬浮窗权限");
}
```


#### hasPermit()

> 是否有悬浮窗权限

- 返回 : {boolean} 是否有悬浮窗权限
- 版本 : 1.0.0


```javascript
//是否有悬浮窗权限
let hasPermit = $floaty.hasPermit();
if(hasPermit){
    log("有悬浮窗权限");
}
```


#### newAdj(xmlOrPath)

> 创建可调节悬浮窗

- 参数 : xmlOrPath {xml|path} xml或路径
- 返回 : {AdjustableFloaty} 可调节悬浮窗
- 版本 : 1.4.4


```javascript
//你可以直接引入一个布局文件创建一个可调节悬浮窗
let adjFloaty = $floaty.newAdj("./res/layout/floaty_adj.xml");
//你也可以直接把xml写成字符串传入
let adjFloaty = $floaty.newAdj(`<ui>...</ui>`);
```


#### newApp(xmlOrPath)

> 创建应用级悬浮窗

- 参数 : xmlOrPath {xml|path} xml或路径
- 返回 : {AppFloaty} 悬浮窗
- 版本 : 1.4.4


```javascript
//你可以直接引入一个布局文件创建一个应用级悬浮窗
let appFloaty = $floaty.newApp("./res/layout/floaty_app.xml");
//你也可以直接把xml写成字符串传入
let appFloaty = $floaty.newApp(`<ui>...</ui>`);
```


#### newApp(xmlOrPath, touchable)

> 创建应用级悬浮窗

- 参数 : xmlOrPath {xml|path} xml或路径
- 参数 : touchable {boolean} 是否可触摸(默认:true)
- 返回 : {AppFloaty} 悬浮窗
- 版本 : 1.8.3


```javascript
//你可以直接引入一个布局文件创建一个应用级悬浮窗
let appFloaty = $floaty.newApp("./res/layout/floaty_app.xml",false);
//你也可以直接把xml写成字符串传入
let appFloaty = $floaty.newApp(`<ui>...</ui>`,false);
```


#### newSys(xmlOrPath)

> 创建系统级悬浮窗
> 
> 系统级悬浮窗可以全屏覆盖包括导航栏和状态栏的位置，不过这种悬浮窗容易被第三方应用检测到，部分游戏检测到此类悬浮窗后会自动闪退。

- 参数 : xmlOrPath {xml|path} xml或路径
- 返回 : {SysFloaty} 悬浮窗
- 版本 : 1.4.4


```javascript
//你可以直接引入一个布局文件创建一个系统级悬浮窗
let sysFloaty = $floaty.newSys("./res/layout/floaty_sys.xml");
//你也可以直接把xml写成字符串传入
let sysFloaty = $floaty.newSys(`<ui>...</ui>`);
```


#### newSys(xmlOrPath, touchable)

> 创建系统级悬浮窗
> 
> 系统级悬浮窗可以全屏覆盖包括导航栏和状态栏的位置，不过这种悬浮窗容易被第三方应用检测到，部分游戏检测到此类悬浮窗后会自动闪退。

- 参数 : xmlOrPath {xml|path} xml或路径
- 参数 : touchable {boolean} 是否可触摸(默认:true)
- 返回 : {SysFloaty} 悬浮窗
- 版本 : 1.8.3


```javascript
//你可以直接引入一个布局文件创建一个系统级悬浮窗
let sysFloaty = $floaty.newSys("./res/layout/floaty_sys.xml",false);
//你也可以直接把xml写成字符串传入
let sysFloaty = $floaty.newSys(`<ui>...</ui>`,false);
```


#### newSelect(callback)

> 创建选择范围悬浮窗
> 
> 该悬浮窗将显示一个范围选择器，你可以调节选框的大小和位置，当悬浮窗关闭的时候，将会回调出选框的位置和范围数据。

- 参数 : callback {SimpleFloatArrCallback} 关闭时回调范围数据
- 返回 : {SelectFloaty} 选择范围悬浮窗
- 版本 : 1.8.3


```javascript
$floaty.newSelect((rect)=>{
    log("用户选择范围:",rect);
});
```


![](./img/floaty_newSelect.png)

#### closeAll()

> 关闭所有悬浮窗

- 版本 : 1.0.0


```javascript
$floaty.closeAll();
```

---

## SysFloaty - 系统级悬浮窗

- 更新时间:2026-01-30 19:32:53

> 系统级悬浮窗
> 
> 通过$floaty.newSys(xml|path)创建，悬浮窗会盖住导航栏和状态栏，是一个比较霸道的悬浮窗。




#### const {WindowManager.LayoutParams} params;

> 悬浮窗参数
> 
> 类型：{android.view.WindowManager.LayoutParams}

- 版本 : 1.3.5


#### const {WindowManager} manager;

> 悬浮窗管理器
> 
> 类型：{android.view.WindowManager}

- 版本 : 1.3.5


#### onScreenChange(callback)

> 设置屏幕旋转监听

- 参数 : callback {(screenInfo)=>{}} 屏幕旋转时回调
- 版本 : 1.4.3


```javascript
let floaty = $floaty.newSys("./floaty/main.xml");
floaty.onScreenChange((screenInfo)=>{
    //屏幕旋转时回调
    floaty.fill(true);//设置成全屏
});
```


#### id(id)

> 获取控件

- 参数 : id {string} 控件id
- 返回 : {XView} 组件
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
        <button id="mButton" text="关闭"/>
    </linear>
</ui>
`);
//获取按钮控件
let mButton = floaty.id("mButton");
//绑定点击事件
mButton.click(()=>{
    //关闭悬浮窗
    floaty.close();
});
```


#### fill(fill)

> 是否全屏显示
> 
> 此函数会将悬浮窗的尺寸设置成全屏大小，之后刷新悬浮窗界面
> 
> 当fill(true)的时候悬浮窗将位置设置为(0,0)并且设置宽高为最大后全屏显示；
> 
> 当fill(false)的时候悬浮窗将位置设置为上次位置，并且宽高设置为自适应，之后显示。

- 参数 : fill {boolean} 是否全屏
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//全屏显示
floaty.fill(true);
```


#### touch(touchable)

> 设置是否可触摸
> 
> 此函数会配置悬浮窗的参数是否可以触摸，之后刷新悬浮窗界面

- 参数 : touchable {boolean} 是否可触摸
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置不可触摸
floaty.touch(false);
```


#### setX(x)

> 设置X坐标
> 
> 此函数会设置悬浮窗x坐标参数，之后刷新悬浮窗界面

- 参数 : x {int} X坐标
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置X坐标
floaty.setX(100);
```


#### setY(y)

> 设置Y坐标
> 
> 此函数会设置悬浮窗y坐标参数，之后刷新悬浮窗界面

- 参数 : y {int} Y坐标
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置Y坐标
floaty.setY(100);
```


#### setXY(x, y)

> 设置XY坐标
> 
> 此函数会设置悬浮窗xy坐标参数，之后刷新悬浮窗界面

- 参数 : x {int} X坐标
- 参数 : y {int} Y坐标
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置XY坐标
floaty.setXY(100, 100);
```


#### setW(w)

> 设置宽度
> 
> 此函数会设置悬浮窗宽度参数，之后刷新悬浮窗界面

- 参数 : w {int} 宽度
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置宽度
floaty.setW(100);
```


#### setH(h)

> 设置高度
> 
> 此函数会设置悬浮窗高度参数，之后刷新悬浮窗界面

- 参数 : h {int} 高度
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置高度
floaty.setH(100);
```


#### setWH(w, h)

> 设置宽高
> 
> 此函数会设置悬浮窗宽高参数，之后刷新悬浮窗界面

- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置宽高
floaty.setWH(100, 100);
```


#### check()

> 断言
> 
> 判断悬浮窗是否处于可此操作状态，不可操作的状态情况如下：
> 
> 1.view为空或被移除
> 
> 2.悬浮窗被关闭

- 返回 : {boolean} 是否可操作
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//断言
if(floaty.check()){
    //可以操作
}else{
    //悬浮窗已经关闭啦，不能操作了
}
```


#### close()

> 关闭悬浮窗

- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//关闭悬浮窗
floaty.close();
```

---

## AppFloaty - 应用级悬浮窗

- 更新时间:2026-01-30 19:32:53

> 应用级悬浮窗
> 
> 通过$floaty.newApp(xml|path)创建，该悬浮窗不会覆盖标题栏和导航栏，是一个比较友好的悬浮窗。




#### const {WindowManager.LayoutParams} params;

> 悬浮窗参数
> 
> 类型：{android.view.WindowManager.LayoutParams}

- 版本 : 1.3.5


#### const {WindowManager} manager;

> 悬浮窗管理器
> 
> 类型：{android.view.WindowManager}

- 版本 : 1.3.5


#### onScreenChange(callback)

> 设置屏幕旋转监听

- 参数 : callback {(screenInfo)=>{}} 屏幕旋转时回调
- 版本 : 1.4.3


```javascript
let floaty = $floaty.newApp("./floaty/main.xml");
floaty.onScreenChange((screenInfo)=>{
    //屏幕旋转时回调
    floaty.fill(true);//设置成全屏
});
```


#### id(id)

> 获取控件

- 参数 : id {string} 控件id
- 返回 : {XView} 组件
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
        <button id="mButton" text="关闭"/>
    </linear>
</ui>
`);
//获取按钮控件
let mButton = floaty.id("mButton");
//绑定点击事件
mButton.click(()=>{
    //关闭悬浮窗
    floaty.close();
});
```


#### fill(fill)

> 是否全屏显示
> 
> 此函数会将悬浮窗的尺寸设置成全屏大小，之后刷新悬浮窗界面
> 
> 当fill(true)的时候悬浮窗将位置设置为(0,0)并且设置宽高为最大后全屏显示；
> 
> 当fill(false)的时候悬浮窗将位置设置为上次位置，并且宽高设置为自适应，之后显示。

- 参数 : fill {boolean} 是否全屏
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//全屏显示
floaty.fill(true);
```


#### touch(touchable)

> 设置是否可触摸
> 
> 此函数会配置悬浮窗的参数是否可以触摸，之后刷新悬浮窗界面

- 参数 : touchable {boolean} 是否可触摸
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置不可触摸
floaty.touch(false);
```


#### setX(x)

> 设置X坐标
> 
> 此函数会设置悬浮窗x坐标参数，之后刷新悬浮窗界面

- 参数 : x {int} X坐标
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置X坐标
floaty.setX(100);
```


#### setY(y)

> 设置Y坐标
> 
> 此函数会设置悬浮窗y坐标参数，之后刷新悬浮窗界面

- 参数 : y {int} Y坐标
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置Y坐标
floaty.setY(100);
```


#### setXY(x, y)

> 设置XY坐标
> 
> 此函数会设置悬浮窗xy坐标参数，之后刷新悬浮窗界面

- 参数 : x {int} X坐标
- 参数 : y {int} Y坐标
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置XY坐标
floaty.setXY(100, 100);
```


#### setW(w)

> 设置宽度
> 
> 此函数会设置悬浮窗宽度参数，之后刷新悬浮窗界面

- 参数 : w {int} 宽度
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置宽度
floaty.setW(100);
```


#### setH(h)

> 设置高度
> 
> 此函数会设置悬浮窗高度参数，之后刷新悬浮窗界面

- 参数 : h {int} 高度
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置高度
floaty.setH(100);
```


#### setWH(w, h)

> 设置宽高
> 
> 此函数会设置悬浮窗宽高参数，之后刷新悬浮窗界面

- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 返回 : {SysFloaty} 自己
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//设置宽高
floaty.setWH(100, 100);
```


#### check()

> 断言
> 
> 判断悬浮窗是否处于可此操作状态，不可操作的状态情况如下：
> 
> 1.view为空或被移除
> 
> 2.悬浮窗被关闭

- 返回 : {boolean} 是否可操作
- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//断言
if(floaty.check()){
    //可以操作
}else{
    //悬浮窗已经关闭啦，不能操作了
}
```


#### close()

> 关闭悬浮窗

- 版本 : 1.3.5


```javascript
//创建悬浮窗对象
let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max">
        <!--省略组件-->
    </linear>
</ui>
`);
//关闭悬浮窗
floaty.close();
```

---

## AdjFloaty - 可调节悬浮窗

- 更新时间:2026-01-30 19:32:53

> 可调节悬浮窗
> 
> 通过$floaty.newAdj(xml|path)创建，天生就是一个可以调节的悬浮窗，支持移动到自己想要移动的位置，调节悬浮窗的大小，关闭悬浮窗等操作。




#### const {WindowManager.LayoutParams} params;

> 悬浮窗参数
> 
> 类型：{android.view.WindowManager.LayoutParams}

- 版本 : 1.5.4


#### const {WindowManager} manager;

> 悬浮窗管理器
> 
> 类型：{android.view.WindowManager}

- 版本 : 1.5.4


#### id(id)

> 选择控件

- 参数 : id {string} 控件id
- 返回 : {XView} 控件


```javascript
let adj = $floaty.newAdj("main.xml");
//找控件
let but = adj.id("button_close");
```


#### close()

> 关闭悬浮窗


```javascript
let adj = $floaty.newAdj("main.xml");
//找控件
let but = adj.id("button_close");
//点击按钮后关闭悬浮窗
but.click(()=>{
    adj.close();
});
```


#### getW()

> 获得宽度

- 返回 : {int} 宽度


```javascript
let adj = $floaty.newAdj("main.xml");
//获得宽度
let w = adj.getW();
```


#### getX()

> 获得x坐标

- 返回 : {int} x坐标


```javascript
let adj = $floaty.newAdj("main.xml");
//获得x坐标
let x = adj.getX();
```


#### getY()

> 获得y坐标

- 返回 : {int} y坐标


```javascript
let adj = $floaty.newAdj("main.xml");
//获得y坐标
let y = adj.getY();
```


#### getH()

> 获得高度

- 返回 : {int} 高度


```javascript
let adj = $floaty.newAdj("main.xml");
//获得高度
let h = adj.getH();
```

---

## SelectFloaty - 选择悬浮窗

- 更新时间:2026-01-30 19:32:53

> 选择悬浮窗
> 
> 通过$floaty.newSelect((rect)=>{})创建，创建后立马会显示一个区域选择方框，当用户关闭的时候会回调选择的范围。




#### const {WindowManager.LayoutParams} params;

> 悬浮窗参数
> 
> 类型：{android.view.WindowManager.LayoutParams}

- 版本 : 1.8.3


#### const {WindowManager} manager;

> 悬浮窗管理器
> 
> 类型：{android.view.WindowManager}

- 版本 : 1.8.3


#### close()

> 关闭悬浮窗

- 版本 : 1.8.3

---

## $draw - 全屏绘制

- 更新时间:2026-01-30 19:32:53

> 全屏绘制




#### 系统限制

在全局绘制框架中，绝大多数情况都会使用到全屏悬浮窗，但是这种方式在部分手机上用户手势会被拦截，这一类现象被称为"卡悬浮"。

```javascript
//这种悬浮窗是小型的，因此不会阻碍到用户手势(无论在任何系统中都适用)
$draw.i("信息");
$draw.d("调试");
$draw.w("警告");
```

经过测试，在MIUI系列的手机中，手机厂家会拦截悬浮窗手势，无论用何种悬浮窗类型，都无效，这是厂家在系统中刻下的基因。

```javascript
//这种悬浮窗是全屏的，对于MIUI的手机(小米红米之类的)会导致拦截用户手势而无法操作界面
$draw.i("信息",100,100);
$draw.d("调试",100,100);
$draw.w("警告",100,100);
$draw.rect(100,100,200,200); //绘制方框
$draw.line(100,100,200,200); //绘制线条
```

全屏绘制类的函数：例如：绘制线、文本、方框等，在ColorOS下(或者大多数国产安卓模拟器)，系统会提示是否允许显示在上层(安卓模拟器大多数默认允许)，经过用户允许之后就可以正常绘制并且不阻碍用户使用手机，
但是在MIUI系统中，没有任何提示，经调试发现该类系统会直接拦截所有用户手势，据了解是为了安全才如此设计。

作为开发者，你必须谨慎使用全局绘制，并不是所有手机都开放了全屏悬浮窗时的触摸事件。

:::tip
在1.8.0版本后，支持在root或者shizuku授权下，会自动尝试解锁卡悬浮，允许悬浮窗的触摸事件到达底层。
:::


#### getPermit()

> 获取悬浮窗权限

- 返回 : {boolean} 是否有权限
- 版本 : 1.0.0


```javascript
$draw.getPermit();
```


#### rect(rect)

> 绘制一个方框

- 参数 : rect {Rect} opencv的Rect对象
- 版本 : 1.0.0


```javascript
//绘制矩形
let rect = new org.opencv.core.Rect(0,0,100,100);
$draw.rect(rect);
```


#### rect(node)

> 绘制一个方框

- 参数 : node {Node} 节点信息
- 版本 : 1.0.0


```javascript
//找到一个节点
let node = $act.selector().textHas("停止").findFirst();
//绘制矩形
$draw.rect(node);
```


#### rect(x, y, w, h)

> 绘制一个方框

- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 版本 : 1.0.0


```javascript
//绘制矩形
$draw.rect(200,200,200,100);
```


#### rect(x, y, w, h, color)

> 绘制一个方框

- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 参数 : color {string} 颜色
- 版本 : 1.1.1


```javascript
//绘制矩形
$draw.rect(200,200,200,100,"#FF0000");
```


#### rect(x, y, w, h, ext)

> 绘制方框

- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 参数 : ext {int} 向四周拓展
- 版本 : 1.0.0


```javascript
//绘制一个向外拓展50像素的矩阵
$draw.rect(200,200,200,100,50);
```


#### rect(x, y, w, h, ext, color)

> 绘制方框

- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 参数 : ext {int} 向四周拓展
- 参数 : color {string} 颜色
- 版本 : 1.1.0


```javascript
//绘制一个向外拓展50像素的矩阵
$draw.rect(200,200,200,100,50,"#FF0000");
```


#### rect(x, y, w, h, ext, color)

> 绘制方框

- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 参数 : ext {int} 向四周拓展
- 参数 : color {int} 颜色
- 版本 : 1.1.1


```javascript
//绘制一个向外拓展50像素的矩阵
$draw.rect(200,200,200,100,50,$color.RED);
```


#### rect(arr, ext, color)

> 绘制方框

- 参数 : arr {int[]} 范围数组
- 参数 : ext {int} 向四周拓展
- 参数 : color {int} 颜色
- 版本 : 1.8.2


```javascript
//绘制一个向外拓展50像素的矩阵
$draw.rect([200,200,200,100],50,$color.RED);
```


#### rect(arr, ext, color)

> 绘制方框

- 参数 : arr {int[]} 范围数组
- 参数 : ext {int} 向四周拓展
- 参数 : color {string} 颜色
- 版本 : 1.8.2


```javascript
//绘制一个向外拓展50像素的矩阵
$draw.rect([200,200,200,100],50,"#FF0000");
```


#### cross(point)

> 绘制一个十字准心

- 参数 : point {point} 位置
- 版本 : 1.0.0


```javascript
let point = new org.opencv.core.Point(100,100);
//绘制准心
$draw.cross(point);
```


#### cross(index)

> 绘制一个十字准心

- 参数 : index {int[]} 位置
- 版本 : 1.0.0


```javascript
//绘制准心
$draw.cross([400,500]);
```


#### cross(node)

> 绘制一个十字准心

- 参数 : node {AccessibilityNodeInfo} 节点信息
- 版本 : 1.0.0


```javascript
//绘制准心
$draw.cross(node);
```


#### cross(node)

> 绘制一个十字准心

- 参数 : node {Node} 节点信息
- 版本 : 1.0.0


```javascript
//绘制准心
$draw.cross(node);
```


#### cross(x, y)

> 绘制一个十字准心

- 参数 : x {int} 中心x
- 参数 : y {int} 中心y
- 版本 : 1.0.0


```javascript
//绘制准心
$draw.cross(400,500);
```


#### cross(x, y, color)

> 绘制一个十字准心

- 参数 : x {int} 中心x
- 参数 : y {int} 中心y
- 参数 : color {string} 颜色
- 版本 : 1.1.0


```javascript
//绘制准心
$draw.cross(400,500,"#FF0000");
```


#### cross(x, y, color)

> 绘制一个十字准心

- 参数 : x {int} 中心x
- 参数 : y {int} 中心y
- 参数 : color {int} 颜色值
- 版本 : 1.1.1


```javascript
//绘制准心
$draw.cross(400,500,$color.RED);
```


#### dot(index)

> 绘制一个点

- 参数 : index {int[]} 点
- 版本 : 1.0.0


```javascript
$draw.dot([400,500]);
```


#### dot(point)

> 绘制一个点

- 参数 : point {point} 点
- 版本 : 1.0.0


```javascript
$draw.dot(point);
```


#### dot(x, y)

> 绘制一个点

- 参数 : x {int} 点x
- 参数 : y {int} 点y
- 版本 : 1.0.0


```javascript
//绘制一个点
$draw.dot(400,500);
```


#### dot(x, y, color)

> 绘制一个点

- 参数 : x {int} 点x
- 参数 : y {int} 点y
- 参数 : color {string} 颜色
- 版本 : 1.0.0


```javascript
//绘制一个点
$draw.dot(400,500);
```


#### dot(x, y, color)

> 绘制一个点

- 参数 : x {int} 点x
- 参数 : y {int} 点y
- 参数 : color {int} 颜色值
- 版本 : 1.1.1


```javascript
//绘制一个点
$draw.dot(400,500,$color.RED);
```


#### text(text, x, y)

> 绘制文字

- 参数 : text {String} 文字
- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 版本 : 1.0.0


```javascript
//绘制文字(默认字体大小:15dp)
$draw.text("Hello aigame !",400,300);
```


#### text(text, x, y, size)

> 绘制文字

- 参数 : text {String} 文字
- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : size {float} 字体大小
- 版本 : 1.0.0


```javascript
//绘制文字(大小为16dp)
$draw.text("Hello aigame !",400,400,16);
```


#### text(text, x, y, size, color)

> 绘制文字

- 参数 : text {String} 文字
- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : size {int} 字体大小
- 参数 : color {string} 颜色
- 版本 : 1.1.1


```javascript
//绘制文字(大小为16dp)
$draw.text("Hello aigame !",400,400,16,"#FF0000");
```


#### text(text, x, y, size, color)

> 绘制文字

- 参数 : text {String} 文字
- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : size {int} 字体大小
- 参数 : color {int} 颜色值
- 版本 : 1.1.1


```javascript
//绘制文字(大小为16dp)
$draw.text("Hello aigame !",400,400,16,$color.RED);
```


#### circle(x, y)

> 绘制一个圆形
> 
> 半径默认为50像素

- 参数 : x {int} 圆心x
- 参数 : y {int} 圆心y
- 版本 : 1.1.1


```javascript
//绘制半径为50像素的圆形
$draw.circle(350,400);
```


#### circle(x, y, r)

> 绘制一个圆形

- 参数 : x {int} 圆心x
- 参数 : y {int} 圆心y
- 参数 : r {int} 圆形半径
- 版本 : 1.0.0


```javascript
//绘制半径为100像素的圆形
$draw.circle(350,400,100);
```


#### circle(x, y, r, ext)

> 绘制一个圆形

- 参数 : x {int} 圆心x
- 参数 : y {int} 圆心y
- 参数 : r {int} 圆形半径
- 参数 : ext {int} 圆形向四周拓展
- 版本 : 1.0.0


```javascript
//向外拓展50像素
$draw.circle(350,400,100,50);
```


#### circle(x, y, r, ext, color)

> 绘制一个圆形

- 参数 : x {int} 圆心x
- 参数 : y {int} 圆心y
- 参数 : r {int} 圆形半径
- 参数 : ext {int} 圆形向四周拓展
- 参数 : color {string} 颜色
- 版本 : 1.0.0


```javascript
//向外拓展50像素
$draw.circle(350,400,100,50,"#FF0000");
```


#### circle(x, y, r, ext, color)

> 绘制一个圆形

- 参数 : x {int} 圆心x
- 参数 : y {int} 圆心y
- 参数 : r {int} 圆形半径
- 参数 : ext {int} 圆形向四周拓展
- 参数 : color {int} 颜色值
- 版本 : 1.1.1


```javascript
//向外拓展50像素
$draw.circle(350,400,100,50,$color.RED);
```


#### img(img, x, y, w, h)

> 绘制图片

- 参数 : img {Image} 图片对象
- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : w {int} 宽度(绘制后的图片宽度)
- 参数 : h {int} 高度(绘制后的图片宽度)
- 版本 : 1.1.0


```javascript
let img = $img.read("/cat.png");
//绘制图片
$draw.img(img,200,200,100,150);
```


#### line(x, y, toX, toY)

> 绘制一条线

- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : toX {int} 目标x
- 参数 : toY {int} 目标y
- 版本 : 1.0.0


```javascript
//绘制一条线
$draw.line(300,0,100,1000);
```


#### line(x, y, toX, toY, color)

> 绘制一条线

- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : toX {int} 目标x
- 参数 : toY {int} 目标y
- 参数 : color {string} 颜色
- 版本 : 1.1.1


```javascript
//绘制一条线
$draw.line(300,0,100,1000,"#FF0000");
```


#### line(x, y, toX, toY, color)

> 绘制一条线

- 参数 : x {int} 起点x
- 参数 : y {int} 起点y
- 参数 : toX {int} 目标x
- 参数 : toY {int} 目标y
- 参数 : color {int} 颜色值
- 版本 : 1.1.1


```javascript
//绘制一条线
$draw.line(300,0,100,1000,$color.RED);
```


#### path(data)

> 绘制路径，传入的就是x和y的数组

- 参数 : data {int[][]} 二维数组，第二维数组是坐标
- 版本 : 1.0.0


```javascript
//国际通用手势
$draw.path([
    [100, 800],
    [120, 750],
    [150, 720],
    [180, 750],
    [200, 800],
    [200, 800],
    [220, 700],
    [250, 680],
    [280, 700],
    [300, 800],
    [300, 800],
    [320, 250],
    [350, 200],
    [380, 250],
    [400, 800],
    [400, 800],
    [420, 740],
    [450, 730],
    [480, 740],
    [500, 800],
    [500, 800],
    [520, 770],
    [550, 760],
    [580, 770],
    [600, 800]
]);
```


#### path(data, color)

> 绘制路径，传入的就是x和y的数组

- 参数 : data {int[][]} 二维数组，第二维数组是坐标
- 参数 : color {string} 颜色
- 版本 : 1.1.1


```javascript
//国际通用手势
$draw.path([
    [100, 800],
    [120, 750],
    [150, 720],
    [180, 750],
    [200, 800],
    [200, 800],
    [220, 700],
    [250, 680],
    [280, 700],
    [300, 800],
    [300, 800],
    [320, 250],
    [350, 200],
    [380, 250],
    [400, 800],
    [400, 800],
    [420, 740],
    [450, 730],
    [480, 740],
    [500, 800],
    [500, 800],
    [520, 770],
    [550, 760],
    [580, 770],
    [600, 800]
],"#FF0000");
```


#### path(data, color)

> 绘制路径，传入的就是x和y的数组

- 参数 : data {int[][]} 二维数组，第二维数组是坐标
- 参数 : color {int} 颜色值
- 版本 : 1.1.1


```javascript
//国际通用手势
$draw.path([
    [100, 800],
    [120, 750],
    [150, 720],
    [180, 750],
    [200, 800],
    [200, 800],
    [220, 700],
    [250, 680],
    [280, 700],
    [300, 800],
    [300, 800],
    [320, 250],
    [350, 200],
    [380, 250],
    [400, 800],
    [400, 800],
    [420, 740],
    [450, 730],
    [480, 740],
    [500, 800],
    [500, 800],
    [520, 770],
    [550, 760],
    [580, 770],
    [600, 800]
],$color.RED);
```


#### i(text, x, y, size)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
//字体大小单位:dp
$draw.i("信息",400,300,20);
```


#### i(text, x, y)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.i("信息",400,300);
```


#### i(text)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.i("信息");
```


#### d(text, x, y, size)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
//字体大小单位:dp
$draw.i("调试",400,300,20);
```


#### d(text, x, y)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.d("调试",400,300);
```


#### d(text)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.d("调试");
```


#### w(text, x, y, size)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
//字体大小单位:dp
$draw.w("警告",400,300,20);
```


#### w(text, x, y)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.w("警告",400,300);
```


#### w(text)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.w("警告");
```


#### e(text, x, y, size)

> 绘制日志文字

- 参数 : text {String} 文字
- 参数 : x {float} 字体大小
- 版本 : 1.0.0


```javascript
//字体大小单位:dp
$draw.e("错误",400,300,20);
```


#### e(text, x, y)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.e("错误",400,300);
```


#### e(text)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.e("错误");
```


#### v(text, x, y, size)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
//字体大小单位:dp
$draw.v("信息",400,300,20);
```


#### v(text, x, y)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.v("信息",400,300);
```


#### v(text)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.v("信息");
```


#### log(text, color, x, y, size)

> 绘制日志文字

- 参数 : text {String} 文字
- 参数 : color {String} 颜色
- 参数 : x {int} 位置x
- 参数 : y {int} 位置y
- 参数 : size {float} 字体大小
- 版本 : 1.0.0


```javascript
//字体大小单位:dp
$draw.log("信息","#57965C",400,300,20);
```


#### log(text, color, x, y)

> 绘制日志文字

- 参数 : text {String} 文字
- 参数 : color {String} 颜色
- 参数 : x {int} 位置x
- 参数 : y {int} 位置y
- 版本 : 1.0.0


```javascript
//字体大小单位:dp 默认日志文字大小:12dp
$draw.log("信息","#57965C",400,300);
```


#### log(text, color)

> 绘制日志文字

- 参数 : text {String} 文字
- 参数 : color {String} 颜色
- 版本 : 1.0.0


```javascript
$draw.log("信息","#57965C");
```


#### log(text)

> 绘制日志文字

- 参数 : text {String} 文字
- 版本 : 1.0.0


```javascript
$draw.log("信息");
```


#### log(text, x, y)

> 绘制日志文字

- 参数 : text {String} 文字
- 参数 : x {int} 位置x
- 参数 : y {int} 位置y
- 版本 : 1.0.0


```javascript
//字体大小单位:dp 默认日志文字大小:12dp
$draw.log("信息",400,300);
```


#### closeAll()

> 关闭绘制日志的悬浮窗

- 版本 : 1.0.0


```javascript
//关闭所有绘制图案
$draw.closeAll();
```


#### closeAll(delay)

> 关闭绘制日志的悬浮窗

- 参数 : delay {long} 延迟关闭时间
- 版本 : 1.0.0


```javascript
$draw.closeAll(1000);
```


#### closeLog(delay)

> 关闭绘制日志的悬浮窗

- 参数 : delay {long} 延迟关闭时间
- 版本 : 1.0.0


```javascript
$draw.closeLog(1000);
```


#### closeLog()

> 关闭绘制日志的悬浮窗

- 版本 : 1.0.0


```javascript
$draw.closeLog();
```


#### clear()

> 清空所有绘制
> 
> 清空绘制本质上也是绘制的一种，因此它和其他绘制函数一样，会优先判断当前悬浮窗是否开启，
> 如果悬浮窗没有开启，则创建一个全局悬浮窗至于屏幕最上层，之后绘制透明颜色以达到清空的效果。
> 
> 如果你已经绘制过图案了，那么此时是存在顶层悬浮窗的，调用次函数的时候会直接绘制透明颜色以达到清空的效果。
> 
> 如果你不理解什么是绘制透明颜色，可以理解为：画布中的橡皮擦（本质上是把橡皮经过的位置绘制成透明颜色）

- 版本 : 1.6.8


```javascript
//清空全局绘制
$draw.clear();
```

---

## $arc - 悬浮球

- 更新时间:2026-01-30 19:32:51

> 悬浮球
> 
> 轻松的实现悬浮球菜单效果，并且可以定制每个按钮的样式。




![](./img/407372540692722.gif)

#### item(iconName)

> 创建悬浮按钮
> 
> 我们必须要先了解两个概念：容器(MenuBody)和悬浮按钮(MenuItem)；
> 
> 容器可以装多个悬浮按钮，并且可以显示出来。
> 
> 而悬浮按钮中每个按钮都有不一样的样式，所以悬浮按钮用来控制自身的样式。

- 参数 : iconName {string} 图标资源名或本地相对路径 
- 返回 : {MenuItem} 悬浮按钮
- 版本 : 1.0.0


```javascript
//创建悬浮小按钮,可以被容器添加进去
let menu1 = $arc.item("logo_ag");//内置图标资源名称或者本地自定义图片相对路径
//之后可以创建容器并且显示，例如：
$arc.body("悬浮球1号").add(menu1).show();
//如果有多个悬浮小按钮：
let menu01 = $arc.item("logo_ag");
let menu02 = $arc.item("ic_color");
$arc.body("悬浮球2号").add(menu01).add(menu02).show();
```


#### body(name)

> 创建容器
> 
> 容器主要用来控制显示和关闭的，它可以装入多个悬浮按钮，之后显示出来。
> 
> 需要注意：如果悬浮球菜单已经存在了，那么将无法显示第二个名称相同的悬浮球。

- 参数 : name {string} 名称 
- 返回 : {MenuBody} 容器
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器,用于存放多个小按钮，并且显示
let mBody01 = $arc.body("悬浮球1号");//指定一个名称，方便后面根据名称关闭
//添加一个按钮并且显示，例如：
mBody01.add($arc.item("logo_ag"));
```


#### has(name)

> 判断悬浮球是否存在

- 参数 : name {string} 名称 
- 返回 : {boolean} 是否存在
- 版本 : 1.0.0


```javascript
if($arc.has("悬浮球1号")){
    toast("悬浮球1号存在");
}
```


#### close(name)

> 关闭
> 
> 根据容器的名称来关闭容器

- 参数 : name {string} 名称 
- 版本 : 1.0.0


```javascript
$arc.close("悬浮球1号");
```


#### closeAll()

> 关闭全部
> 
> 将所有创建的悬浮球都关闭掉

- 版本 : 1.0.0


```javascript
//关闭全部悬浮球(容器)
$arc.closeAll();
```

---

## MenuBody - 按钮容器

- 更新时间:2026-01-30 19:32:58

> 按钮容器
> 
> 用于装载多个悬浮按钮的容器，并控制显示与关闭。




#### add(menu)

> 添加悬浮按钮
> 
> 可以向按钮容器中添加多个悬浮小按钮

- 参数 : menu {MenuItem} 悬浮按钮
- 返回 : {MenuBody} 自己
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器(MenuBody是用来装小按钮MenuItem的)
let menuBody = $arc.body("我的悬浮球1号"); //指定容器名称
//创建小按钮(MenuItem主要控制小按钮的样式)
let menuItem = $arc.item("logo_ag");
//添加按钮(用容器添加小按钮)
menuBody.add(menuItem);
//之后就可以显示出来了(容器主要是控制显示和关闭的)
menuBody.show();
```


#### show()

> 显示悬浮按钮
> 
> 会优先判断是否存在悬浮球名称了，如果存在则不显示，如果不存在则记录悬浮球名称并且显示。

- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器(用来装小按钮(MenuItem))
let menuBody = $arc.body("我的悬浮球1号");
//创建小按钮(自定义按钮的各种样式)
let menu1 = $arc.item("logo_ag").bg("#55FFFFFF"); //指定按钮图标
let menu2 = $arc.item("ic_close").style("outline").iconTint("#FF0000"); //可以这样指定样式[方法1]
let menu3 = $arc.item("ic_code_run");
let menu4 = $arc.item("ic_cloud");
let menu5 = $arc.item("ic_color");
//连续添加小按钮并且显示
menuBody.add(menu1) //添加小按钮1
        .add(menu2) //添加小按钮2
        .add(menu3) //添加小按钮3
        .add(menu4) //添加小按钮4
        .add(menu5) //添加小按钮5
        .show(); //这里直接调用显示
```


#### name(name)

> 设置悬浮球名称
> 
> 每个悬浮球被显示之前都会判断当前悬浮球的名称是否已经存在了，如果存在了，就不显示。

- 参数 : name {string} 悬浮窗名称
- 返回 : {MenuBody} 自己
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器(用来装小按钮(MenuItem))
let menuBody = $arc.body("我的悬浮球1号") //创建悬浮球按钮容器
.name("悬浮球1号"); //为容器设置一个名称
```


#### margin(left, right)

> 设置贴边边距

- 参数 : left {int} 左边距，默认为 0
- 参数 : right {int} 右边距，默认为 0
- 返回 : {MenuBody} 自己
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器(用来装小按钮(MenuItem))
let menuBody = $arc.body("我的悬浮球1号") //创建悬浮球按钮容器
.margin(50,50); //设置左右两边的贴边边距
```


#### radius(radius)

> 设置圆弧半径
> 
> 圆弧半径决定了容器中每个小按钮展开时的距离

- 参数 : radius {int} 半径
- 返回 : {MenuBody} 自己
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器(用来装小按钮(MenuItem))
let menuBody = $arc.body("我的悬浮球1号") //创建悬浮球按钮容器
.radius(25); //设置圆弧半径
```


#### global(isGlobalShow)

> 设置是否全局显示
> 
> 默认就是全局显示的（需要悬浮窗权限），任何应用都能够看到这个悬浮球，如果不是全局显示的，那么就只能在当前应用中显示。

- 参数 : isGlobalShow {boolean} 是否全局显示(默认:true)
- 返回 : {MenuBody} 自己
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器(用来装小按钮(MenuItem))
let menuBody = $arc.body("我的悬浮球1号") //创建悬浮球按钮容器
.global(true); //设置为全局显示(需要悬浮窗权限)
```


#### dur(expandAnimDur)

> 设置展开动画时间
> 
> 默认是 250 毫秒

- 参数 : expandAnimDur {int} 展开动画时长
- 返回 : {MenuBody} 自己
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器(用来装小按钮(MenuItem))
let menuBody = $arc.body("我的悬浮球1号") //创建悬浮球按钮容器
.dur(500); //设置展开动画时间
```


#### x(x)

> 设置初始位置
> 
> 初始位置决定了悬浮球最开始显示时的位置

- 参数 : x {int} x坐标
- 返回 : {MenuBody} 自己
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器(用来装小按钮(MenuItem))
let menuBody = $arc.body("我的悬浮球1号") //创建悬浮球按钮容器
.x(300); //设置初始位置
```


#### y(y)

> 设置初始位置
> 
> 初始位置决定了悬浮球最开始显示时的位置

- 参数 : y {int} y坐标
- 返回 : {MenuBody} 自己
- 版本 : 1.0.0


```javascript
//创建悬浮按钮容器(用来装小按钮(MenuItem))
let menuBody = $arc.body("我的悬浮球1号") //创建悬浮球按钮容器
.y(500); //设置初始位置
```

---

## MenuItem - 悬浮按钮

- 更新时间:2026-01-30 19:32:58

> 悬浮按钮
> 
> 一个悬浮球中只能有一个容器，而一个容器可以添加多个悬浮小按钮，容器用来控制按钮的展开与关闭动画，而按钮主要是用于功能交互。




#### style(style)

> 设置样式
> 
> 注意：此方法必须要优先调用!因为会重置其他设置的所有属性

- 参数 : style {String} 按钮样式(default,outline,tonal)
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.style("outline"); //(优先调用)设置样式
```


#### click(click)

> 设置点击事件
> 
> 当小按钮被点击的时候会执行其中的回调函数

- 参数 : click {()=>{}} 回调函数
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag");//图标资源名称或者图标的相对路径
//设置点击事件
item.click(()=>{
    //点击事件
    info("我被点击了");
});
```


#### ripper(color)

> 设置涟漪颜色
> 
> 小按钮被点击时背景阴影会有水波涟漪的效果

- 参数 : color {string} 颜色
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮(图标资源名称或者图标的相对路径)
.ripper("#FF0000");//设置涟漪颜色
```


#### ripper(color)

> 设置涟漪颜色

- 参数 : color {int} 颜色值
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.ripper($颜色.红色);//设置涟漪颜色
```


#### tip(tip)

> 设置提示
> 
> 按钮被长按的时候就会显示提示文字

- 参数 : tip {string} 提示文字
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.tip("提示文字");//设置长按提示文字
```


#### bg(color)

> 设置背景颜色

- 参数 : color {string} 背景颜色
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.bg("#FF0000");//设置按钮背景颜色
```


#### bg(color)

> 设置背景颜色

- 参数 : color {int} 背景颜色值
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.bg($颜色.红色); //设置背景颜色值
```


#### radius(radius)

> 设置圆角大小

- 参数 : radius {float} 圆角大小
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.radius(15); //设置圆角弧度大小
```


#### icon(resName)

> 设置图标
> 
> 支持内置的icon设置
> 
> 支持路径中的图片(最好是相对于项目路径的)

- 参数 : resName {string} 资源名称或者本地路径
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//创建一个按钮
let item = $arc.item("ic_code_run"); //创建一个按钮
//设置点击事件
item.click(()=>{
    //点击时我们切换图标(设置图标)
    item.icon("ic_stop");//图标资源名称或者图标的相对路径
});
```


#### iconPadding(padding)

> 设置图标内边距

- 参数 : padding {int} 边距
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.iconPadding(10); //设置图标内边距
```


#### iconSize(size)

> 设置图标尺寸

- 参数 : size {int} 尺寸
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.iconSize(30); //设置按钮大小
```


#### cancelIconTint()

> 取消填充颜色
> 
> 此函数等价于：iconTint(null);

- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.cancelIconTint(); //清空图标的颜色
```


#### iconTint(color)

> 设置图标填充颜色
> 
> 当颜色值为null时，会取消填充颜色，即：cancelIconTint();

- 参数 : color {string} 颜色
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.iconTint("#000000"); //设置图标颜色
```


#### iconTint(color)

> 设置图标填充颜色

- 参数 : color {int} 颜色值
- 返回 : {MenuItem} 自己
- 版本 : 1.0.0


```javascript
//先创建小按钮
let item = $arc.item("logo_ag") //创建一个按钮
.iconTint($颜色.红色); //设置图标颜色值
```


#### getW()

> 获取按钮宽度

- 返回 : {int} 宽度


```javascript
//先创建小按钮
let item = $arc.item("logo_ag");  //创建一个按钮
//获取宽度
item.getW();
//一般获取宽度可以用来设置弧度，例如：
item.setRadius(item.getW()/2);
```


#### getH()

> 获取按钮高度

- 返回 : {int} 高度


```javascript
//先创建小按钮
let item = $arc.item("logo_ag");  //创建一个按钮
//获取高度
item.getH();
```