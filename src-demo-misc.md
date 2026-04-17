# 示例：拓展示例与综合案例


## #U5168#U5c40#U51fd#U6570-01.#U7761#U7720

```javascript
//官方示例

//停止1秒钟
sleep(1000);







//示例结束
```


## #U5168#U5c40#U51fd#U6570-02.#U571f#U53f8

```javascript
//官方示例



toast("我是土司");






//示例结束
```


## #U5168#U5c40#U51fd#U6570-03.#U63d0#U793a

```javascript
//官方示例



tip("我是提示");






//示例结束
```


## #U5168#U5c40#U51fd#U6570-04.#U63d0#U793a#U5bf9#U8bdd#U6846

```javascript
//官方示例


alert("提示对话框","我很好");



//示例结束
```


## #U5168#U5c40#U51fd#U6570-06.#U526a#U5207#U677f

```javascript
//官方示例


setClip("设置的内容");

if(hasClip()){
    let clip = getClip();
    alert("剪切板内容",clip);
}

//清空剪切板
clearClip();

//示例结束
```


## #U5168#U5c40#U51fd#U6570-07.#U968f#U673a#U51fd#U6570

```javascript
//官方示例


let num1 = random();//0-1之间的随机数
alert("随机数(0-1)",num1);

let num2 = random(10);//0-10之间的随机数(不包含10)
alert("随机数(0-10)",num2);

let num3 = random(10,30);//0-10之间的随机数
alert("随机数(10-30)",num3);


//示例结束
```


## #U5168#U5c40#U51fd#U6570-08.#U5168#U5c40#U571f#U53f8

```javascript
//官方示例


//本质上是一个悬浮窗提示土司
info("我是土司");


//示例结束
```


## #U62d3#U5c55#U793a#U4f8b-01.#U6388#U6743#U65e0#U969c#U788d-#U6839#U636e#U5305#U540d#U5224#U65ad#U662f#U5426#U6709#U65e0#U969c#U788d

```javascript
//AIGame官方示例

//这个示例很好的展现了脚本与安卓API的交互，你可以实现任何你想实现的功能

//这里就是与java交互的代码：新版本中，直接定义即可：
var Settings = android.provider.Settings;
var TextUtils = android.text.TextUtils;


let hasAccessibilityPermis = function(pkgName) {
    let accessibilityEnabled = 0;
    let packageName = pkgName.toUpperCase();
    let contentResolver = context.getContentResolver();
    try {
        accessibilityEnabled = Settings.Secure.getInt(contentResolver, Settings.Secure.ACCESSIBILITY_ENABLED);
    } catch (err) {
        //系统不支持无障碍服务
        return false;
    }
    let splitter = new TextUtils.SimpleStringSplitter(':');
    if (accessibilityEnabled == 1) {
        let settingValue = Settings.Secure.getString(contentResolver, Settings.Secure.ENABLED_ACCESSIBILITY_SERVICES);
        if (settingValue != null) {
            splitter.setString(settingValue);
            while (splitter.hasNext()) {
                let acServiceName = splitter.next().toUpperCase();
                if (acServiceName.contains(packageName)) {
                    return true;
                }
            }
        }
    }
    return false;
}



//测试一下：应用"org.aigame.pro"是否获取了无障碍权限
//alert("类名",hasAccessibilityPermis("org.aigame.pro"));




//导出这个函数
hasAccessibilityPermis;



//示例结束
```


## #U62d3#U5c55#U793a#U4f8b-01.#U6388#U6743#U65e0#U969c#U788d-#U6839#U636e#U5305#U540d#U83b7#U53d6#U65e0#U969c#U788d#U7c7b#U540d

