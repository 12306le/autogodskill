# API 07 - 工具类：加密 & 日期 & 字符串 & 日志 & 媒体 & 二维码

> 模块：`$date`、`$str`、`$crypt`、`$log`、`$media`、`$tts`、`$qr`
> 返回 [README](README.md)

## 目录

- [$date - 日期时间](#date---日期时间)
- [$str - 字符串工具](#str---字符串工具)
- [$crypt - 加密解密](#crypt---加密解密)
- [$log - 日志输出](#log---日志输出)
- [$media - 音频播放](#media---音频播放)
- [$tts - 文字转语音](#tts---文字转语音)
- [$qr - 二维码工具](#qr---二维码工具)

---

## $date - 日期时间

### 获取当前日期时间字符串

```javascript
let dateStr = $date.dt(); // 返回 "2025-10-25 18:32:53"
alert("日期时间", dateStr);

let dateStr2 = $date.d(); // 返回 "2025-10-25"
alert("日期", dateStr2);
```

### 解析日期字符串

```javascript
// 指定格式解析
let date = $date.parse("2025/12/08 12/35/24", "yyyy/MM/dd HH/mm/ss");
alert("日期对象", date); // Dec 8, 2025 12:35:24 PM

// 自动匹配格式（无需模板）
let date = $date.parse("2025/12/08 12/35/24");
alert("日期对象", date);
```

### 获取当前日期信息

```javascript
let info = $date.info();
alert("日期信息", info);
// info 对象包含 year, month, day, hour, minute, second 等字段
```

### 格式化时间戳

```javascript
let info = $date.format(1747985594110, "yyyy年MM月dd日 HH时mm分ss秒");
alert("格式化日期", info);
```

### 创建日期对象

```javascript
let date = $date.date();
alert("当前日期对象", date);
```

### 时间戳转可读描述

```javascript
// 将毫秒数转为"X天X时X分X秒"格式
let info = $date.dur(1234567890);
alert("时间", info); // 输出：14天6时56分7秒
```

---

## $str - 字符串工具

### 随机字符

```javascript
// 从字符集中随机取一个字符
let str = $str.random("abcdefghijk");
alert("随机字符", str);

// 从数组中随机取一个元素
let str = $str.random(["abc", "defg", "hijk", "lmn"]);
alert("随机字符串", str);
```

### 截取字符串

```javascript
// 截取开头 N 个字符
let str = $str.subStart("ABCDEFG", 3); // 返回 "ABC"
alert("截取开头", str);

// 截取末尾 N 个字符
let str = $str.subEnd("ABCDEFG", 3);   // 返回 "EFG"
alert("截取末尾", str);
```

### 去除空格

```javascript
let str = $str.trim("   嗯？   ");
alert("去除首尾空格", str); // 返回 "嗯？"
```

### 判断前缀

```javascript
let result = $str.startWith("Hello World", "Hello"); // true
```

---

## $crypt - 加密解密

### AES 加密解密（快捷方法）

```javascript
// 自动生成 16 位密钥
let key = $crypt.aesKey();
let myData = "今天天气真好!";

let encrypted = $crypt.aesJiami(myData, key);
alert("AES加密结果", encrypted);

let decrypted = $crypt.aesJiemi(encrypted, key);
alert("AES解密结果", decrypted);
```

### 通用加密接口（jiami / jiemi）

#### AES 加密

```javascript
let key = "ACSDFGHJUYDLOPSD"; // 16 位密钥

let encrypted = $crypt.jiami("我是被加密的明文", key, "AES", {
    input: "string",
    output: "base64"
});
alert("AES加密结果", encrypted);

let decrypted = $crypt.jiemi(encrypted, key, "AES", {
    input: "base64",
    output: "string"
});
alert("AES解密结果", decrypted);
```

#### DES 加密

```javascript
let key = "ACSDFGHJ"; // 8 位密钥

let encrypted = $crypt.jiami("我是被加密的明文", key, "DES", {
    input: "string",
    output: "base64"
});
alert("DES加密", encrypted);

let decrypted = $crypt.jiemi(encrypted, key, "DES", {
    input: "base64",
    output: "string"
});
alert("DES解密", decrypted);
```

#### RSA 加密解密

```javascript
// 生成密钥对
let keyPair = $crypt.generateKeyPair("RSA", 1024);
alert("RSA密钥信息", keyPair);
// keyPair.privateKey: 私钥
// keyPair.publicKey: 公钥

// 使用私钥加密
let encrypted = $crypt.jiami("我是被加密的内容", keyPair.privateKey, "RSA/ECB/PKCS1Padding", {
    input: "string",
    output: "base64"
});
alert("RSA加密结果", encrypted);

// 使用公钥解密
let decrypted = $crypt.jiemi(encrypted, keyPair.publicKey, "RSA/ECB/PKCS1Padding", {
    input: "base64",
    output: "string"
});
alert("RSA解密结果", decrypted);
```

### 哈希摘要（digest）

#### 查看所有支持的算法

```javascript
let digests = $crypt.digests();
for (let i = 0; i < digests.size(); i++) {
    let algorithm = digests.get(i);
    let result = $crypt.digest("今天天气真好呀", algorithm, {
        input: "string",
        output: "hex"
    });
    alert("算法:" + algorithm, "加密后的数据:\n" + result);
}
```

#### MD5

```javascript
// 快捷方法
let salt = $crypt.md5Key(16); // 生成 16 位 MD5 盐值
let result16 = $crypt.md516(salt, "今天天气真好!"); // MD5 16位
let result32 = $crypt.md532(salt, "今天天气真好!"); // MD5 32位
alert("MD5加密:16位", result16);
alert("MD5加密:32位", result32);

// 通用方法
let result = $crypt.digest("今天天气真好呀", "MD5", {
    input: "string",
    output: "hex"
});
alert("MD5加密", result);
```

### DSA 数字签名

```javascript
let keyPair = $crypt.generateKeyPair("DSA", 1024);

// 签名（使用私钥）
let signData = $crypt.sign("我是被签名的内容", keyPair.privateKey, "DSA", {
    input: "string",
    output: "byte"
});
alert("DSA签名结果", signData.join());

// 验证（使用公钥）
let verified = $crypt.verify(
    "我是被签名的内容",
    signData,
    keyPair.publicKey,
    "DSA",
    { input: "string", output: "byte" }, // 签名时的配置
    { input: "byte" }                     // 验证数据的配置
);
alert("DSA验证结果", verified);
```

### input/output 参数说明

| 值 | 说明 |
|----|------|
| `"string"` | 普通字符串 |
| `"base64"` | Base64 编码字符串 |
| `"hex"` | 十六进制字符串 |
| `"byte"` | 字节数组 |

---

## $log - 日志输出

> 所有日志均会显示在 AIGame 的日志界面中。

```javascript
$log.i("信息");   // 信息（蓝色）
$log.d("调试");   // 调试（灰色）
$log.w("警告");   // 警告（黄色）
$log.e("异常");   // 错误（红色）
$log.v("冗余");   // 冗余（绿色）
$log.log("hello"); // 普通日志

// 显示悬浮日志窗口
$log.floaty();
```

> 全局函数 `log()` 等同于 `$log.log()`。

---

## $media - 音频播放

### 播放音频文件

```javascript
let resArr = [
    "example/$media - 音频播放/res/qq系统提示音.mp3",
    "example/$media - 音频播放/res/开机音效.mp3",
    "example/$media - 音频播放/res/微信消息.mp3",
    "example/$media - 音频播放/res/短信音效.mp3"
];

$media.play(resArr[0]); // 播放第一个音频
```

---

## $tts - 文字转语音

### 基础用法

```javascript
// 使用默认参数朗读
$tts.read("你好呀，早安~");
```

### 自定义参数

```javascript
let options = {
    rate: 1,          // 语速（默认1）
    pitch: 1,         // 音调（默认1）
    volume: 1,        // 音量（默认1）
    language: "zh",   // 语言（"zh" 中文，"en" 英文等）
    streamType: "system" // 播放流（"system" 音量最大）
};

$tts.read("你好呀，早安~", options);
```

---

## $qr - 二维码工具

### 生成二维码

```javascript
// 带自定义样式
let img = $qr.make("Hello AIGame !", {
    w: 500,            // 宽度（默认500）
    h: 500,            // 高度（默认500）
    margin: 2,         // 边距（默认2）
    foreColor: "#2AACB8", // 前景色（默认黑色）
    bgColor: "#2B2D30",   // 背景色（默认白色）
});

if (img != null) {
    img.show();                    // 显示二维码
    img.save("/sdcard/qr.png");   // 保存到本地
}

// 使用默认样式（简洁写法）
let img = $qr.make("欢迎来到AIGame!");
img.show();
img.save("/sdcard/qr.png");
```

### 解析二维码

```javascript
// 从本地文件路径解析
let content = $qr.parse("./example/$qr - 二维码工具/imgs/t01.png");
alert("二维码内容", content);

// 从已保存的文件解析
let path = "/sdcard/qr.png";
if ($file.exists(path)) {
    showImg(path);
    let content = $qr.parse(path);
    alert("二维码内容", content);
} else {
    alert("本地图片", "图片不存在:\n" + path);
}
```

---

## 附录：JavaScript（Rhino）常用示例

> AIGame 使用 Rhino JS 引擎，支持大部分 ES5 及部分 ES6 特性。

### 数组操作

```javascript
let fruits = ["apple", "banana", "cherry"];
fruits.push("date");
fruits.forEach((fruit, index) => {
    console.log("索引" + index + ":", fruit);
});
let numbers = [3, 1, 4, 1, 5];
numbers.sort();
console.log("排序后:", numbers); // 1,1,3,4,5
```

### 正则表达式

```javascript
// URL 解析
var url = "https://www.example.com:8080/path?name=test#fragment";
var urlPattern = /^(\w+):\/\/([\w.]+):?(\d*)?([^?#]+)?\??([^#]*)?#?(.*)?$/;
var matches = url.match(urlPattern);
// matches[1]=https, matches[2]=www.example.com, matches[3]=8080

// 邮箱验证
function validateEmail(email) {
    var pattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
    return pattern.test(email);
}

// 驼峰命名转下划线
function camelToUnderscore(str) {
    return str.replace(/([A-Z])/g, function(match, p1, offset) {
        return (offset > 0 ? "_" : "") + p1.toLowerCase();
    });
}
```

### 闭包 & 高阶函数

```javascript
// 工厂函数（闭包）
function createCounter(initialValue) {
    var count = initialValue;
    return {
        increment: function(step) { count += (step || 1); return count; },
        decrement: function(step) { count -= (step || 1); return count; },
        getCount: function() { return count; },
        reset: function() { count = initialValue; }
    };
}
var counter = createCounter(0);
counter.increment(3); // 3
counter.decrement();  // 2

// 高阶函数
function processNumbers(numbers, processor) {
    var result = [];
    for (var i = 0; i < numbers.length; i++) {
        result.push(processor(numbers[i]));
    }
    return result;
}
var squared = processNumbers([1,2,3,4], function(n) { return n * n; });
// [1, 4, 9, 16]
```

### 原型继承

```javascript
function Animal(name) {
    this.name = name;
}
Animal.prototype.speak = function() {
    console.log(this.name + " makes a noise.");
};

function Dog(name) {
    Animal.call(this, name);
}
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
Dog.prototype.speak = function() {
    console.log(this.name + " barks.");
};

var dog = new Dog("Buddy");
dog.speak(); // Buddy barks.
```

### JSON 操作

```javascript
var user = { name: "李四", age: 30, hobbies: ["读书", "运动"] };
var jsonStr = JSON.stringify(user);
console.log("JSON字符串:", jsonStr);
var parsedUser = JSON.parse(jsonStr);
console.log("解析后对象:", parsedUser.name);
```

### instanceof 类型检查

```javascript
var arr = [1, 2, 3];
print(arr instanceof Array);    // true
print(arr instanceof Object);   // true
print(null instanceof Object);  // false

// 继承链检查
function Mammal(name) { Animal.call(this, name); }
Mammal.prototype = Object.create(Animal.prototype);
var lion = new Mammal("狮子");
print(lion instanceof Mammal); // true
print(lion instanceof Animal); // true（继承关系）
```

### 模块模式

```javascript
var Calculator = (function() {
    // 私有方法和变量
    var PI = 3.1415926535;
    function validateNumber(n) {
        if (typeof n !== "number" || isNaN(n)) throw new Error("无效数字: " + n);
    }
    // 公共接口
    return {
        add: function(a, b) { validateNumber(a); validateNumber(b); return a + b; },
        circleArea: function(radius) { validateNumber(radius); return PI * radius * radius; }
    };
})();

console.log(Calculator.add(2, 3));         // 5
console.log(Calculator.circleArea(2));     // 12.566...
console.log(Calculator.PI);               // undefined（私有）
```

### Promise（基础支持）

```javascript
function asyncOperation() {
    return new Promise((resolve, reject) => {
        sleep(1000);
        const success = true;
        if (success) {
            resolve("Operation successful");
        } else {
            reject("Operation failed");
        }
    });
}

asyncOperation()
    .then((result) => { console.log(result); })
    .catch((error) => { console.log(error); });
```

### Generator

```javascript
function* generatorFunction() {
    yield 1;
    yield 2;
    yield 3;
}
var gen = generatorFunction();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

### Proxy

```javascript
var target = { name: "John", age: 30 };
var handler = {
    get: function(target, property) {
        console.log("Getting property " + property);
        return target[property];
    },
    set: function(target, property, value) {
        console.log("Setting " + property + " to " + value);
        target[property] = value;
        return true;
    }
};
var proxy = new Proxy(target, handler);
console.log(proxy.name);
proxy.age = 31;
```
