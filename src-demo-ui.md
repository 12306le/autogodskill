# 示例：界面/对话框/悬浮窗


## #U62d3#U5c55#U793a#U4f8b-02.#U5907#U4efd#U5e94#U7528-main

```javascript
//AIGame官方示例

//注意：本示例并不完善，只用于参考和学习
//本实例主要用来教学AppInfo的原生交互
//具体在代码的40行左右位置

//解析界面并且显示
let ui = $ui.layout("example/拓展示例/02.备份应用/ui.xml");
ui.show();
ui.id("mAppbar").back(()=> {
    ui.finish();
});
ui.id("mAppbar").menu((title)=> {
    if(title=="帮助"){
        alert("帮助","本示例教学如何使用AppInfo的原生交互来实现备份应用的功能,具体在代码的40行左右位置");
    }
});

//获取列表控件
let ls = ui.id("mLs");

//刷新列表中的应用信息数据
let flushList = function() {
    //获取应用列表信息
    let appList = $app.lsUserApp(); //获取用户应用：而不是系统应用
    ls.flush(appList); //每个元素的对象都是AppInfo类型的，参考文档{AppInfo}
}


//绑定视图解析
ls.bindHolder((holder,data,position)=> {
    holder.id("appName").setText(data.appName);
    holder.id("pkgName").setText(data.pkgName);
    //data本身就是AppInfo对象，参考文档{AppInfo}我们发现它存在icon属性
    //icon属性的类型是Image，参考文档{Image}它可以获取Bitmap对象
    holder.id("appIcon").setImg(data.icon.getBitmap());
    holder.id("card").click((view)=> {
        //点击后开始给当前应用进行备份
        $tip.input("备份路径","/sdcard/Pictures/"+data.appName+".apk",(value)=>{
            //接下来就涉及到原生交互了
            //我们通过AppInfo的info属性拿到：{ApplicationInfo}对象(android.content.pm.ApplicationInfo)
            let applicationInfo = data.info;
            //在安卓中{ApplicationInfo}有属性sourceDir可以获得apk的安装位置
            let apkPath = applicationInfo.sourceDir;
            log("Apk安装位置："+apkPath);
            //我们把这个路径下的apk拷贝到输入的路径下面就行了
            $file.copy(apkPath,value);
            holder.id("card").snack("拷贝完成!");
        });
    });
});



//界面显示后自动刷新一下列表
flushList();

//下拉刷新控件
ui.id("mFlush").flush(()=> {
    flushList();
});


//结束示例
```


## #U62d3#U5c55#U793a#U4f8b-03.DeepSeek#U5bf9#U8bdd-main

```javascript
let ui = $ui.layout("example/拓展示例/03.DeepSeek对话/xml/main.xml");
ui.show(); //显示界面

//[存储]
let storage = $storage.create("org.aigame.demo.deepseek");

//[组件]
let mAppbar = ui.id("mAppbar"); //应用条
let nested = ui.id("nested"); //显示对话内容的
let layout = ui.id("layout"); //显示对话内容的

mAppbar.back(()=> {
    ui.finish();
});

mAppbar.menu((title)=> {
    if (title == "清除") {
        $tip.show("清除对话","确认清空对话内容吗？",()=> {
            //清空所有布局
            layout.removeAll();
        });
    }
    if (title == "设置") {
        $tip.input("Api Key",(value)=> {
            if ($str.isEmpty(value)) {
                toast("不允许输入空值");
                return;
            }
            storage.put("apiKey",value);
        });
    }
});


//(1)创建deepseek对话视图
let createDsView = function(content) {
    let ui = $ui.layout("example/拓展示例/03.DeepSeek对话/xml/DeepSeek.xml");
    ui.id("content").setText(content);
    return {
        ui: ui,
        view: ui.getView()
    };
}

//(2)创建我的对话视图
let createMwView = function(content) {
    let ui = $ui.layout("example/拓展示例/03.DeepSeek对话/xml/Mine.xml");
    ui.id("content").setText(content);
    return ui.getView();
}

//(3)请求调用
let requireContent = function(apiKey,content) {
    let res = $http.post({
        url: "https://api.deepseek.com/chat/completions",
        readTimeout: 60,//deepseek响应有时候会很慢，如果超时了，就设置这个
        head: {
            "Content-Type": "application/json",
            "Authorization": "Bearer "+apiKey,//输入ApiKey
        },
        data: {
            model: "deepseek-chat",
            messages: [{
                role: "system",
                content: "你是一个智能生活助手"
            },
                {
                    role: "user",
                    //我的对话内容：
                    content: content
                }],
            stream: false
        }
    });

    //解析json内容
    let data = res.json();

    return data.choices[0].message.content;
}

//(4)滑动NestedScrollView到最底部
let scrollBottom = function() {
    //通过安卓原生类的post函数，可以直接发送一条ui线程事件(确保视图刷新后在ui线程中调用)
    layout.getView().post(()=> {
        let nestedScrollView = nested.getView(); //获取原生对象
        //要滑动到的高度
        let toH = layout.getH();
        //开始滑动
        nestedScrollView.smoothScrollTo(0,toH);
        //调用安卓原生类{NestedScrollView}的smoothScrollTo方法(请参考安卓api)
    });
}


//输入内容
ui.id("input").click((view)=> {
    //判断ApiKey是否是空的
    let apiKey = storage.get("apiKey","");
    if ($str.isEmpty(apiKey)) {
        alert("ApiKey为空","请前往DeepSeek官网申请ApiKey后，点击右上角设置图标，配置ApiKey内容。\n类似于：sk-xxxx 这样的字符串");
        return null;
    }
    $tip.input("输入内容",(value)=> {
        if ($str.isEmpty(value)) {
            return null;
        }
        //创建我的对话视图
        layout.addView(createMwView(value));
        //创建deepseek对话视图
        let dsView = createDsView("正在思考...");
        layout.addView(dsView.view);
        //网络请求不允许在ui线程中进行，于是就用线程
        $thread.run(()=> {
            //调用请求
            let answer = requireContent(apiKey,value);
            //设置回答
            dsView.ui.id("content").setText(answer);
            //滑动到底部
            scrollBottom();
        });
    });
});





//..
```