```javascript
//AIGame官方示例

//这个示例很好的展现了脚本与安卓API的交互，你可以实现任何你想实现的功能

//这里就是与java交互的代码：新版本中，不再使用任何关键字或者方法属性来导入包，而是直接定义即可：
var PackageInfo = android.content.pm.PackageInfo;
var PackageManager = android.content.pm.PackageManager;
var PackageInfo = android.content.pm.ServiceInfo;
var AccessibilityService = android.accessibilityservice.AccessibilityService;
var Intent = android.content.Intent;

// 判断ServiceInfo是否为无障碍服务
let isAccessibilityService = function(serviceInfo) {
    // 方法1：检查服务权限
    if (serviceInfo.permission != null && serviceInfo.permission.equals("android.permission.BIND_ACCESSIBILITY_SERVICE")) {
        return true;
    }
    // 方法2：使用 GET_RESOLVED_FILTER 标志获取 intent filter
    let intent = new Intent(AccessibilityService.SERVICE_INTERFACE);
    let resolveInfoList = context.getPackageManager().queryIntentServices(intent, PackageManager.GET_RESOLVED_FILTER);
    for (let resolveInfo of resolveInfoList) {
        if (resolveInfo.serviceInfo.name.equals(serviceInfo.name) && resolveInfo.serviceInfo.packageName.equals(serviceInfo.packageName)) {
            return true;
        }
    }
    return false;
}


// 获取应用的无障碍服务类名列表
let getAccessibilityServiceClass = function(packageName) {
    // 获取应用服务信息（包含无障碍服务）
    let packageInfo = context.getPackageManager().getPackageInfo(packageName, PackageManager.GET_SERVICES | PackageManager.GET_META_DATA);
    if (packageInfo.services != null) {
        for (let service of packageInfo.services) {
            // 通过权限和 intent-filter 判断是否为无障碍服务
            if (isAccessibilityService(service)) {
                return service.name;
            }
        }
    }
    return null;
}

//测试一下：获取包名为"org.aigame.pro"的无障碍类名
//alert("类名",getAccessibilityServiceClass("org.aigame.pro"));




//导出这个函数
getAccessibilityServiceClass;





//示例结束
```


## #U62d3#U5c55#U793a#U4f8b-01.#U6388#U6743#U65e0#U969c#U788d-main

```javascript
//AIGame官方示例

//注意：本示例并不完善，只用于参考和学习

let hasAccessibilityPermis = require("example/拓展示例/01.授权无障碍/根据包名判断是否有无障碍.js");
let getAccessibilityServiceClassName = require("example/拓展示例/01.授权无障碍/根据包名获取无障碍类名.js");

//解析界面并且显示
let ui = $ui.layout("example/拓展示例/01.授权无障碍/ui.xml");
ui.show();
ui.id("mAppbar").back(()=> {
    ui.finish();
});
ui.id("mAppbar").menu((title)=> {
    if(title=="帮助"){
        alert("帮助","你需要先获取Shizuku的授权，之后就可以给其他应用授权无障碍服务了");
    }
});

//获取列表控件
let ls = ui.id("mLs");

//刷新列表中的应用信息数据
let flushList = function() {
    //获取应用列表信息
    let allAppList = $app.lsUserApp(); //所有的应用：但是不是所有的应用都需要无障碍
    let newAppList = [];
    for (let info of allAppList) {
        let clsName = getAccessibilityServiceClassName(info.pkgName);
        if (clsName == null || clsName.trim().isEmpty()) {
            //无障碍类名为空说明这个app就不需要获取无障碍权限
            continue;
        }
        newAppList.push(info);
    }
    //刷新列表数据：只显示需要无障碍授权的应用
    ls.flush(newAppList);
}


//绑定视图解析
ls.bindHolder((holder,data,position)=> {
    holder.id("appName").setText(data.appName);
    holder.id("pkgName").setText(data.pkgName);
    holder.id("appIcon").setImg(data.icon.getBitmap());
    //设置图标放在子线程中
//    $thread.run(()=>{
//        let iconImg = $app.getIcon(data.pkgName);
//        if(iconImg!=null){
//            holder.id("appIcon").setImg(iconImg.getBitmap());
//        }
//    });

    let permitStatus = holder.id("permitStatus");
    if (hasAccessibilityPermis(data.pkgName)) {
        permitStatus.setText("已授权");
        permitStatus.setColor("#3574F0");
    } else {
        permitStatus.setText("未授权");
        permitStatus.setColor("#FF0000");
    }
    holder.id("card").click(()=> {
        //点击后开始给当前应用进行授权
        if ($szk.hasPermit()) {
            let clsName = getAccessibilityServiceClassName(data.pkgName);
            if (clsName == null || clsName.trim().isEmpty()) {
                toast("当前应用无需无障碍权限");
            } else {
                $tip.show(data.appName,"点击确定开始为应用授权无障碍权限：\n\n应用:"+data.appName+"\n包名:"+data.pkgName+"\n类名:\n"+clsName,()=> {
                    $szk.exe("settings put secure enabled_accessibility_services "+data.pkgName+"/"+clsName,(info)=> {
                        $log.d(info);
                    },(err)=> {
                        $log.e(err);
                    },(result)=> {
                        holder.id("permitStatus").snack("正在授权...");
                        //如果result为null一般就说明当前命令执行成功，没有任何异常信息产生
                        log(result);
                        if (result == null || result == "null") {
                            log("执行成功");
                        }
                        sleep(3000); //该命令执行后未必马上生效，所以3秒后刷新一下列表
                        holder.id("permitStatus").snack("授权完毕");
                        flushList(); //刷新列表
                    });
                });
            }
        } else {
            alert("无Shizuku授权","请先用Shizuku为本app授权");
        }
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


## #U6a21#U5757#U5f00#U53d1-01.#U51fd#U6570#U6a21#U5757-#U6a21#U5757#U4ee3#U7801

```javascript
//写一个函数
let add = function(a,b){
    return a+b
}
//导出函数
add;//不要写成"add()"了这个是调用函数
```


## #U6a21#U5757#U5f00#U53d1-02.#U5bf9#U8c61#U6a21#U5757-#U6a21#U5757#U4ee3#U7801

```javascript
//写一个对象
let obj = {
    name:"张三",
    age:18,
    sex:"男"
}

