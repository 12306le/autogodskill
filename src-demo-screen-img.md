# 示例：截图/图像/OCR/绘图


## #U5168#U5c40#U51fd#U6570-05.#U663e#U793a#U56fe#U7247

```javascript
//官方示例

//【方式一】显示图片路径上的图片
showImg("example/全局函数/t01.png");

//【方式二】显示图片对象(Image)
let imgPath = "example/全局函数/t01.png";
let img = $img.read(imgPath);//获取(Image)图片对象
showImg(img);//显示图片对象(Image)



//示例结束
```


## $canvas-#U753b#U5e03-01.#U663e#U793a#U65b9#U5f0f-02.#U5728#U5bf9#U8bdd#U6846#U4e2d#U663e#U793a

```javascript
//AIGame官方示例

//创建画布对象
let canvas = $canvas.create(500,500);

//创建画笔
let paint = $canvas.paint();
paint.setColor($color.RED); //红色

//绘制红色方框
canvas.drawRect(30,30,400,400,paint);

//转换成Image对象后显示(AIGame的内置对象:$img的操作对象)
canvas.show();

//或者使用 canvas.toImg().show();    来显示图片
//或者使用 $img.show(canvas.toImg());来显示图片





//示例结束
```


## $canvas-#U753b#U5e03-02.#U62df#U5b9a#U5408#U540c-#U62df#U5b9a#U5408#U540c

```javascript
//AIGame官方示例

//创建画布对象(加载图片对象)
let canvas = $canvas.create("example/$canvas - 画布/02.拟定合同/合同.jpg");

//创建黑色彩笔
let paint = $canvas.paint("#000000");
paint.setTextSize(25);

//绘制颜色
canvas.drawText("张三丰",170,145,paint);
canvas.drawText("420321200006524388",480,145,paint);
canvas.drawText("13564962035",900,145,paint);
canvas.drawText("翻斗花园2号街A501",170,195,paint);

//显示图片
canvas.show();
//保存图片
canvas.save("/sdcard/新合同.jpg");


//示例结束
```


## $canvas-#U753b#U5e03-04.#U753b#U4e2a#U9a8c#U8bc1#U7801

```javascript
//AIGame官方示例

//创建画布对象
let size = 20;
let canvas = $canvas.create(100,size+10);

//生成6位验证码
let vcode = random(10)+""+random(10)+random(10)+random(10)+random(10)+random(10);

//创建画笔
let txtPaint = $canvas.paint("#000000");
txtPaint.setTextSize(size);

//绘制文字
canvas.drawText(vcode,0,size,txtPaint);

//布局显示画布
canvas.show();




//示例结束
```


## $color-#U989c#U8272#U5de5#U5177-01.#U8ba1#U7b97#U989c#U8272#U76f8#U4f3c#U5ea6

```javascript
let result = $color.similar("#1E1F22","#2B2D30");

alert("相似度",result);
```


## $color-#U989c#U8272#U5de5#U5177-02.#U989c#U8272#U503c#U8f6c#U5b57#U7b26#U4e32

```javascript
//转为#00000000
let color1 = $color.toString(-166780);

//转为#000000
let color2 = $color.str(-166780);

alert("8位颜色值",color1);

alert("6位颜色值",color2);
```


## $color-#U989c#U8272#U5de5#U5177-03.#U89e3#U6790rgb#U62ff#U5230#U989c#U8272#U503c

```javascript
let colorValue1 = $color.parse("#784cde");
let colorValue2 = $color.parse(105,78,230);
let colorValue3 = $color.rgb(105,78,230);
let colorValue4 = $color.argb(255,105,78,230);


let info = `
colorValue1=${colorValue1}
colorValue2=${colorValue2}
colorValue3=${colorValue3}
colorValue4=${colorValue4}
`;

alert("颜色值",info);
```


## $color-#U989c#U8272#U5de5#U5177-04.#U89e3#U6790#U989c#U8272#U901a#U9053

```javascript
let a = $color.a("#357C94");
let r = $color.r("#357C94");
let g = $color.g("#357C94");
let b = $color.b("#357C94");

let info = `
a=${a}
r=${r}
g=${g}
b=${b}
`;
alert("解析通道",info);
```