## $alert-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-01.#U57fa#U672c#U4f7f#U7528

```javascript
//官方示例
//$alert比$dialog更适合显示较大的视图

$alert.create()
.title("标题")
.msg("我是信息内容")
.but1("按钮1")
.but2("按钮2")
.but3("按钮3")
.show();


//示例结束
```


## $alert-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-02.#U4e0d#U51c6#U81ea#U52a8#U5173#U95ed

```javascript
//官方示例


$alert.create()
.title("禁止自动关闭")
.msg("不允许通过点击外部自动关闭对话框")
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $alert-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-03.#U5355#U9009#U6587#U672c#U884c

```javascript
//官方示例


$alert.create()
.title("单选")
//.msg("我是信息") 注意：使用了items就不能再使用msg设置消息体了
.items(["选项1","选项2","选项3"],(di,which)=> {
    info("选中了:"+which);
})
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $alert-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-04.#U5355#U9009#U6309#U94ae#U884c

```javascript
//官方示例


$alert.create()
.title("单选")
//.msg("我是信息") 注意：使用了oneItems就不能再使用msg设置消息体了
.oneItems(
    ["选项1","选项2","选项3"],
    0 ,//默认单选中第一个
    (di,which)=> {
        info("选中了:"+which);
    })
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $alert-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-05.#U591a#U9009#U65e0#U9ed8#U8ba4#U503c

```javascript
//官方示例


$alert.create()
.title("单选")
//.msg("我是信息") 注意：使用了moreItems就不能再使用msg设置消息体了
.moreItems(
    ["选项1","选项2","选项3"],
    (di,which)=> {
        info("选中了:"+which);
    })
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $alert-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-06.#U591a#U9009#U6709#U9ed8#U8ba4#U503c

```javascript
//官方示例


$alert.create()
.title("单选")
//.msg("我是信息") 注意：使用了moreItems就不能再使用msg设置消息体了
.moreItems(
    ["选项1","选项2","选项3"],
    [true , true , false],//默认多选中第一个和第二个
    (di,which)=> {
        info("选中了:"+which);
    })
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $alert-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-07.#U8bbe#U7f6e#U56fe#U6807

```javascript
//官方示例


$alert.create()
.title("设置图标")
.icon("logo_ag")
.msg("看看我的图标")
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $alert-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-08.#U81ea#U5b9a#U4e49#U5e03#U5c40

```javascript
//官方示例

let mAlert = $alert.create();

let ui = $ui.layout(`
<ui w="max">
    <button id="mButton1" style="text" text="点我试试" w="max"/>
    <button id="mButton2" text="关闭对话框" style="text" w="max" />
</ui>
`);

ui.id("mButton1").click(()=>{
    info("我被点击了");
});

ui.id("mButton2").click(()=>{
    mAlert.close();//关闭对话框
});

let mView = ui.getView();

mAlert
//不允许通过点击外部自动关闭对话框
//但是要记住一定要自己设置一个可以关闭对话框的方式
.cancelable(false) 
.view(mView) // 设置自定义布局
.show();


//示例结束
```


## $app-#U5e94#U7528#U64cd#U4f5c-01.#U83b7#U53d6#U5e94#U7528#U56fe#U6807

```javascript
// AIGame官方示例


//获取悬浮窗权限
$floaty.getPermit();

//获取图标
let icon = $app.getIcon("QQ");

//显示图片
$img.show(icon);//(需要用悬浮窗权限)




// 示例结束
```


## $arc-#U60ac#U6d6e#U7403#U83dc#U5355-01.#U5404#U79cd#U6837#U5f0f#U60ac#U6d6e#U6309#U94ae

```javascript
//AIGame 官方示例

let myName = "悬浮球1号";

if (!$arc.has(myName)) {
    //当前名称如果不存在，那么就开始创建自己的悬浮球

    //创建按钮容器(用来装小按钮)
    let menuBody = $arc.body(myName); //指定菜单名称

    //创建小按钮
    let menu1 = $arc.item("logo").bg("#55FFFFFF"); //指定按钮图标
    let menu2 = $arc.item("ic_color_lens_outline").bg("#FAFDFA");
    let menu3 = $arc.item("ic_play_arrow_outline");
    let menu4 = $arc.item("ic_cloud_upload_outline").bg("#C7DFD9");
    let menu5 = $arc.item("ic_clear_outline").style("outline").iconTint("#FF0000"); //可以这样指定样式[方法1]

    //可以这样指定样式[方法2]
    menu3.radius(15).iconSize(80).iconPadding(0).iconTint("#57965C").bg("#55FFFFFF");
    let play = false;
    menu3.click(()=> {
        if (play) {
            menu3.icon("ic_play_arrow_outline").iconTint("#57965C");
            play = false;
        } else {
            menu3.icon("ic_stop_fill").iconTint("#FF0000");
            play = true;
        }
    });

    //为menu5绑定事件
    menu5.click(()=> {
        //$arc.close(myName); //关闭悬浮窗(指定名称)
        $arc.closeAll(); //或者直接关闭全部的悬浮菜单
    });

    //向容器中添加小按钮
    menuBody
    .add(menu1) //添加小按钮[主按钮]
    .add(menu2) //添加小按钮[关闭]
    .add(menu3) //添加小按钮[运行/停止]
    .add(menu4.iconTint("#F2C55C")) //可以这样指定样式[方法3]
    .add(menu5) //添加小按钮[调色盘]
    .show(); //显示
}else{
    log(myName+"已存在");
}




//示例结束
```


## $arc-#U60ac#U6d6e#U7403#U83dc#U5355-02.#U5f88#U7b80#U5355#U7684#U60ac#U6d6e#U6309#U94ae