//导出对象
obj;
```


## #U6a21#U5757#U5f00#U53d1-03.#U7c7b#U6a21#U5757-#U6a21#U5757#U4ee3#U7801

```javascript
function MyClass(){
    this.name = "张三";
    this.age = 18;

    this.show = function(){
        alert("我的信息",this.name+"\n"+this.age);
    }
}

MyClass;//导出类
```


## #U811a#U672c#U8bed#U6cd5-01.#U53d8#U91cf#U58f0#U660e

```javascript
// var声明（函数作用域）
var globalVar = "我是全局变量";
function testVar() {
    var funcVar = "我是函数内变量";
    console.log("函数内var变量:", funcVar); // 输出: 函数内var变量: 我是函数内变量
}
testVar();
console.log("全局var变量:", globalVar); // 输出: 全局var变量: 我是全局变量

// let声明（块级作用域）
let blockLet = "块外let变量";
if (true) {
    let blockLet = "块内let变量";
    console.log("块内let变量:", blockLet); // 输出: 块内let变量: 块内let变量
}
console.log("块外let变量:", blockLet); // 输出: 块外let变量: 块外let变量

// const声明（常量）
const PI = 3.14159;
console.log("常量PI:", PI); // 输出: 常量PI: 3.14159
// PI = 3.14; // 报错：常量不能重新赋值
```


## #U811a#U672c#U8bed#U6cd5-02.#U6570#U636e#U7c7b#U578b

```javascript
// 原始类型
console.log("undefined类型:", typeof undefined); // 输出: undefined类型: undefined
console.log("null类型:", typeof null); // 输出: null类型: object（特殊情况）
console.log("布尔类型:", typeof true); // 输出: 布尔类型: boolean
console.log("数字类型:", typeof 123); // 输出: 数字类型: number
console.log("字符串类型:", typeof "hello"); // 输出: 字符串类型: string