## $color-#U989c#U8272#U5de5#U5177-05.#U6bd4#U8f83#U989c#U8272

```javascript
let color = "#1E1F22"; 

let colorValue =-14803166;

let same = $color.equals(color,colorValue);

if (same) {
    alert("比较颜色","颜色相同");
} else {
    alert("比较颜色","颜色不同");
}
```


## $draw-#U5168#U5c40#U7ed8#U5236-01.#U7ed8#U5236#U65b9#U6846

```javascript
//AIGame 官方示例


//关闭所有绘制图案
$draw.closeAll();

//绘制矩形
$draw.rect(200,200,200,100);

sleep(2000);

//绘制一个向外拓展50像素的矩阵
$draw.rect(200,200,200,100,50);




//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-02.#U7ed8#U5236#U5706#U5f62

```javascript
//AIGame 官方示例


//关闭所有绘制图案
$draw.closeAll();

//绘制半径为100像素的圆形
$draw.circle(350,400,100);

sleep(2000);

//向外拓展50像素
$draw.circle(350,400,100,50);




//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-03.#U7ed8#U5236#U51c6#U5fc3

```javascript
//AIGame 官方示例


//关闭所有绘制图案
$draw.closeAll();

//绘制准心
$draw.cross(400,500);





//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-04.#U7ed8#U5236#U70b9

```javascript
//AIGame 官方示例


//关闭所有绘制图案
$draw.closeAll();

//绘制一个点
$draw.dot(400,500);





//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-05.#U7ed8#U5236#U6587#U5b57

```javascript
//AIGame 官方示例


//关闭所有绘制图案
$draw.closeAll();

//绘制文字
$draw.text("Hello aigame !",400,300);

//绘制文字(大小为20像素)
$draw.text("Hello aigame !",400,400,20);




//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-06.#U7ed8#U5236#U7ebf

```javascript
//AIGame 官方示例


//关闭所有绘制图案
$draw.closeAll();

//绘制一条线
$draw.line(300,0,100,1000);

//再绘制几条
$draw.line(300,0,200,1000);
$draw.line(300,0,400,1000);
$draw.line(300,0,700,1000);

//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-07.#U7ed8#U5236#U8def#U5f84-#U753b#U7231#U5fc3

```javascript
//AIGame 官方示例


//关闭所有绘制图案
$draw.closeAll();


function generateHeartCoordinates(size, offsetX , offsetY) {
    const coordinates = [];
    for (let t = 0; t < 2 * Math.PI; t += 0.01) {
        // 根据爱心参数方程计算 x 和 y
        let x = 16 * Math.pow(Math.sin(t), 3);
        let y = 13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t);

        // 缩放坐标，size 控制爱心大小
        x = x * size / 32;
        y = -y * size / 32;

        // 偏移坐标，让爱心居中
        x += size / 2;
        y += size / 2;

        // 应用额外的偏移量来设置爱心位置
        x += offsetX;
        y += offsetY;

        coordinates.push([Math.round(x), Math.round(y)]);
    }
    return coordinates;
}

// 调用函数生成爱心坐标数组
const size = 250;
const offsetX = 300; // 设置爱心在 x 轴上的偏移量
const offsetY = 260; // 设置爱心在 y 轴上的偏移量
const heartCoordinates = generateHeartCoordinates(size, offsetX, offsetY);




$draw.path(heartCoordinates);




//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-08.#U7ed8#U5236#U65e5#U5fd7

```javascript
//AIGame 官方示例


//关闭所有绘制图案
$draw.closeAll();

$draw.i("信息");

sleep(2000);

$draw.d("调试");

sleep(2000);

$draw.w("警告");

sleep(2000);

$draw.e("异常");

sleep(2000);

$draw.v("忽略");

sleep(2000);



//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-09.#U5173#U95ed#U7ed8#U5236

```javascript
//AIGame 官方示例


//关闭所有绘制的图案
$draw.closeAll();



//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-10.#U56fd#U9645#U624b#U52bf

```javascript
//AIGame 官方示例

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

//示例结束
```


## $draw-#U5168#U5c40#U7ed8#U5236-11.#U6d41#U7545#U6e05#U7a7a#U7ed8#U5236

```javascript
//开头先清空所有
$draw.closeAll();
sleep(1000);