```javascript
//AIGame 官方示例

let myName = "悬浮球2号";
if (!$arc.has(myName)) {

    //创建按钮容器(用来装小按钮)
    let menuBody = $arc.body(myName); //指定菜单名称

    //创建小按钮
    let menu1 = $arc.item("ic_app").iconTint("#3574F0"); //指定按钮图标
    let menu2 = $arc.item("ic_clear");

    //为按钮2绑定事件
    menu2.click(()=> {
        $arc.close(myName); //关闭悬浮窗(和悬浮菜单名称一致)
        //$arc.closeAll();//或者直接关闭全部的悬浮菜单
    });

    //向容器中添加小按钮
    menuBody
    .add(menu1.bg("#55FFFFFF")) //添加小按钮
    .add(menu2.bg("#55000000").iconTint("#55FF0000").ripper("#550000FF")) //添加小按钮
    .show(); //显示



}

//示例结束
```


## $bus-#U6d88#U606f#U603b#U7ebf-02.Tasker#U6267#U884c#U811a#U672c-01.#U4f7f#U7528#U6559#U5b66

```javascript
$dialog.create()
.title("Tasker执行脚本")
.msg(`
1.打开Tasker
2.创建Tasker意图任务
3.操作(action)填写:'runJs:/sdcard/main.js'
4.包名(package)填写:'org.aigame.pro'
5.类名(class)填写:'org.aigame.api.bus.receiver.AgBusReceiver'
6.目标(type)设置成:'(广播)BroadcastReceiver'
7.最后执行任务,发送意图,AIGame便会执行/sdcard/main.js脚本
`)
.but1("复制类名",(dialog)=>{
    dialog.dismiss();
    setClip("org.aigame.api.bus.receiver.AgBusReceiver");
})
.but2("复制包名",(dialog)=>{
    dialog.dismiss();
    setClip("org.aigame.pro");
})
.but3("关闭",(dialog)=>{
    dialog.dismiss();
})
.show();
```


## $canvas-#U753b#U5e03-01.#U663e#U793a#U65b9#U5f0f-01.#U5728#U5e03#U5c40#U4e2d#U663e#U793a

```javascript
//AIGame官方示例

let ui= $ui.layout(`
<ui>
    <statusbar/>
    <appbar back="true" id="mAppbar" title="显示画布图片" w="max"/>
    <img id="mImg" w="max" h="max" gravity="center|top" padding="10"/>
</ui>
`);
ui.show();
ui.id("mAppbar").back(()=>{
    ui.finish();
});

//创建画布对象
let canvas = $canvas.create(500,500);
//创建画笔
let paint = $canvas.paint();
paint.setColor($color.RED);//红色
//绘制红色方框
canvas.drawRect(30,30,400,400,paint);
//布局显示画布中的图片
ui.id("mImg").setImg(canvas.getBitmap());



//示例结束
```


## $canvas-#U753b#U5e03-03.#U753b#U4e2a#U8868#U683c

```javascript
//AIGame官方示例

let ui= $ui.layout(`
<ui>
    <statusbar/>
    <appbar back="true" id="mAppbar" title="我的表格" w="max"/>
    <img id="mImg" w="max" h="max" gravity="center|top" padding="10"/>
</ui>
`);
ui.show();
ui.id("mAppbar").back(()=>{
    ui.finish();
});

let aw = 750; //合同宽度
let ah = 750; //合同高度
let th01_h = 45; //第1行表格线条高度("姓名之类的")
let th02_h = 45; //第2行表格线条高度("调查地址")
let th03_h = 300; //第3行表格线条高度("立案事由")
let th04_h = 60; //第4行表格线条高度("联系微信啥的")

//创建画布对象
let canvas = $canvas.create(aw,ah);

//绘制表格
let tabs = [
    1,1,aw-2,1,//上边框
    1,1,1,ah-2,//左边框
    1,ah-2,aw-2,ah-2,//下边框
    aw-2,1,aw-2,ah-2,//右边框
    //第1行表格线条高度(横线)
    1,1+th01_h,aw-2,1+th01_h,
    //第1行表格线条高度(竖线)
    70,1,70,1+th01_h,
    150,1,150,1+th01_h,
    270,1,270,1+th01_h,
    500,1,500,1+th01_h,
    570,1,570,1+th01_h,
    //第2行表格线条高度(横线)
    1,1+th01_h+th02_h,aw-2,1+th01_h+th02_h,
    100,1+th01_h,100,1+th01_h+th02_h,
    //第3行表格线条高度(横线)
    1,1+th01_h+th02_h+th03_h,aw-2,1+th01_h+th02_h+th03_h,
    100,1+th01_h+th02_h,100,1+th01_h+th02_h+th03_h,
    //第4行表格线条高度(横线)
    1,1+th01_h+th02_h+th03_h+th04_h,aw-2,1+th01_h+th02_h+th03_h+th04_h,
];
canvas.drawLines(tabs ,$canvas.paint("#000000"));
//绘制文字
let txtPaint = $canvas.paint("#000000");
txtPaint.setTextSize(20);
canvas.drawText("姓名",10,30,txtPaint);
canvas.drawText("身份证号",10+150,30,txtPaint);
canvas.drawText("号码",10+500,30,txtPaint);
canvas.drawText("调查地址",10,30+th01_h,txtPaint);
canvas.drawText("立案事由",10,30+th01_h+(th02_h+th03_h)/2,txtPaint);
let lxPaint = $canvas.paint($color.RED);
lxPaint.setTextSize(26);
canvas.drawText("1小时内联系:132584946(微信同号)偿还欠款可办理撤案",15,45+th01_h+th02_h+th03_h,lxPaint);


//布局显示画布
ui.id("mImg").setImg(canvas.getBitmap());





//示例结束
```


## $dialog-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-01.#U57fa#U672c#U4f7f#U7528

```javascript
//官方示例


$dialog.create()
.title("标题")
.msg("我是信息内容")
.but1("按钮1")
.but2("按钮2")
.but3("按钮3")
.show();


//示例结束
```


## $dialog-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-02.#U4e0d#U51c6#U81ea#U52a8#U5173#U95ed

