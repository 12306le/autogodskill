# 文件与存储 API

> 文件系统操作、键值存储、SQLite数据库。

## 目录
- [$file - 文件系统](#file---文件系统)
- [$storage - 应用内存储](#storage---应用内存储)
- [$sqlite - 轻量数据库](#sqlite---轻量数据库)

---

## $file - 文件系统

- 更新时间:2026-01-30 19:32:52

> 文件系统
> 
> 文件系统本身是用来操作外部存储(sdcard)文件的，但是部分函数也可以操作assets目录(app打包后的项目目录)下的文件。
> 
> 如果你希望通过$file操作assets下的文件，你需要知道如下规则：
> 
> 1.assets中的文件夹不能以_开头(安卓机制)否则无法读取文件
> 
> 2.assets只能进行读取操作，因此我们可以进行的操作有：罗列文件、拷贝文件、读取文件




#### uri(path)

> 获得Uri对象
> 
> 通过文件提供器{FileProvider}来解析文件路径，获得{Uri}对象。
> 
> 如果你想单纯的解析字符串构建Uri对象，那么可以使用$http.uri("uriStr");函数
> 
> 该函数只能操作外部存储(sdcard)文件，不能操作assets目录下的文件。

- 参数 : path {String} 路径 
- 返回 : {Uri} Uri对象
- 版本 : 1.3.7


```javascript
//一般用来获取图片uri
let uri = $file.uri("/storage/emulated/0/Pictures/小红.png");
```


#### open(path)

> 获得File对象
> 
> 该函数本质上是一个拼接函数，无论传入的path是否存在，都会根据构想返回一个完整路径。

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {File} 文件对象
- 版本 : 1.0.0


```javascript
//获得res目录
let file = $file.open("res");
alert("文件对象",file);///storage/emulated/0/Pictures/API教学/res
```


#### isFile(path)

> 是否是文件
> 
> 如果传入的路径不存在或者不是目录都会返回false，该函数只能操作外部存储(sdcard)文件，不能操作assets目录下的文件。

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {boolean} 是否是文件
- 版本 : 1.0.0


```javascript
//是否是文件
log($file.isFile("res"));//false
log($file.isFile("main.js"));//true
```


#### isDir(path)

> 是否是文件夹
> 
> 如果传入的路径不存在或者不是目录都会返回false，该函数只能操作外部存储(sdcard)文件，不能操作assets目录下的文件。

- 参数 : path {string} 路径 
- 返回 : {boolean} 是否是文件夹
- 版本 : 1.0.0


```javascript
//是否是目录
log($file.isDir("res"));//true
log($file.isDir("main.js"));//false
```


#### isEmptyDir(path)

> 是否是空文件夹
> 
> 只有当目标路径是目录并且存在文件的时候才会返回false，如果文件不存在或者不是目录都会返回true。

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {boolean} 是否是空文件夹
- 版本 : 1.0.0


```javascript
//是否是空目录
log($file.isEmptyDir("res"));//false
log($file.isEmptyDir("xml"));//true
```


#### isEmpty(path)

> 是否是空文件或文件夹
> 
> 如果不存在则返回false
> 
> 如果是文件则判断文件内容是否为空
> 
> 如果是文件夹则判断文件夹是否为空

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {boolean} 是否是文件夹
- 版本 : 1.0.0


```javascript
//是否是空文件或文件夹
log($file.isEmpty("res"));//false
log($file.isEmpty("xml"));//true
log($file.isEmpty("main.js"));//false
```


#### join(parent, child)

> 路径拼接

- 参数 : parent {string} 路径(不支持相对路径) 
- 参数 : child {string} 路径(不支持相对路径) 
- 返回 : {string} 路径
- 版本 : 1.0.0


```javascript
let path = $file.join("sdcard", "Pictures");
alert("路径",path);
```


#### join(path)

> 拼接路径

- 参数 : path {string[]} 路径数组(不支持相对路径) 
- 返回 : {string} 拼接好的路径
- 版本 : 1.0.0


```javascript
let path = $file.join(["sdcard", "Pictures", "我的项目", "res"]);
alert("路径",path);
```


#### create(path)

> 创建文件
> 
> 如果目录不存在,则会自动创建目录。此函数只能操作外部存储(sdcard)文件，不能操作assets目录下的文件。

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {boolean} 是否创建成功(文件存在会返回false)
- 版本 : 1.0.0


```javascript
$file.create("xml/res/test.js");
```


#### mkdir(path)

> 创建目录
> 
> 只能操作外部存储(sdcard)目录，不能操作assets目录下的目录。

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {boolean} 是否创建成功
- 版本 : 1.0.0


```javascript
$file.mkdir("xml/kir");
```


#### exists(path)

> 路径是否存在

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {boolean} 是否存在
- 版本 : 1.0.0


```javascript
$file.create("./测试文件夹/a.js");
if($file.exists("./测试文件夹/a.js")){
    alert("文件","路径存在");
}
```


#### ensureDir(path)

> 确保文件夹存在
> 
> 如果路径中的目录不存在则会创建目录

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {string} 路径
- 版本 : 1.0.0


```javascript
//创建目录:/测试文件夹/demo
$file.ensureDir("./测试文件夹/demo/a.js");
```


#### read(path)

> 读取文件
> 
> 此函数支持读取assets中的文件，适用于打包app后读取文本文件。在未打包时将会读取sdcard上的文件。

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {string} 文本内容
- 版本 : 1.0.0


```javascript
//开始读取文件
let content = $file.read("./main.js");
alert("内容",content);
```


#### read(path, encoding)

> 读取文件
> 
> 此函数支持读取assets中的文件，适用于打包app后读取文本文件。在未打包时将会读取sdcard上的文件。

- 参数 : path {string} 路径(支持相对路径) 
- 参数 : encoding {string} 编码 
- 返回 : {string} 文本内容
- 版本 : 1.0.0


```javascript
let content = $file.read("./main.js","gbk");
alert("内容",content);
```


#### reads(path)

> 读取文件行
> 
> 此函数支持读取assets中的文件，适用于打包app后读取文本文件。在未打包时将会读取sdcard上的文件。

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {string[]} 文件行列表
- 版本 : 1.0.0


```javascript
let list = $file.reads("./main.js");
alert("内容",list);
```


#### readByte(path)

> 读取文件字节
> 
> 此函数支持读取assets中的文件，适用于打包app后读取二进制文件。在未打包时将会读取sdcard上的二进制文件。

- 参数 : path {string} 路径 
- 返回 : {byte[]} 文件字节
- 版本 : 1.0.0


```javascript
let data = $file.readByte("./main.js");
log("内容:",data);
```


#### write(content, path)

> 写入文件
> 
> 只适用于写入到外部存储

- 参数 : content {string} 内容 
- 参数 : path {string} 路径(支持相对路径) 
- 版本 : 1.0.0


```javascript
$file.write("我是内容","./xml/a.js");
```


#### write(content, path, encoding)

> 写入文件
> 
> 只适用于写入到外部存储

- 参数 : content {string} 内容 
- 参数 : path {string} 路径 
- 参数 : encoding {string} 编码 
- 版本 : 1.0.0


```javascript
$file.write("我是内容","./code/a.js","GBK");
```


#### writes(lines, path)

> 写入行数据
> 
> 只适用于写入到外部存储

- 参数 : lines {string[]} 行数据 
- 参数 : path {string} 路径(支持相对路径) 
- 版本 : 1.0.0


```javascript
$file.writes(["我是内容1","我是内容2","我是内容3"],"./code/a.js");
```


#### add(content, path)

> 追加文件
> 
> 只适用于写入到外部存储

- 参数 : content {string} 内容 
- 参数 : path {string} 路径(支持相对路径) 
- 版本 : 1.0.0


```javascript
//追加一行字符并且换行
$file.add("我是新的内容\n","./code/a.js");
```


#### adds(lines, path)

> 追加行数据
> 
> 只适用于写入到外部存储

- 参数 : lines {string[]} 行数据 
- 参数 : path {string} 路径(支持相对路径) 
- 版本 : 1.0.0


```javascript
//无需换行符号,自动换行
$file.adds(["追加01","追加02","追加03"],"./code/a.js");
```


#### writeByte(bytes, path)

> 写入文件
> 
> 只适用于写入到外部存储

- 参数 : bytes {byte[]} 内容 
- 参数 : path {string} 路径(支持相对路径) 
- 版本 : 1.0.0


```javascript
$file.writeByte([09,46,36,7,89,34],"./xml/mFile.txt");
```


#### copy(src, dest)

> 拷贝文件
> 
> 支持将assets文件拷贝到外部存储，也支持将外部存储文件拷贝到指定路径中，虽然目标路径支持书写相对路径，但是建议源路径使用相对路径，而目标路径最好用绝对路径。

- 参数 : src {string} 源(支持相对路径) 
- 参数 : dest {string} 目标(支持相对路径) 
- 版本 : 1.6.8


```javascript
//把assets文件拷贝到sdcard上
$file.copy("res/a.txt","/sdcard/Pictures/测试项目/res/a.txt");
```


#### move(src, dest)

> 移动文件或文件夹
> 
> 此函数只适用于操作外部存储文件

- 参数 : src {string} 源文件夹(支持相对路径) 
- 参数 : dest {string} 目标文件夹(支持相对路径) 
- 版本 : 1.0.0


```javascript
//把位于modules文件夹下的所有文件都移动到xml下
//注意传入的都是目录(可以是相对路径)
let ok = $file.move("modules","xml");
if(ok){
    alert("移动文件","成功");
}else{
    alert("移动文件","失败");
}
//移动文件的话,src必须是存在的(支持相对路径)
let ok = $file.move("res/code.js","/");
if(ok){
    alert("移动文件","成功");
}else{
    alert("移动文件","失败");
}
```


#### rename(src, dest)

> 重命名文件
> 
> 此函数只适用于操作外部存储文件

- 参数 : src {string} 源 
- 参数 : dest {string} 目标 
- 返回 : {boolean} 是否重命名成功
- 版本 : 1.0.0


```javascript
let ok = $file.rename("run.js","res/code.js");
if(ok){
    alert("重命名","成功");
}else{
    alert("重命名","失败");
}
```


#### size(path)

> 获取文件大小
> 
> 如果文件不存在,则返回0，此函数只适用于操作外部存储文件

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {number} 文件大小
- 版本 : 1.0.0


```javascript
let size = $file.size("./xml/mFile.txt");
alert("文件大小",size);//6(字节)
```


#### sizeStr(size)

> 获取文件可视化大小
> 
> 如果文件不存在，则返回0b，此函数只适用于操作外部存储文件

- 参数 : size {long} 文件长度
- 返回 : {string} 文件大小
- 版本 : 1.0.0


```javascript
let size = $file.size(1099);
alert("文件大小",size);//6(字节)
```


#### sizeStr(path)

> 获取文件可视化大小
> 
> 如果文件不存在，则返回0b，此函数只适用于操作外部存储文件

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {string} 文件大小(格式化单位)
- 版本 : 1.0.0


```javascript
let size = $file.sizeStr("./xml/mFile.txt");
alert("文件大小",size);//6 B
```


#### name(path)

> 文件名称
> 
> 该函数本质上就是字符串操作，解析得到文件名称。

- 参数 : path {string} 路径 
- 返回 : {string} 文件名称
- 版本 : 1.0.0


```javascript
let fn = $file.name("./xml/mFile.txt");
alert("文件名称",fn);//mFile.txt
```


#### mainName(path)

> 主文件名
> 
> 不包含后缀名的文件名称，该函数本质上就是字符串操作，解析得到文件名称(不包含后缀)。

- 参数 : path {string} 路径 
- 返回 : {string} 文件名称
- 版本 : 1.0.0


```javascript
let fn = $file.mainName("./xml/mFile.txt");
alert("文件名称",fn);//mFile
```


#### ext(path)

> 后缀名
> 
> 该函数本质上就是字符串操作，解析得到文件后缀名。

- 参数 : path {string} 路径 
- 返回 : {string} 文件名称
- 版本 : 1.0.0


```javascript
let fn = $file.ext("./xml/mFile.txt");
alert("后缀名",fn);//txt
```


#### sd()

> 获得存储目录

- 返回 : {string} sdcard路径
- 版本 : 1.0.0


```javascript
let path = $file.sd();
alert("SDCard路径",path);///storage/emulated/0
```


#### del(path)

> 删除文件或文件夹
> 
> 递归删除文件或者文件夹,如果没有删除成功,则内部会有三次重试机制,强制进行删除
> 
> 该函数只适用于操作外部存储文件

- 参数 : path {string} 文件路径(支持相对路径) 
- 返回 : {boolean} 是否删除成功
- 版本 : 1.0.0


```javascript
//删除目录
$file.del("tools");
//删除文件
$file.del("main.js");
```


#### ls(path)

> 罗列文件
> 
> 该函数支持罗列打包后apk中的资源文件(assets目录)，但是注意书写相对路径

- 参数 : path {string} 路径(支持相对路径) 
- 返回 : {list[string]} 文件路径集合
- 版本 : 1.6.8


```javascript
let arr = $file.ls("res");
for(let path of arr){
    log(path);
}
```


#### ls(path, filter)

> 罗列文件
> 
> 支持罗列打包后apk中的资源文件，但是注意书写相对路径

- 参数 : path {string} 路径(支持相对路径) 
- 参数 : filter {(path)=>{return true;}} 过滤函数 
- 返回 : {list[string]} 文件路径集合
- 版本 : 1.6.8


```javascript
let arr = $file.ls("res",(path)=>{
    //过滤器
    return true;
});
for(let path of arr){
    log(path);
}
```


#### loopFiles(path, accept)

> 递归遍历文件
> 
> 该函数只适用于操作外部存储文件

- 参数 : path {string}  路径(支持相对路径)
- 参数 : accept {(file)=>{return false;}} 过滤函数 
- 返回 : {File[]} 文件列表
- 版本 : 1.4.9


```javascript
$file.looFiles("/res",(file)=>{
    //参数类型:file:java.io.File
    return true;
});
```


#### lsVideo()

> 罗列视频文件
> 
> 通过安卓媒体库获取视频文件,需要获取读取视频权限($permit.readVideo())

- 返回 : {VideoInfo[]} 视频文件列表
- 版本 : 1.5.4


```javascript
//VideoInfo属性:
let info = {
    id: 0,    //视频id
    name: "视频名称",
    path: "视频路径",
    size: 0,  //视频大小
    dur: 0,   //视频时长
    time: 0,  //时间
}
//获取视频列表
let arr = $file.lsVideo();
//遍历视频列表
for(let info of arr){
    log(info);
}
```


#### lsAudio()

> 罗列音频文件
> 
> 通过安卓媒体库获取音频文件,需要获取读取音频权限($permit.readAudio())

- 返回 : {AudioInfo[]} 音频文件列表
- 版本 : 1.5.4


```javascript
//AudioInfo属性:
let info = {
    id: 0,    //音频id
    name: "音频名称",
    path: "音频路径",
    size: 0,  //音频大小
    dur: 0,   //音频时长
    artist: "艺术家",
    album: "专辑",
    time: 0,  //时间
}
//获取音频列表
let arr = $file.lsAudio();
//遍历音频列表
for(let info of arr){
    log(info);
}
```


#### lsImages()

> 罗列图片文件
> 
> 通过安卓媒体库获取图片文件,需要获取读取图片权限($permit.readImage())

- 返回 : {ImageInfo[]} 图片文件列表
- 版本 : 1.5.4


```javascript
//ImageInfo属性:
let info = {
    id: 0,    //图片id
    name: "图片名称",
    path: "图片路径",
    size: 0,  //图片大小
    width: 0, //图片宽度
    height: 0,//图片高度
    time: 0,  //时间
}
//获取图片列表
let arr = $file.lsImages();
//遍历图片列表
for(let info of arr){
    log(info);
}
```


#### getDir(name, isPublic)

> 获取安卓目录路径
> 
> 获取安卓系统指定目录的路径，根据目录类型返回对应的目录路径字符串。
> 
> 目录类型可选项有: "pictures","图片", "downloads","下载", "dcim", "music","音乐", "movies","视频", "documents", "文档", "alarms", "闹钟", "notifications", "通知", "podcasts", "播客", "ringtones", "铃声"
> 
> 如果目录类型为自己自己自定义的目录名称，则会返回应用内部私有目录路径，并且以传入的目录类型作为目录的名称。

- 参数 : name {string} 目录类型,可选项有: "pictures","图片", "downloads","下载", "dcim", "music","音乐", "movies","视频", "documents", "文档", "alarms", "闹钟", "notifications", "通知", "podcasts", "播客", "ringtones", "铃声"
- 参数 : isPublic {boolean} 是否为公共目录(true为公共目录，false为私有目录)，默认为true，公共目录访问时都需要存储权限
- 返回 : {string} 目录路径字符串
- 版本 : 1.6.1


```javascript
let videoPath = $file.getDir("视频",true);
```


#### getDir(name)

> 获取安卓公共目录路径
> 
> 获取安卓系统指定目录的路径，根据目录类型返回对应的目录路径字符串。
> 
> 目录类型可选项有: "pictures","图片", "downloads","下载", "dcim", "music","音乐", "movies","视频", "documents", "文档", "alarms", "闹钟", "notifications", "通知", "podcasts", "播客", "ringtones", "铃声"
> 
> 如果目录类型为自己自己自定义的目录名称，则会返回应用内部私有目录路径，并且以传入的目录类型作为目录的名称。

- 参数 : name {string} 目录类型,可选项有: "pictures","图片", "downloads","下载", "dcim", "music","音乐", "movies","视频", "documents", "文档", "alarms", "闹钟", "notifications", "通知", "podcasts", "播客", "ringtones", "铃声"
- 返回 : {string} 目录路径字符串
- 版本 : 1.6.1


```javascript
let videoPath = $file.getDir("视频");
```


#### flushSd(successCallback, failCallback)

---

## $storage - 应用内存储

- 更新时间:2026-01-30 19:32:55

> 应用内存储
> 
> 轻量级的存储方案，用于存储一些简单基础的数据，一般用作于全局配置，当应用被卸载后，这些配置也会随之清空。




#### create(namespace)

> 创建storage
> 
> 其实如果不创建应用存储也可以，因为默认就有一个命名空间，但是建议还是自己创建一个自定义的命名空间。

- 参数 : namespace {string} 命名空间
- 返回 : {$storage} 存储对象
- 版本 : 1.0.0


```javascript
//命名空间的名称随意
let storage = $storage.create("namespace");
```


#### get(key, defaultValue)

> 获取值
> 
> 如果设置了默认值，就算拿不到数据，也会返回默认值

- 参数 : key {string} 关键字
- 参数 : defaultValue {Object} 默认值
- 返回 : {Object} 获取到的值
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
alert("数据",storage.get("MyStr","我是默认值"));
```


#### get(key)

> 获取值

- 参数 : key {string} 关键字
- 返回 : {Object} 获取到的值
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.put("MyStr","我是被存放进来的数据");
alert("数据",storage.get("MyStr"));
```


#### put(key, value)

> 存放数据

- 参数 : key {string} 关键字
- 参数 : value {Object} 数据
- 版本 : 1.0.0


```javascript
//只要保持命名空间的名称一致,就能正常读取到数据
let storage = $storage.create("namespace");
storage.put("MyStr","我是被存放进来的数据");
```


#### getStr(key)

> 获得字符串数据
> 
> 如果没有,就返回null

- 参数 : key {string} 关键字
- 返回 : {string} 数据
- 版本 : 1.0.0


```javascript
//只要保持命名空间的名称一致,就能正常读取到数据
let storage = $storage.create("namespace");
storage.put("MyStr","我是被存放进来的数据");
alert("数据",storage.getStr("MyStr"));
```


#### getString(key)

> 获得字符串数据
> 
> 等价于getStr方法，如果没有,就返回null

- 参数 : key {string} 关键字
- 返回 : {string} 数据
- 版本 : 1.5.4


```javascript
//只要保持命名空间的名称一致,就能正常读取到数据
let storage = $storage.create("namespace");
storage.put("MyStr","我是被存放进来的数据");
alert("数据",storage.getStr("MyStr"));
```


#### getStr(key, defaultValue)

> 获得字符串数据

- 参数 : key {string} 关键字
- 参数 : defaultValue {string} 默认值
- 返回 : {string} 数据
- 版本 : 1.0.0


```javascript
//只要保持命名空间的名称一致,就能正常读取到数据
let storage = $storage.create("namespace");
storage.put("MyStr","我是被存放进来的数据");
alert("数据",storage.getStr("MyStr","默认数据"));
```


#### getString(key, defaultValue)

> 获得字符串数据
> 
> 等价于getStr方法

- 参数 : key {string} 关键字
- 参数 : defaultValue {string} 默认值
- 返回 : {string} 数据
- 版本 : 1.5.4


```javascript
//只要保持命名空间的名称一致,就能正常读取到数据
let storage = $storage.create("namespace");
storage.put("MyStr","我是被存放进来的数据");
alert("数据",storage.getString("MyStr","默认数据"));
```


#### putStr(key, value)

> 存放字符串数据

- 参数 : key {string} 关键字
- 参数 : value {string} 存放的数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putStr("MyStr","我是内容");
alert("数据",storage.getStr("MyStr")); //我是内容
```


#### putString(key, value)

> 存放字符串数据
> 
> 等价于putStr方法

- 参数 : key {string} 关键字
- 参数 : value {string} 存放的数据
- 版本 : 1.5.4


```javascript
let storage = $storage.create("namespace");
storage.putString("MyStr","我是内容");
alert("数据",storage.getStr("MyStr")); //我是内容
```


#### getInt(key, defaultValue)

> 获得整数数据

- 参数 : key {int} 关键字
- 参数 : defaultValue {int} 默认值
- 返回 : {int} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
alert("数据",storage.getInt("MyIntDefault",20)); //20
```


#### getInt(key)

> 获得整数数据
> 
> 如果没有找打就返回默认值-1

- 参数 : key {int} 关键字
- 返回 : {int} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
alert("数据",storage.getInt("MyIntDefault")); //-1
```


#### putInt(key, value)

> 存放数字数据

- 参数 : key {string} 关键字
- 参数 : value {int} 存放的数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putInt("MyInt",100);
alert("数据",storage.getInt("MyInt")); //100
```


#### getBool(key, defaultValue)

> 获得布尔数据

- 参数 : key {Boolean} 关键字
- 参数 : defaultValue {Boolean} 默认值
- 返回 : {Boolean} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putBool("MyBool",true);
alert("数据",storage.getBool("MyBoolDefault")); //false
//如果默认值是true，那么就在找不到数据的时候返回true
alert("数据",storage.getBool("MyBoolDefault",true)); //true
```


#### getBoolean(key, defaultValue)

> 获得布尔数据
> 
> 等价于getBool方法

- 参数 : key {Boolean} 关键字
- 参数 : defaultValue {Boolean} 默认值
- 返回 : {Boolean} 数据
- 版本 : 1.5.4


```javascript
let storage = $storage.create("namespace");
storage.putBool("MyBool",true);
alert("数据",storage.getBool("MyBoolDefault")); //false
//如果默认值是true，那么就在找不到数据的时候返回true
alert("数据",storage.getBoolean("MyBoolDefault",true)); //true
```


#### getBool(key)

> 获得布尔数据

- 参数 : key {Boolean} 关键字
- 返回 : {Boolean} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putBool("MyBool",true);
alert("数据",storage.getBool("MyBool")); //true
```


#### getBoolean(key)

> 获得布尔数据
> 
> 等价于getBool方法

- 参数 : key {Boolean} 关键字
- 返回 : {Boolean} 数据
- 版本 : 1.5.4


```javascript
let storage = $storage.create("namespace");
storage.putBool("MyBool",true);
alert("数据",storage.getBoolean("MyBool")); //true
```


#### putBool(key, value)

> 存放布尔数据

- 参数 : key {string} 关键字
- 参数 : value {Boolean} 存放的数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putBool("MyBool",true);
alert("数据",storage.getBool("MyBool")); //true
```


#### putBoolean(key, value)

> 存放布尔数据
> 
> 等价于putBool方法

- 参数 : key {string} 关键字
- 参数 : value {Boolean} 存放的数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putBoolean("MyBool",true);
alert("数据",storage.getBoolean("MyBool")); //true
```


#### getFloat(key, defaultValue)

> 获得浮点数数据

- 参数 : key {float} 关键字
- 参数 : defaultValue {float} 默认值
- 返回 : {float} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
alert("数据",storage.getFloat("MyFloatDefault")); //-1.0
```


#### getFloat(key)

> 获得浮点数数据

- 参数 : key {float} 关键字
- 返回 : {float} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putFloat("MyFloat",3.1415926);
alert("数据",storage.getFloat("MyFloat")); //3.1415926
```


#### putFloat(key, value)

> 存放浮点数数据

- 参数 : key {string} 关键字
- 参数 : value {float} 存放的数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putFloat("MyFloat",3.1415926);
alert("数据",storage.getFloat("MyFloat",0)); //3.1415926
```


#### getLong(key, defaultValue)

> 获得长数字数据

- 参数 : key {long} 关键字
- 参数 : defaultValue {long} 默认值
- 返回 : {Long} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
alert("数据",storage.getLong("MyLongDefault",100));
```


#### getLong(key)

> 获得长数字数据

- 参数 : key {String} 关键字
- 返回 : {Long} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putLong("MyLong",5201314);
alert("数据",storage.getLong("MyLong"));
```


#### putLong(key, value)

> 存放长数字数据
> 

- 参数 : key {string} 关键字
- 参数 : value {Long} 存放的数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putLong("MyLong",5201314);
alert("数据",storage.getLong("MyLong",100));//5201314
```


#### getStrSet(key, defaultValue)

> 获得字符串集合数据

- 参数 : key {string} 关键字
- 参数 : defaultValue {string[]} 默认值
- 返回 : {string[]} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putStrSet("MySet",["数据1","数据2","数据3"]);
alert("数据",storage.getStrSet("MySet",[])); //["数据1","数据2","数据3"]
```


#### getStrSet(key)

> 获得字符串集合数据
> 
> 如果没有数据就默认返回空集合

- 参数 : key {string} 关键字
- 返回 : {string[]} 数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putStrSet("MySet",["数据1","数据2","数据3"]);
alert("数据",storage.getStrSet("MySet")); //["数据1","数据2","数据3"]
```


#### putStrSet(key, value)

> 存放字符串集合数据

- 参数 : key {string} 关键字
- 参数 : value {string[]} 存放的数据
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.putStrSet("MySet",["数据1","数据2","数据3"]);
alert("数据",storage.getStrSet("MySet",[])); //["数据1","数据2","数据3"]
```


#### getAll()

> 获得全部数据

- 返回 : {obj} 数据(使用时直接当作js对象打.调用即可)
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
alert("数据",storage.getAll());
```


#### has(key)

> 是否包含

- 参数 : key {string} 关键字
- 返回 : {boolean} 是否包含
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.put("MyInt",100);
log(storage.has("MyInt"));//true
storage.clear();
log(storage.has("MyInt"));//false
alert("数据",storage.getInt("MyInt"));//-1
```


#### clear()

> 删除全部数据

- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.put("MyInt",100);
storage.clear();
alert("数据",storage.getInt("MyInt"));//-1
```


#### del(key)

> 移除数据

- 参数 : key {string} 关键字
- 版本 : 1.0.0


```javascript
let storage = $storage.create("namespace");
storage.put("MyInt",100);
storage.del("MyInt");
alert("数据",storage.getInt("MyInt"));//-1(默认值)
```

---

## $sqlite - 轻量数据库

- 更新时间:2026-01-30 19:32:55

> 轻量数据库
> 
> 线程安全,支持并发编程,本地轻量级数据库存储,存储的文件会随着应用的卸载而清空。




#### newSqlite()

> 创建新对象
> 
> 创建一个新的数据库对象，你可以用这个对象来操作其他数据库

- 返回 : {this} 自己


```javascript
let sqlite = $sqlite.newSqlite();
let hasOpen = sqlite.open("myDb");
if(hasOpen){
    log("链接成功");
}
```


#### open(dbName, external)

> 打开数据库
> 
> 如果数据库文件存在则会加载数据库，如果不存在则先创建数据库文件后加载数据库

- 参数 : dbName {string} 数据库名称 
- 参数 : external {boolean} 是否保存到外部存储(默认:false) 
- 返回 : {boolean} 是否连接成功


```javascript
//第二个参数的含义:
//false:保存到内部存储:无需后缀，只需要取一个数据库名称即可，应用卸载后数据会被删除
//true:保存到外部存储:需全路径，包括文件名和后缀，应用卸载后数据不会被删除
let hasOpen = $sqlite.open("/sdcard/mData.db",true);
if(hasOpen){
    log("链接成功");
}
```


#### open(dbName)

> 打开数据库
> 
> 如果数据库文件存在则会加载数据库，如果不存在则先创建数据库文件后加载数据库

- 参数 : dbName {string} 数据库名称 
- 返回 : {boolean} 是否连接成功


```javascript
//无需后缀，只需要取一个数据库名称即可
let hasOpen = $sqlite.open("VideoData");
if(hasOpen){
    log("链接成功");
}
```


#### newTab(tableName, columns)

> 创建数据表
> 
> 如果这个表已经在数据库中存在了，那么就不继续创建了
> 
> 注意:不管你的数据是什么类型都用字符串类型存储

- 参数 : tableName {string} 表名称 
- 参数 : columns {string[]} 列名称 
- 返回 : {boolean} 是否执行成功


```javascript
let hasTable = $sqlite.newTab("table1",["name","sex","age"]);
if(hasTable){
    log("建表成功");
}
```


#### add(tableName, data)

> 添加数据
> 
> 注意:不管你的数据是什么类型都用字符串类型存储，默认使用自增id作为主键

- 参数 : tableName {string} 表名 
- 参数 : data {obj}  数据对象 
- 返回 : {boolean} 是否执行成功


```javascript
//其实此函数等价于 $sqlite.exe("INSERT INTO table1 (name, sex, age) VALUES ('张三', '男', 20)");
let hasAdd = $sqlite.add("table1",{
    name:"张三",
    sex:"男",
    age:20
});
if(hasAdd){
    log("添加成功");
}
```


#### update(tableName, map, where)

> 更新数据

- 参数 : tableName {string} 表名称 
- 参数 : map {obj} 数据对象 
- 参数 : where {string} 条件语句 
- 返回 : {boolean} 是否执行成功


```javascript
//更新数据
let okUpdate = $sqlite.update("table1", {
    name: "张三",
    sex: "女",
    age: 20
},"name='张三'");
if (okUpdate) {
    log("更新成功");
}
```


#### ls(tableName)

> 罗列数据
> 
> 注意:不管你的数据是什么类型，查询出来的必是字符串类型，即使是报错也不会返回null，而是返回空列表，因此可以不用判断数据是否为空

- 参数 : tableName {string} 表名称
- 返回 : {obj[]} 数据集合对象


```javascript
//即使是报错也不会返回null，而是返回空列表，因此可以不用判断数据是否为空
let result = $sqlite.ls("table1");
for(let item of result){
    log(item);
}
```


#### ls()

> 罗列表名
> 
> 查询数据库中的所有表名并且返回表名列表

- 返回 : {string[]} 表名列表


```javascript
//罗列数据库中的表
let result = $sqlite.ls();
for(let item of result){
    log(item);
}
```


#### select(selectSql)

> 执行查询语句
> 
> 注意:不管你的数据是什么类型，查询出来统一是字符串类型。

- 参数 : selectSql {string} 查询语句
- 返回 : {obj[]} 数据集合对象


```javascript
//即使是报错也不会返回null，而是返回空列表，因此可以不用判断数据是否为空
let result = $sqlite.select("select * from table1");
for(let item of result){
    log(item);
}
```


#### hasTab(tableName)

> 判断表是否存在

- 参数 : tableName {string} 表名称
- 返回 : {boolean} 是否存在该表


```javascript
let result = $sqlite.hasTab("table1");
if(result){
    log("存在表");
} else {
    log("不存在表");
}
```


#### exe(sql)

> 执行SQL语句

- 参数 : sql {string} sql语句
- 返回 : {boolean} 是否执行成功


```javascript
//删除表
$sqlite.exe("drop table if exists table1");
```


#### delDb(external)


#### delDb(dbName, external)

> 删除数据库
> 
> 我将直接删除本地数据库的存储文件，那么你将丢失所有数据

- 参数 : dbName {string} 数据库名称
- 返回 : {boolean} 是否执行成功


```javascript
//无需打开数据库，直接就能删除数据库文件
let hasDelDb = $sqlite.delDb("VideoData");
if(hasDelDb){
    log("删库成功");
}
```


#### delDb(dbName)

> 删除数据库
> 
> 我将直接删除本地数据库的存储文件，那么你将丢失所有数据

- 参数 : dbName {string} 数据库名称
- 返回 : {boolean} 是否执行成功


```javascript
//无需打开数据库，直接就能删除数据库文件
let hasDelDb = $sqlite.delDb("VideoData");
if(hasDelDb){
    log("删库成功");
}
```


#### delTab(table)

> 删除表

- 参数 : table {string} 表名
- 返回 : {boolean} 是否删除成功


```javascript
let hasDel = $sqlite.delTab("table1");
if(hasDel){
    log("删除表成功");
}
```


#### close()

> 关闭数据库
> 
> 当你操作完毕后可以关闭数据库链接，释放资源。

- 返回 : {boolean} 是否关闭成功


```javascript
let okFinish = $sqlite.close();
if(okFinish){
    log("结束操作");
}
```