// 引用类型
var obj = {name: "测试对象"};
var arr = [1, 2, 3];
var func = function() {};
console.log("对象类型:", typeof obj); // 输出: 对象类型: object
console.log("数组类型:", typeof arr); // 输出: 数组类型: object
console.log("函数类型:", typeof func); // 输出: 函数类型: function
```


## #U811a#U672c#U8bed#U6cd5-03.#U8fd0#U7b97#U7b26

```javascript
// 算术运算符
var a = 10, b = 3;
console.log("加法:", a + b); // 输出: 加法: 13
console.log("除法:", a / b); // 输出: 除法: 3.3333333333333335
console.log("取余:", a % b); // 输出: 取余: 1

// 比较运算符
console.log("等于(==):", 5 == "5"); // 输出: 等于(==): true
console.log("严格等于(===):", 5 === "5"); // 输出: 严格等于(===): false

// 逻辑运算符
console.log("与运算:", true && false); // 输出: 与运算: false
console.log("或运算:", true || false); // 输出: 或运算: true
```


## #U811a#U672c#U8bed#U6cd5-04.#U6761#U4ef6#U8bed#U53e5

```javascript
// if-else语句
var score = 85;
if (score >= 90) {
    console.log("优秀");
} else if (score >= 80) {
    console.log("良好"); // 输出: 良好
} else {
    console.log("及格");
}

// switch语句
var day = 3;
switch (day) {
    case 1:
        console.log("星期一");
        break;
    case 2:
        console.log("星期二");
        break;
    case 3:
        console.log("星期三"); // 输出: 星期三
        break;
    default:
        console.log("其他天");
}
```


## #U811a#U672c#U8bed#U6cd5-05.#U5faa#U73af#U8bed#U53e5

```javascript
// for循环
console.log("for循环:");
for (var i = 1; i <= 3; i++) {
    console.log("  循环次数:", i); // 依次输出1, 2, 3
}

// for-in循环
var person = {name: "张三", age: 20, gender: "男"};
console.log("for-in循环:");
for (var key in person) {
    console.log("  " + key + ":", person[key]); // 输出所有属性
}

// while循环
console.log("while循环:");
var count = 0;
while (count < 3) {
    console.log("  计数:", count); // 依次输出0, 1, 2
    count++;
}
```


## #U811a#U672c#U8bed#U6cd5-06.#U51fd#U6570#U5b9a#U4e49

```javascript
// 命名函数
function add(a, b) {
    return a + b;
}
console.log("add(2, 3) =", add(2, 3)); // 输出: add(2, 3) = 5

// 匿名函数
var multiply = function(a, b) {
    return a * b;
};
console.log("multiply(4, 5) =", multiply(4, 5)); // 输出: multiply(4, 5) = 20

// 自执行函数
(function() {
    console.log("自执行函数被调用了"); // 输出: 自执行函数被调用了
})();
```


## #U811a#U672c#U8bed#U6cd5-07.#U5bf9#U8c61#U4e0e#U5c5e#U6027

```javascript
// 对象字面量
var car = {
    brand: "特斯拉",
    price: 300000,
    run: function() {
        console.log(this.brand + "正在行驶");
    }
};
console.log("汽车品牌:", car.brand); // 输出: 汽车品牌: 特斯拉
console.log("汽车价格:", car["price"]); // 输出: 汽车价格: 300000
car.run(); // 输出: 特斯拉正在行驶


car.showType = function() {
    return typeof this;
};
console.log("car的类型:", car.showType()); // 输出: car的类型: object
```


## #U811a#U672c#U8bed#U6cd5-08.#U6570#U7ec4#U64cd#U4f5c

```javascript
var fruits = ["苹果", "香蕉", "橙子"];
console.log("数组长度:", fruits.length); // 输出: 数组长度: 3

// 添加元素
fruits.push("葡萄");
console.log("添加后数组:", fruits); // 输出: 添加后数组: 苹果,香蕉,橙子,葡萄

// 遍历数组
console.log("数组元素:");
fruits.forEach(function(fruit, index) {
    console.log("  索引" + index + ":", fruit); // 输出所有元素
});