```javascript
//官方示例


$dialog.create()
.title("禁止自动关闭")
.msg("不允许通过点击外部自动关闭对话框")
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $dialog-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-03.#U5355#U9009#U6587#U672c#U884c

```javascript
//官方示例


$dialog.create()
.title("单选")
//.msg("我是信息") 注意：使用了items就不能再使用msg设置消息体了
.items(["选项1","选项2","选项3"],(di,which)=> {
    info("选中了:"+which);
})
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $dialog-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-04.#U5355#U9009#U6309#U94ae#U884c

```javascript
//官方示例


$dialog.create()
.title("单选")
//.msg("我是信息") 注意：使用了oneItems就不能再使用msg设置消息体了
.oneItems(
    ["选项1","选项2","选项3"],
    0 ,//默认单选中第一个
    (di,which)=> {
        info("选中了:"+which);
    })
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $dialog-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-05.#U591a#U9009#U65e0#U9ed8#U8ba4#U503c

```javascript
//官方示例


$dialog.create()
.title("单选")
//.msg("我是信息") 注意：使用了moreItems就不能再使用msg设置消息体了
.moreItems(
    ["选项1","选项2","选项3"],
    (di,which)=> {
        info("选中了:"+which);
    })
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $dialog-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-06.#U591a#U9009#U6709#U9ed8#U8ba4#U503c

```javascript
//官方示例


$dialog.create()
.title("单选")
//.msg("我是信息") 注意：使用了moreItems就不能再使用msg设置消息体了
.moreItems(
    ["选项1","选项2","选项3"],
    [true , true , false],//默认多选中第一个和第二个
    (di,which)=> {
        info("选中了:"+which);
    })
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $dialog-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-07.#U8bbe#U7f6e#U56fe#U6807

```javascript
//官方示例


$dialog.create()
.title("设置图标")
.icon("logo_ag")
.msg("看看我的图标")
.but3("取消")
.cancelable(false) //不允许通过点击外部自动关闭对话框
.show();


//示例结束
```


## $dialog-#U975e#U963b#U585e#U5bf9#U8bdd#U6846-08.#U81ea#U5b9a#U4e49#U5e03#U5c40

```javascript
//官方示例

let dialog = $dialog.create();

let ui = $ui.layout(`
<ui w="max">
    <button id="mButton1" style="text" text="点我试试" w="max"/>
    <button id="mButton2" text="关闭对话框" style="text" w="max" />
</ui>
`);

ui.id("mButton1").click(()=>{
    info("我被点击了");
});

ui.id("mButton2").click(()=>{
    dialog.close();//关闭对话框
});

let mView = ui.getView();

dialog
//不允许通过点击外部自动关闭对话框
//但是要记住一定要自己设置一个可以关闭对话框的方式
.cancelable(false) 
.view(mView) // 设置自定义布局
.show();


//示例结束
```


## $engine-#U811a#U672c#U5f15#U64ce-04.#U6682#U505c#U4e0e#U8fd0#U884c

```javascript
//官方示例

//定义脚本路径
let path = "/example/$engine - 脚本引擎/test/delay.js";

//执行脚本(目的是拿到任务ID)
let id = $engine.run(path);

//我先创建一个应用级悬浮窗方便控制脚本引擎的暂停和开始
let appFloaty = $floaty.newApp(`
<ui>
    <button id="pause" text="暂停" />
    <button id="run" text="运行" />
    <button id="close" text="关闭" />
</ui>
`);

//绑定按钮点击事件
appFloaty.id("pause").click(() => {
    //暂停任务ID对应的脚本
    $engine.pause(id);
});

appFloaty.id("run").click(() => {
    //开始执行任务ID对应的脚本
    $engine.start(id);
});

appFloaty.id("close").click(() => {
    //关闭应用级悬浮窗
    appFloaty.close();
});



//示例结束
```


## $floaty-#U60ac#U6d6e#U7a97-01.#U53ef#U8c03#U8282#U60ac#U6d6e#U7a97-01.#U7b80#U5355#U6848#U4f8b

```javascript
//官方示例

//(1)创建并且显示可调节悬浮窗
let floaty = $floaty.newAdj(`
<ui>
    <linear dir="v" w="max">
        <button text="按钮1" w="max"/>
        <button text="按钮2" w="max"/>
        <button id="closeButton" text="关闭" w="max"/>
    </linear>
</ui>
`);

//(2).绑定按钮点击事件
floaty.id("closeButton").click(()=>{
    floaty.close();
});


//示例结束
```


## $floaty-#U60ac#U6d6e#U7a97-02.#U5e94#U7528#U7ea7#U60ac#U6d6e#U7a97-01.#U7efc#U5408#U6848#U4f8b

```javascript
//AIGame官方示例

//先把之前创建的悬浮窗全部关掉
$floaty.closeAll();


let floaty = $floaty.newApp(`
<ui>
    <linear w="max" h="max" bg="#33FF0000" >
        <button id="mButton" text="关闭" ripper="#FFFFFF" />
        <button id="mBut1" text="全屏" ripper="#FFFFFF" />
        <button id="mBut2" text="非全屏" ripper="#FFFFFF" />
        <button id="mBut3" text="取消触摸" ripper="#FFFFFF" />
        <button id="mBut4" text="修改位置" ripper="#FFFFFF" />
    </linear>
</ui>
`);


//监听按钮：点击后关闭这个悬浮窗
floaty.id("mButton").click(()=>{
    floaty.close();
});

//全屏
floaty.id("mBut1").click(()=>{
    floaty.fill(true);
});

//非全屏
floaty.id("mBut2").click(()=>{
    floaty.fill(false);
});

//取消触摸 3秒之后 开启触摸
floaty.id("mBut3").click(()=>{
    floaty.touch(false);
    $thread.run(()=>{
       sleep(3000);
       floaty.touch(true);
       toast("开启触摸啦");
    });
});

//修改位置
floaty.id("mBut4").click(()=>{
    floaty.setXY(300,400);
});



