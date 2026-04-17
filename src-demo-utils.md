# 示例：工具类/脚本语法


## #U6a21#U5757#U5f00#U53d1-01.#U51fd#U6570#U6a21#U5757-#U8c03#U7528#U6a21#U5757

```javascript
let mFunc = require("example/模块开发/01.函数模块/模块代码.js");

//执行函数
alert("函数模块","结果："+mFunc(1, 2));
```


## #U6a21#U5757#U5f00#U53d1-02.#U5bf9#U8c61#U6a21#U5757-#U8c03#U7528#U6a21#U5757

```javascript
let mObj = require("example/模块开发/02.对象模块/模块代码.js");

//使用对象
alert("对象模块",mObj.name+"\n"+mObj.age+"\n"+mObj.sex);
```


## #U6a21#U5757#U5f00#U53d1-03.#U7c7b#U6a21#U5757-#U8c03#U7528#U6a21#U5757

```javascript
let mClass = require("example/模块开发/03.类模块/模块代码.js");

//使用这个类:创建对象
let m = new mClass();
//调用类的show方法
m.show();
```


## $crypt-#U52a0#U5bc6#U7b97#U6cd5-01.#U5bf9#U79f0#U52a0#U5bc6-01.AES#U52a0#U5bc6(#U5de5#U5177#U7248)

```javascript
//AIGame 官方示例

//(1)准备16位密钥
let key = $crypt.aesKey();

//(2)准备要加密的明文
let myData = "今天天气真好!";

//(3)开始加密
let jiamiResult = $crypt.aesJiami(myData, key);

alert("AES加密结果", jiamiResult);

//(4)开始解密
let jiemiResult = $crypt.aesJiemi(jiamiResult, key);

alert("AES解密结果", jiemiResult);




//示例结束
```


## $crypt-#U52a0#U5bc6#U7b97#U6cd5-01.#U5bf9#U79f0#U52a0#U5bc6-02.AES#U52a0#U5bc6(#U5e38#U89c4#U7248)

```javascript
//AIGame 官方示例

//准备一个长度为16的密钥
let key = "ACSDFGHJUYDLOPSD";

//准备需要加密的明文
let text = "我是被加密的明文";

//开始加密
let result = $crypt.jiami(text,key,"AES",{
    input:"string",
    output:"base64"
});

alert("AES加密结果", result);

//开始解密
let jiemiResult = $crypt.jiemi(result,key,"AES",{
    input:"base64",
    output:"string"
});


alert("AES解密结果", jiemiResult);





//示例结束
```


## $crypt-#U52a0#U5bc6#U7b97#U6cd5-01.#U5bf9#U79f0#U52a0#U5bc6-03.DES#U52a0#U5bc6

```javascript
//AIGame 官方示例


let key = "ACSDFGHJ";
let text = "我是被加密的明文";


let result = $crypt.jiami(text,key,"DES",{
    input:"string",
    output:"base64"
});

alert("DES加密",result)

let result2 = $crypt.jiemi(result,key,"DES",{
    input:"base64",
    output:"string"
});


alert("DES解密",result2)









//示例结束
```


## $crypt-#U52a0#U5bc6#U7b97#U6cd5-01.#U5bf9#U79f0#U52a0#U5bc6-04.RSA#U52a0#U5bc6

```javascript
//AIGame 官方示例




//生成密钥对
let keyPair = $crypt.generateKeyPair("RSA", 1024);

alert("RSA密钥信息", keyPair);

log("使用私钥加密");
let jiamiStr = $crypt.jiami("我是被加密的内容", keyPair.privateKey, "RSA/ECB/PKCS1Padding", {
    input: "string",
    output: "base64"
});
log(jiamiStr);

alert("RSA加密结果", jiamiStr);

log("使用公钥解密");
let jiemiStr = $crypt.jiemi(jiamiStr, keyPair.publicKey, "RSA/ECB/PKCS1Padding", {
    input: "base64",
    output: "string"
});
log(jiemiStr);


alert("RSA解密结果", jiemiStr);



//示例结束
```


## $crypt-#U52a0#U5bc6#U7b97#U6cd5-02.#U975e#U5bf9#U79f0#U52a0#U5bc6-01.#U6458#U8981#U52a0#U5bc6

