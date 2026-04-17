# 示例：文件/网络/数据库


## $excel-#U8868#U683c#U64cd#U4f5c-01.#U8bfb#U53d6#U7b2c1#U4e2a#U8868

```javascript
//官方示例


//读取第一个表格数据
let data = $excel.read("example/$excel - 表格操作/data.xlsx");//相对路径
alert("表格数据",data);




//示例结束
```


## $excel-#U8868#U683c#U64cd#U4f5c-02.#U8bfb#U53d6#U7b2c2#U4e2a#U8868

```javascript
//官方示例


//读取第2个表格数据:指定下标
let data = $excel.read(
"example/$excel - 表格操作/data.xlsx" ,//相对路径
 1 //表格下标
);
alert("表格数据",data);



//示例结束
```


## $excel-#U8868#U683c#U64cd#U4f5c-03.#U83b7#U53d6#U8868#U683c#U6570#U91cf

```javascript
//官方示例


//获取表格数量
let sheetNum = $excel.num("example/$excel - 表格操作/data.xlsx");
alert("表格数量",sheetNum);



//示例结束
```


## $excel-#U8868#U683c#U64cd#U4f5c-04.#U7f57#U5217#U8868#U683c#U540d#U79f0

```javascript
//官方示例


//获取表格名称列表
let sheetList = $excel.ls("example/$excel - 表格操作/data.xlsx");
alert("表格名称",sheetList);



//示例结束
```


## $excel-#U8868#U683c#U64cd#U4f5c-05.#U904d#U5386#U6240#U6709#U8868#U683c#U6570#U636e

```javascript
//官方示例


//遍历所有表格数据
let path = "example/$excel - 表格操作/data.xlsx";
$excel.loop(path, (name, data) => {
    alert(name,data);
});



//示例结束
```


## $excel-#U8868#U683c#U64cd#U4f5c-06.#U5199#U5165#U6570#U636e#U5230#U8868#U683c

```javascript
//官方示例


//数据
let sheetData = [
    ["姓名", "年龄"],
    ["小红", "18"],//注意必须都是字符串类型
    ["小明", "19"]
];
//表名
let sheetName = "我的表格";
//路径
let savePath = "/sdcard/demo.xlsx";
$excel.write(sheetName, sheetData, savePath);

toast("写入完毕");

//之后再读取出来看看
sleep(1000);
alert("表格数据",$excel.read(savePath));

//示例结束
```


## $ext-#U52a0#U8f7dApkDexJarSo#U6587#U4ef6-#U52a0#U8f7d#U5355#U4e2aapk#U6587#U4ef6#U793a#U4f8b

```javascript
//官方示例

//先加载apk文件
$ext.loadApk("example/$ext - 加载ApkDexJarSo文件/libs/apk/lib.apk");

//开始直接使用apk中的类(参考源代码)
let demo = new org.aigame.apk.ApkDemo();

//调用类中的方法
alert("示例",demo.getStr());



//示例结束
```


## $ext-#U52a0#U8f7dApkDexJarSo#U6587#U4ef6-#U52a0#U8f7d#U5355#U4e2adex#U6587#U4ef6#U793a#U4f8b

```javascript
//官方示例

//先加载dex文件
$ext.loadDex("example/$ext - 加载ApkDexJarSo文件/libs/dex/classes.dex");

//开始直接使用dex中的类(参考源代码)
let demo = new org.aigame.demo.DexDemo();

//调用类中的方法
alert("示例",demo.getStr());



//示例结束
```


## $ext-#U52a0#U8f7dApkDexJarSo#U6587#U4ef6-#U52a0#U8f7d#U5355#U4e2ajar#U6587#U4ef6#U793a#U4f8b

```javascript
//官方示例

//先加载jar文件
$ext.loadJar("example/$ext - 加载ApkDexJarSo文件/libs/jar/classes.jar");

//开始直接使用dex中的类(参考源代码)
let demo = new org.aigame.demo.JarDemo();

//调用类中的方法
alert("示例",demo.getStr());



//示例结束
```


## $ext-#U52a0#U8f7dApkDexJarSo#U6587#U4ef6-#U52a0#U8f7d#U591a#U4e2adex#U6587#U4ef6#U793a#U4f8b