//示例结束
```


## $floaty-#U60ac#U6d6e#U7a97-02.#U5e94#U7528#U7ea7#U60ac#U6d6e#U7a97-02.#U62fe#U53d6#U5750#U6807

```javascript
//AIGame官方示例

//先把之前创建的悬浮窗全部关掉
$floaty.closeAll();

alert("提示","我将显示一个全屏的悬浮窗，你可以触摸任意位置，我会显示你触摸位置的坐标并且显示一个准心图片，点击关闭后，我会复制这个位置到剪切板上！");

let floaty = $floaty.newApp(`
<ui>
    <linear id="mLinear" w="max" h="max" gravity="center">
        <text id="mText"/>
        <button id="mButton" text="关闭" ripper="#FFFFFF" />
        <img id="mImg" src="ic_record" tint="colorPrimary" />
    </linear>
</ui>
`);

let x = 0;
let y = 0;

floaty.fill(true);
//获取安卓原生控件：监听touch事件 (原生交互案例,仅供学习)
floaty.id("mLinear").getView().setOnTouchListener((view,event)=> {
    x = Math.round(event.getRawX());
    y = Math.round(event.getRawY());
    floaty.id("mText").setText(x+","+y);
    //显示一个准心图标
    let img = floaty.id("mImg");
    img.setX(x-img.getW()/2);
    img.setY(y-img.getH()/2);
    return true;
});



//监听按钮：点击后关闭这个悬浮窗
floaty.id("mButton").click(()=> {
    floaty.close();
    setClip(x+","+y);
    toast("坐标复制完成");
});






//示例结束
```


## $floaty-#U60ac#U6d6e#U7a97-02.#U5e94#U7528#U7ea7#U60ac#U6d6e#U7a97-03.#U5173#U95ed#U60ac#U6d6e#U7a97

```javascript
//AIGame 官方示例


//关闭悬浮窗
$floaty.closeAll();



//示例结束
```


## $floaty-#U60ac#U6d6e#U7a97-03.#U7cfb#U7edf#U7ea7#U60ac#U6d6e#U7a97-01.#U7efc#U5408#U6848#U4f8b

```javascript
//AIGame官方示例

//先把之前创建的悬浮窗全部关掉
$floaty.closeAll();


let floaty = $floaty.newSys(`
<ui>
    <linear w="max" h="max" bg="#33FF0000" >
        <button id="mButton" text="关闭" ripper="#FFFFFF" />
        <button id="mBut1" text="全屏" ripper="#FFFFFF" />
        <button id="mBut2" text="非全屏" ripper="#FFFFFF" />
        <button id="mBut3" text="取消触摸" ripper="#FFFFFF" />
        <button id="mBut4" text="修改位置" ripper="#FFFFFF" />
    </linear>
</ui>
`);


//监听按钮：点击后关闭这个悬浮窗
floaty.id("mButton").click(()=>{
    floaty.close();
});

//全屏
floaty.id("mBut1").click(()=>{
    floaty.fill(true);
});

//非全屏
floaty.id("mBut2").click(()=>{
    floaty.fill(false);
});

//取消触摸 3秒之后 开启触摸
floaty.id("mBut3").click(()=>{
    floaty.touch(false);
    $thread.run(()=>{
       sleep(3000);
       floaty.touch(true);
       toast("开启触摸啦");
    });
});

//修改位置
floaty.id("mBut4").click(()=>{
    floaty.setXY(300,400);
});



//示例结束
```


## $floaty-#U60ac#U6d6e#U7a97-03.#U7cfb#U7edf#U7ea7#U60ac#U6d6e#U7a97-02.#U62fe#U53d6#U5750#U6807

```javascript
//AIGame官方示例

//先把之前创建的悬浮窗全部关掉
$floaty.closeAll();

alert("提示","我将显示一个全屏的悬浮窗，你可以触摸任意位置，我会显示你触摸位置的坐标并且显示一个准心图片，点击关闭后，我会复制这个位置到剪切板上！");

let floaty = $floaty.newSys(`
<ui>
    <linear id="mLinear" w="max" h="max" gravity="center">
        <text id="mText"/>
        <button id="mButton" text="关闭" ripper="#FFFFFF" />
        <img id="mImg" src="ic_record" tint="colorPrimary" />
    </linear>
</ui>
`);

let x = 0;
let y = 0;

floaty.fill(true);
//获取安卓原生控件：监听touch事件 (原生交互案例,仅供学习)
floaty.id("mLinear").getView().setOnTouchListener((view,event)=> {
    x = Math.round(event.getRawX());
    y = Math.round(event.getRawY());
    floaty.id("mText").setText(x+","+y);
    //显示一个准心图标
    let img = floaty.id("mImg");
    img.setX(x-img.getW()/2);
    img.setY(y-img.getH()/2);
    return true;
});



//监听按钮：点击后关闭这个悬浮窗
floaty.id("mButton").click(()=> {
    floaty.close();
    setClip(x+","+y);
    toast("坐标复制完成");
});






//示例结束
```


## $floaty-#U60ac#U6d6e#U7a97-03.#U7cfb#U7edf#U7ea7#U60ac#U6d6e#U7a97-03.#U5173#U95ed#U60ac#U6d6e#U7a97

```javascript
//AIGame 官方示例


//关闭悬浮窗
$floaty.closeAll();



//示例结束
```


## $floaty-#U60ac#U6d6e#U7a97-04.#U9009#U62e9#U533a#U57df

```javascript
//选择区域悬浮窗
$floaty.newSelect((rect)=>{
    log("用户选择范围:",rect);
});
```


## $img-#U56fe#U7247#U5904#U7406-#U989c#U8272#U503c#U8f6c#U989c#U8272

```javascript
$tip.input("请输入颜色值",(value)=> {
    $thread.run(()=>{
        alert("颜色代码",$color.str(value * 1));
    });
});
```


## $img-#U56fe#U7247#U5904#U7406-#U989c#U8272#U8f6c#U989c#U8272#U503c

```javascript
$tip.input("请输入颜色",(value)=> {
    $thread.run(()=>{
        alert("颜色值",$color.parse(value));
    });
});
```


## $permit-#U6743#U9650#U5de5#U5177-01.#U5199#U5165#U65e5#U5386#U6743#U9650

```javascript
//判断是否有写入日历权限
let has = $permit.hasWriteCalendar();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取写入日历权限
        $permit.writeCalendar();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-02.#U5199#U5165#U8054#U7cfb#U4eba#U6743#U9650