//设置速度
let speed = 3;

//动态的绘制一个点
for (let i = 0; i < $screen.getWidth(); i += speed) {
    $draw.dot(i, 500);
    //显示10毫秒后再清空(时间太短了就看不到绘制的内容了)
    sleep(10);
    //[重要]这个函数不会销毁悬浮窗，只会清空绘制
    $draw.clear();
}

//结尾再清空所有
sleep(1000);
$draw.closeAll();//这个函数会销毁悬浮窗
```


## $img-#U56fe#U7247#U5904#U7406-#U4e8c#U503c#U5316

```javascript
//读取要处理的图片
let img = $img.read("example/$img - 图片处理/img/t01.png");
//二值化操作
let resultImg = $img.threshold(img,100);
//显示二值化结果图片
resultImg.show();
```


## $img-#U56fe#U7247#U5904#U7406-#U53d6#U51fa#U989c#U8272

```javascript
let colorArr = [[107, 28],
[108, 28],
[105, 29],
[106, 29],
[107, 29],
[103, 30],
[104, 30],
[105, 30],
[106, 30],
[102, 31],
[103, 31],
[104, 31],
[105, 31],
[101, 32],
[102, 32],
[103, 32],
[104, 32],
[100, 33],
[101, 33],
[102, 33],
[103, 33],
[100, 34],
[101, 34],
[102, 34],
[100, 35],
[101, 35],
[102, 35],
[99, 36],
[100, 36],
[101, 36],
[99, 37],
[100, 37],
[98, 38],
[99, 38],
[100, 38],
[98, 39],
[99, 39],
[99, 40],
[104, 103],
[144, 120]];

let img = $img.read("example/$img - 图片处理/img/t02.png");

for(let index of colorArr){
    let x = index[0];
    let y = index[1];
    let color = img.pixel(x,y);
    log("坐标:"+x+","+y);
    log("颜色:"+color);
    log("代码:"+$color.str(color),"\n");
}
```


## $img-#U56fe#U7247#U5904#U7406-#U591a#U70b9#U627e#U8272

```javascript
//读取图片
let img = $img.read("example/$img - 图片处理/img/t02.png");
//在这张图片中执行多点找色
let result = $img.findMultiColors(img,null,"#E9AF6D",5,[
                	-10, 1, "#908E8A", 5,
                	-4, -8, "#908E8A", 5,
                	-18, -4, "#FBFBFB", 5
]);
alert("执行结果",result);
```


## $img-#U56fe#U7247#U5904#U7406-#U989c#U8272#U4fe1#U606f

```javascript
let color = "#908E8A";
let r = $color.r(color);
let g = $color.g(color);
let b = $color.b(color);
log(r,g,b);
```


## $ocr-#U6587#U5b57#U8bc6#U522b-mlkit-#U4e8c#U503c#U5316#U8bc6#U522b

```javascript
//二值化识别:截屏某个区域识别
//识别前会将图片进行二值化处理:会把主要的颜色保留成白色,其余的都是黑色
$screen.getPermit();

//指定ocr引擎为mlkit
$ocr.v("mlkit");

//注意:mlkit无法计算出相似度,所以similar固定为0.85

//显示出图片
showImg("./example/$ocr - 文字识别/imgs/t02.png");

//根据屏幕大小计算出大致的范围(如果你的手机识别失败,请手动修改)
let si = $screen.getScreenInfo();
let re = [0,si.h/3,si.w ,si.h/3];

//绘制出大概的识别范围
$draw.rect(re[0],re[1],re[2],re[3]);

sleep(1000); //延迟1秒(免得图片还没显示,就开始识别了)

//开始识别
let result = $ocr.detect({
    region: [re[0],re[1],re[2],re[3]],
    gray: false,//关闭灰度化识别
    color: "#356EFF",//(必须)设置主要颜色(蓝色)
    threshold: 30,//(必须)二值化阈值
    save: true,//(可选)开启保存图片
    savePath: "/sdcard/ocr-thre.png",//(可选)保存位置
});


alert("识别结果",result);

if ($file.exists("/sdcard/ocr-thre.png")) {
    showImg("/sdcard/ocr-thre.png"); //显示二值化后的图片
}

