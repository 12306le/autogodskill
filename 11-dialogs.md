# 对话框与提示 API

> 原生对话框、Material Design 3对话框、阻塞式对话框。

## 目录
- [$alert - 原生对话框](#alert---原生对话框)
- [$dialog - M3对话框](#dialog---m3对话框)
- [$tip - 阻塞式对话框](#tip---阻塞式对话框)

---

## $alert - 原生对话框

- 更新时间:2026-01-30 19:32:56

> 矩形对话框
> 
> 目前我们的对话框有三种:$tip($提示)、$dialog($对话框)、$alert($提示框)，这三种有哪些特点？
> 
> - $tip($提示):阻塞式对话框，很适合流程脚本，当对话框关闭后，下面的代码才会接着运行
> - $dialog($对话框):非阻塞式对话框，采用M3的风格，缺点就是由于遵循了M3布局规则导致显示的视图范围有限。
> - $alert($提示框):非阻塞式对话框，采用安卓默认实体风格，弥补$dialog显示视图小的缺点，可以通过maxWH(true)显示较大的视图区域。




#### create()

> 创建一个对话框

- 返回 : {alert} 对话框对象
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
```


#### title(title)

> 设置对话框标题

- 参数 : title {string} 对话框标题
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置对话框标题
alt.title("标题");
```


#### isShowing()

> 检查对话框是否正在显示

- 返回 : {boolean} 对话框是否正在显示
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//是否显示了
log(alt.isShowing());//false
```


#### msg(msg)

> 设置对话框消息

- 参数 : msg {string} 对话框消息
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置内容
alt.msg("内容");
```


#### cancelable(cancelable)

> 设置对话框是否可以取消

- 参数 : cancelable {boolean} 是否可以取消
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置是否可以取消
alt.cancelable(true);
```


#### icon(icon)

> 设置对话框图标

- 参数 : icon {string} 图标资源路径
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置对话框图标
alt.icon("ag_logo");
```


#### view(view)

> 设置对话框视图

- 参数 : view {view} 视图
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//解析一个布局
let ui = $ui.layout("main.xml");
let view = ui.getView();//获取视图
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置对话框视图
alt.view(view);
```


#### view(view)

> 设置对话框视图

- 参数 : view {xview} 视图
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//解析一个布局
let ui = $ui.layout("main.xml");
let xview = ui.id("myView");//获取XView组件视图
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置对话框视图
alt.view(xview);
```


#### maxH(max)

> 设置最高显示

- 参数 : max {boolean} 是否最宽高显示
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置最高显示，对话框的高度会显示到最大
alt.maxH(true);
```


#### maxW(max)

> 设置最宽显示

- 参数 : max {boolean} 是否最宽显示
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置最宽显示，对话框的宽度会显示到最大
alt.maxW(true);
```


#### maxWH(max)

> 设置最大宽高显示

- 参数 : max {xview} 是否最大宽高显示
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置最宽高显示，对话框的宽高会显示到最大
alt.maxWH(true);
```


#### but1(text)

> 设置对话框第一个按钮

- 参数 : text {string} 按钮文本
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置按钮
alt.but1("按钮1");
```


#### but1(text, callback)

> 设置对话框第一个按钮
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : text {string} 按钮文本
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置按钮
alt.but1("按钮1",(di,which)=>{
    //点击事件
});
```


#### but2(text)

> 设置对话框第二个按钮

- 参数 : text {string} 按钮文本
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置按钮
alt.but2("按钮2");
```


#### but2(text, callback)

> 设置对话框第二个按钮
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : text {string} 按钮文本
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置按钮
alt.but2("按钮2",(di,which)=>{
    //点击事件
});
```


#### but3(text)

> 设置对话框第三个按钮

- 参数 : text {string} 按钮文本
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置按钮
alt.but3("按钮3");
```


#### but3(text, callback)

> 设置对话框第三个按钮
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : text {string} 按钮文本
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置按钮
alt.but3("按钮3",(di,which)=>{
    //点击事件
});
```


#### items(items, callback)

> 设置对话框选项
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : items {string[]} 选项数组
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置对话框选项
alt.items(["选项1","选项2","选项3"],(di,which)=>{
    //点击事件
});
```


#### oneItems(items, checkedItem, callback)

> 设置对话框单选选项
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : items {string[]} 选项数组
- 参数 : checkedItem {int} 选中的选项位置
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置对话框选项
alt.oneItems(["选项1","选项2","选项3"],0,(di,which)=>{
    //点击事件
});
```


#### moreItems(items, callback)

> 设置对话框多选选项
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置 isChecked:{boolean} 是否被选中

- 参数 : items {string[]} 选项数组
- 参数 : callback {(di,which,isChecked)=>{}} 回调函数
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置对话框选项
alt.moreItems(["选项1","选项2","选项3"],(di,which,isChecked)=>{
    //点击事件
});
```


#### moreItems(items, checkedItems, callback)

> 设置对话框多选选项
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置 isChecked:{boolean} 是否被选中

- 参数 : items {string[]} 选项数组
- 参数 : checkedItems {boolean[]} 选中的选项数组
- 参数 : callback {(di,which,isChecked)=>{}} 回调函数
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//创建一个对话框(注意对象名称不要和全局函数alert相同)
let alt = $alert.create();
//设置对话框选项
alt.moreItems(["选项1","选项2","选项3"],[false,false,true],(di,which,isChecked)=>{
    //点击事件
});
```


#### show()

> 显示对话框

- 返回 : {AlertDialog} 对话框对象
- 版本 : 1.5.1


```javascript
$alert.create()
.title("标题")
.msg("我是信息")
.but3("确定",()=>{
    log("我被点击了");
})
.show();//显示对话框
```


#### showBefore(callback)

> 对话框显示前回调
> 
> 需要注意的是:该回调是放在UI线程中执行的

- 参数 : callback {()=>{}} 回调函数 
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
$alert.create()
.title("标题")
.msg("我是信息")
.but3("确定",()=>{
    log("我被点击了");
})
.showBefore(()=>{
    log("准备显示对话框啦");
})
.show();//显示对话框
```


#### showAfter(callback)

> 对话框显示后回调
> 
> 需要注意的是:该回调是放在UI线程中执行的

- 参数 : callback {()=>{}} 回调函数 
- 返回 : {alert} 自己
- 版本 : 1.5.1


```javascript
//在自定义view中，如果有界面元素需要刷新，那么就最好在alert显示之后再操作
//例如:
let ui = $ui.layout("ui.xml");//解析一个视图
let mAlert = $alert.create();//创建一个对话框
mAlert.showAfter(()=>{
    //如果自定义视图中存在需要操作的ui元素，可以放到这里操作
    let but = ui.id("mButtonClose");
    mButtonClose.click(()=>{
        mAlert.close();//关闭对话框
    });
}).view(ui.getView()).show();//显示自定义视图
```


#### onClose(callback)

> 监听提示框关闭

- 参数 : callback {()=>{}} 提示框关闭后回调
- 版本 : 1.8.0


```javascript
let alt = $alert.create()
.title("标题")
.msg("我是信息")
.but3("关闭",()=>{
    //这里关闭提示框
    alt.close();
})
.onClose(()=>{
    log("对话框被关闭了");
})
.show();//显示提示框
```


#### close()

> 关闭对话框

- 版本 : 1.5.1


```javascript
let alt = $alert.create()
.title("标题")
.msg("我是信息")
.but3("关闭",()=>{
    //这里关闭对话框
    alt.close();
})
.show();//显示对话框
```

---

## $dialog - M3对话框

- 更新时间:2026-01-30 19:32:57

> M3对话框
> 
> 与$alert($提示框)不同，$dialog($对话框)是一个Material Design 3风格的对话框。




#### create()

> 创建一个对话框

- 返回 : {dialog} 对话框对象


```javascript
// 创建一个对话框
let dlg = $dialog.create()
```


#### title(title)

> 设置对话框标题

- 参数 : title {string} 对话框标题
- 返回 : {dialog} 自己


```javascript
// 创建一个对话框
let dlg = $dialog.create()
// 设置对话框标题
dlg.title("标题")
```


#### isShowing()

> 检查对话框是否正在显示

- 返回 : {boolean} 对话框是否正在显示


```javascript
// 创建一个对话框
let dlg = $dialog.create()
// 设置对话框标题
if(dlg.isShowing()){
    log("对话框正再显示");
}
```


#### msg(msg)

> 设置对话框消息

- 参数 : msg {string} 对话框消息
- 返回 : {dialog} 自己


```javascript
// 创建一个对话框
let dlg = $dialog.create()
// 设置对话框消息
dlg.msg("内容");
```


#### cancelable(cancelable)

> 设置对话框是否可以取消

- 参数 : cancelable {boolean} 是否可以取消
- 返回 : {dialog} 自己


```javascript
// 创建一个对话框
let dlg = $dialog.create()
// 设置对话框是否可以取消
dlg.cancelable(true);
```


#### icon(icon)

> 设置对话框图标

- 参数 : icon {string} 图标资源路径
- 返回 : {dialog} 自己


```javascript
// 创建一个对话框
let dlg = $dialog.create()
// 设置对话框图标
dlg.icon("ag_logo);
```


#### view(view)

> 设置对话框视图

- 参数 : view {view} 视图
- 返回 : {dialog} 自己


```javascript
//解析一个布局
let ui = $ui.layout("main.xml");
let view = ui.getView();//获取视图
//创建一个对话框
let dlg = $dialog.create()
//设置对话框视图
dlg.view(view);
```


#### view(view)

> 设置对话框视图

- 参数 : view {xview} 视图
- 返回 : {dialog} 自己


```javascript
//解析一个布局
let ui = $ui.layout("main.xml");
let view = ui.id("myView");//获取XView对象
//创建一个对话框
let dlg = $dialog.create()
//设置对话框视图
dlg.view(view);
```


#### but1(text)

> 设置对话框第一个按钮

- 参数 : text {string} 按钮文本
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
//设置按钮
dlg.but1("按钮1");
```


#### but1(text, callback)

> 设置对话框第一个按钮
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : text {string} 按钮文本
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
//设置按钮
dlg.but1("按钮1",(di,which)=>{
    log("我被点击了");
});
```


#### but2(text)

> 设置对话框第二个按钮

- 参数 : text {string} 按钮文本
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
//设置按钮
dlg.but2("按钮2");
```


#### but2(text, callback)

> 设置对话框第二个按钮
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : text {string} 按钮文本
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
//设置按钮
dlg.but2("按钮2",(di,which)=>{
    log("我被点击了");
});
```


#### but3(text)

> 设置对话框第三个按钮

- 参数 : text {string} 按钮文本
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
//设置按钮
dlg.but3("按钮3");
```


#### but3(text, callback)

> 设置对话框第三个按钮
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : text {string} 按钮文本
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
//设置按钮
dlg.but3("按钮3",(di,which)=>{
    log("我被点击了");
});
```


#### items(items, callback)

> 设置对话框选项
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : items {string[]} 选项数组
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
.items(["选项1","选项2","选项3"],(di,which)=>{
    log("我被点击了");
})
.show();
```


#### oneItems(items, checkedItem, callback)

> 设置对话框单选选项
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置

- 参数 : items {string[]} 选项数组
- 参数 : checkedItem {int} 选中的选项位置
- 参数 : callback {(di,which)=>{}} 回调函数
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
.oneItems(["选项1","选项2","选项3"],0,(di,which)=>{
    log("我被点击了");
})
.show();
```


#### moreItems(items, callback)

> 设置对话框多选选项
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置 isChecked:{boolean} 是否被选中

- 参数 : items {string[]} 选项数组
- 参数 : callback {(di,which,isChecked)=>{}} 回调函数
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
.moreItems(["选项1","选项2","选项3"],(di,which)=>{
    log("我被点击了");
})
.show();
```


#### moreItems(items, checkedItems, callback)

> 设置对话框多选选项
> 
> 回调参数：di:{DialogInterface} 接收到点击的对话框 which:{int}被点击的按钮位置 isChecked:{boolean} 是否被选中

- 参数 : items {string[]} 选项数组
- 参数 : checkedItems {boolean[]} 选中的选项数组
- 参数 : callback {(di,which,isChecked)=>{}} 回调函数
- 返回 : {dialog} 自己


```javascript
//创建一个对话框
let dlg = $dialog.create()
.moreItems(["选项1","选项2","选项3"],[false,true,false],(di,which,isChecked)=>{
    log("我被点击了");
})
.show();
```


#### show()

> 显示对话框

- 返回 : {AlertDialog} 对话框对象


```javascript
//创建一个对话框
let dlg = $dialog.create()
.title("提示")
.msg("我是一个对话框")
.show();//显示对话框
```


#### showBefore(callback)

> 对话框显示前回调
> 
> 需要注意的是:该回调是放在UI线程中执行的

- 参数 : callback {()=>{}} 回调函数 
- 返回 : {dialog} 自己
- 版本 : 1.5.0


```javascript
//创建一个对话框
let dlg = $dialog.create()
.title("提示")
.msg("我是一个对话框")
.showBefore(()=>{
    log("对话框显示前回调");
})
.show();//显示对话框
```


#### showAfter(callback)

> 对话框显示后回调
> 
> 需要注意的是:该回调是放在UI线程中执行的

- 参数 : callback {()=>{}} 回调函数 
- 返回 : {dialog} 自己
- 版本 : 1.5.0


```javascript
//在自定义view中，如果有界面元素需要刷新，那么就最好在dialog显示之后再操作
//例如:
let ui = $ui.layout("ui.xml");//解析一个视图
let dialog = $dialog.create();//创建一个对话框
dialog.showAfter(()=>{
    //如果自定义视图中存在需要操作的ui元素，可以放到这里操作
    let but = ui.id("mButtonClose");
    mButtonClose.click(()=>{
        dialog.close();//关闭对话框
    });
}).view(ui.getView()).show();//显示自定义视图
```


#### onClose(callback)

> 监听对话框关闭

- 参数 : callback {()=>{}} 对话框关闭后回调
- 版本 : 1.8.0


```javascript
let alt = $dialog.create()
.title("标题")
.msg("我是信息")
.but3("关闭",()=>{
    //这里关闭对话框
    alt.close();
})
.onClose(()=>{
    log("对话框被关闭了");
})
.show();//显示对话框
```


#### close()

> 关闭对话框


```javascript
//创建一个对话框
let dlg = $dialog.create()
.title("提示")
.msg("我是一个对话框")
.but1("关闭",()=>{
    dlg.close();//关闭对话框
})
.show();//显示对话框
```

---

## $tip - 阻塞式对话框

- 更新时间:2026-01-30 19:32:57

> 阻塞式对话框
> 
> 什么是阻塞式对话框？
> 
> 答：当对话框发起调用时，阻塞当前线程不向下执行代码，当对话框处理完事件之后，下面的代码才会执行。




#### i(msg)

> [信息]对话框

- 参数 : msg {Object...} 信息内容
- 版本 : 1.0.0


```javascript
$tip.i("我是信息");
```


#### v(msg)

> [说明]对话框

- 参数 : msg {Object...} 信息内容
- 版本 : 1.0.0


```javascript
$tip.v("我是信息");
```


#### w(msg)

> [警告]对话框

- 参数 : msg {Object...} 信息内容
- 版本 : 1.0.0


```javascript
$tip.w("我是信息");
```


#### e(msg)

> [异常]对话框

- 参数 : msg {Object...} 信息内容
- 版本 : 1.0.0


```javascript
$tip.e("我是信息");
```


#### d(msg)

> [调试]对话框

- 参数 : msg {Object...} 信息内容
- 版本 : 1.0.0


```javascript
$tip.d("我是信息");
```


#### input(title, callback)

> 输入对话框

- 参数 : title {string} 标题
- 参数 : callback {(value)=>{}} 确定按钮回调
- 版本 : 1.0.0


```javascript
$tip.input("请输入你的名字",(value)=> {
    toast("输入的内容:"+value);
});
```


#### input(title, def, callback)

> 输入对话框(默认值)

- 参数 : title {string} 标题
- 参数 : def {string} 默认值
- 参数 : callback {(value)=>{}} 确定按钮回调
- 版本 : 1.0.0


```javascript
$tip.input("请输入你的名字","张三",(value)=> {
    toast("输入的内容:"+value);
});
```


#### input(title, hint, def, callback)

> 输入对话框(默认值)

- 参数 : title {string} 标题
- 参数 : hint {string} 提示
- 参数 : def {string} 默认值
- 参数 : callback {(value)=>{}} 确定按钮回调
- 版本 : 1.0.0


```javascript
$tip.input("你是?","输入名字","张三",(value)=> {
    toast("输入的内容:"+value);
});
```


#### inputInt(title, callback)

> 输入整数
> 
> 如果输入的字符串最后无法解析成数字则回调结果为0
> 
> 引导文字默认为标题
> 
> 默认值为0

- 参数 : title {string} 标题
- 参数 : callback {(num)=>{}} 结果回调


```javascript
$tip.inputInt("年龄",(num)=> {
    toast("刚满"+num+"岁~");
});
```


#### inputInt(title, def, callback)

> 输入整数
> 
> 如果输入的字符串最后无法解析成数字则回调结果为0
> 
> 引导文字默认为标题

- 参数 : title {string} 标题
- 参数 : def {int} 默认值
- 参数 : callback {(num)=>{}} 结果回调


```javascript
$tip.inputInt("年龄",18,(num)=> {
    toast("刚满"+num+"岁~");
});
```


#### inputInt(title, hint, callback)

> 输入整数
> 
> 如果输入的字符串最后无法解析成数字则回调结果为0
> 
> 默认值为0

- 参数 : title {string} 标题
- 参数 : hint {string} 引导文字
- 参数 : callback {(num)=>{}} 结果回调


```javascript
$tip.inputInt("年龄","请输入年龄:",(num)=> {
    toast("刚满"+num+"岁~");
});
```


#### inputInt(title, hint, def, callback)

> 输入整数
> 
> 如果输入的字符串最后无法解析成数字则回调结果为0

- 参数 : title {string} 标题
- 参数 : hint {string} 引导文字
- 参数 : def {int} 默认值
- 参数 : callback {(num)=>{}} 结果回调


```javascript
$tip.inputInt("年龄","请输入你的年龄:",18,(num)=> {
    toast("刚满"+num+"岁~");
});
```


#### show(title, msg)

> 文本提示对话框

- 参数 : title {string} 标题
- 参数 : msg {string} 信息
- 版本 : 1.0.0


```javascript
$tip.show("你好新人","我是你的AIGame助手");
```


#### show(title, msg, click)

> 文本提示对话框(有回调)

- 参数 : title {string} 标题
- 参数 : msg {string} 信息
- 参数 : click {()=>{}} [确定]按钮回调
- 版本 : 1.0.0


```javascript
$tip.show("你好新人","我是你的AIGame助手",()=> {
    toast("你好!");
});
```


#### show(title, view)

> 自定义对话框(右上角关闭)

- 参数 : title {string} 标题
- 参数 : view {View} 自定义view
- 版本 : 1.0.0


```javascript
//解析xml并且获得ui对象
let ui = $ui.layout("ag-app-example/$tip - 阻塞式对话框/01.自定义对话框/ui.xml");
//通过ui对象拿到View对象
let view = ui.getView();
//这种方式不会显示底部的按钮
$tip.show("自定义对话框", view);
```


#### show(title, view, click)

> 自定义对话框(确定关闭)

- 参数 : title {string} 标题
- 参数 : view {View} 自定义view
- 参数 : click {()=>{}} 点击确定按钮的回调
- 版本 : 1.0.0


```javascript
//解析xml并且获得ui对象
let ui = $ui.layout("ag-app-example/$tip - 阻塞式对话框/01.自定义对话框/ui.xml");
//通过ui对象拿到View对象
let view = ui.getView();
//通过tip显示这个view
$tip.show("自定义对话框", view, ()=> {
    toast("保存成功");
});
```


#### one(title, items, callback)

> 单选对话框

- 参数 : title {string} 标题
- 参数 : items {list[string]} 选项
- 参数 : callback {(value)=>{}} 选择回调
- 版本 : 1.0.0


```javascript
let arr = ["小狗","小猫","小猪"];
$tip.one("请选择",arr,(value)=> {
    toast("你选择了:"+value);
});
```


#### more(title, items, callback)

> 多选对话框

- 参数 : title {string} 标题
- 参数 : items {list[string]} 选项
- 参数 : callback {(values)=>{}} 选择回调
- 版本 : 1.0.0


```javascript
let arr = ["小狗","小猫","小猪"];
$tip.more("请选择",arr,(values)=> {
    toast("你选择了:"+values);
});
```


#### calendar(callback)

> 日期选择对话框

- 参数 : callback {(dateInfo)=>{}} 选择回调
- 版本 : 1.7.0


```javascript
//选择日期
$tip.calendar((info)=> {
    //此回调处于第三方线程
    let year = info.year; //年
    let month = info.month; //月
    let day = info.day; //日
    //显示日期
    alert("日期",year+"-"+month+"-"+day);
});
```


#### date(callback)

> 滚轮方式选择日期

- 参数 : callback {(timeInfo)=>{}} 选择回调
- 版本 : 1.2.8


```javascript
//滚轮方式选择日期
$tip.date((info)=> {
    //此回调处于第三方线程
    let year = info.year; //年
    let month = info.month; //月
    let day = info.day; //日
    //显示日期
    alert("日期",year+"-"+month+"-"+day);
});
```


#### clock(callback)

> 时间选择对话框

- 参数 : callback {(timeInfo)=>{}} 选择回调
- 版本 : 1.7.0


```javascript
//24小时制:时间选择对话框
$tip.clock((info)=> {
    //此回调处于第三方线程
    let hour = info.hour; //时
    let minute = info.minute; //分
    //显示时间
    alert("时间",hour+":"+minute);
});
```


#### time(callback)

> 时间滚动选择对话框

- 参数 : callback {(timeInfo)=>{}} 选择回调
- 版本 : 1.2.8


```javascript
//24小时制:滚轮方式时间选择对话框
$tip.time((info)=> {
    //此回调处于第三方线程
    let hour = info.hour; //时
    let minute = info.minute; //分
    //显示时间
    alert("时间",hour+":"+minute);
});
```