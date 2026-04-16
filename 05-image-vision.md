# 图像与视觉 API

> 图片处理、OCR文字识别、YOLO目标检测。

## 目录
- [Image - 图片对象](#image---图片对象)
- [$img - 图片操作](#img---图片操作)
- [OcrOptions - 识别配置](#ocroptions---识别配置)
- [$ocr - 文字识别](#ocr---文字识别)
- [训练模型-环境搭建](#训练模型-环境搭建)
- [输入输出层名称对照表](#输入输出层名称对照表)
- [结果排序规则表](#结果排序规则表)
- [导出ONNX格式](#导出onnx格式)
- [YoloObject - 检测对象](#yoloobject---检测对象)
- [YoloResult - 检测结果](#yoloresult---检测结果)
- [$yolo - 目标检测](#yolo---目标检测)

---

## Image - 图片

- 更新时间:2026-01-30 19:32:54

> 表示图片
> 
> 是为了防止图片占用太大的内存,于是封装此对象用于表示图片,一般情况下,在本应用中绝大多数使用图片的场景都会自动回收图片,以免占用过多内存。




#### const {int} width;

> 图片宽度


#### const {int} height;

> 图片高度


#### getBitmap()

> 获取bitmap类型


#### width()

> 图片宽度


#### height()

> 图片高度


#### getWidth()

> 图片宽度


#### getHeight()

> 图片高度


#### close()

> 释放资源


#### recycle()

> 释放资源


#### pixel(x, y)

> 获取像素值

- 参数 : x {int} x坐标
- 参数 : y {int} y坐标
- 返回 : {int} 像素值


#### pixel(point)

> 获取像素值

- 参数 : point {Point} 坐标
- 返回 : {int} 像素值


#### save(path)

> 保存图片

- 参数 : path {String} 保存路径


#### show()

> 显示图片


#### copy()

> 复制图片
> 
> 从源图片数据中拷贝一份图片后返回

- 返回 : {Image} 拷贝后的图片
- 版本 : 1.7.0


```javascript
let screenImg = $screen.getScreen();
let img = screenImg.copy();
//接下来可以对 screenImg 以及 img 分别进行操作
```


#### base64()

> 转为base64

- 返回 : {String} base64
- 版本 : 1.8.7


```javascript
//获取图片
let screenImg = $screen.getScreen();
//转为base64
let base64 = screenImg.base64();
```


#### json()

> 转json字符串

- 返回 : {String} json字符串

---

## $img - 图片操作

- 更新时间:2026-01-30 19:32:54

> 图片操作




#### read(imgPath)

> 读取图片
> 
> 支持相对路径写法
> 
> 读取资源失败时会返回空null

- 参数 : imgPath {string} 图片路径
- 返回 : {Image} 读取的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p01.png";
//读取图片
let img = $img.read(path);
```


#### open(imgPath)

> 构建img对象
> 
> 和read效果一样的

- 参数 : imgPath {string} 图片路径
- 返回 : {Image} 图片对象
- 版本 : 1.2.4


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p01.png";
//读取图片
let img = $img.open(path);
```


#### open(bitmap)

> 构建img对象

- 参数 : bitmap {Bitmap} 安卓图片对象
- 返回 : {Image} 图片对象
- 版本 : 1.2.4


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let mImg = ui.id("mImg");
//获取图片(安卓图片对象)
let bitmap = mImg.getImg();
//构建$img对象
let img = $img.open(bitmap);
```


#### read(imgFile)

> 读取图片
> 
> 读取资源失败时会返回空null

- 参数 : imgFile {File} 图片路径
- 返回 : {Image} 读取的图片


#### save(image, path, format, quality)

> 保存图片
> 
> 支持相对路径写法

- 参数 : image {Image} 需要保存的图片
- 参数 : path {string} 保存路径
- 参数 : format {string} 格式
- 参数 : quality {int} 质量


```javascript
//截屏并且保存到本地
//但是在实际中我们可以直接调用$screen.save("路径");更加方便
$screen.getPermit();
let screenImg = $screen.getScreen();
$img.save(screenImg,"/$img/img/s05.png","png",100);
```


#### save(image, path)

> 保存图片
> 
> 默认保存png格式，质量为100，支持相对路径写法

- 参数 : image {Image} 需要保存的图片
- 参数 : path {string} 保存路径


```javascript
//截屏并且保存到本地
//但是在实际中我们可以直接调用$screen.save("路径");更加方便
$screen.getPermit();
let screenImg = $screen.getScreen();
$img.save(screenImg,"/$img/img/s05.png");
```


#### toBase64(image, format, quality)

> 转换base64

- 参数 : image {Image} 需要转换为base64的图片
- 参数 : format {string} 格式
- 参数 : quality {int} 质量
- 返回 : 图片的base64字符串


```javascript
let img = $img.read("/$img/res/t01.png");
let baseStr = $img.toBase64( img ,"png" , 50);
alert("图片Base64",baseStr);
```


#### toBase64(image)

> 转换base64

- 参数 : image {Image} 需要转换的图片
- 返回 : {string} base64字符串


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p01.png";
//读取图片
let img = $img.read(path);
//转化为base64
let imgBase64 = $img.toBase64(img);
log(imgBase64)
```


#### toBase64(path)

> 转换base64

- 参数 : path {string} 需要转换的图片
- 返回 : {string} base64字符串


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p01.png";
//转化为base64
let imgBase64 = $img.toBase64(path);
log(imgBase64)
```


#### readBase64(base64)

> 加载base64

- 参数 : base64 {string} base64字符串
- 返回 : {Image} 图片对象


```javascript
let img = $img.read("/$img/res/t01.png");
let baseStr = $img.toBase64( img ,"png" , 50);
alert("图片Base64",baseStr);
//从base64中读取图片
let img2 = $img.readBase64(baseStr);
showImg(img2);
```


#### clip(image, x, y, w, h)

> 裁剪图片

- 参数 : image {img} 原本的图片
- 参数 : x {int}  开始坐标
- 参数 : y {int} 开始坐标
- 参数 : w {int}  宽度
- 参数 : h {int} 高度
- 返回 : {Image} 新的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p03.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.clip(img, 0, 0, 300, 200);
//显示图片
$img.show(image);
```


#### resize(image, w, h, interpolation)

> 设置尺寸
> 
> 插值方式(忽略大小写)：
> NEAREST,
> LINEAR,
> CUBIC,
> AREA,
> LANCZOS4,
> EXACT

- 参数 : image {Image}      需要处理的图片
- 参数 : w {int} 宽度
- 参数 : h {int}  高度
- 参数 : interpolation {string} 插值方式
- 返回 : 图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.resize(img, 200, 200, "INTER_CUBIC");
//显示图片
$img.show(image);
```


#### resize(image, w, h)

> 设置尺寸
> 
> 使用默认插值方式:LINEAR

- 参数 : image {Image} 需要处理的图片
- 参数 : w {int} 宽度
- 参数 : h {int} 高度
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.resize(img, 200, 200);
//显示图片
$img.show(image);
```


#### scale(image, scaleX, scaleY, interpolation)

> 缩放图片

- 参数 : image {Image}  需要处理的图片
- 参数 : scaleX {double} 宽度缩放倍数
- 参数 : scaleY {double}   高度缩放倍数
- 参数 : interpolation {string}  插值方式
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.scale(img, 0.3, 0.2, "CUBIC");
//显示图片
$img.show(image);
```


#### scale(image, scaleX, scaleY)

> 缩放图片

- 参数 : image {Image}  需要处理的图片
- 参数 : scaleX {double} 宽度缩放倍数
- 参数 : scaleY {double} 高度缩放倍数
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.scale(img, 0.3, 0.2);
//显示图片
$img.show(image);
```


#### rotate(image, degree, x, y)

> 旋转图片

- 参数 : image {Image} 需要处理的图片
- 参数 : degree {float} 旋转的角度
- 参数 : x {int} 旋转中心点x坐标
- 参数 : y {int} 旋转中心点y =坐标
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.rotate(img, 45, 100, 200);
//显示图片
$img.show(image);
```


#### rotate(image, degree)

> 旋转图片

- 参数 : image {Image}  需要处理的图片
- 参数 : degree {float} 旋转的角度
- 返回 : {Image}  处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.rotate(img, 45);
//显示图片
$img.show(image);
```


#### rotate(image)

> 旋转图片
> 
> 默认旋转90度

- 参数 : image {Image}   需要处理的图片
- 返回 : {Image}   处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.rotate(img);//默认旋转90度
//显示图片
$img.show(image);
```


#### concat(img1, img2, dir)

> 拼接图片

- 参数 : img1 {Image}     需要拼接的图片1
- 参数 : img2 {Image}  需要拼接的图片2
- 参数 : dir {string} 拼接方向(left,right,top,bottom)
- 返回 : {Image}  拼接好的图片


```javascript
//相对于项目的路径
let t1 = $img.read("/$img/res/t02.png");
let t2 = $img.read("/$img/res/t03.png");
//调整一下尺寸(保持一致)
t1 = $img.resize(t1,300,200);
t2 = $img.resize(t2,300,200);
//调整一下大小
let img = $img.concat(t1,t2,"bottom");
showImg(img);
```


#### gray(image)

> 灰度化

- 参数 : image {Image} 需要灰度化的图片
- 返回 : {Image}  灰度化的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.gray(img);
//显示图片
$img.show(image);
```


#### threshold(image, thre)

> 二值化图片

- 参数 : image {Image} 需要处理的图片
- 参数 : thre {double} 阈值
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.threshold(img, 150);
//显示图片
$img.show(image);
```


#### adaptiveThreshold(image, maxValue, adaptiveMethod, thresholdType, blockSize, C)

> 自适应二值化

- 参数 : image {Image} 图片
- 参数 : maxValue {number} 最大值
- 参数 : adaptiveMethod {string} 在一个邻域内计算阈值所采用的算法 默认值是：GAUSSIAN_C
- 参数 : thresholdType {string} 阈值化类型 默认值是：BINARY
- 参数 : blockSize {number} 邻域块大小
- 参数 : C {number} 偏移值调整量
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.adaptiveThreshold(img,255,"MEAN_C","BINARY", 11, 2);
//显示图片
$img.show(image);
```


#### cvtColor(img, code, dstCn)

> 颜色空间转换

- 参数 : img {Image} 图片
- 参数 : code {string} 颜色空间转换的类型，可选的值有一共有205个 默认值:COLOR_BGR2GRAY
- 参数 : dstCn {int} 目标图像的颜色通道数量，如果不填写则根据其他参数自动决定。
- 返回 : {Image} 颜色转换后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.cvtColor(img,"RGBA2BGR",null);
//显示图片
$img.show(image);
```


#### cvtColor(img, code)

> 颜色空间转换

- 参数 : img {Image} 图片
- 参数 : code {string} 颜色空间转换的类型，可选的值有一共有205个 默认值:COLOR_BGR2GRAY
- 返回 : {Image} 颜色转换后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.cvtColor(img,"RGBA2BGR");
//显示图片
$img.show(image);
```


#### inRange(img, lowerBound, upperBound)

> 图片二值化

- 参数 : img {Image} 图片
- 参数 : lowerBound {string|number}  颜色下界
- 参数 : upperBound {string|number}  颜色上界
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.inRange(img,"#666666","#FFFFFF");
//显示图片
$img.show(image);
```


#### blur(img, size, point, type)

> 模糊处理
> 
> 模糊类型(不区分大小写)：
> CONSTANT,
> REPLICATE,
> REFLECT,
> WRAP,
> REFLECT_101,
> TRANSPARENT,
> REFLECT101,
> DEFAULT,
> ISOLATED

- 参数 : img {Image} 图片
- 参数 : size {double[]} 定义滤波器的大小，如[3, 3]
- 参数 : point {double[]} 指定锚点位置(被平滑点)，默认为图像中心
- 参数 : type {string} 推断边缘像素类型，默认为"DEFAULT"
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.blur(img,[10,10],[-1,-1],"REPLICATE");
//显示图片
$img.show(image);
```


#### medianBlur(img, size)

> 中值滤波

- 参数 : img {Image} 图片
- 参数 : size {int} 定义滤波器的大小
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.medianBlur(img,3);
//显示图片
$img.show(image);
```


#### gaussianBlur(img, size, sigmaX, sigmaY, type)

> 高斯模糊
> 
> 模糊类型(不区分大小写)：
> CONSTANT,
> REPLICATE,
> REFLECT,
> WRAP,
> REFLECT_101,
> TRANSPARENT,
> REFLECT101,
> DEFAULT,
> ISOLATED

- 参数 : img {Image} 图片
- 参数 : size {double[]} 定义滤波器的大小，如[3, 3]
- 参数 : sigmaX {double} x方向的标准方差，不填写则自动计算
- 参数 : sigmaY {double} y方向的标准方差，不填写则自动计算
- 参数 : type {string} 推断边缘像素类型，默认为"DEFAULT"
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.gaussianBlur(img,[15,15],0,0,"WRAP");
//显示图片
$img.show(image);
```


#### flip(image)

> 左右翻转

- 参数 : image {Image} 需要处理的图片
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.flip(img);
//显示图片
$img.show(image);
```


#### upside(image)

> 上下翻转

- 参数 : image {Image} 需要处理的图片
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片
let image = $img.upside(img);
//显示图片
$img.show(image);
```


#### flip(image, sx, sy)

> 水平翻转

- 参数 : image {Image} 需要处理的图片
- 参数 : sx {float}   横向翻转的方向
- 参数 : sy {float}  纵向翻转的方向
- 返回 : {Image} 处理后的图片


```javascript
//图片路径
let path = "sdcard/Pictures/示例/$img/res/p02.png";
//读取图片
let img = $img.read(path);
//操作图片(上下反转)
let image = $img.flip(img,-1,-1);
//显示图片
$img.show(image);
```


#### putTop(bigImg, smallImg, x, y)

> 在大图片上面放置一个小图片

- 参数 : bigImg {Image} 大图片
- 参数 : smallImg {Image} 小图片
- 参数 : x {int} 小图片左上角x
- 参数 : y {int} 小图片左上角y
- 返回 : {Image}  处理完成的图片


```javascript
//图片路径
let path1 = "sdcard/Pictures/示例/$img/res/p02.png"; //大图片
let path2 = "sdcard/Pictures/示例/$img/res/p04.png"; //小图片
let bigImg = $img.read(path1);
let smallImg = $img.read(path2);
//设置放置的位置
let image = $img.putTop(bigImg, smallImg, 20, 20);
//显示图片
$img.show(image);
```


#### findColor(image, color, threshold, x, y, w, h)

> 查找颜色

- 参数 : image {Image} 需要处理的图片
- 参数 : color {string} 需要查找的颜色
- 参数 : threshold {int} 阈值
- 参数 : x {int} 范围x起点坐标
- 参数 : y {int} 范围y起点坐标
- 参数 : w {int} 范围宽度
- 参数 : h {int} 范围高度
- 返回 : {Image} 处理后的图片


```javascript
let img = $img.read("/$img/res/t01.png");
let point = $img.findColor(img,"#d80005",5,0,0,100,100);
alert("结果",point);
```


#### findColor(image, color, threshold, region)

> 查找颜色

- 参数 : image {Image} 需要处理的图片
- 参数 : color {string} 需要查找的颜色
- 参数 : threshold {int} 阈值
- 参数 : region {int[]}  找色范围
- 返回 : {Point} 找到的结果


```javascript
let img = $img.read("/$img/res/t01.png");
let point = $img.findColor(img,"#d80005",5,[0,0,100,100]);
alert("结果",point);
```


#### findColor(image, color, threshold)

> 查找颜色

- 参数 : image {Image}  需要处理的图片
- 参数 : color {string} 需要查找的颜色
- 参数 : threshold {int} 阈值
- 返回 : {Image} 处理后的图片


```javascript
let img = $img.read("/$img/res/t01.png");
let point = $img.findColor(img,"#d80005",5);
alert("结果",point);
```


#### findColor(image, color)

> 查找颜色

- 参数 : image {Image} 需要处理的图片
- 参数 : color {string} 需要查找的颜色
- 返回 : {Image} 处理后的图片


```javascript
let img = $img.read("/$img/res/t01.png");
let point = $img.findColor(img,"#d80005");
alert("结果",point);
```


#### findMultiColors(image, region, color, threshold, colors)

> 多点找色

- 参数 : image {Image} 图片
- 参数 : region {int[]} 范围
- 参数 : color {string} 起点颜色
- 参数 : threshold {int} 起点色阈值
- 参数 : colors {int[]} 点色数据
- 返回 : {point} 位置


```javascript
let img = $img.read("/$img/res/t01.png");
let point = $img.findMultiColors(img,[0],"#e70216",5,[
	-54, -13, "#db0306", 5,
	-121, -13, "#dc0407", 5,
	-155, -18, "#d80306", 5,
	-132, -85, "#da0306", 5,
	-78, -63, "#dd0206", 5,
	-49, -100, "#db0306", 5,
	6, -77, "#db0306", 5,
	3, -42, "#db0306", 5,
	-103, -52, "#dc0406", 5,
]);
alert("结果",point);
```


#### findImg(bigImg, minImg, options)

> 找图

- 参数 : bigImg {Image} 大图片
- 参数 : minImg {Image} 小图片
- 参数 : options {object} 参数
- 返回 : {Point} 找到的位置(中心点)


```javascript
//相对于项目的路径
let img1 = $img.read("/$img/res/t04.png");
let img2 = $img.read("/$img/res/t05.png");
let point = $img.findImg(img1,img2,{
    similar:0.8,//(可选)相似度
    region:[0,0,500,600],//(可选)范围
    trans:false,//(可选)是否开启透明找图模式
    drawResult:true,//(可选)是否保存结果图片
    savePath:"/$img/img/result.png",//(可选)保存结果图片
});
alert("结果",point);
if($file.exists("/$img/img/result.png")){
    showImg("/$img/img/result.png");
}
```


#### findImg(bigImg, minImg)

> 找图

- 参数 : bigImg 大图片
- 参数 : minImg 小图片
- 返回 : 找到的位置(中心点)


```javascript
//相对于项目的路径
let img1 = $img.read("/$img/res/t05.png");
let img2 = $img.read("/$img/res/t04.png");
let point = $img.findImg(img1,img2);
alert("结果",point);
```


#### findImgAll(bigImg, minImg, options)

> 找到所有图片位置

- 参数 : bigImg {Image} 大图片
- 参数 : minImg {Image} 需要查找的小图片
- 参数 : options {object} 查找参数
- 返回 : {point[]} 所有的位置集合


```javascript
let img1 = $img.read("/$img/res/t06.png");
let img2 = $img.read("/$img/res/t07.png");
let point = $img.findImgAll(img1,img2,{
    similar:0.8,//(可选)相似度
    region:[0,0,350,280],//(可选)范围
    trans:false,//(可选)是否开启透明找图模式
    drawResult:true,//(可选)是否保存结果图片
    savePath:"/$img/img/result.png",//(可选)保存结果图片
});
alert("结果",point);
if($file.exists("/$img/img/result.png")){
    showImg("/$img/img/result.png");
}
```


#### findImgAll(bigImg, minImg)

> 找到所有图片位置

- 参数 : bigImg {Image} 大图片
- 参数 : minImg {Image} 需要查找的小图片
- 返回 : {point[]} 所有的位置集合


```javascript
let img1 = $img.read("/$img/res/t06.png");
let img2 = $img.read("/$img/res/t07.png");
let point = $img.findImgAll(img1,img2);
alert("结果",point);
if($file.exists("/$img/img/result.png")){
    showImg("/$img/img/result.png");
}
```


#### show(image)

> 显示图片

- 参数 : image 需要显示的图片


#### show(path)

> 显示图片

- 参数 : path {string} 图片路径


```javascript
//把图片显示在屏幕上
let imgPath = "sdcard/Pictures/t01.png";
$img.show(imgPath);
```

---

## OcrOptions - 识别配置

- 更新时间:2026-01-30 19:32:54

> 识别配置




#### const {String} color;

> 二值化识别需要指定文字颜色


#### const {Number[]} region;

> 识别区域


#### const {Integer} threshold;

> 二值化识别文字用到的阈值


#### const {Boolean} gray;

> 是否使用灰度化识别


#### const {Boolean} number;

> 是否提取数字


#### const {Boolean} save;

> 是否保存结果


#### const {String} savePath;

> 保存路径
> 
> 当开启保存结果图片的时候才会按照这个路径来保存处理后的图片

---

## $ocr - 文字识别

- 更新时间:2026-01-30 19:32:54

> 文字识别
> 
> 文字识别是指通过计算机视觉技术，将图片中的文字提取出来，转换为程序可处理的文本格式。文字识别在很多场景下都有广泛的应用，比如文档扫描、图片识别、验证码识别等等。
> 
> 目前本应用内涵盖三种识别引擎,分别是 PaddleOcr、PpOcrV5、GoogleMlkit。




#### v(name)

> 设置要使用的OCR引擎
> 
> 下面我简单介绍几个识别引擎的特点,ncnn速度最快,但是部分手机会出现识别混乱的现象;
> mlkit是google提供的OCR引擎,速度较慢,但是识别准确率较高,并且兼容性比ncnn好很多;
> ppv5是2025年比较流行的一款OCR识别方案,支持识别中英文以及特殊字符,精确度高,不过它是和ncnn同系列的产品;

- 参数 : name {string} 可选:ncnn,mlkit(默认),ppv5 
- 版本 : 1.2.2


```javascript
//此函数要放在识别之前调用
$ocr.v("mlkit");//设置要使用的OCR引擎
```


#### init()

> 初始化ocr
> 
> 在使用OCR(文字识别)之前,需要加载文字模型,因此需要进行初始化,不过目前版本来看,初始化速度都很快,一般都在1秒左右
> 
> 实际上mlkit是不需要初始化的,此外如果你忘记了初始化,在进行识别文字的时候,也会自动进行初始化

- 返回 : {DetectResult} 结果
- 版本 : 1.0.0


```javascript
$ocr.init();
```


#### getPoint(word, options)

> 识别文字拿位置
> 
> 识别后将把每行结果去除空格和换行符后,判断是否包含指定文字,如果包含则返回该文字识别出来的位置
> 
> 该函数其实是对detect函数的封装,只是在识别到文字后,会判断文字关系是否包含指定文字,如果包含则返回该文字识别出来的位置

- 参数 : word {string} 文字 
- 参数 : options {OcrOptions} 配置 
- 返回 : {Point} 位置
- 版本 : 1.0.0


```javascript
//配置方式1:灰度化识别
let options = {
    region: [0,0,200,100], //(可选)识别范围(为空则识别整个屏幕)
    gray: true, //(必须)开启灰度化(默认:false),开启后会将图片转换为灰度图,识别速度会快很多,但是识别准确率会低一些
    save: true, //(可选)是否保存图片(默认:false),开启后会将识别到的图片保存到指定路径
    savePath: "/sdcard/ocr.png" //(可选)保存图片路径(为空则不保存图片),仅开启保存图片功能时有效
};
//配置方式2:二值化识别
let options = {
    region: [0,0,200,100], //(可选)识别范围(为空则识别整个屏幕)
    color: "#EEEEEE", //(必须)文字颜色(默认:#EEEEEE)
    threshold: 20, //(可选)二值化阈值(默认:20)推荐在20-50之间
    save: true, //(可选)是否保存图片(默认:false),开启后会将识别到的图片保存到指定路径
    savePath: "/sdcard/ocr.png" //保存图片路径(为空则不保存图片),仅开启保存图片功能时有效
};
//上面的配置自己根据自身需求选择一个即可
//返回opencv的Point对象
let point = $ocr.getPoint("文字", options);
if (point != null) {
    //直接点击opencv的Point对象
    $act.click(point);
}
```


#### line(options)

> 识别单行文字
> 
> 识别的方式有二值化和灰度化，自行配置即可，识别完成后会对识别的结果进行包装处理，提取出文字为单行字符串，并且去除不需要的空格和换行符。
> 
> 当你开启提取数字的时候,该函数会把提取的数字按照','号进行分隔。
> 
> 该函数是对detect函数的封装,只是在识别到文字后,会先去除空白字符之后拼接成一行;

- 参数 : options {OcrOptions} 配置 
- 返回 : {String} 一行字符
- 版本 : 1.0.0


```javascript
let options = {
    region: [0,0,200,100], //(推荐)识别范围(为空则识别整个屏幕)
    number: true, //(可选)是否提取数字(用,号分割)
    //其他配置项目参考detect方法
};
let result = $ocr.line(options);
```


#### detect(options)

> 识别文字
> 
> 会自动截屏并且识别文字,支持灰度化识别,支持二值化(默认)识别
> 
> 如果你是小白,那么请记住:二值化其实就是把图片转换为黑白的图片,而灰度化就是把图片转换为灰度的图片,经过处理之后的图片识别起来更加准确。

- 参数 : options {OcrOptions} 参数 
- 返回 : {DetectResult} 结果
- 版本 : 1.0.0


```javascript
//灰度化识别
let options = {
    region: [0,0,200,100], //识别范围(为空则识别整个屏幕)
    gray: true, //开启灰度化
    save: true, //是否保存图片
    savePath: "/sdcard/ocr.png" //保存图片路径(为空则不保存图片)
};
let result = $ocr.detect(options);
//二值化识别
let options = {
    region: [0,0,200,100], //识别范围(为空则识别整个屏幕)
    color: "#EEEEEE", //文字颜色(默认:#EEEEEE)
    threshold: 20, //二值化阈值(默认:20)
    save: true, //是否保存图片
    savePath: "/sdcard/ocr.png" //保存图片路径(为空则不保存图片)
};
//最原始的识别函数
let result = $ocr.detect(options);
```


#### detect64(base64)

> 识别base64图片

- 参数 : base64 {String} 图片base64字符串 
- 返回 : {DetectResult} 结果
- 版本 : 1.0.0


```javascript
//识别base64图片
let img = $img.read("/sdcard/test.png");
let base64 = $img.toBase64(img);
//一般情况下,base64可以从服务器端获取,而上面的代码是把本地图片转成base64的
let result = $ocr.detect64(base64);
```


#### detectPath(imgPath)

> 识别路径中图片

- 参数 : imgPath {String} 图片路径 
- 返回 : {DetectResult} 结果
- 版本 : 1.0.0


```javascript
//识别本地图片
let result = $ocr.detectPath("/sdcard/test.png");
```


#### detectImg(img)

> 识别图片

- 参数 : img {Image} 图片对象 
- 返回 : {DetectResult} 结果
- 版本 : 1.0.0


```javascript
//获取本地图片对象
let img = $img.read("/sdcard/test.png");
//识别图片对象
let result = $ocr.detectImg(img);
if (result.isSuccess()) {
    //...
}
```


#### detectBitmap(bitmap)

> 识别路径中图片

- 参数 : bitmap {Bitmap} 位图对象 
- 返回 : {DetectResult} 结果
- 版本 : 1.7.0


```javascript
//获取一个位图对象
let img = $img.read("/sdcard/t01.png");
let bitmap = img.getBitmap();
//识别本地图片
let result = $ocr.detectBitmap(bitmap);
```

---

## 训练模型-环境搭建

- 更新时间:2026-01-30 19:32:57

> 训练模型-环境搭建
> 
> 这个教程是适合小白的教程，但是你需要具备如下基础：会下载文件、会安装软件、会打字、会点按钮、会执行命令。




### 下载Python

下载python3.12.0 https://www.python.org/downloads/release/python-3120/

注意：不要下载最新版本，我规定下载这个版本当然是有说法的，不然后面安装依赖的时候报错别怪我。打开连接之后网页滑动到最后，找到适合自己电脑的版本下载安装即可，随便你安装到哪都行，但是你要知道自己安装的路径在哪，后面会用到。
这是专门用来执行python代码的。

[点击前往下载](https://www.python.org/downloads/release/python-3120/)

![](../img/395994874847000.png)


### 打开命令窗口执行一堆命令

当我们安装完python之后，需要安装一堆依赖，不过不用紧张，这个教程是给小白看的，你不需要有编程基础，会用电脑就行。

首先按住电脑快捷键Win+R，看到一个窗口输入"cmd"后回车就能打开黑窗口了。

![](../img/396597681211100.png)


当python安装完之后，打卡cmd黑色窗口直接按照寻徐运行下面的命令：(你不需要担心网速问题，这些命令用的都是国内的仓库地址，速度都很快)

注意：一定要只在一个黑色窗口中依次运行，不要为了方便开多个黑窗口执行命令，否则可能会造成pip安装工具冲突，严重点会损坏pip组件。

下面的命令是训练yolo模型需要的依赖
```bash
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ torch torchvision torchaudio
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ ultralytics
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ PyYAML
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ matplotlib
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ polars
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ scipy
```

下面的命令是将pt模型转换为onnx模型需要的依赖
```bash
pip install onnx==1.16.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install onnxruntime==1.22.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install onnxscript==0.5.7.dev20251113 -i https://pypi.tuna.tsinghua.edu.cn/simple/
pip install onnxslim==0.1.74 -i https://pypi.tuna.tsinghua.edu.cn/simple
```

下面的命令是将onnx模型转换为ncnn模型需要的依赖
```bash
pip install pnnx -i https://pypi.tuna.tsinghua.edu.cn/simple
```

我在安装onnxslim的时候遇到路径长度限制，解决方法：电脑下面搜索 power 就能看到 "Windows PowerShell"

以管理员身份打开PowerShell 执行命令：
```bash
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" -Name "LongPathsEnabled"
-Value 1 -PropertyType DWORD -Force
```


### 下载PyCharm

下载PyCharm: https://www.jetbrains.com/pycharm/download/?section=windows

下载最新版就行，随便安装在什么位置。这个工具是帮助我们运行python代码的，不过不用担心，我都把代码写好了，你只需要会配置、会点运行按钮即可。

[点击前往下载](https://www.jetbrains.com/pycharm/download/?section=windows)

![](../img/396328945123500.png)

---

## 输入输出层名称对照表

- 更新时间:2026-01-30 19:32:57

> 输入输出层名称对照表
> 
> 使用任何模型之前，确保param文件的输入层名称和输出层名称一致。




### 输入输出层名称对照表

在onnx转换为ncnn模型文件的时候，如果导出的param文件中输入输出层对应不上，则会出现闪退。为此，我将源码中的输入输出层罗列出来，方便开发者们对照各个版本的输入输出层名称来调整模型转换参数。

| 版本  | input  | output         | 尺寸      |
|-----|--------|----------------|---------|
| V5  | images | output、数字、数字   | 320x320 |
| V6  | images | output         | 640x640 |
| V7  | in0    | out0、out1、out2 | 640x640 |
| V8  | images | output         | 640x640 |
| V9  | images | output0        | 640x640 |
| V10 | in0    | out0、out1、out2 | 640x640 |
| V11 | in0    | out0、out1、out2 | 640x640 |
| V12 | in0    | out0           | 640x640 |
| V13 | in0    | out0           | 640x640 |

YoloV5版本后面输出层的两个"数字"需要看param文件的末尾"Permute"开头的行

例如:

```bash
Permute                  Transpose_590            1 1 780 781 0=1
Convolution              Conv_591                 1 1 741 782 0=255 1=1 5=1 6=130560
Reshape                  Reshape_605              1 1 782 800 0=-1 1=85 2=3
Permute                  Transpose_606            1 1 800 801 0=1
```

两个Permute行的输出层分别是：781、801 (需要你自己找找看，有一定规律，一般在"0=1"这个字段前一个，或者 1 1
800 801 这里的801就是第三个输出层名称)

那么在脚本开发的过程中如何设置yolo的输入输出层的名称呢？仔细观察输入输出层名称对照表，可以发现输入层的名称是固定的，只有一个，而输出层的名称要么是一个，要么就是三个，因此我提供了三个函数用来配置：

```javascript
$yolo.v(5);//指定版本之后才能调用，不然我不知道你要对哪个版本的yolo进行配置
$yolo.input("");//输入层只有一个名称
//输出层
$yolo.output("");//适用于yolo6、8、9(参看对照表)
$yolo.output("", "", "");//适用于yolo5、7、10、11(参看对照表)
//当你指定完输入输出层名称之后再加载模型，模型加载的时候会使用你指定的输入输出层名称
$yolo.init("demo.bin","demo.params","labels.txt");
```

其实将pt或者onnx转为ncnn模型有狠多坑要踩，为了减少一些乱七八糟的坑，我提供了输入输出层名称对照表，方便开发者们配置。


### 默认参数对照表

使用'$yolo.config()'即可配置参数，设计这个函数的主要作用是用来调优的，如果不配置则使用默认配置数据。

```js
//首先指定版本,若不指定版本，默认使用Yolo V8
$yolo.v(5);//指定使用的yolo版本为:Yolo V5
//为Yolo V5设置配置参数
$yolo.config(targetSize, meanVals, normVals, useGpu, probThreshold, nmsThreshold);
```

参数说明：不需要配置的参数填null即可

- targetSize {int} : 期望的输入图像边长（通常为正方形），例如 640 表示 640×640 像素。图像会被缩放至该尺寸后输入网络
- meanVals {float[3]} : 图像通道归一化的均值，格式为[B_mean, G_mean, R_mean] 元素范围:(0-255)
- normVals {float[3]} : 图像通道归一化的标准差，格式为[B_std, G_std, R_std] 元素范围:(0.001-0.1)
- useGpu {boolean} : 是否使用 GPU 加速
- probThreshold {float} : 过滤低置信度预测框的阈值，范围[0,1]
- nmsThreshold {float} : 抑制重叠检测框的阈值，范围[0,1]

但是我在开发yolo系列的时候，发现有些版本对于配置参数的支持也是不一样的，所以我在C/C++中尽可能的完善了所有yolo的配置参数，
不过呢还是存在无法完成的配置参数，具体的配置支持度如下：

打`Y`的表示支持配置此参数,打`N`表示不支持此参数,如果配置了这个参数也不会生效。

| 版本        | targetSize | meanVals     | normVals                          | useGpu | probThreshold | nmsThreshold |
|-----------|------------|--------------|-----------------------------------|--------|---------------|--------------|
| V5        | Y          | Y            | Y                                 | Y      | Y             | Y            |
| V6        | Y          | Y            | Y                                 | Y      | Y             | Y            |
| V7        | Y          | Y            | Y                                 | Y      | Y             | Y            |
| V8        | Y          | Y            | Y                                 | Y      | Y             | Y            |
| V9        | Y          | Y            | Y                                 | Y      | Y             | Y            |
| V10       | Y          | Y            | Y                                 | Y      | Y             | N            |
| V11       | Y          | Y            | Y                                 | Y      | Y             | Y            |
| V12       | Y          | Y            | Y                                 | Y      | Y             | Y            |
| V13       | Y          | Y            | Y                                 | Y      | Y             | Y            |
| VX        | Y          | Y            | Y                                 | Y      | Y             | Y            |
| AIGame默认值 | 640        | [0f, 0f, 0f] | [1 / 255.f, 1 / 255.f, 1 / 255.f] | false  | 0.25          | 0.45         |

总的来说，除了YoloV10不支持NMS阈值配置外，其他版本都支持全部配置。


### 如何查看输出层名称

让我们来学习几个param文件是如何查看输出层名称的吧：

在yolo5的param文件后面几行可以在0=1的地方看到781、801这样的名称作为输出层名称，所以yolo5的坑是最隐蔽的，很多人训练完模型后，高高兴兴的用移动端部署运行模型，结果闪退报错等等。

```bash
Permute                  Transpose_590            1 1 780 781 0=1
Convolution              Conv_591                 1 1 741 782 0=255 1=1 5=1 6=130560
Reshape                  Reshape_605              1 1 782 800 0=-1 1=85 2=3
Permute                  Transpose_606            1 1 800 801 0=1
```

![](../img/407162455999700.png)


在yolo8的param文件中可以找到最后一行看到output这样的输出层名称

```bash
Reshape                  Reshape_287              1 1 405 434 0=-1 1=144
Reshape                  Reshape_288              1 1 420 441 0=-1 1=144
Concat                   Concat_289               3 1 427 434 441 442 0=1
Permute                  Transpose_526            1 1 442 output 0=1
```

![](../img/407224323928300.png)


在yolo11的param文件中：可以看见out0、out1、out2这样的输出层名称

```bash
Permute                  permute_171              1 1 300 301 0=3
Concat                   cat_19                   2 1 291 301 out2 0=2
```

![](../img/407372540692700.png)

---

## 结果排序规则表

- 更新时间:2026-01-30 19:32:57

> 结果排序规则表




### YOLO识别结果排序规则表

| 参数     | 排序方向/规则    | 描述                           |
|--------|------------|------------------------------|
| -1     | 不排序（默认）    | 不对识别结果集进行任何排序操作（追求效率可选）      |
| 1      | 从左到右       | 按矩形框的x坐标升序排列（x越小，越靠左，排在前面）   |
| 2      | 从右到左       | 按矩形框的x坐标降序排列（x越大，越靠右，排在前面）   |
| 3      | 从上到下       | 按矩形框的y坐标升序排列（y越小，越靠上，排在前面）   |
| 4      | 从下到上       | 按矩形框的y坐标降序排列（y越大，越靠下，排在前面）   |
| 5      | 从左上到右下     | 按矩形框x+y的和升序排列（左上区域值更小，排在前面）  |
| 6      | 从右上到左下     | 按矩形框x-y的差降序排列（右上区域差值更大，排在前面） |
| 7      | 从左下到右上     | 按矩形框x-y的差升序排列（左下区域差值更小，排在前面） |
| 8      | 从右下到左上     | 按矩形框x+y的和降序排列（右下区域值更大，排在前面）  |
| 9      | 从左到右并且从上到下 | 优先按x坐标升序，x相同时按y坐标升序          |
| 10     | 从右到左并且从上到下 | 优先按x坐标降序，x相同时按y坐标升序          |
| 11     | 从左到右并且从下到上 | 优先按x坐标升序，x相同时按y坐标降序          |
| 12     | 从右到左并且从下到上 | 优先按x坐标降序，x相同时按y坐标降序          |
| 13     | 大的面积在前面    | 按矩形框面积降序排列（面积越大，排在前面）        |
| 14     | 小的面积在前面    | 按矩形框面积升序排列（面积越小，排在前面）        |
| 其他（默认） | 从左到右（默认规则） | 按矩形框的x坐标升序排列（与编码1的规则一致）      |


### 具体应用

例如现在我有一个数据集，我主要用来识别数字和一个逗号字符串，我的数据集大多数都是205x30的图片，你觉得我应该用什么样的尺寸比较合适？用什么样的排序规则比较合适？

![](../img/3811231098900.png)

首先我们要知道：yolo输入的图片尺寸必须是32的倍数，我们的图片是高度为30的，因此使用32来作为模型的输入高度，宽度是205，我们找到最近的32的倍数，就是192，因此输入的尺寸就定好了：192x32



```python
//训练模型的py代码 ：
from ultralytics import YOLO
if __name__ == '__main__':
    model = YOLO(r"yolo11n.pt")  # 指定权重 (项目/yolo11n.pt)
    model.train(
        data=r"hydd2.yaml",  # 指定你的数据集配置文件 (项目/ultralytics/cfg/datasets/cm.yaml)
        epochs=50,  # 定义训练的总轮数
        imgsz=[32, 192],  # 指定输入图片的尺寸[高度,宽度]
        batch=2,  # 定义批次大小 每次同时向模型喂送 2 张图片进行处理
        cache=False,  # 不用缓存 避免内存溢出 （如果电脑内存大、可以开启，因为速度会快一点）
        workers=4,  # 指定数据加载时使用的 CPU 线程数 推荐：0、4、8 都是可以的
    )
```



```python

---

## 导出为ONNX格式（高在前、宽在后）
model.export(format='onnx', imgsz=[32, 192])
```


最终把onnx转为ncnn模型时的参数：高在前、宽在后


```bash
pnnx best.onnx inputshape=[1,3,32,192]f32 device=cpu
```


接下来确定排序方向，由于我制作的是文字识别，排序方向当然就是从左到右的，因此代码这么写：


```javascript
let yolo = $yolo.create(12);
yolo.setSize(192,32);//先宽、后高
yolo.setDir(1);//识别结果按照从左到右排序
//开始加载模型
yolo.init("res/ocr.bin","res/ocr.param",["0","1","2","3","4","5","6","7","8","9",","]);
```

---

## YoloObject - 目标检测对象

- 更新时间:2026-01-30 19:32:57

> Yolo对象




#### init(binPath, paramPath, labelPath)

> 初始化

- 参数 : binPath {string} 模型文件路径
- 参数 : paramPath {string} 参数文件路径
- 参数 : labelPath {string} 标签文件路径
- 返回 : {YoloResult} 结果
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.init("res/yolov5s.bin", "res/yolov5s.param", "res/classes.txt")
```


#### init(binPath, paramPath, labels)

> 初始化

- 参数 : binPath {string} 模型文件路径
- 参数 : paramPath {string} 参数文件路径
- 参数 : labels {string[]} 标签
- 返回 : {YoloResult} 结果
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.init("res/yolov5s.bin", "res/yolov5s.param", ["人","鸟","自行车"])
```


#### detect()

> 检测屏幕
> 
> 需要截屏权限

- 返回 : {YoloResult} 结果
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.init("res/yolov5s.bin", "res/yolov5s.param", "res/classes.txt");
let res = yolo.detect();
log("检测结果",res);
```


#### detect(img)

> 检测图片

- 参数 : img {Image} 图片
- 返回 : {YoloResult} 结果
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.init("res/yolov5s.bin", "res/yolov5s.param", "res/classes.txt");
let img = $img.read("res/t01.png");
let res = yolo.detect(img);
log("检测结果",res);
```


#### detect(bitmap)

> 检测位图

- 参数 : bitmap {Bitmap} 位图
- 返回 : {YoloResult} 结果
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.init("res/yolov5s.bin", "res/yolov5s.param", "res/classes.txt");
let img = $img.read("res/t01.png");
let res = yolo.detect(img.getBitmap());
log("检测结果",res);
```


#### detect(imgPath)

> 检测路径中的图片

- 参数 : imgPath {string} 图片路径
- 返回 : {YoloResult} 结果
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.init("res/yolov5s.bin", "res/yolov5s.param", "res/classes.txt");
let res = yolo.detect("res/test.jpg");
```


#### isInit()

> 是否初始化
> 
> 只有成功加载模型之后才会返回true

- 返回 : {boolean} 是否初始化了
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.init("res/yolov5s.bin", "res/yolov5s.param", "res/classes.txt");
if(yolo.isInit()) {
    log("初始化成功");
}
```


#### setDir(dir)

> 设置排序方向
> 
> 排序方向一共有15种，默认是不排序，具体排序顺序请参考：结果排序规则表

- 参数 : dir {int} 排序方向(默认:-1)
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setDir(-1);//如果不需要排序就不排序，以免影响速度
```


#### setSize(w, h)

> 设置输入尺寸

- 参数 : w {int} 宽
- 参数 : h {int} 高
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setSize(640,640);
```


#### setUseGpu(use)

> 设置是否使用GPU

- 参数 : use {boolean} 是否使用GPU
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setUseGpu(true);
```


#### setProbThreshold(pt)

> 设置相似度阈值

- 参数 : pt {float} 相似度阈值
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setProbThreshold(0.5f);
```


#### setNmsThreshold(nt)

> 设置抑制阈值

- 参数 : nt {float} 抑制阈值
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setNmsThreshold(0.5f);
```


#### setMeanVals(meanVals)

> 设置均值

- 参数 : meanVals {float[]} 均值
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setMeanVals([0.485f, 0.456f, 0.406]);
```


#### setNormVals(normVals)

> 设置归一化

- 参数 : normVals {float[]} 归一化
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setNormVals([0.00392157f, 0.00392157f, 0.00392157f]);
```


#### setInputName(inputName)

> 设置输入层名称
> 
> 输入层一般只有一个

- 参数 : inputName {string} 输入层名称
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setInputName("images");
```


#### setOutputName(outputName1)

> 设置输出层名称
> 
> 有些版本的模型输出层可能有多个，当模型输出层只有一个的时候可以使用这个函数。

- 参数 : outputName1 {string} 输出层名称1
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setOutputName("output1");
```


#### setOutputName(outputName1, outputName2, outputName3)

> 设置输出层名称
> 
> 有些版本的模型有多个输出层，但是有些输出层只有一个，即便你设置了三个，也只会生效第一个。

- 参数 : outputName1 {string} 输出层名称1
- 参数 : outputName2 {string} 输出层名称2
- 参数 : outputName3 {string} 输出层名称3
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.setOutputName("output1", "output2", "output3");
```


#### getId()

> 获取id

- 返回 : {String} id
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
log(yolo.getId());
```


#### recycle()

> 释放资源
> 
> 释放资源，效果和 'close()' 等价

- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.recycle();
```


#### close()

> 关闭
> 
> 释放资源，效果和 'recycle()' 等价

- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
yolo.close();
```

---

## YoloResult - 检测结果

- 更新时间:2026-01-30 19:32:58

> yolo检测结果




#### const {boolean} success;


#### const {String} des;


#### const {String} err;


#### const {List<YoloResultCell>} data;


#### const {List<YoloResultCell>} 数据;


#### isSuccess()


#### setSuccess(success)


#### getDes()


#### setDes(des)


#### getData()


#### setData(data)


#### getErr()


#### setErr(err)


#### json()


#### json_zn()

---

## $yolo - 目标检测

- 更新时间:2026-01-30 19:32:57

> 目标检测
> 
> $yolo支持全系列的yolo版本：yoloV5、yoloV6、yoloV7、yoloV8、yoloV9、yoloV10、yoloV11、yoloV12、yoloV13；




#### create(version)

> 创建yolo对象
> 
> 当前支持的Yolo版本有：YoloX、YoloV5、YoloV6、YoloV7、YoloV8、YoloV9、YoloV10、YoloV11、YoloV12、YoloV13，
> 当你传入版本号为0，则创建一个YoloX对象；当你传入版本号为5，则创建一个YoloV5对象；为11，则创建一个YoloV11对象，以此类推。
> 
> 每当创建一个yolo对象的时候，我会存储一个键值对[yoloId,yolo对象]，因此你可以在任何脚本中通过这个id拿到对象。

- 参数 : version {int} yolo版本
- 返回 : {YoloObject} yolo对象
- 版本 : 1.8.3


```javascript
//首选创建一个对象
let yolo12 = $yolo.create(12);
//接下来就可以设置一些基础配置了
//使用gpu这个配置必须在初始化之前调用才能生效，其他的配置可以在任何地方调用
yolo12.setUseGpu(true);//是否使用GPU加速
yolo12.setSize(192,64);//注意尺寸必须是32的倍数
yolo12.setProbThreshold(0.5);//设置相似度
```


#### has(id)

> 是否有yolo对象

- 参数 : id {string} yoloID
- 返回 : {boolean} 是否有
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
log($yolo.has(yolo.getId()));//true
```


#### get(id)

> 获取yolo对象

- 参数 : id {string} yoloID
- 返回 : {YoloObject} yolo对象
- 版本 : 1.8.3


```javascript
//[初始化脚本.js]:
let storage = $storage.create("我的YOLO");
let yolo = $yolo.create(12);
yolo.setSize(192,64);
yolo.setUseGpu(true);
storage.putStr("mYoloId",yolo.getId());//保存yolo对象id
//[其他脚本.js]:
let storage = $storage.create("我的YOLO");
let yolo = $yolo.get(storage.getStr("mYoloId","null"));
yolo.detect(img);//使用yolo对象进行检测
```


#### close(id)

> 关闭yolo对象
> 
> 由于java端只是持有了C端的(yolo对象)对象句柄，双端的回收机制无法相互干涉，如果java端回收了对象，并不会回收C端的对象，因此需要手动释放资源。
> 
> 因此在使用yolo的时候，在初始化阶段就先存好一个yolo对象的ID，之后就可以在任何脚本中获取这个对象了。

- 参数 : id {string} yoloID
- 版本 : 1.8.3


```javascript
let yolo = $yolo.create(12);
//拿到id
let id = yolo.getId();
//释放(C端)yolo对象
$yolo.close(id);
```


#### closeAll()

> 释放所有yolo对象
> 
> 由于java端只是持有了C端的(yolo对象)对象句柄，双端的回收机制无法相互干涉，如果java端回收了对象，并不会回收C端的对象，因此需要手动释放资源。
> 
> 因此在使用yolo的时候，在初始化阶段就先存好一个yolo对象的ID，之后就可以在任何脚本中获取这个对象了。

- 版本 : 1.8.3


```javascript
//释放所有(C端)yolo对象
$yolo.closeAll();
```