```javascript
//判断是否有写入联系人权限
let has = $permit.hasWriteContact();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取写入联系人权限
        $permit.writeContact();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-05.#U53d1#U9001#U77ed#U4fe1#U6743#U9650

```javascript
//判断是否有发送短信权限
let has = $permit.hasSendSms();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取发送短信权限
        $permit.sendSms();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-06.#U5916#U90e8#U5b58#U50a8#U6743#U9650

```javascript
//判断是否有外部存储权限
let has = $permit.hasSd();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取外部存储权限
        $permit.sd();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-07.#U5b9a#U4f4d#U6743#U9650

```javascript
//判断是否有定位权限
let has = $permit.hasLoc();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取定位权限
        $permit.loc();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-08.#U5f55#U97f3#U6743#U9650

```javascript
//判断是否有录音权限
let has = $permit.hasRecord();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取录音权限
        $permit.record();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-09.#U60ac#U6d6e#U7a97#U6743#U9650

```javascript
//判断是否有悬浮窗权限
let has = $permit.hasFloaty();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取悬浮窗权限
        $permit.floaty();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-10.#U65e0#U969c#U788d#U6743#U9650

```javascript
//判断是否有无障碍权限
let has = $permit.hasWza();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取无障碍权限
        $permit.wza();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-13.#U76f8#U673a#U6743#U9650

```javascript
//判断是否有相机权限
let has = $permit.hasCamera();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取相机权限
        $permit.camera();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-14.#U7cfb#U7edf#U8bbe#U7f6e#U6743#U9650

```javascript
//判断是否有系统设置权限
let has = $permit.hasSet();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取系统设置权限
        $permit.set();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-15.#U7f51#U7edc#U6743#U9650

```javascript
//判断是否有网络权限
let has = $permit.hasNet();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取网络权限
        $permit.net();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-16.#U8bfb#U53d6#U4fe1#U606f

```javascript
//判断是否有读取信息权限
let has = $permit.hasReadSms();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取读取信息权限
        $permit.readSms();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-17.#U8bfb#U53d6#U65e5#U5386#U6743#U9650

```javascript
//判断是否有读取日历权限
let has = $permit.hasReadCalendar();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取读取日历权限
        $permit.readCalendar();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-18.#U8bfb#U53d6#U8054#U7cfb#U4eba#U6743#U9650

```javascript
//判断是否有读取联系人权限
let has = $permit.hasReadContact();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取读取联系人权限
        $permit.readContact();
    });
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


## $permit-#U6743#U9650#U5de5#U5177-19.#U901a#U8bdd#U6743#U9650

```javascript
//判断是否有通话权限
let has = $permit.hasCall();