// 数组方法
var numbers = [3, 1, 4, 1, 5];
numbers.sort();
console.log("排序后数组:", numbers); // 输出: 排序后数组: 1,1,3,4,5
```


## #U811a#U672c#U8bed#U6cd5-09.#U5b57#U7b26#U4e32#U65b9#U6cd5

```javascript
var str = "Hello, Rhino!";
console.log("字符串长度:", str.length); // 输出: 字符串长度: 12
console.log("子串位置:", str.indexOf("Rhino")); // 输出: 子串位置: 7
console.log("截取子串:", str.substring(0, 5)); // 输出: 截取子串: Hello
console.log("分割字符串:", str.split(",")); // 输出: 分割字符串: Hello, Rhino!
console.log("小写转换:", str.toLowerCase()); // 输出: 小写转换: hello, rhino!
```


## #U811a#U672c#U8bed#U6cd5-10.#U6b63#U5219#U8868#U8fbe#U5f0f

```javascript
var text = "Rhino 1.8.0 is a JavaScript engine";
var pattern = /Rhino/;
console.log("是否匹配:", pattern.test(text)); // 输出: 是否匹配: true

var versionPattern = /\d+\.\d+\.\d+/;
console.log("版本号:", text.match(versionPattern)); // 输出: 版本号: 1.8.0

var globalPattern = /s/g;
console.log("全局匹配:", text.match(globalPattern)); // 输出: 全局匹配: s,s
```


## #U811a#U672c#U8bed#U6cd5-11.#U81ea#U5b9a#U4e49#U5f02#U5e38

```javascript
try {
    console.log("尝试执行代码");
    var result = 10 / 0; // 不会抛出异常，但会得到Infinity
    console.log("除法结果:", result); // 输出: 除法结果: Infinity

    // 主动抛出异常
    throw new Error("这是一个自定义错误");
} catch (e) {
    console.log("捕获到异常:", e.message); // 输出: 捕获到异常: 这是一个自定义错误
} finally {
    console.log("无论是否异常，都会执行"); // 输出: 无论是否异常，都会执行
}
```


## #U811a#U672c#U8bed#U6cd5-12.JSON#U652f#U6301

```javascript
var user = {name: "李四", age: 30, hobbies: ["读书", "运动"]};
// 对象转JSON
var jsonStr = JSON.stringify(user);
console.log("JSON字符串:", jsonStr); // 输出: {"name":"李四","age":30,"hobbies":["读书","运动"]}

// JSON转对象
var parsedUser = JSON.parse(jsonStr);
console.log("解析后的对象:", parsedUser.name); // 输出: 解析后的对象: 李四
```


## #U811a#U672c#U8bed#U6cd5-13.#U65e5#U671f#U4e0e#U65f6#U95f4

```javascript
var now = new Date();
console.log("当前日期:", now.toLocaleString()); // 输出本地日期时间
console.log("时间戳:", now.getTime()); // 输出毫秒级时间戳
console.log("年份:", now.getFullYear()); // 输出当前年份
console.log("月份:", now.getMonth() + 1); // 输出当前月份（注意月份从0开始）
```


## #U811a#U672c#U8bed#U6cd5-14.#U6a21#U5757#U5316#U6784#U9020

```javascript
// 模块模式：使用立即执行函数创建独立作用域
var Calculator = (function() {
    // 私有方法
    function validateNumber(n) {
        if (typeof n !== "number" || isNaN(n)) {
            throw new Error("无效的数字: " + n);
        }
    }

    // 私有常量
    var PI = 3.1415926535;

    // 公共接口
    return {
        add: function(a, b) {
            validateNumber(a);
            validateNumber(b);
            return a + b;
        },
        multiply: function(a, b) {
            validateNumber(a);
            validateNumber(b);
            return a * b;
        },
        circleArea: function(radius) {
            validateNumber(radius);
            return PI * radius * radius;
        }
    };
})();

// 测试模块
console.log("加法结果:", Calculator.add(2, 3)); // 输出: 5
console.log("乘法结果:", Calculator.multiply(4, 5)); // 输出: 20
console.log("圆面积(半径2):", Calculator.circleArea(2)); // 输出: 12.566370614

