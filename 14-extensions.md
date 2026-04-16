# 扩展与插件 API

> 加载Dex/Apk/Jar/So扩展、插件系统、资源管理、Excel、文件选择器。

## 目录
- [LoadExtConfig - 扩展配置](#loadextconfig---扩展配置)
- [LoadSoConfig - So文件配置](#loadsoconfig---so文件配置)
- [$ext - 加载扩展](#ext---加载扩展)
- [$plugin - 插件系统](#plugin---插件系统)
- [$res - 资源管理器](#res---资源管理器)
- [$excel - 表格操作](#excel---表格操作)
- [FcConfig - 文件选择配置](#fcconfig---文件选择配置)
- [$fc - 文件选择器](#fc---文件选择器)

---

## LoadExtConfig - 加载扩展配置

- 更新时间:2026-01-30 19:32:58

> 加载扩展配置




#### const {List<String>} path;

> dex、apk、jar等拓展包的路径
> 
> 类型：字符串数组


#### const {List<LoadSoConfig>} so;

> so文件加载情况配置
> 
> 类型：LoadSoConfig[] so文件加载配置数组

---

## LoadSoConfig - 加载so文件配置

- 更新时间:2026-01-30 19:32:58

> 加载so文件配置




#### const {String} path;

> so文件路径
> 
> 类型：字符串


#### const {boolean} load;

> 是否加载so文件
> 
> 类型：布尔值

---

## $ext - 拓展:加载Dex,Apk,Jar,So

- 更新时间:2026-01-30 19:32:52

> 加载DexApkJarSo拓展API
> 
> $ext顾名思义就是"拓展"的意思，主要用来加载第三方库，拓展本应用中没有的功能。




#### loadApk(apkPath)

> 加载apk文件

- 参数 : apkPath {string} apk文件路径
- 返回 : {DexClassLoader} 类加载器
- 版本 : 1.2.5


```javascript
$ext.loadApk("/sdcard/测试.apk");
```


#### loadDex(dexPath)

> 加载dex文件
> 
> $ext中存在一个内置的缓存机制,被加载的dex文件会被生成一个唯一的id作为类加载器的标识,
> 
> 在起初加载dex文件的时候会保存id和类加载器对象
> 
> 当再次加载相同的dex文件时,会通过id直接取得类加载器对象来执行类
> 
> 如果想重新加载需要调用$ext.clear()清除id和类加载器

- 参数 : dexPath {string} dex文件路径
- 返回 : {DexClassLoader} 类加载器
- 版本 : 1.1.0


```javascript
$ext.loadDex("./res/demo.dex");
//开始使用dex中的类
```


#### loadDexs(paths)

> 加载多个dex文件

- 参数 : paths {string[]} dex文件路径
- 返回 : {DexClassLoader} 类加载器
- 版本 : 1.2.6


```javascript
//加载多个dex文件(传入所有dex文件的路径数组即可)
$ext.loadDexs(["/res/demo1.dex","/res/demo2.dex","/res/demo3.dex"]);
```


#### loadJar(jarPath)

> 加载jar文件
> 
> $ext中存在一个内置的缓存机制,被加载的jar文件会被生成一个唯一的id作为类加载器的标识,
> 
> 在起初加载jar文件的时候会保存id和类加载器对象
> 
> 当再次加载相同的jar文件时,会通过id直接取得类加载器对象来执行类
> 
> 如果想重新加载需要调用$ext.clear()清除id和类加载器
> 
> 注意:被加载的jar必须经过安卓开发环境(AndroidStudio)编译生成class字节码归档文件才可被加载

- 参数 : jarPath {string} jar文件路径
- 返回 : {DexClassLoader} 类加载器
- 版本 : 1.1.0


```javascript
$ext.loadJar("/res/demo.jar");
//开始使用jar中的类
```


#### loadJars(paths)

> 加载多个jar文件
> 
> 注意:被加载的jar必须经过安卓开发环境(AndroidStudio)编译生成class字节码归档文件才可被加载

- 参数 : paths {string[]} jar文件路径
- 返回 : {DexClassLoader} 类加载器
- 版本 : 1.2.6


```javascript
//加载多个jar文件(传入所有jar文件的路径数组即可)
$ext.loadJars(["/res/demo1.dex","/res/demo2.dex","/res/demo3.dex"]);
```


#### loadDex(options)

> 加载dex/so文件
> 
> 值得注意的就是so文件也有很多架构(x86_64,arm64_v8a等),根据自己手机的架构来选择需要加载的so文件(安卓特性);
> 此外:如果dex(java代码)中已经使用System.load(so);加载过的so文件不要重复加载,因为so文件只能被类加载器加载一次(安卓机制)

- 参数 : options {LoadExtConfig} 加载配置
- 返回 : {DexClassLoader} 类加载器
- 版本 : 1.1.0


```javascript
let options = {
    path:["dexOrJarPath"],//jar或者dex文件路径数组(可以传入多个dex或jar文件路径)
    so:[
         {path:"soPath", load:false},
         {
            path:"soPath",//so文件路径
            load:false //是否执行系统加载System.load(so);
         },
         //...
    ]
}
$ext.loadDex(options);
//开始使用dex里面的类
```


#### loadJar(options)

> 加载jar/so文件
> 
> 值得注意的就是so文件也有很多架构(x86_64,arm64_v8a等),根据自己手机的架构来选择需要加载的so文件(安卓特性);
> 此外:如果dex(java代码)中已经使用System.load(so);加载过的so文件不要重复加载,因为so文件只能被类加载器加载一次(安卓机制)
> 
> 注意:被加载的jar必须经过安卓开发环境(AndroidStudio)编译生成class字节码归档文件才可被加载

- 参数 : options {LoadExtConfig} 加载配置
- 返回 : {DexClassLoader} 类加载器
- 版本 : 1.1.0


```javascript
let options = {
    path:["dexOrJarPath"],//jar或者dex文件路径数组,可以传入多个dex或jar文件路径
    so:[
         {path:"soPath", load:false},
         {
            path:"soPath",//so文件路径
            load:false //是否执行系统加载System.load(so);
         },
         //...
    ]
}
$ext.loadJar(options);
//开始使用jar里面的类
```


#### loadApk(options)

> 加载apk/so文件

- 参数 : options {LoadExtConfig} 加载配置
- 返回 : {DexClassLoader} 类加载器
- 版本 : 1.2.5


```javascript
let options = {
    path:["apk路径"],数组格式,但是只支持一个apk路径,传入多个apk文件路径,只会加载第一个apk文件
    so:[
         {path:"soPath", load:false},
         {
            path:"soPath", //so文件路径
            load:false //是否执行系统加载System.load(so);
         },
         //...
    ]
}
$ext.loadApk(options);
//开始使用apk里面的类
```


#### clear()

> 清除缓存的类加载器
> 
> $ext中存在一个内置的缓存机制,被加载的jar/dex文件会被生成一个唯一的id作为类加载器的标识,
> 
> 在起初加载jar/dex文件的时候会保存id和类加载器对象
> 
> 当再次加载相同的jar/dex文件时,会通过id直接取得类加载器对象来执行类
> 
> 如果想重新加载需要调用$ext.clear()清除id和类加载器
> 
> 如果只是单纯的加载dex/jar文件,这个函数可以随便调用;
> 但是如果加载了so文件,这个函数最好只使用一次,因为so文件只能被一个类加载器加载一次
> 
> 就算不小心把加载过so文件的类加载器清空了也没有关系，重启app重新运行即可。

- 版本 : 1.1.0


```javascript
$ext.clear();
```


#### delete()

> 删除缓存文件
> 
> dex加载必须要在安卓的私有目录(安卓机制),所以每次加载的dex文件都会放在私有目录下面
> 
> 然而我们最主要只是拿到类加载器,当加载完后dex文件也就不需要了,所以可以调用这个函数来删除dex文件

- 版本 : 1.1.1


```javascript
$ext.delete();
```

---

## $plugin - 插件系统

- 更新时间:2026-01-30 19:32:54

> 插件系统
> 
> 本应用内置一个使用非常方便的插件系统，开发者可以开发自己的apk插件并且在这里进行调用。
> 
> 一个插件其实就是一个apk文件，它被安装在安卓手机上，之后就可以在本应用中使用$plugin进行调用。
> 
> 
> 和$ext不同的地方在于：
> 
> 1.$ext主要用于加载dex、jar、so、apk文件，$ext加载的是apk文件，无需安装apk文件，并且可以直接使用apk中的类。
> 
> 2.$plugin对象主要通过load("包名")加载已安装的插件apk，加载完成后，会返回一个主类对象，该对象中的函数可以直接调用，无需像$ext加载的apk那样需要导包调用。
> 
> 3.$plugin插件机制访问插件apk的资源更加方便。




#### load(packageName)

> 加载插件

- 参数 : packageName {string} 插件的包名 
- 返回 : {object} 插件的实例对象
- 版本 : 1.4.0


```javascript
//加载插件
let myObj = $plugin.load("com.example.myplugin");
//使用api
myObj.myApi();
```


#### ls()

> 获得插件列表

- 返回 : {AppInfo[]} 插件列表
- 版本 : 1.4.0


```javascript
//罗列所有插件应用
let infoList = $plugin.ls();
//打印信息
for (let info of infoList) {
    log("应用名:",info.appName);
    log("包名:",info.pkgName);
    //显示图标: info.icon.show();
}
```

---

## $res - 资源管理器

- 更新时间:2026-01-30 19:32:54

> 资源管理器
> 
> 针对脚本引擎设计的资源管理器，方便存储和读取资源，支持跨线程访问，在对于一些大型项目中，可以起到非常好的维护效果。




#### create(appName)

> 创建一个资源对象

- 参数 : appName {string} 应用名称,决定了资源文件存放的位置 
- 返回 : {AgRes} 资源对象
- 版本 : 1.0.0


```javascript
let res = $res.create("我的资源");
```


#### set(resName, resData)

> 设置一个资源

- 参数 : resName {string} 资源名称 
- 参数 : resData {object} 资源数据,就是js对象,可以直接把js对象存入进来,用的时候打点调用即可 
- 版本 : 1.0.0


```javascript
//(1)创建资源对象(指定名称)
let res = $res.create("我的资源");
//(2)添加资源
res.set("名字","张三");
```


#### get(resName)

> 获取一个资源

- 参数 : resName {string} 资源名称 
- 返回 : {object} 资源数据
- 版本 : 1.0.0


```javascript
//(1)创建资源对象(指定名称)
let res = $res.create("我的资源");
//(2)添加资源
res.set("名字","张三");
//(3)获取资源
log(res.get("名字"));
```


#### get(resName, defaultValue)

> 获取资源

- 参数 : resName {String} 资源名称 
- 参数 : defaultValue {String} 默认值 
- 返回 : {String} 资源值


```javascript
//如果本身就不存在数据，就会返回默认值
let data = $res.get("name","张三");
```


#### get(resName, defaultValue)

> 获取资源

- 参数 : resName {String} 资源名称 
- 参数 : defaultValue {float} 默认值 
- 返回 : {float} 资源值


```javascript
//如果本身就不存在数据，就会返回默认值
let data = $res.get("PI",3.14);
```


#### get(resName, defaultValue)

> 获取资源

- 参数 : resName {String} 资源名称 
- 参数 : defaultValue {int} 默认值 
- 返回 : {int} 资源值


```javascript
//如果本身就不存在数据，就会返回默认值
let data = $res.get("age",18);
```


#### get(resName, defaultValue)

> 获取资源

- 参数 : resName {String} 资源名称 
- 参数 : defaultValue {boolean} 默认值 
- 返回 : {boolean} 资源值


```javascript
//如果本身就不存在数据，就会返回默认值
let isBoy = $res.get("sex",false);
```


#### load(path)

> 加载本地资源到内部存储中
> 
> 本质上就是把sdcard下的资源文件拷贝到内部存储中

- 参数 : path {string} 本地资源路径,可以是相对路径,但前提是文件必须要存在 
- 返回 : {boolean} 是否加载成功
- 版本 : 1.1.4


```javascript
//先准备数据名称
let res = $res.create("我的资源");
//加载数据到应用内部存储空间中(导入时不会添加.res后缀名,所以要写全文件名)
res.load("/data.res");//sdcard/当前项目/data.res
//看看数据
log(res.cat());
```


#### ls()

> 列出所有资源名称

- 返回 : {string[]} 资源名称列表
- 版本 : 1.0.0


```javascript
//(1)创建资源对象(指定名称)
let res = $res.create("我的资源");
//(2)查询所有资源名称
let resList = res.ls();
log(resList);
```


#### cat()

> 查看当前资源内容
> 
> 本质上是将存储的js对象转换成格式化美化后的json字符串

- 返回 : {string} 资源内容
- 版本 : 1.0.0


```javascript
//(1)加载资源对象(指定名称)
let res = $res.create("我的资源");
//(2)获得资源内容
let content = res.cat();
alert("资源内容", content);
```


#### dump(path)

> 导出资源
> 
> 本质上是将内部存储的数据拷贝到指定路径下

- 参数 : path {string} 导出路径,可以使用相对路径,文件可以不存在,如果文件存在,则会覆盖 
- 返回 : {string} 导出路径
- 版本 : 1.0.0


```javascript
//先准备一点数据
let res = $res.create("我的资源");
res.set("人", {
    name: "张三",
    age: 16
});
//下载资源到当前项目的文件夹下(会自动添加.res后缀名)
res.dump("/data");//sdcard/当前项目/data.res
```

---

## $excel - 表格操作

- 更新时间:2026-01-30 19:32:51

> 表格操作
> 
> 用于读取和写入二维数组到表格中，这个库需要在安卓8+的系统上才能完美运行。




#### read(path)

> 读取第一个表格

- 参数 : path {String} 路径(支持相对路径)
- 返回 : {String[][]} 表格数据
- 版本 : 1.7.8


```javascript
//读取第一个表格数据
let data = $excel.read("data.xlsx");//相对路径
log(data);
// 输出:
// [
//    ["学号","姓名","年龄","性别","入学日期"],
//    ["2023001","张三","20","男","2023-09-01"],
//    ["2023002","李四","19","女","2023-09-01"],
//    ["2023003","王五","21","男","2022-09-01"],
//    ["2023004","赵六","20","女","2023-09-01"]
// ]
```


![](./img/228115506309900.png)

#### read(path, index)

> 读取表格

- 参数 : path {String} 路径(支持相对路径)
- 参数 : index {int} 表格索引
- 返回 : {String[][]} 表格数据
- 版本 : 1.7.8


```javascript
//读取第2个表格数据
let data = $excel.read("data.xlsx", 1);//相对路径
log(data);
// 输出:
// [
//    ["商品ID","商品名称","商品单价","库存"],
//    ["P001","笔记本电脑","4999","10"],
//    ["P002","智能手机","3999","25"],
//    ["P003","平板电脑","2499","18"],
//    ["P004","无线耳机","799","50"]
// ]
```


![](./img/228156133564800.png)

#### num(path)

> 表格数量

- 参数 : path {String} 路径(支持相对路径)
- 返回 : {int} 表格数量
- 版本 : 1.7.8


```javascript
//获取表格的数量
let sheetNum = $excel.num("data.xlsx");//相对路径
log(sheetNum);//输出:3
```


#### ls(path)

> 列表

- 参数 : path {String} 路径(支持相对路径)
- 返回 : {String[]} 表格名称列表
- 版本 : 1.7.8


```javascript
//获取表格的数量
let sheetList = $excel.ls("data.xlsx");//相对路径
log(sheetList);//输出:["班级表","商品表","部门表"]
```


#### loop(path, onSheet)

> 遍历所有表格

- 参数 : path {String} 路径(支持相对路径)
- 参数 : onSheet {(sheetName,sheetData)=>{}} 数据回调
- 版本 : 1.7.8


```javascript
//遍历所有表格数据
let data = $excel.loop("data.xlsx", (name, data) => {
    alert(name,data);
});
```


#### write(sheetName, sheetData, path)

> 写入表格

- 参数 : sheetName {String} 表格名称
- 参数 : sheetData {String[][]} 表格数据
- 参数 : path {String} 保存路径(不支持相对路径,必须是绝对路径)
- 版本 : 1.7.8


```javascript
//数据
let sheetData = [
    ["姓名", "年龄"],
    ["小红", "18"],//注意必须都是字符串类型
    ["小明", "19"]
];
//表名
let sheetName = "我的表格";
//路径(必须是绝对路径)
let savePath = "/sdcard/demo.xlsx";
$excel.write(sheetName, sheetData, savePath);
```


![](./img/227580225758600.png)

---

## FcConfig - 文件选择配置

- 更新时间:2026-01-30 19:32:52

> 文件选择配置




#### const {String} mode;

> 选择模式:多选或者单选(single,multi)


#### const {String} type;

> 选择类型:文件还是目录,还是两者都(file,mkdir,all)


#### const {String} path;

> 默认路径 /sdcard


#### const {String} root;

> 最高根路径 /sdcard


#### const {String} ext;

> 后缀过滤(使用逗号分割)

---

## $fc - 文件选择器

- 更新时间:2026-01-30 19:32:52

> 文件选择器




#### show(callback)

> 显示文件选择器
> 
> 默认是单选文件

- 参数 : callback {(files)=>{}}回调
- 版本 : 1.0.0


```javascript
$fc.show((files)=> {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
});
```


#### show(callback, options)

> 显示文件选择器

- 参数 : callback {(files)=>{}}回调
- 参数 : options {object} 配置参数
- 版本 : 1.0.0


```javascript
//多选：文件和目录
$fc.show((files)=> {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "m",
    type: "a"
});
//配置参数如下:
let options = {
    mode: "m", //多选模式("single","multi")写一个字母就行了
    type: "a", //文件和目录("file","mkdir","all")写一个字母就行了
    root: "/sdcard", //[可选]最高根路径
    path: "/sdcard/Pictures", //[可选]默认路径
    ext: "jpg,png" //[可选]后缀过滤
}
```