```javascript
//官方示例

//加载多个dex文件
let basePath = "example/$ext - 加载ApkDexJarSo文件/libs/dexs/多个dex";

//拼接目录
let paths = [
    `${basePath}/classes1.dex`,
    `${basePath}/classes2.dex`,
    `${basePath}/classes3.dex`
];

//加载多个dex文件(传入所有dex文件的路径数组即可)
$ext.loadDexs(paths);

//开始直接使用dex中的类(参考源代码)
let dex1 = new org.aigame.dex1.DexDemo();//classes1.dex
let dex2 = new org.aigame.dex2.DexDemo();//classes2.dex
let dex3 = new org.aigame.dex3.DexDemo();//classes3.dex

//调用类中的方法
alert("示例",dex1.getStr()+"\n"+dex2.getStr()+"\n"+dex3.getStr());



//示例结束
```


## $ext-#U52a0#U8f7dApkDexJarSo#U6587#U4ef6-#U52a0#U8f7d#U591a#U4e2ajar#U6587#U4ef6#U793a#U4f8b

```javascript
//官方示例

//加载多个jar文件
let basePath = "example/$ext - 加载ApkDexJarSo文件/libs/jars/多个jar文件";

//拼接目录
let paths = [
    `${basePath}/classes1.jar`,
    `${basePath}/classes2.jar`,
    `${basePath}/classes3.jar`
];

//加载多个jar文件(传入所有jar文件的路径数组即可)
$ext.loadJars(paths);

//开始直接使用jar中的类(参考源代码)
let jar1 = new org.aigame.jar1.JarDemo();//classes1.jar
let jar2 = new org.aigame.jar2.JarDemo();//classes2.jar
let jar3 = new org.aigame.jar3.JarDemo();//classes3.jar

//调用类中的方法
alert("示例",jar1.getStr()+"\n"+jar2.getStr()+"\n"+jar3.getStr());



//示例结束
```


## $ext-#U52a0#U8f7dApkDexJarSo#U6587#U4ef6-#U52a0#U8f7ddex#U548cso#U6587#U4ef6#U793a#U4f8b

```javascript
//官方示例

//先加载dex文件
$ext.loadDex({
    path:["example/$ext - 加载ApkDexJarSo文件/libs/dex_so/classes.dex"],
    so:[
        {
            //根据自己手机的情况,选正确的架构,不然so文件的C代码无法运行
            path:"example/$ext - 加载ApkDexJarSo文件/libs/dex_so/lib/arm64-v8a/libdemo.so",
            load:false,//因为在dex的类中已经静态加载了so文件,所以不能再重复加载了(安卓机制)
        }
    ]
});

//开始直接使用dex中的类(参考源代码)
let demo = new org.aigame.demo.CallC();

//调用类中的方法
alert("示例",demo.getStr());



//示例结束
```


## $ext-#U52a0#U8f7dApkDexJarSo#U6587#U4ef6-#U52a0#U8f7djar#U548cso#U6587#U4ef6#U793a#U4f8b

```javascript
//官方示例


//先加载jar文件
$ext.loadJar({
    path:["example/$ext - 加载ApkDexJarSo文件/libs/jar_so/classes.jar"],
    so:[
        {
            //根据自己手机的情况,选正确的架构,不然so文件的C代码无法运行
            path:"example/$ext - 加载ApkDexJarSo文件/libs/jar_so/lib/arm64-v8a/libdemo.so",
            load:false,//因为在jar的类中已经静态加载了so文件,所以不能再重复加载了(安卓机制)
        }
    ]
});

//开始直接使用jar中的类(参考源代码)
let demo = new org.aigame.demo.JarCallC();

//调用类中的方法
alert("示例",demo.getStr());



//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-01.#U7f57#U5217#U6587#U4ef6

```javascript
//AIGame 官方示例

//准备路径
let path = "/sdcard";
//罗列出文件
let files = $file.ls(path);

for(let i = 0 ; i < files.size() ; i++){
    log(files.get(i));
}

log("罗列(使用过滤器)");
let files_A = $file.ls(path,(path)=>{
    let fileName = $file.name(path);
    //如果文件名称以'.'开始,那么就通过
    return $str.startWith(fileName, ".");
});

//找到隐藏文件夹
for(let i = 0 ; i < files_A.size() ; i++){
    log(files_A.get(i));
}


//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-02.#U5224#U65ad#U6587#U4ef6