if (has) {
    toast("有权限");
} else {
    toast("无权限");
    $tip.show("获取权限","是否获取权限?",()=> {
        //获取通话权限
        $permit.call();
    });
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


## $res-#U8d44#U6e90#U7ba1#U7406#U5668-04.#U67e5#U770b#U8d44#U6e90#U5185#U5bb9

```javascript
//AIGame 官方示例

//(1)加载资源对象(指定名称)
let res = $res.create("我的资源");

//(2)获得资源内容
let content = res.cat();

$tip.show("资源内容", content, null);


//示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-07.#U5c4f#U5e55#U4fe1#U606f

```javascript
// AIGame官方示例


let info = $screen.getScreenInfo();

$tip.show("详细信息",info.toString());




// 示例结束
```


## $sys-#U7cfb#U7edf#U5de5#U5177-07.#U5224#U65ad#U526a#U5207#U677f#U662f#U5426#U6709#U5185#U5bb9

```javascript
// AIGame官方示例


//判断是否有内容
if($sys.hasClip()){
    //获得内容
    let content = $sys.getClip();

    $tip.i(content);
}




// 示例结束
```


## $task-#U811a#U672c#U4efb#U52a1-04.#U63a7#U5236#U811a#U672c#U6682#U505c#U4e0e#U8fd0#U884c

```javascript
//(1)创建可调节悬浮窗并且显示
let ui = $floaty.newAdj(
`
<ui>
    <linear dir="v" w="max">
        <button id="bt1" text="暂停" w="max"/>
        <button id="bt2" text="开始" w="max"/>
        <button id="bt3" text="是否活着" w="max"/>
    </linear>
</ui>
`);

//(2)绑定事件
ui.id("bt1").click(()=>{
    $task.pause();//暂停脚本(原理是控制脚本引擎的解释执行)
});
ui.id("bt2").click(()=>{
    $task.start();//继续执行(原理是控制脚本引擎的解释执行)
});
ui.id("bt3").click(()=>{
    if($task.isRunning()){
        info("我还活着");
    }else{
        info("我已经死了");
    }
});

//当执行到这里的时候，上面的脚本都被执行了，所以可以正常的控制暂停和运行下面的代码
//假设这是任务代码：
for(let i = 0;i<20;i++){
    sleep(1000);
    info("正在运行"+i);
}

//当循环代码走完之后，当前任务就死了。所以点击按钮[是否活着]会提示"我已经死了"
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-01.#U81ea#U5b9a#U4e49#U5bf9#U8bdd#U6846-01.#U9ed8#U8ba4#U663e#U793a

```javascript
// AIGame官方示例


//解析xml并且获得ui对象
let ui = $ui.layout("example/$tip - 阻塞式对话框/01.自定义对话框/ui.xml");
//通过ui对象拿到View对象
let view = ui.getView();



//通过tip显示这个view
$tip.show("自定义对话框", view, ()=> {
    toast("保存成功");
});




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-01.#U81ea#U5b9a#U4e49#U5bf9#U8bdd#U6846-02.#U4e0d#U663e#U793a#U5e95#U90e8#U6309#U94ae

```javascript
// AIGame官方示例


//解析xml并且获得ui对象
let ui = $ui.layout("example/$tip - 阻塞式对话框/01.自定义对话框/ui.xml");
//通过ui对象拿到View对象
let view = ui.getView();


//这种方式不会显示底部的按钮
$tip.show("自定义对话框", view);




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-01.[#U4fe1#U606f]#U5bf9#U8bdd#U6846

```javascript
// AIGame官方示例


$tip.i("我是信息");




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-02.[#U8bf4#U660e]#U5bf9#U8bdd#U6846

```javascript
// AIGame官方示例


$tip.v("我是信息");




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-03.[#U8b66#U544a]#U5bf9#U8bdd#U6846

```javascript
// AIGame官方示例


$tip.w("我是信息");




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-04.[#U5f02#U5e38]#U5bf9#U8bdd#U6846

```javascript
// AIGame官方示例


$tip.e("我是信息");




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-05.[#U8c03#U8bd5]#U5bf9#U8bdd#U6846

```javascript
// AIGame官方示例


$tip.d("我是信息");




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-06.#U8f93#U5165#U5bf9#U8bdd#U6846

```javascript
// AIGame官方示例


$tip.input("请输入你的名字",(value)=> {
    toast("输入的内容:"+value);
});




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-07.#U8f93#U5165#U5bf9#U8bdd#U6846(#U9ed8#U8ba4#U503c)

```javascript
// AIGame官方示例


$tip.input("请输入你的名字","张三",(value)=> {
    toast("输入的内容:"+value);
});




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-08.#U6587#U672c#U63d0#U793a#U5bf9#U8bdd#U6846

```javascript
// AIGame官方示例


$tip.show("你好新人","我是你的AIGame助手");




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-09.#U6587#U672c#U63d0#U793a#U5bf9#U8bdd#U6846(#U6709#U56de#U8c03)

```javascript
// AIGame官方示例


$tip.show("你好新人","我是你的AIGame助手",()=> {
    toast("你好!");
});




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-10.#U81ea#U5b9a#U4e49#U5bf9#U8bdd#U6846(#U70b9#U51fb#U5176#U4ed6#U5730#U65b9#U5173#U95ed)

```javascript
// AIGame官方示例


//解析xml并且获得ui对象
let ui = $ui.layout("example/$tip - 阻塞式对话框/01.自定义对话框/ui.xml");
//通过ui对象拿到View对象
let view = ui.getView();


//这种方式不会显示底部的按钮
$tip.show("自定义对话框", view);




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-11.#U81ea#U5b9a#U4e49#U5bf9#U8bdd#U6846(#U786e#U5b9a#U5173#U95ed)

```javascript
// AIGame官方示例


//解析xml并且获得ui对象
let ui = $ui.layout("example/$tip - 阻塞式对话框/01.自定义对话框/ui.xml");
//通过ui对象拿到View对象
let view = ui.getView();



//通过tip显示这个view
$tip.show("自定义对话框", view, ()=> {
    toast("保存成功");
});




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-12.#U5355#U9009#U5bf9#U8bdd#U6846

```javascript
// AIGame官方示例


let arr = ["小狗","小猫","小猪"];

$tip.one("请选择",arr,(value)=> {
    toast("你选择了:"+value);
});




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-13.#U591a#U9009#U5bf9#U8bdd#U6846

```javascript
// AIGame官方示例


let arr = ["小狗","小猫","小猪"];

$tip.more("请选择",arr,(values)=> {
    toast("你选择了:"+values);
});




// 示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-14.#U65e5#U671f#U9009#U62e9(#U65e5#U5386)

```javascript
//AIGame 官方示例


//选择日期
$tip.calendar((info)=> {
    //此回调处于第三方线程
    log(info); //用log打印具体的元素
    //常用调用：
    let year = info.year; //年
    let month = info.month; //月
    let day = info.day; //日
    //或者：
    year = info.y; //年
    month = info.m; //月
    day = info.d; //日
    //显示日期
    alert("日期",year+"-"+month+"-"+day);
});




//示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-15.#U65e5#U671f#U9009#U62e9(#U6eda#U8f6e)

```javascript
//AIGame 官方示例


//选择日期
$tip.date((info)=> {
    //此回调处于第三方线程
    log(info); //用log打印具体的元素
    //常用调用：
    let year = info.year; //年
    let month = info.month; //月
    let day = info.day; //日
    //或者：
    year = info.y; //年
    month = info.m; //月
    day = info.d; //日
    //显示日期
    alert("日期",year+"-"+month+"-"+day);
});




//示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-16.#U65f6#U95f4#U9009#U62e9(#U65f6#U949f)

```javascript
//AIGame 官方示例


//24小时制:选择时间对话框
$tip.clock((info)=> {
    //此回调处于第三方线程
    log(info); //用log打印具体的元素
    //常用调用：
    let hour = info.hour; //时
    let minute = info.minute; //分
    //或者：
    hour = info.h; //时
    minute = info.m; //分
    //显示时间
    alert("时间",hour+":"+minute);
});




//示例结束
```


## $tip-#U963b#U585e#U5f0f#U5bf9#U8bdd#U6846-17.#U65f6#U95f4#U9009#U62e9(#U6eda#U8f6e)

```javascript
//AIGame 官方示例


//24小时制:选择时间对话框
$tip.time((info)=> {
    //此回调处于第三方线程
    log(info); //用log打印具体的元素
    //常用调用：
    let hour = info.hour; //时
    let minute = info.minute; //分
    //或者：
    hour = info.h; //时
    minute = info.m; //分
    //显示时间
    alert("时间",hour+":"+minute);
});




//示例结束
```


## $ui-#U4ea4#U4e92#U754c#U9762-01#U8fdb#U9636#U7528#U6cd5-01.#U52a8#U6001#U6dfb#U52a0#U63a7#U4ef6#U4e0e#U5220#U9664

```javascript
alert("注意","开始运行后,我会在10秒内添加9个卡片,最后1秒删除所有卡片");

//解析一个可以滑动的界面
let mainUi = $ui.layout(`
<ui>
    <statusbar/>
    <nested w="max">
        <linear w="max" id="mLayout" />
    </nested>
</ui>
`);
let mLayout = mainUi.id("mLayout");

$thread.create(()=> {
    for (let i = 0; i < 10; i ++) {
        sleep(1000);
        //由于我们需要动态的添加布局,所以每次都必须使用layout重新解析生成新的布局
        //因为view被添加后,已经归属于父容器了,就不允许添加到其他容器,因此view不能被重复使用(安卓机制)
        //所以需要重新使用layout解析生成新的布局
        let itemUi = $ui.layout(`
            <ui>
                <card w="max" id="mCard" margin="3">
                    <text text="我是卡片" margin="15" />
                </card>
            </ui>
            `);
        let card = itemUi.id("mCard");
        //[核心方法]直接在第三方线程操作view,因为已经封装好了,不需要手动调用ui线程操作view
        mLayout.addView(card);
    }
    //[核心方法]最后移除所有元素
    mLayout.removeAll();
    alert("结束","执行结束了");
    mainUi.finish();
}).start();



mainUi.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-01.appbar-#U5e94#U7528#U6761-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/01.appbar-应用条/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-02.button-#U6309#U94ae-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/02.button-按钮/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-03.button-group-#U6309#U94ae#U7ec4-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/03.button-group-按钮组/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-04.card-#U5361#U7247-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/04.card-卡片/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-05.check-#U591a#U9009#U6846-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/05.check-多选框/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-06.chip-#U5c0f#U7247-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/06.chip-小片/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-06.chip-group-#U5c0f#U7247#U7ec4-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/06.chip-group-小片组/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-07.drop-#U4e0b#U62c9#U6846-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/07.drop-下拉框/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-08.edit-#U7f16#U8f91#U5668-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/08.edit-编辑器/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-09.fab-#U60ac#U6d6e#U6309#U94ae-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/09.fab-悬浮按钮/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-10.hr-#U5206#U5272#U7ebf-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/10.hr-分割线/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-11.img-#U56fe#U7247-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/11.img-图片/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-12.input-#U8f93#U5165#U6846-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/12.input-输入框/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-13.ls-#U5217#U8868-main

```javascript
//解析布局获得ui对象
let ui = $ui.layout("example/$ui - 交互界面/13.ls-列表/ui.xml");
//返回按钮
ui.id("mAppbar").back(()=> {
    ui.finish();
});
//显示界面
ui.show();

//获取列表控件
let ls = ui.id("mLs");
//设置绑定数据(优先调用)
ls.bindHolder((holder,data,position)=> {
    //适配器会不断的创建layout标签中的视图放在holder中
    let tv = holder.id("mText");
    //data就是通过ls.flush传入进来的数组元素
    tv.setText(data);

    //[删除按钮]
    holder.id("delBut").click(()=> {
        $tip.show("删除","确定删除："+data+"吗?",()=> {
            //删除指定下标的元素
            ls.del(position);
        });
    });

    //[修改按钮]
    holder.id("edtBut").click(()=> {
        $tip.input("修改名称",data,(value)=> {
            //修改指定下标的元素
            ls.flush(value,position);
        });
    });
});
//设置一些基础的元素
ls.flush(["张三","李四","王五"]);

//获取按钮(点击就添加一个元素进去)
let i = 0;
ui.id("mAppbar").menu((title)=> {
    if (title == "添加元素") {
        i++;
        //列表添加一个数据
        ls.add("数据"+i);//还有一个函数 ls.add("数据",1); 添加到指定的位置中
        //列表滚动到最底部
        ls.scrollBottom();//还有函数 scrollTop() 滚动到顶部 scroll(index) 滚动到指定位置
    }
});



//..
```


## $ui-#U4ea4#U4e92#U754c#U9762-14.nav-#U5bfc#U822a#U680f-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/14.nav-导航栏/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-15.pager-#U6ed1#U52a8#U9875#U9762-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/15.pager-滑动页面/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}

//滑动页面(pager)与标签(tab)联动
let mPager = ui.id("mPager");
let mTab = ui.id("mTab");
if(mPager!=null&&mTab!=null){
    mPager.bind(mTab);
}

ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-16.progress-#U8fdb#U5ea6#U6761-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/16.progress-进度条/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-17.radio-#U5355#U9009#U6309#U94ae-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/17.radio-单选按钮/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-18.radio-group-#U5355#U9009#U6309#U94ae#U7ec4-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/18.radio-group-单选按钮组/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-19.rail-#U8f68#U9053#U5de5#U5177#U680f-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/19.rail-轨道工具栏/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-20.range-#U8303#U56f4#U6761-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/20.range-范围条/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-21.slider-#U62d6#U62fd#U6761-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/21.slider-拖拽条/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-22.statusbar-#U72b6#U6001#U680f-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/22.statusbar-状态栏/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-23.switch-#U5f00#U5173-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/23.switch-开关/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-24.text-#U6587#U672c-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/25.toolbar-工具栏/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-25.toolbar-#U5de5#U5177#U680f-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/25.toolbar-工具栏/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-26.webview-#U7f51#U9875#U63a7#U4ef6-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/26.webview-网页控件/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-27.log-#U65e5#U5fd7#U663e#U793a#U63a7#U4ef6-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/27.log-日志显示控件/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```


## $ui-#U4ea4#U4e92#U754c#U9762-28.video-#U89c6#U9891-main

```javascript
let ui = $ui.layout("example/$ui - 交互界面/28.video-视频/ui.xml");

let mAppbar = ui.id("mAppbar");

if(mAppbar!=null){
    mAppbar.back((view) => {
        ui.finish();
    });
}


ui.show();
```