$draw.closeAll(); //关闭全局绘制
//..
```


## $ocr-#U6587#U5b57#U8bc6#U522b-mlkit-#U7070#U5ea6#U5316#U8bc6#U522b

```javascript
//灰度化识别会截屏,在屏幕的某个区域进行识别
//识别前会将图片进行灰度化,之后在进行识别
$screen.getPermit();

//指定ocr引擎为mlkit
$ocr.v("mlkit");

//注意:mlkit无法计算出相似度,所以similar固定为0.85

//显示出图片
showImg("./example/$ocr - 文字识别/imgs/t01.png");

//根据屏幕大小计算出大致的范围(如果你的手机识别失败,请手动修改)
let si = $screen.getScreenInfo();
let re = [0,si.h/3,si.w ,si.h/3];

//绘制出大概的识别范围
$draw.rect(re[0],re[1],re[2],re[3]);

sleep(1000);//延迟1秒(免得图片还没显示,就开始识别了)

//开始识别
let result = $ocr.detect({
    region: [re[0],re[1],re[2],re[3]],
    gray:true,//开启灰度化识别
    save: true,//(可选)开启保存图片
    savePath: "/sdcard/ocr-gray.png",//(可选)保存位置
});


alert("识别结果",result);

if($file.exists("/sdcard/ocr-gray.png")){
    showImg("/sdcard/ocr-gray.png");//显示灰度化后的图片
}

$draw.closeAll();//关闭全局绘制
//..
```


## $ocr-#U6587#U5b57#U8bc6#U522b-mlkit-#U8bc6#U522b#U672c#U5730#U56fe#U7247

```javascript
//指定ocr引擎为mlkit
$ocr.v("mlkit");

//开始识别本地图片
let res = $ocr.detectPath("./example/$ocr - 文字识别/imgs/t01.png");

alert("识别结果",res);

//注意:mlkit无法计算出相似度,所以similar固定为0.85
```


## $ocr-#U6587#U5b57#U8bc6#U522b-ncnn-#U4e8c#U503c#U5316#U8bc6#U522b

```javascript
//二值化识别:截屏某个区域识别
//识别前会将图片进行二值化处理:会把主要的颜色保留成白色,其余的都是黑色
$screen.getPermit();

//指定ocr引擎为ncnn
$ocr.v("ncnn");

//ncnn识别引擎需要初始化,但是mlkit不用
$ocr.init();

//显示出图片
showImg("./example/$ocr - 文字识别/imgs/t02.png");

//根据屏幕大小计算出大致的范围(如果你的手机识别失败,请手动修改)
let si = $screen.getScreenInfo();
let re = [0,si.h/3,si.w ,si.h/3];

//绘制出大概的识别范围
$draw.rect(re[0],re[1],re[2],re[3]);

sleep(1000); //延迟1秒(免得图片还没显示,就开始识别了)

//开始识别
let result = $ocr.detect({
    region: [re[0],re[1],re[2],re[3]],
    gray: false,//关闭灰度化识别
    color: "#356EFF",//(必须)设置主要颜色(蓝色)
    threshold: 30,//(必须)二值化阈值
    save: true,//(可选)开启保存图片
    savePath: "/sdcard/ocr-thre.png",//(可选)保存位置
});


alert("识别结果",result);

if ($file.exists("/sdcard/ocr-thre.png")) {
    showImg("/sdcard/ocr-thre.png"); //显示二值化后的图片
}

$draw.closeAll(); //关闭全局绘制
//..
```


## $ocr-#U6587#U5b57#U8bc6#U522b-ncnn-#U7070#U5ea6#U5316#U8bc6#U522b

```javascript
//灰度化识别会截屏,在屏幕的某个区域进行识别
//识别前会将图片进行灰度化,之后在进行识别
$screen.getPermit();

//指定ocr引擎为ncnn
$ocr.v("ncnn");
//ncnn识别引擎需要初始化,但是mlkit不用
$ocr.init();

//显示出图片
showImg("./example/$ocr - 文字识别/imgs/t01.png");

//根据屏幕大小计算出大致的范围(如果你的手机识别失败,请手动修改)
let si = $screen.getScreenInfo();
let re = [0,si.h/3,si.w ,si.h/3];

//绘制出大概的识别范围
$draw.rect(re[0],re[1],re[2],re[3]);