```javascript
//AIGame 官方示例

//false:文件不存在或存在是目录
let isFile = $file.isFile("/sdcard/a.txt");
log("是否是文件",isFile);

//是否是目录
let isDir = $file.isDir("/sdcard");
log("是否是目录",isDir);

//是否是空目录
let isEmptyDir = $file.isEmptyDir("/sdcard");
log("是否是空目录",isEmptyDir);

//是否是空文件或文件夹
let isEmpty = $file.isEmpty("/sdcard");
log("是否是空文件",isEmpty);

//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-03.#U62fc#U63a5#U8def#U5f84

```javascript
//AIGame 官方示例


let path1 = $file.join("sdcard", "Pictures");

log(path1);

let path2 = $file.join("sdcard", "Pictures", "我的项目", "res");

log(path2);

//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-04.#U521b#U5efa#U6587#U4ef6

```javascript
//AIGame 官方示例

$file.create("/sdcard/测试.txt");


//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-05.#U521b#U5efa#U76ee#U5f55

```javascript
//AIGame 官方示例

let path = "/sdcard/AAA";
$file.mkdir(path);

//判断目录是否存在
if($file.exists(path)){
    log("目录创建完成");
}

//最后删除(没必要留着)
$file.del(path);

//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-06.#U8bfb#U53d6#U6587#U4ef6

```javascript
//AIGame 官方示例

//开始读取文件
let content = $file.read("/sdcard/测试.txt");
log(content);

//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-07.#U5199#U5165#U6587#U4ef6

```javascript
//AIGame 官方示例


$file.write("我是内容","/sdcard/测试.txt");


//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-08.#U8ffd#U52a0#U6587#U4ef6

```javascript
//AIGame 官方示例


$file.append("我是内容","/sdcard/测试.txt");

//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-09.#U62f7#U8d1d#U6587#U4ef6

```javascript
//AIGame 官方示例

let from = "/sdcard/测试.txt";
let to = "/sdcard/测试2.txt";
$file.copy(from, to);

//最后判断文件是否存在
if($file.exists(to)){
    log("拷贝成功");
}

//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-10.#U79fb#U52a8#U6587#U4ef6

```javascript
//AIGame 官方示例

let from = "/sdcard/测试.txt";
let to = "/sdcard/Pictures/测试2.txt";
$file.move(from, to);

//最后判断文件是否存在
if($file.exists(to)){
    log("移动成功");
}


//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-11.#U5220#U9664#U6587#U4ef6

```javascript
//AIGame 官方示例

let path = "/sdcard/Pictures/测试2.txt";
$file.del(path);

//最后判断文件是否存在
if(!$file.exists(path)){
    log("删除成功");
}


//示例结束
```


## $file-#U6587#U4ef6#U7cfb#U7edf-12.#U91cd#U547d#U540d

```javascript
//AIGame 官方示例

let from = "/sdcard/测试.txt";
let to = "/sdcard/测试2.txt";
$file.rename(from, to);

//最后判断文件是否存在
if($file.exists(to)){
    log("命名成功");
}


//示例结束
```


## $http-#U7f51#U7edc#U8bf7#U6c42-01.post#U53d1#U9001#U5b57#U7b26#U4e32

```javascript
//此示例的服务器我已经临时搭建,可以直接运行看到效果

let ip = "47.105.110.90";
let port = "8347";
let mode = "postString";

let res = $http.post({
    url: `http://${ip}:${port}/org/aigame/pro/example/${mode}`,
    data: "本地字符串",
});


alert("结果",res.str());
```


## $http-#U7f51#U7edc#U8bf7#U6c42-01.post#U53d1#U9001json

```javascript
//此示例的服务器我已经临时搭建,可以直接运行看到效果

let ip = "47.105.110.90";
let port = "8347";
let mode = "postJson";

let res = $http.post({
    url: `http://${ip}:${port}/org/aigame/pro/example/${mode}`,
    //直接发送json对象或者json字符串也可以
    data: {
        sex:"女"
    },
});


alert("结果",res.str());
```


## $http-#U7f51#U7edc#U8bf7#U6c42-03.DeepSeek#U8c03#U7528#U793a#U4f8b

```javascript
let url = "https://api.deepseek.com/chat/completions";

alert("注意","请到代码中填写ApiKey才能调用成功!");

//自己填写key
let apiKey = ""; //类似于"sk-m451xc526v394f82b90163272c577s"