```javascript
//AIGame 官方示例

//获得所有哈希算法的名称
let digests = $crypt.digests();

//每个算法都用一遍
for (let i = 0; i < digests.size(); i ++) {

    //(1)准备需要加密的明文
    let myData = "今天天气真好呀";
    //(2)准备用到的算法名称
    let algorithm = digests.get(i);
    let result = $crypt.digest(myData, algorithm, {
        input: "string",
        output: "hex"
    });
    
    alert("算法:"+algorithm,"加密后的数据:\n"+result);
    
}




//示例结束
```


## $crypt-#U52a0#U5bc6#U7b97#U6cd5-02.#U975e#U5bf9#U79f0#U52a0#U5bc6-02.MD5#U52a0#U5bc6(#U5de5#U5177#U7248)

```javascript
//AIGame 官方示例

//生成16位的md5加密盐值
let salt = $crypt.md5Key(16);

//(1)准备加密的明文
let myData = "今天天气真好!";
//(2)开始加密
let result1 = $crypt.md516(salt,myData);//md5加密成16位结果
let result2 = $crypt.md532(salt,myData);//md5加密成32位结果

alert("MD5加密:16位",result1);
alert("MD5加密:32位",result2);



//示例结束
```


## $crypt-#U52a0#U5bc6#U7b97#U6cd5-02.#U975e#U5bf9#U79f0#U52a0#U5bc6-03.MD5#U52a0#U5bc6(#U5e38#U89c4#U7248)

```javascript
//AIGame 官方示例

//(1)准备需要加密的明文
let myData = "今天天气真好呀";

//(2)开始加密
let result = $crypt.digest(myData, "MD5", {
    input: "string",
    output: "hex"
});

alert("MD5加密",result);


//示例结束
```


## $crypt-#U52a0#U5bc6#U7b97#U6cd5-03.#U6570#U5b57#U7b7e#U540d-01.DSA#U9a8c#U8bc1

```javascript
//AIGame 官方示例


//生成密钥对
let keyPair = $crypt.generateKeyPair("DSA", 1024);


alert("DSA密钥信息", keyPair);

log("签名:"); 
//数字签名只能用私钥进行签名
let signData = $crypt.sign("我是被签名的内容", keyPair.privateKey, "DSA", {
    input: "string",
    output: "byte"
});

//由于输出的是数组,所以使用join方法转换成字符串
alert("DSA签名结果", signData.join());

log("验证:"); 
//数字签名只能用公钥进行验证
let verified = $crypt.verify("我是被签名的内容",signData, keyPair.publicKey, "DSA", {
    //(1)这个配置是签名时的配置(需要和上面sign参数保持一致)
    input: "string",
    output: "byte"
},{
    //(2)这个配置是验证的数据配置
    //输入签名的类型
    input: "byte",
});


alert("DSA验证结果", verified);





//示例结束
```


## $date-#U65e5#U671f#U4e0e#U65f6#U95f4-01.#U65e5#U671f#U65f6#U95f4#U5b57#U7b26#U4e32

```javascript
//官方示例

let dateStr = $date.dt();

alert("日期时间字符串",dateStr);//2025-10-25 18:32:53


//示例结束
```


## $date-#U65e5#U671f#U4e0e#U65f6#U95f4-02.#U65e5#U671f#U5b57#U7b26#U4e32

```javascript
//官方示例

let dateStr = $date.d();

alert("日期时间字符串",dateStr);//2025-10-25


//示例结束
```


## $date-#U65e5#U671f#U4e0e#U65f6#U95f4-03.#U89e3#U6790#U65e5#U671f#U5b57#U7b26#U4e32

```javascript
//官方示例

let date = $date.parse("2025/12/08 12/35/24","yyyy/MM/dd HH/mm/ss");
//获得日期对象
alert("日期对象",date);//Dec 8, 2025 12:35:24 PM


//示例结束
```


## $date-#U65e5#U671f#U4e0e#U65f6#U95f4-04.#U89e3#U6790#U65e5#U671f

```javascript
//官方示例

//无需日期模板，自动匹配
let date = $date.parse("2025/12/08 12/35/24");
//获得日期对象
alert("日期对象",date);//Dec 8, 2025 12:35:24 PM


//示例结束
```


## $date-#U65e5#U671f#U4e0e#U65f6#U95f4-05.#U65e5#U671f#U4fe1#U606f

```javascript
//官方示例

//获取当前日期信息
let info = $date.info();

alert("日期信息",info);


//示例结束
```


## $date-#U65e5#U671f#U4e0e#U65f6#U95f4-06.#U683c#U5f0f#U5316

```javascript
//官方示例

//格式化指定日期
let info = $date.format(1747985594110,"yyyy年MM月dd日 HH时mm分ss秒");

alert("日期信息",info);


//示例结束
```


