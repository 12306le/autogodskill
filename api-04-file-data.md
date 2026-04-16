# API 04 - 文件 & 数据库 & Excel & 资源

> 模块：`$file`、`$excel`、`$sqlite`、`$res`、`$fc`、`$ext`
> 返回 [README](README.md)

## 目录

- [$file - 文件操作](#file---文件操作)
- [$excel - Excel表格](#excel---excel表格)
- [$sqlite - SQLite数据库](#sqlite---sqlite数据库)
- [$res - 资源管理](#res---资源管理)
- [$fc - 文件选择器](#fc---文件选择器)
- [$ext - 加载扩展文件](#ext---加载扩展文件)

---

## $file - 文件操作

### 列出文件

```javascript
// 列出目录中的文件
let path = "/sdcard";
let files = $file.ls(path);
for (let i = 0; i < files.size(); i++) {
    log(files.get(i));
}

// 使用过滤器（过滤出以'.'开头的隐藏文件）
let files_A = $file.ls(path, (path) => {
    let fileName = $file.name(path);
    return $str.startWith(fileName, ".");
});
for (let i = 0; i < files_A.size(); i++) {
    log(files_A.get(i));
}
```

### 判断文件/目录状态

```javascript
let isFile = $file.isFile("/sdcard/a.txt");      // 是否是文件
let isDir = $file.isDir("/sdcard");               // 是否是目录
let isEmptyDir = $file.isEmptyDir("/sdcard");     // 是否是空目录
let isEmpty = $file.isEmpty("/sdcard");           // 是否是空（文件或目录）
let exists = $file.exists("/sdcard/a.txt");       // 是否存在
```

### 路径操作

```javascript
// 拼接路径
let path1 = $file.join("sdcard", "Pictures");
// 结果：sdcard/Pictures

let path2 = $file.join("sdcard", "Pictures", "我的项目", "res");
// 结果：sdcard/Pictures/我的项目/res

// 获取文件名
let name = $file.name("/sdcard/Pictures/test.txt"); // 返回 "test.txt"
```

### 创建文件/目录

```javascript
$file.create("/sdcard/测试.txt"); // 创建文件

let path = "/sdcard/AAA";
$file.mkdir(path);                // 创建目录
if ($file.exists(path)) {
    log("目录创建完成");
}
```

### 读取文件

```javascript
let content = $file.read("/sdcard/测试.txt");
log(content);
```

### 写入文件

```javascript
$file.write("我是内容", "/sdcard/测试.txt");  // 覆盖写入
$file.append("我是内容", "/sdcard/测试.txt"); // 追加写入
```

### 复制 / 移动 / 删除 / 重命名

```javascript
// 复制
$file.copy("/sdcard/测试.txt", "/sdcard/测试2.txt");
if ($file.exists("/sdcard/测试2.txt")) {
    log("拷贝成功");
}

// 移动
$file.move("/sdcard/测试.txt", "/sdcard/Pictures/测试2.txt");
if ($file.exists("/sdcard/Pictures/测试2.txt")) {
    log("移动成功");
}

// 删除
$file.del("/sdcard/Pictures/测试2.txt");
if (!$file.exists("/sdcard/Pictures/测试2.txt")) {
    log("删除成功");
}

// 重命名
$file.rename("/sdcard/测试.txt", "/sdcard/测试2.txt");
if ($file.exists("/sdcard/测试2.txt")) {
    log("重命名成功");
}
```

---

## $excel - Excel表格

### 读取表格

```javascript
// 读取第一个 Sheet（默认 index=0）
let data = $excel.read("example/$excel - 表格操作/data.xlsx");
alert("表格数据", data);

// 读取指定下标的 Sheet
let data = $excel.read("example/$excel - 表格操作/data.xlsx", 1);
alert("表格数据", data);
```

### 获取 Sheet 信息

```javascript
// 获取 Sheet 数量
let sheetNum = $excel.num("example/$excel - 表格操作/data.xlsx");
alert("表格数量", sheetNum);

// 获取 Sheet 名称列表
let sheetList = $excel.ls("example/$excel - 表格操作/data.xlsx");
alert("表格名称", sheetList);
```

### 遍历所有 Sheet

```javascript
let path = "example/$excel - 表格操作/data.xlsx";
$excel.loop(path, (name, data) => {
    alert(name, data);
});
```

### 写入表格

```javascript
// 数据（注意：所有元素必须是字符串类型）
let sheetData = [
    ["姓名", "年龄"],
    ["小红", "18"],
    ["小明", "19"]
];
let sheetName = "我的表格";
let savePath = "/sdcard/demo.xlsx";
$excel.write(sheetName, sheetData, savePath);
toast("写入完毕");

// 验证写入
sleep(1000);
alert("表格数据", $excel.read(savePath));
```

---

## $sqlite - SQLite数据库

### 完整操作流程

```javascript
// 1. 打开/创建数据库（数据库名称）
let hasOpen = $sqlite.open("mData");
if (hasOpen) {
    log("链接成功");
}

// 2. 创建表（表名，字段列表）
let hasTable = $sqlite.newTab("table1", ["name", "sex", "age"]);
if (hasTable) {
    log("建表成功");
}

// 3. 插入数据
// 等价于：INSERT INTO table1 (name, sex, age) VALUES ('张三', '男', 20)
let hasAdd = $sqlite.add("table1", {
    name: "张三",
    sex: "男",
    age: 20
});
if (hasAdd) {
    log("添加成功");
}

// 4. 更新数据
let okUpdate = $sqlite.update("table1", {
    name: "张三",
    sex: "女",
    age: 20
}, "name='张三'"); // WHERE 条件
if (okUpdate) {
    log("更新成功");
}

// 5. 查询数据
let result = $sqlite.ls("table1");
for (let item of result) {
    log(item);
}

// 6. 执行原生 SQL
$sqlite.exe("DROP TABLE IF EXISTS table1");
$sqlite.exe("INSERT INTO table1 (name, sex, age) VALUES ('李四', '男', 25)");

// 7. 删除表
let hasDel = $sqlite.delTab("table1");
if (hasDel) {
    log("删除表成功");
}

// 8. 关闭数据库
let okFinish = $sqlite.close();
if (okFinish) {
    log("关闭成功");
}

// 9. 删除数据库文件（无需先打开）
let hasDelDb = $sqlite.delDb("mData");
if (hasDelDb) {
    log("删库成功");
}
```

---

## $res - 资源管理

> 用于脚本间共享数据（内存级别，不持久化到文件）。

### 存储与读取

```javascript
// 创建（或获取已有）资源对象
let res = $res.create("我的资源");

// 存储各种类型
res.set("名字", "张三");
res.set("对象", {
    名字: "翠花",
    年龄: 18,
    身高: 175,
    体重: 98,
    儿子: { 名字: "小安", 年龄: 1 }
});
res.set("列表", [1, 2, 3]);

// 读取
log(res.get("名字"));
log(res.get("对象").名字);
log(res.get("对象").儿子.名字);
log(res.get("列表"));
```

### 查询资源列表

```javascript
let res = $res.create("我的资源");
let resList = res.ls();
log(resList);
```

### 导出资源

```javascript
let res = $res.create("我的资源");
res.dump("sdcard/Pictures/示例/$res/资源.res");
```

### 查看资源内容

```javascript
let res = $res.create("我的资源");
let content = res.cat();
$tip.show("资源内容", content, null);
```

---

## $fc - 文件选择器

> 显示文件选择界面，让用户选择文件或目录。

### 参数说明

| 参数 | 说明 | 可选值 |
|------|------|--------|
| `mode` | 选择模式 | `"s"` 单选，`"m"` 多选 |
| `type` | 文件类型 | `"f"` 仅文件，`"d"` 仅目录，`"a"` 全部 |
| `root` | 根目录 | 路径字符串 |
| `path` | 起始路径 | 路径字符串 |

### 基础用法（无配置，默认选择）

```javascript
$fc.show((files) => {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
});
```

### 单选文件

```javascript
$fc.show((files) => {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "s",  // 单选
    type: "f"   // 仅文件
});
```

### 单选目录

```javascript
$fc.show((files) => {
    log(files[0]);
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "s",
    type: "m"  // 仅目录（m = mkdir = directory）
});
```

### 单选（文件+目录）

```javascript
$fc.show((files) => {
    log(files[0]);
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "s",
    type: "a"  // 所有（all）
});
```

### 多选文件

```javascript
$fc.show((files) => {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "m",  // 多选
    type: "f"   // 仅文件
});
```

### 多选（文件+目录）

```javascript
$fc.show((files) => {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "m",
    type: "a"
});
```

---

## $ext - 加载扩展文件

> 支持加载 APK、DEX、JAR、SO 文件，扩展 AIGame 的能力。

### 加载 APK

```javascript
$ext.loadApk("example/$ext - 加载ApkDexJarSo文件/libs/apk/lib.apk");

// 使用 APK 中的类
let demo = new org.aigame.apk.ApkDemo();
alert("示例", demo.getStr());
```

### 加载单个 DEX

```javascript
$ext.loadDex("example/$ext - 加载ApkDexJarSo文件/libs/dex/classes.dex");

let demo = new org.aigame.demo.DexDemo();
alert("示例", demo.getStr());
```

### 加载 DEX + SO（组合加载）

```javascript
$ext.loadDex({
    path: ["example/$ext - 加载ApkDexJarSo文件/libs/dex_so/classes.dex"],
    so: [{
        // 根据手机架构选择正确的 so 文件
        path: "example/$ext - 加载ApkDexJarSo文件/libs/dex_so/lib/arm64-v8a/libdemo.so",
        load: false, // DEX 已静态加载 SO，不重复加载
    }]
});

let demo = new org.aigame.demo.CallC();
alert("示例", demo.getStr());
```

### 加载多个 DEX 文件

```javascript
let basePath = "example/$ext - 加载ApkDexJarSo文件/libs/dexs/多个dex";
let paths = [
    `${basePath}/classes1.dex`,
    `${basePath}/classes2.dex`,
    `${basePath}/classes3.dex`
];
$ext.loadDexs(paths);

let dex1 = new org.aigame.dex1.DexDemo();
let dex2 = new org.aigame.dex2.DexDemo();
let dex3 = new org.aigame.dex3.DexDemo();
alert("示例", dex1.getStr() + "\n" + dex2.getStr() + "\n" + dex3.getStr());
```

### 加载单个 JAR

```javascript
$ext.loadJar("example/$ext - 加载ApkDexJarSo文件/libs/jar/classes.jar");

let demo = new org.aigame.demo.JarDemo();
alert("示例", demo.getStr());
```

### 加载 JAR + SO（组合加载）

```javascript
$ext.loadJar({
    path: ["example/$ext - 加载ApkDexJarSo文件/libs/jar_so/classes.jar"],
    so: [{
        path: "example/$ext - 加载ApkDexJarSo文件/libs/jar_so/lib/arm64-v8a/libdemo.so",
        load: false,
    }]
});

let demo = new org.aigame.demo.JarCallC();
alert("示例", demo.getStr());
```

### 加载多个 JAR 文件

```javascript
let basePath = "example/$ext - 加载ApkDexJarSo文件/libs/jars/多个jar文件";
let paths = [
    `${basePath}/classes1.jar`,
    `${basePath}/classes2.jar`,
    `${basePath}/classes3.jar`
];
$ext.loadJars(paths);

let jar1 = new org.aigame.jar1.JarDemo();
let jar2 = new org.aigame.jar2.JarDemo();
let jar3 = new org.aigame.jar3.JarDemo();
alert("示例", jar1.getStr() + "\n" + jar2.getStr() + "\n" + jar3.getStr());
```

### 注意事项

| 项目 | 说明 |
|------|------|
| SO 架构 | 根据手机 CPU 架构选择（arm64-v8a / armeabi-v7a 等） |
| `load: false` | 当 DEX/JAR 内部已静态加载了 SO 时，`load` 设为 `false` 避免重复加载 |
| APK | APK 内部类可直接用 `new` 实例化 |