let res = $http.post({
    url: url,
    head: {
        "Content-Type": "application/json",
        "Authorization": "Bearer "+apiKey,
    },
    data: {
            model: "deepseek-chat",
            messages: [
            {
                role: "system",
                content: "You are a helpful assistant."
            },
            {
                role: "user",
                content: "Hello!"
            }],
            stream: false
    }
});


/*
原理很简单，就是把官方网站提供的curl调用示例，用javascript翻译过来就行了

curl https://api.deepseek.com/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <DeepSeek API Key>" \
  -d '{
        "model": "deepseek-chat",
        "messages": [
          {"role": "system", "content": "You are a helpful assistant."},
          {"role": "user", "content": "Hello!"}
        ],
        "stream": false
      }'

*/


alert("请求结果",res.str());

/*
注意：res.str();是返回响应的字符串

如果你想直接操作json对象，那么请调用 res.json(); 然后打点调属性即可


*/
```


## $http-#U7f51#U7edc#U8bf7#U6c42-04.#U4e0b#U8f7d#U6587#U4ef6

```javascript
let url = "https://pics0.baidu.com/feed/f11f3a292df5e0feee2783e88baf3fa75fdf727e.jpeg?token=4afc91463326e4f4a44e2cde691a54a0";
let path = "/sdcard/美女.png";

//异步下载
$http.download(url,path,(cur,total,percent)=>{
    log("下载进度",percent);
},()=>{
    log("下载完毕，正在显示美女图片...");
    showImg(path);
},(res)=>{
    log("下载失败",res);
});
```


## $qr-#U4e8c#U7ef4#U7801#U5de5#U5177-#U8bc6#U522b#U672c#U5730

```javascript
let path = "/sdcard/qr.png";
if ($file.exists(path)) {
    //显示图片
    showImg(path);
    //解析这个二维码内容
    let content = $qr.parse(path);
    //显示内容
    alert("二维码内容",content);
}else{
    alert("本地图片","图片不存在:\n"+path);
}
```


## $res-#U8d44#U6e90#U7ba1#U7406#U5668-01.#U5b58#U50a8#U5bf9#U8c61

```javascript
//AIGame 官方示例

//(1)创建资源对象(指定名称)
let res = $res.create("我的资源");

//(2)添加资源

//1.存储一个字符串
res.set("名字","张三");

//2.存储一个对象
res.set("对象", {
    名字: "翠花",
    年龄: 18,
    身高: 175,
    体重: 98,
    儿子: {
        名字: "小安",
        年龄: 1,
        身高: 45,
    }
});

//3.存储一个列表
res.set("列表",[1,2,3]);


//(3)获取资源
log(res.get("名字"));
log(res.get("对象").名字);
log(res.get("对象").年龄);
log(res.get("对象").身高);
log(res.get("对象").体重);
log(res.get("对象").儿子.名字);
log(res.get("对象").儿子.年龄);
log(res.get("对象").儿子.身高);
log(res.get("列表"));




//示例结束
```


## $res-#U8d44#U6e90#U7ba1#U7406#U5668-02.#U67e5#U8be2#U8d44#U6e90#U540d#U79f0

```javascript
//AIGame 官方示例

//(1)创建资源对象(指定名称)
let res = $res.create("我的资源");

//(2)查询所有资源名称
let resList = res.ls();

log(resList);





//示例结束
```


## $res-#U8d44#U6e90#U7ba1#U7406#U5668-03.#U5bfc#U51fa#U8d44#U6e90

```javascript
//AIGame 官方示例

//(1)加载资源对象(指定名称)
let res = $res.create("我的资源");

//(2)导出资源
res.dump("sdcard/Pictures/示例/$res/资源.res");


//示例结束
```


## $sqlite-#U8f7b#U91cf#U6570#U636e#U5e93-01.#U94fe#U63a5#U6570#U636e#U5e93

```javascript
//示例开始

let hasOpen = $sqlite.open("mData");
if(hasOpen){
    log("链接成功");
}

//示例结束
```


## $sqlite-#U8f7b#U91cf#U6570#U636e#U5e93-02.#U521b#U5efa#U8868

```javascript
//示例开始

let hasTable = $sqlite.newTab("table1",["name","sex","age"]);
if(hasTable){
    log("建表成功");
}