## $date-#U65e5#U671f#U4e0e#U65f6#U95f4-07.#U65b0#U5efa#U65e5#U671f#U5bf9#U8c61

```javascript
//官方示例

//新建日期对象
let date = $date.date();

alert("日期对象",date);


//示例结束
```


## $date-#U65e5#U671f#U4e0e#U65f6#U95f4-08.#U65f6#U95f4#U5b57#U7b26#U4e32

```javascript
//官方示例

//将时间戳转为时间描述
let info = $date.dur(1234567890);

alert("时间", info);//14天6时56分7秒


//示例结束
```


## $log-#U65e5#U5fd7#U6846#U67b6-01.#U6253#U5370#U4fe1#U606f#U65e5#U5fd7

```javascript
// AIGame官方示例


$log.i("信息");




// 示例结束
```


## $log-#U65e5#U5fd7#U6846#U67b6-02.#U6253#U5370#U8c03#U8bd5#U65e5#U5fd7

```javascript
// AIGame官方示例


$log.d("调试");




// 示例结束
```


## $log-#U65e5#U5fd7#U6846#U67b6-03.#U6253#U5370#U8b66#U544a#U65e5#U5fd7

```javascript
// AIGame官方示例


$log.w("警告");




// 示例结束
```


## $log-#U65e5#U5fd7#U6846#U67b6-04.#U6253#U5370#U5f02#U5e38#U65e5#U5fd7

```javascript
// AIGame官方示例


$log.e("异常");




// 示例结束
```


## $log-#U65e5#U5fd7#U6846#U67b6-05.#U6253#U5370#U5197#U4f59#U65e5#U5fd7

```javascript
// AIGame官方示例


$log.v("冗余");




// 示例结束
```


## $log-#U65e5#U5fd7#U6846#U67b6-06.#U6253#U5370#U65e5#U5fd7

```javascript
// AIGame官方示例


$log.log("hello");




// 示例结束
```


## $log-#U65e5#U5fd7#U6846#U67b6-07.#U6253#U5f00#U65e5#U5fd7#U60ac#U6d6e#U7a97

```javascript
// AIGame官方示例


$log.floaty();




// 示例结束
```


## $media-#U97f3#U9891#U64ad#U653e-01.#U76f4#U63a5#U64ad#U653e

```javascript
//官方示例

// 我自己放了几个音频文件，你可以自己选择一个播放
let resArr = [
"example/$media - 音频播放/res/qq系统提示音.mp3",
"example/$media - 音频播放/res/开机音效.mp3",
"example/$media - 音频播放/res/微信消息.mp3",
"example/$media - 音频播放/res/短信音效.mp3"
];

// 开始播放音频
$media.play(resArr[0]);


//示例结束
```


## $qr-#U4e8c#U7ef4#U7801#U5de5#U5177-#U751f#U6210#U4e8c#U7ef4#U7801-#U5168#U90e8#U53c2#U6570

```javascript
//生成二维码
let img = $qr.make("Hello AIGame !", {
    w: 500,//宽度(默认:500)
    h: 500,//高度(默认:500)
    margin: 2,//边距(默认:2)
    foreColor: "#2AACB8",//前景色(默认:#000000)
    bgColor: "#2B2D30",//背景色(默认:#FFFFFF)
});

if (img != null) {
    //显示图片
    img.show(); //或者调用 showImg(img); 全局函数也可也显示图片

    //保存到本地
    img.save("/sdcard/qr.png");
}





//..
```


## $qr-#U4e8c#U7ef4#U7801#U5de5#U5177-#U751f#U6210#U4e8c#U7ef4#U7801

```javascript
//生成二维码
let img = $qr.make("欢迎来到AIGame!");

//显示图片
img.show();//或者调用 showImg(img); 全局函数也可也显示图片

//保存到本地
img.save("/sdcard/qr.png");
```


## $qr-#U4e8c#U7ef4#U7801#U5de5#U5177-#U8bc6#U522b#U4e8c#U7ef4#U7801

```javascript
//显示图片
showImg("./example/$qr - 二维码工具/imgs/t01.png");
//解析这个二维码内容
let content = $qr.parse("./example/$qr - 二维码工具/imgs/t01.png");
//显示内容
alert("二维码内容",content);
```


## $str-#U5b57#U7b26#U4e32#U5de5#U5177-01.#U968f#U673a#U5b57#U7b26#U4e32