// 尝试访问私有成员（会失败）
console.log("尝试访问私有PI:", Calculator.PI); // 输出: undefined
```


## #U811a#U672c#U8bed#U6cd5-15.#U6a21#U62df#U5f02#U6b65#U8bf7#U6c42

```javascript
// 模拟异步操作
function fetchData(url, callback) {
    console.log("开始请求:", url);

    // 使用Java线程模拟异步延迟
    var thread = new java.lang.Thread(function() {
        try {
            // 模拟网络延迟（1秒）
            java.lang.Thread.sleep(1000);

            // 模拟返回数据
            var data = {
                url: url,
                content: "模拟从" + url + "获取的数据",
                timestamp: new Date().getTime()
            };

            // 执行回调函数
            callback(null, data);
        } catch (e) {
            callback(e, null);
        }
    });

    thread.start();
}

// 串行执行多个异步操作
console.log("开始串行异步操作");
fetchData("https://api.example.com/data1", function(err, data1) {
    if (err) {
        console.log("错误:", err);
        return;
    }
    console.log("收到数据1:", data1.content);

    fetchData("https://api.example.com/data2", function(err, data2) {
        if (err) {
            console.log("错误:", err);
            return;
        }
        console.log("收到数据2:", data2.content);
        console.log("所有异步操作完成");
    });
});

// 等待异步操作完成（Rhino会等待所有线程结束）
java.lang.Thread.sleep(2500);
```


## #U811a#U672c#U8bed#U6cd5-16.#U95ed#U5305#U4e0e#U9ad8#U9636#U51fd#U6570

```javascript
// 闭包实现计数器工厂
function createCounter(initialValue) {
    var count = initialValue; // 私有变量（闭包保存）

    return {
        increment: function(step) {
            count += (step || 1);
            return count;
        },
        decrement: function(step) {
            count -= (step || 1);
            return count;
        },
        getCount: function() {
            return count;
        },
        reset: function() {
            count = initialValue;
        }
    };
}

// 创建两个独立计数器
var counter1 = createCounter(0);
var counter2 = createCounter(100);

console.log("counter1初始值:", counter1.getCount()); // 输出: 0
console.log("counter1+3:", counter1.increment(3)); // 输出: 3
console.log("counter1-1:", counter1.decrement()); // 输出: 2

console.log("counter2初始值:", counter2.getCount()); // 输出: 100
console.log("counter2+50:", counter2.increment(50)); // 输出: 150

// 高阶函数：函数作为参数
function processNumbers(numbers, processor) {
    var result = [];
    for (var i = 0; i < numbers.length; i++) {
        result.push(processor(numbers[i]));
    }
    return result;
}

var numbers = [1, 2, 3, 4];
var squared = processNumbers(numbers, function(n) {
    return n * n;
});
console.log("平方处理结果:", squared); // 输出: [1, 4, 9, 16]