sleep(1000);//延迟1秒(免得图片还没显示,就开始识别了)

//开始识别
let result = $ocr.detect({
    region: [re[0],re[1],re[2],re[3]],
    gray:true,//开启灰度化识别
    save: true,//(可选)开启保存图片
    savePath: "/sdcard/ocr-gray.png",//(可选)保存位置
});


alert("识别结果",result);

if($file.exists("/sdcard/ocr-gray.png")){
    showImg("/sdcard/ocr-gray.png");//显示灰度化后的图片
}

$draw.closeAll();//关闭全局绘制
//..
```


## $ocr-#U6587#U5b57#U8bc6#U522b-ncnn-#U8bc6#U522b#U672c#U5730#U56fe#U7247

```javascript
//指定ocr引擎为ncnn
$ocr.v("ncnn");
//ncnn识别引擎需要初始化,但是mlkit不用
$ocr.init();

//开始识别本地图片
let res = $ocr.detectPath("./example/$ocr - 文字识别/imgs/t01.png");

alert("识别结果",res);
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-01.#U83b7#U53d6#U622a#U5c4f#U6743#U9650

```javascript
// AIGame官方示例


//等待获取截屏权限
$screen.getPermit();




// 示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-02.#U622a#U5c4f

```javascript
// AIGame官方示例


//如果没有无障碍权限，则会获取录屏权限
if(!$screen.hasPermit()){
    //阻塞方法:直到获取录屏权限为止，才会继续向下执行代码
    $screen.getPermit();
}

//如果有无障碍则会优先使用无障碍截屏，否则就使用录屏权限截屏
let img = $screen.getScreen();//获得屏幕截屏

if(img!=null){
    img.show();//显示截屏
}


// 示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-03.#U8bbe#U7f6e#U5c4f#U5e55#U4eae#U5ea6

```javascript
// AIGame官方示例


//设置屏幕亮度
$screen.bright(100);




// 示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-04.#U8bbe#U7f6e#U5c4f#U5e55#U65b9#U5411

```javascript
// AIGame官方示例


//设置屏幕方向
$screen.dir(0);//(强制)竖屏
$screen.dir(90);//(强制)右转横屏
$screen.dir(180);//(强制)倒置竖屏
$screen.dir(270);//(强制)左转横屏
$screen.dir(-1);//(不强制)自动旋转(任何其他数字都是自动旋转)

// 模拟器测试：
// 逍遥     安卓5  : 成功旋转屏幕 会闪退
// 逍遥     安卓7  : 成功旋转屏幕 会闪退
// 逍遥     安卓9  : 成功旋转屏幕 会闪退
// 逍遥     安卓12 : 完美!!!
// 雷电     安卓9  : 毫无反应

//真机测试：
// OPPO    安卓12 : 完美!!!




// 示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-05.#U5c4f#U5e55#U9ad8

```javascript
// AIGame官方示例


let w = $screen.getWidth();
let h = $screen.getHeight();

alert("屏幕宽高",w+"x"+h);




// 示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-06.#U5c4f#U5e55#U5bbd

```javascript
// AIGame官方示例


let w = $screen.getWidth();
let h = $screen.getHeight();

alert("屏幕宽高",w+"x"+h);




// 示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-08.#U5f53#U524d#U8bbe#U5907#U7684#U5bc6#U5ea6

```javascript
// AIGame官方示例


let density = $screen.getDensity();




// 示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-09.#U5224#U65ad#U5c4f#U5e55#U662f#U5426#U606f#U5c4f

```javascript
// AIGame官方示例


if($screen.isScreenOff()){
    toast("屏幕息屏");
}




// 示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-10.#U5224#U65ad#U5c4f#U5e55#U662f#U5426#U4eae#U5c4f

```javascript
// AIGame官方示例


if($screen.isScreenOn()){
    toast("屏幕亮屏");
}




// 示例结束
```


## $screen-#U5c4f#U5e55#U64cd#U4f5c-11.#U622a#U5c4f#U5e76#U4fdd#U5b58

```javascript
// AIGame官方示例


//截屏并且保存
let imgPath = "/sdcard/Pictures/截屏.png";
$screen.save(imgPath);




// 示例结束
```