```javascript
//官方示例

let str = $str.random("abcdefghijk");

alert("随机字符",str);






//示例结束
```


## $str-#U5b57#U7b26#U4e32#U5de5#U5177-02.#U968f#U673a#U5b57#U7b26#U4e32#U5217#U8868

```javascript
//官方示例

let str = $str.random(["abc","defg","hijk","lmn","opq","rst"]);

alert("随机字符列表",str);






//示例结束
```


## $str-#U5b57#U7b26#U4e32#U5de5#U5177-03.#U622a#U53d6#U5f00#U5934

```javascript
//官方示例

let str = $str.subStart("ABCDEFG",3);

alert("截取开头",str);






//示例结束
```


## $str-#U5b57#U7b26#U4e32#U5de5#U5177-04.#U622a#U53d6#U672b#U5c3e

```javascript
//官方示例

let str = $str.subEnd("ABCDEFG",3);

alert("截取末尾",str);






//示例结束
```


## $str-#U5b57#U7b26#U4e32#U5de5#U5177-05.#U53bb#U9664#U9996#U4f4d#U7a7a#U683c

```javascript
//官方示例

let str = $str.trim("   嗯？   ");

alert("去除首尾空格",str);






//示例结束
```


## $tts-#U8bed#U97f3#U9605#U8bfb-01.#U64ad#U653e#U6587#U672c(#U914d#U7f6e)

```javascript
// AIGame官方示例


let options = {
    rate: 1,//速度
    pitch: 1,//音调
    volume: 1,//音量
    language: "zh",//语言
    streamType: "system"//播放流('system'播放声音最大)
}


$tts.read("你好呀，早安~",options);




// 示例结束
```


## $tts-#U8bed#U97f3#U9605#U8bfb-02.#U64ad#U653e#U6587#U672c

```javascript
// AIGame官方示例


$tts.read("你好呀，早安~");




// 示例结束
```


## E4X#U652f#U6301-E4X-#U5c5e#U6027#U6ce8#U5165

```javascript
//属性注入
var empId = "E001";
var status = "active";
var employee2 = <employee id={empId} status={status}>
    <name>{"Employee " + empId}</name>
    <created>{new Date().getFullYear()}</created>
</employee>;
console.log("属性注入: " + employee2.toXMLString());
```


## E4X#U652f#U6301-E4X-#U5f02#U5e38#U5904#U7406

```javascript
// 错误处理示例
try {
    var riskyValue = null;
    var safeXml = <test>
        <value>{riskyValue !== null ? riskyValue : "default"}</value>
    </test>;
    console.log("安全注入:" + safeXml.toXMLString());
} catch(e) {
    console.log("注入异常:" + e.message);
}
```


## E4X#U652f#U6301-E4X-#U6ce8#U5165#U51fd#U6570

```javascript
// 注入函数调用
function formatSalary(salary) {
    return "$" + salary.toLocaleString();
}

var salary = 75000;
var myEmployee = <employee>
    <name>格式化薪资</name>
    <salary>{formatSalary(salary)}</salary>
    <tax>{Math.round(salary * 0.2)}</tax>
</employee>;

console.log("注入函数: " + myEmployee.toXMLString());
```


## E4X#U652f#U6301-E4X-#U6ce8#U5165#U53d8#U91cf

```javascript
// 注入变量
var name = "John";
var age = 30;
var dept = "IT";

// 注入到元素内容中
var employee1 = <employee id="1">
    <name>{name}</name>
    <age>{age}</age>
    <department>{dept.toUpperCase()}</department>
</employee>;

console.log("注入变量: " + employee1.toXMLString());
```


## E4X#U652f#U6301-E4X-#U8ba1#U7b97#U5c5e#U6027

```javascript
// 计算属性值
var dynamicAttr = "customValue";
var dynamicElement = <element {"attr-" + "name"}={dynamicAttr} custom={true}>
    <content>{dynamicAttr.toUpperCase()}</content>
</element>;

console.log("计算属性: " + dynamicElement.toXMLString());
```


## E4X#U652f#U6301-E4X-UI#U4ea4#U4e92

```javascript
//此示例简单的演示E4X与UI的交互

let getButtonText = function () {
    return "我是按钮";
}

//E4X中调用js函数
let uiXml = <ui>
    <statusbar />
    <linear w="max" h="max" gravity="center">
        <button text={getButtonText()} />
    </linear>
</ui>;

//解析xml并显示
let ui = $ui.layout(uiXml);
ui.show();
```