var doubled = processNumbers(numbers, function(n) {
    return n * 2;
});
console.log("加倍处理结果:", doubled); // 输出: [2, 4, 6, 8]
```


## #U811a#U672c#U8bed#U6cd5-17.#U9ad8#U7ea7#U6b63#U5219#U8868#U8fbe#U5f0f

```javascript
// 1. 解析URL
var url = "https://www.example.com:8080/path?name=test&age=20#fragment";
var urlPattern = /^(\w+):\/\/([\w.]+):?(\d*)?([^?#]+)?\??([^#]*)?#?(.*)?$/;

var matches = url.match(urlPattern);
if (matches) {
    console.log("URL解析结果:");
    console.log("  协议:", matches[1]); // 输出: https
    console.log("  域名:", matches[2]); // 输出: www.example.com
    console.log("  端口:", matches[3] || "默认"); // 输出: 8080
    console.log("  路径:", matches[4]); // 输出: /path
    console.log("  查询参数:", matches[5]); // 输出: name=test&age=20
    console.log("  锚点:", matches[6]); // 输出: fragment
}

// 2. 复杂替换（驼峰命名转下划线）
function camelToUnderscore(str) {
    return str.replace(/([A-Z])/g, function(match, p1, offset) {
        return (offset > 0 ? "_" : "") + p1.toLowerCase();
    });
}

var testStr = "userName ageInYears isActive";
console.log("驼峰转下划线:", camelToUnderscore(testStr));
// 输出: user_name age_in_years is_active

// 3. 验证邮箱格式
function validateEmail(email) {
    var pattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
    return pattern.test(email);
}

var emails = ["test@example.com", "invalid-email", "user.name+tag@domain.co"];
emails.forEach(function(email) {
    console.log("邮箱'" + email + "'是否有效:", validateEmail(email));
});
// 输出:
// 邮箱'test@example.com'是否有效: true
// 邮箱'invalid-email'是否有效: false
// 邮箱'user.name+tag@domain.co'是否有效: true
```


## #U811a#U672c#U8bed#U6cd5-18.promise

```javascript
function asyncOperation() {
    return new Promise((resolve, reject) => {
        sleep(1000);
        const success = true;
        if (success) {
            resolve('Operation successful');
        } else {
            reject('Operation failed');
        }
    });
}

asyncOperation()
.then((result) => {
    console.log(result);
})
.catch((error) => {
    console.log(error);
});
```


## #U811a#U672c#U8bed#U6cd5-19.#U95ed#U5305

```javascript
function outerFunction() {
    var outerVariable = 'I am from outer function';

    function innerFunction() {
        console.log(outerVariable);
    }

    return innerFunction;
}

var closure = outerFunction();
closure();
```


## #U811a#U672c#U8bed#U6cd5-20.#U4ee3#U7406

```javascript
var target = {
    name: 'John',
    age: 30
};

var handler = {
    get: function(target, property) {
        console.log(`Getting property ${property}`);
        return target[property];
    },
    set: function(target, property, value) {
        console.log(`Setting property ${property} to ${value}`);
        target[property] = value;
        return true;
    }
};

var proxy = new Proxy(target, handler);
console.log(proxy.name);
proxy.age = 31;
```


## #U811a#U672c#U8bed#U6cd5-21.#U5bf9#U8c61#U64cd#U4f5c

```javascript
// 对象操作
var person = {
    name: 'John',
    age: 30
};
console.log(person.name);
person.gender = 'male';
console.log(person);
```


## #U811a#U672c#U8bed#U6cd5-22.#U9ad8#U9636#U51fd#U6570

```javascript
function multiplyBy(factor) {
    return function(number) {
        return number * factor;
    };
}

var double = multiplyBy(2);
var triple = multiplyBy(3);

console.log(double(5));
console.log(triple(5));
```


## #U811a#U672c#U8bed#U6cd5-23.#U56de#U8c03#U51fd#U6570

```javascript
function fetchData(callback) {
    sleep(1000);
    var data = 'Some data from server';
    callback(data);
}

fetchData(function(result) {
    console.log(result);
});
```


## #U811a#U672c#U8bed#U6cd5-24.#U751f#U6210#U5f0f#U51fd#U6570

```javascript
function* generatorFunction() {
    yield 1;
    yield 2;
    yield 3;
}

var gen = generatorFunction();
console.log(gen.next().value);
console.log(gen.next().value);
console.log(gen.next().value);
```


## #U811a#U672c#U8bed#U6cd5-25.#U539f#U578b#U94fe

```javascript
// 构造函数
function Animal(name) {
    this.name = name;
}

// 原型方法
Animal.prototype.speak = function() {
    console.log(this.name + ' makes a noise.');
};

// 子类构造函数
function Dog(name) {
    Animal.call(this, name);
}

// 继承原型
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

// 重写方法
Dog.prototype.speak = function() {
    console.log(this.name + ' barks.');
};

var dog = new Dog('Buddy');
dog.speak();
```


## #U811a#U672c#U8bed#U6cd5-26.#U6b63#U5219#U8868#U8fbe#U5f0f

```javascript
// 检查字符串是否包含邮箱格式的文本
const strWithEmail = "Contact me at test@example.com";
const emailRegex = /\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b/;
const hasEmail = emailRegex.test(strWithEmail);
console.log(`字符串是否包含邮箱: ${hasEmail}`);

// 提取字符串里的所有数字
const strWithNumbers = "There are 12 apples and 3 bananas";
const numberRegex = /\d+/g;
const numbers = strWithNumbers.match(numberRegex);
console.log("提取到的数字: "+ numbers);
```


## #U811a#U672c#U8bed#U6cd5-27.#U7c7b#U578b#U6821#U9a8c

```javascript
// 示例1：基本类型检查
function Animal(name) {
    this.name = name;
}

// 创建Animal实例
var dog = new Animal("小狗");
var cat = new Animal("小猫");
var notAnimal = {name: "不是动物"};

print(dog instanceof Animal);  // 输出 true（dog是Animal的实例）
print(cat instanceof Animal);  // 输出 true（cat是Animal的实例）
print(notAnimal instanceof Animal);  // 输出 false（不是通过Animal构造的）


// 示例2：继承关系中的类型检查
function Mammal(name) {
    Animal.call(this, name);
}
// 实现继承
Mammal.prototype = Object.create(Animal.prototype);
Mammal.prototype.constructor = Mammal;

function Bird(name) {
    Animal.call(this, name);
}
Bird.prototype = Object.create(Animal.prototype);
Bird.prototype.constructor = Bird;

var lion = new Mammal("狮子");

print(lion instanceof Mammal);  // 输出 true（直接实例）
print(lion instanceof Animal);  // 输出 true（继承自Animal）
print(lion instanceof Bird);    // 输出 false（不属于Bird分支）


// 示例3：原生对象类型检查
var arr = [1, 2, 3];
var date = new Date();
var func = function() {};
var strObj = new String("hello");
var strPrim = "hello";  // 字符串字面量（基本类型）

print(arr instanceof Array);    // 输出 true
print(date instanceof Date);    // 输出 true
print(func instanceof Function); // 输出 true
print(strObj instanceof String); // 输出 true（对象类型）
print(strPrim instanceof String); // 输出 false（基本类型不是实例）


// 示例4：特殊情况处理
var nullVal = null;
var undefVal = undefined;

print(nullVal instanceof Object);  // 输出 false（null不是任何对象的实例）
print(undefVal instanceof Object); // 输出 false（undefined不是任何对象的实例）
```


## $fc-#U6587#U4ef6#U9009#U62e9#U5668-01.#U9ed8#U8ba4#U5355#U9009#U6587#U4ef6

```javascript
//文件选择器

$fc.show((files)=> {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
});



//..
```


## $fc-#U6587#U4ef6#U9009#U62e9#U5668-02.#U5355#U9009#U76ee#U5f55

```javascript
//文件选择器

$fc.show((files)=> {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "s",
    type: "m"
});



//..
```


## $fc-#U6587#U4ef6#U9009#U62e9#U5668-03.#U5355#U9009#U6240#U6709

```javascript
//文件选择器

$fc.show((files)=> {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "s",
    type: "a"
});



//..
```


## $fc-#U6587#U4ef6#U9009#U62e9#U5668-04.#U5355#U9009#U6587#U4ef6

```javascript
//文件选择器

$fc.show((files)=> {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "s",
    type: "f"
});



//..
```


## $fc-#U6587#U4ef6#U9009#U62e9#U5668-05.#U591a#U9009#U76ee#U5f55

```javascript
//文件选择器

$fc.show((files)=> {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "m",
    type: "m"
});



//..
```


## $fc-#U6587#U4ef6#U9009#U62e9#U5668-06.#U591a#U9009#U6240#U6709

```javascript
//文件选择器

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



//..
```


## $fc-#U6587#U4ef6#U9009#U62e9#U5668-07.#U591a#U9009#U6587#U4ef6

```javascript
//文件选择器

$fc.show((files)=> {
    for (let i = 0; i < files.length; i++) {
        log(files[i]);
    }
}, {
    root: "/sdcard",
    path: "/sdcard/Pictures",
    mode: "m",
    type: "f"
});



//..
```