//示例结束
```


## $sqlite-#U8f7b#U91cf#U6570#U636e#U5e93-03.#U6dfb#U52a0#U6570#U636e

```javascript
//示例开始

//其实此函数等价于 $sqlite.exe("INSERT INTO table1 (name, sex, age) VALUES ('张三', '男', 20)");
let hasAdd = $sqlite.add("table1",{
    name:"张三",
    sex:"男",
    age:20
});
if(hasAdd){
    log("添加成功");
}

//示例结束
```


## $sqlite-#U8f7b#U91cf#U6570#U636e#U5e93-04.#U66f4#U65b0#U6570#U636e

```javascript
//示例开始

let okUpdate = $sqlite.update("table1", {
    name: "张三",
    sex: "女",
    age: 20
},"name='张三'");
if (okUpdate) {
    log("更新成功");
}

//示例结束
```


## $sqlite-#U8f7b#U91cf#U6570#U636e#U5e93-05.#U67e5#U8be2#U6570#U636e

```javascript
//示例开始

//即使是报错也不会返回null，而是返回空列表，因此可以不用判断数据是否为空
let result = $sqlite.ls("table1");
for(let item of result){
    log(item);
}

//示例结束
```


## $sqlite-#U8f7b#U91cf#U6570#U636e#U5e93-06.#U5220#U9664#U8868

```javascript
//示例开始

let hasDel = $sqlite.delTab("table1");
if(hasDel){
    log("删除表成功");
}

//示例结束
```


## $sqlite-#U8f7b#U91cf#U6570#U636e#U5e93-07.#U5173#U95ed#U94fe#U63a5

```javascript
//示例开始

let okFinish = $sqlite.close();
if(okFinish){
    log("结束操作");
}

//示例结束
```


## $sqlite-#U8f7b#U91cf#U6570#U636e#U5e93-08.#U5220#U9664#U6570#U636e#U5e93

```javascript
//示例开始

//无需打开数据库，直接就能删除数据库文件
let hasDelDb = $sqlite.delDb("mData");
if(hasDelDb){
    log("删库成功");
}

//示例结束
```


## $sqlite-#U8f7b#U91cf#U6570#U636e#U5e93-09.#U6267#U884csql

```javascript
//示例开始

//删除表
$sqlite.exe("drop table if exists table1");



//示例结束
```


## $ws-WebSocket-#U57fa#U7840#U4f7f#U7528

```javascript
//AIGame 官方示例

//返回的ws是经过封装的WebSocket对象(不是okhttp3.WebSocket原生对象)
let ws = $ws.create("wss://echo.websocket.org");

//设置监听
ws.onOpen((res,ws)=> {
    //当成功连接时回调(此函数可以不用设置，拥有默认回调:打印信息)
    console.log("链接成功");
    //参数说明：
    // res: okhttp3.Response (参考okhttp3文档)
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onClosed((code,reason,ws)=> {
    //当关闭后回调(此函数可以不用设置，拥有默认回调:打印信息)
    console.log("关闭成功");
    //参数说明：
    // code:   int    数字
    // reason: String 字符串
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onClosing((code,reason,ws)=> {
    //处于关闭时回调(此函数可以不用设置，拥有默认回调:打印信息)
    console.log("正在关闭");
    //参数说明：
    // code:   int    数字
    // reason: String 字符串
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onFail((err,res,ws)=> {
    //出现异常时回调(此函数可以不用设置，拥有默认回调:打印信息)
    console.log("出现异常",err);
    //参数说明：
    // err: Throwable
    // res: okhttp3.Response (参考okhttp3文档)
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onMsgStr((str, ws)=> {
    //接收到字符串信息时回调
    console.log("收到字符串：",str);
    //参数说明：
    // str: String 字符串数据
    // ws: okhttp3.WebSocket (参考okhttp3文档)
})
.onMsgByte((bs)=> {
    //接收到字节数据时回调
    console.log("收到二进制消息：大小 ", bs.size());
    console.log("hex: ", bs.hex());
    console.log("base64: ", bs.base64());
    console.log("md5: ", bs.md5());
    console.log("bytes: ", bs.toByteArray());
    //参数说明：
    // bs: okio.ByteString (参考okhttp3文档)
});

//发送字符串消息
ws.send("Hello AIGame!");

//发送二进制消息
//ws.send([10,15,1,1,0,5]);



//示例结束
```
