# $ui 控件 (二): img/input/ls/nav/pager/progress/radio/range/switch/text/webview

# 多页布局

- 更新时间:2026-01-30 19:33:13

> 多页布局-pager
> 
> 多页布局允许用户在里面写多个界面并实现界面左右滑动，并且支持绑定标签页布局(tab)以及导航栏(nav)
> 
> 原生类型:{androidx.viewpager2.widget.ViewPager2}




## 一、常用属性


## 二、常用函数


### 设置下标(index)

> 设置当前页面索引

- 参数 : index {int} 当前页面索引


```javascript
//解析界面,获得ui布局
定义 我的界面 = $界面.解析布局("./界面/主界面.xml");
//获得控件(传入"标识")
定义 多页布局 = 我的界面.找控件("我的多页布局");
//设置当前页面索引为0
多页布局.设置下标(0);
```


### 获取下标()

> 获得当前页面索引

- 返回 : {int} 当前页面索引


```javascript
//解析界面,获得界面布局
定义 我的界面 = $界面.解析布局("./界面/主界面.xml");
//获得控件
定义 多页布局 = 我的界面.找控件("我的多页布局");
//获得当前页面索引
定义 下标 = 多页布局.获取下标();
```


### 绑定(xTab)

> 绑定与标签页联动

- 参数 : xTab {tab} 标签页布局


```javascript
//解析界面,获得界面布局
定义 我的界面 = $界面.解析布局("./界面/主界面.xml");
//获得控件
定义 多页布局 = 我的界面.找控件("我的多页布局");
定义 标签页 = 我的界面.找控件("我的标签页");
//与标签页布局联动
多页布局.绑定(标签页);
```


### 绑定(xNav)

> 绑定与导航栏联动

- 参数 : xNav {nav} 底部导航布局


```javascript
//解析界面,获得界面布局
定义 我的界面 = $界面.解析布局("./界面/主界面.xml");
//获得控件
定义 多页布局 = 我的界面.找控件("我的多页布局");
定义 导航栏 = 我的界面.找控件("我的导航栏");
//与导航栏联动
多页布局.绑定(导航栏);
```


### 监听界面切换(回调)

> 监听界面切换事件

- 参数 : 回调 {(下标)=>{}} 界面切换事件回调


```javascript
//解析界面,获得界面布局
定义 我的界面 = $界面.解析布局("./界面/主界面.xml");
//获得控件
定义 多页布局 = 我的界面.找控件("我的多页布局");
//监听界面切换事件
多页布局.监听界面切换((下标)=>{
    //..
});
```


### 监听状态改变(回调)

> 监听状态改变事件

- 参数 : 回调 {(状态)=>{}} 状态改变事件回调


```javascript
//解析界面,获得界面布局
定义 我的界面 = $界面.解析布局("./界面/主界面.xml");
//获得控件
定义 多页布局 = 我的界面.找控件("我的多页布局");
//监听状态改变事件
多页布局.监听状态改变((状态)=>{
    //...
});
```

---

# 进度条

- 更新时间:2026-01-30 19:33:13

> 进度条-progress
> 
> 圆形原生类型:{com.google.android.material.progressindicator.CircularProgressIndicator}
> 线性原生类型:{com.google.android.material.progressindicator.LinearProgressIndicator}




进度条：比如下载进度，游戏进度，进度条就是用来显示进度的控件


![](./img/progress_demo.gif)


```html
<ui>
    <statusbar />
    <linear w="max" padding="10">
        <linear w="max" dir="h">
            <progress w="max" padding="10" run="true" />
            <progress w="max" color="#518855" padding="10" run="true" />
            <progress w="max" color="#B44A4A" padding="10" run="true" />
        </linear>
        <progress w="max" style="line" run="true" padding="10" />
        <progress w="max" style="line" color="#518855" padding="10" run="true" />
        <progress w="max" style="line" color="#B44A4A" padding="10" run="true" />
    </linear>
</ui>
```


## 一、基础用法


```html
<ui>
    <statusbar />
    <linear w="max" padding="10">
        <!-- 指定进度条的id -->
        <progress id="circularProgress" w="max"/>
        <progress id="lineProgress" w="max" style="line"/>
    </linear>
</ui>
```

```javascript
//解析布局
let ui = $ui.layout("ui.xml");
ui.show();//显示界面
//获取圆形/线性进度条
let cp = ui.id("circularProgress");
let lp = ui.id("lineProgress");
//动态模拟进度条的走动
for (let i = 1; i <= 10; i++) {
    sleep(150);
    //[核心]:设置进度
    cp.setProgress(i * 10);
    lp.setProgress(i * 10);
}
```


## 二、常用属性


![](./img/progress_style.png)

![](./img/progress_thickness.png)

![](./img/progress_color.png)

![](./img/progress_padding.png)

![](./img/progress_bg.png)

![](./img/progress_bgImg.png)

## 三、常用函数


### 设置进度(进度值)

> 设置进度
> 
> 此方法需要安卓7.0以上生效

- 参数 : 进度值 {int} 进度值(0-100)


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 进度条 = 界面.找控件("我的进度条");
//设置进度
进度条.设置进度(50);
```


### 设置最大值(最大值)

> 设置最大进度

- 参数 : 最大值 {int} 最大进度值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 进度条 = 界面.找控件("我的进度条");
//设置最大进度
进度条.设置最大值(100);
```


### 获取进度()

> 获取进度

- 返回 : {int} 当前进度值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 进度条 = 界面.找控件("我的进度条");
//获得进度
定义 进度 = 进度条.获取进度();
```


### 显示()

> 显示进度条


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 进度条 = 界面.找控件("我的进度条");
//显示进度条
进度条.显示();
```


### 隐藏()

> 隐藏进度条


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 进度条 = 界面.找控件("我的进度条");
//隐藏进度条
进度条.隐藏();
```

---

# 单选按钮组

- 更新时间:2026-01-30 19:33:13

> 单选按钮组-radio-group
> 
> 在此布局中，单选按钮会自动取消和选中，保证一组按钮只被选中一个
> 
> 是布局父类的(XLayout)的子类
> 
> 原生类型:{android.widget.RadioGroup}




## 一、常用属性


### 选中(下标)

> 设置选中的下标

- 参数 : 下标 {int} 按钮下标


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获得控件
定义 单选组 = 界面.找控件("我的单选组");
//设置选中的下标
单选组.选中(0);
```


### 监听选中(回调函数)

> 监听选中按钮的下标

- 参数 : 回调函数 ((下标)=>{}) 回调函数


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获得控件
定义 单选组 = 界面.找控件("我的单选组");
//监听选中按钮的下标
单选组.监听选中((下标)=>{
    $界面.土司("当前下标:"+下标);
});
```


### 获取选中下标()

> 获取选中的下标

- 返回 : {int} 下标 (-1表示没有选择)


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获得控件
定义 单选组 = 界面.找控件("我的单选组");
//获得选中的下标
定义 下标 = 单选组.获取选中下标();
```


### 获取选中文本()

> 获取选中的文本

- 返回 : {string} 文本 (null表示没有选择)


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获得控件
定义 单选组 = 界面.找控件("我的单选组");
//获得选中的文本
定义 文本 = 单选组.获取选中文本();
```

---

# 单选按钮

- 更新时间:2026-01-30 19:33:13

> 单选按钮-radio
> 
> 原生类型:{com.google.android.material.radiobutton.MaterialRadioButton}




单选按钮：一般需要配合单选按钮组(radio-group)的配合才能实现互相排斥的效果，这个控件常用在只需要在多个选择中选择一个的情况。


![](./img/radio_color.png)

## 一、常用属性


![](./img/radio_color.png)

![](./img/radio_check.png)

![](./img/radio_text.png)

![](./img/radio_textColor.png)

![](./img/radio_padding.png)

![](./img/radio_gravity.png)

![](./img/radio_bg.png)

![](./img/radio_bgImg.png)

## 二、常用函数


### 是选中的()

> 判断选中状态

- 返回 : {布尔值} 是否选中
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 单选按钮 = 界面.找控件("我的单选按钮");
//判断选中状态
如果(单选按钮.是选中的()){
    日志("选中了");
}
```


### 设置选中(状态)

> 设置选中状态

- 参数 : 状态 {boolean} 是否选中


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 单选按钮 = 界面.找控件("我的单选按钮");
//设置选中状态
单选按钮.设置选中(是);
```


### 监听选中(回调)

> 监听选中事件

- 参数 : 回调 {(是否选中)=>{}} 选中事件回调


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 单选按钮 = 界面.找控件("我的单选按钮");
//监听选中事件
单选按钮.监听选中((是否选中)=>{
    //..
});
```


### 设置重力(重力)

> 设置重力

- 参数 : 重力 {String} 重力值，例如:"中|下"


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 单选按钮 = 界面.找控件("我的单选按钮");
//设置重力
单选按钮.设置重力("中|下");
```


### 设置文字(文本)

> 设置文字

- 参数 : 文本 {String} 文字内容


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 单选按钮 = 界面.找控件("我的单选按钮");
//设置文字
单选按钮.设置文字("吃饭");
```


### 获取文字()

> 获取文字

- 返回 : {String} 文字内容


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 单选按钮 = 界面.找控件("我的单选按钮");
//获得文字
定义 文本 = 单选按钮.获取文字();
```


### 设置主题颜色(颜色)

> 设置主题颜色

- 参数 : 颜色 {String} 颜色值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 单选按钮 = 界面.找控件("我的单选按钮");
//设置主题颜色
单选按钮.设置主题颜色("#26282E");
```


### 设置文本颜色(颜色)

> 设置文本颜色

- 参数 : 颜色 {String} 颜色值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 单选按钮 = 界面.找控件("我的单选按钮");
//设置文本颜色
单选按钮.设置文本颜色("#26282E");
```

---

# 轨道

- 更新时间:2026-01-30 19:33:13

> 轨道-rail
> 
> 这个控件和nav导航栏控件很像，只不过是竖向排列的
> 
> 原生类型:{com.google.android.material.navigationrail.NavigationRailView}




## 一、常用属性


## 二、常用函数


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {数字} 文本颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//设置背景颜色
轨道栏.设置背景颜色($颜色.红色);
```


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//设置背景颜色
轨道栏.设置背景颜色("#1E1F22");
```


### 设置图标颜色(颜色)

> 设置图标颜色

- 参数 : 颜色 {数字} 文本颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//设置图标颜色
轨道栏.设置图标颜色($颜色.红色);
```


### 设置图标颜色(颜色)

> 设置图标颜色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//设置图标颜色
轨道栏.设置图标颜色("#1E1F22");
```


### 设置文本颜色(颜色)

> 设置文本颜色

- 参数 : 颜色 {数字} 文本颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//设置文本颜色
轨道栏.设置文本颜色($颜色.红色);
```


### 设置文本颜色(颜色)

> 设置文本颜色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//设置文本颜色
轨道栏.设置文本颜色("#1E1F22");
```


### 设置选中颜色(颜色)

> 设置选中颜色

- 参数 : 颜色 {数字} 文本颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//设置选中颜色
轨道栏.设置选中颜色($颜色.红色);
```


### 设置选中颜色(颜色)

> 设置选中颜色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//设置选中颜色
轨道栏.设置选中颜色("#1E1F22");
```


### 选中(索引)

> 选中指定菜单

- 参数 : 索引 {int} 菜单索引


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//选中指定菜单
轨道栏.选中(0);
```


### 菜单(回调)

> 监听菜单事件

- 参数 : 回调 {(标题)=>{}} 菜单点击事件


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./主界面.xml");
//获取控件
定义 轨道栏 = 界面.找控件("我的轨道栏");
//监听菜单事件
轨道栏.菜单((标题)=>{
    土司(标题);
});
```

---

# 范围

- 更新时间:2026-01-30 19:33:13

> 范围-range
> 
> 原生类型:{com.google.android.material.slider.RangeSlider}




## 一、常用属性


## 二、常用函数


### 标签格式化(回调)

> 设置标签格式化

- 参数 : 回调 {(浮点值)=>{ return "标签"; }} 格式化回调


### 监听变化(回调)

> 监听数据变化

- 参数 : 回调 {(开始,结束)=>{}} 回调函数


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 范围 = 界面.找控件("我的范围");
//监听数据变化
范围.监听变化((开始,结束)=>{
    //..
});
```


### 获取范围()

> 获取范围

- 返回 : {number[]}


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 范围 = 界面.找控件("我的范围");
//获得范围数据
定义 范围数据 = 范围.获取范围();
```


### 设置数据(开始, 结束)

> 设置数据

- 参数 : 开始 {float} 开始值
- 参数 : 结束 {float} 结束值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 范围 = 界面.找控件("我的范围");
//设置数据(开始,结束)
范围.设置数据(0,100);
```

---

# 拖动条

- 更新时间:2026-01-30 19:33:13

> 拖动条-seek
> 
> 该组件比slider更加小巧，属于安卓原生组件。
> 
> 原生类型:{android.widget.SeekBar}




## 一、常用属性


## 二、常用函数


### onChange(callback)

> 设置数值变化监听
> 
> 注意:只监听由用户手动触发的数值变化,若为编程时设置的数值,则忽略

- 参数 : callback {(value)=>{}}


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let seek = ui.id("mSeek");
//设置选中的下标
seek.onChange((value)=>{
    //..
});
```


### getValue()

> 获取当前数值

- 返回 : {int} 当前数值


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let seek = ui.id("mSeek");
//获取进度数值
let value = seek.getValue();
```


### getMin()

> 获取最小值

- 返回 : {int} 当前数值


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let seek = ui.id("mSeek");
//获取最小值
let minVal = seek.getMin();
```


### getMax()

> 获取最大值

- 返回 : {int} 当前数值


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let seek = ui.id("mSeek");
//获取最大值
let maxVal = seek.getMax();
```


### setValue(value)

> 设置数值

- 参数 : value {int} 数值


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let seek = ui.id("mSeek");
//设置数值
seek.setValue(50);
```


### setMax(value)

> 设置最大值

- 参数 : value {int} 数值


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let seek = ui.id("mSeek");
//设置最大值
seek.setMax(50);
```


### setMin(value)

> 设置最小值

- 参数 : value {int} 数值


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let seek = ui.id("mSeek");
//设置最小值
seek.setMin(0);
```

---

# 滑动条

- 更新时间:2026-01-30 19:33:13

> 滑动条-slider
> 
> 原生类型:{com.google.android.material.slider.Slider}




滚动条：常用于动态设置数字参数，通过滑动就可以变换数值。


![](./img/slider_demo.png)

## 一、常用属性


![](./img/slider_from.png)

![](./img/slider_to.png)

![](./img/slider_value.png)

![](./img/slider_step.png)

![](./img/slider_demo.png)

![](./img/slider_label.png)

![](./img/slider_labelEnd.png)

![](./img/slider_padding.png)

![](./img/slider_bg.png)

![](./img/slider_bgImg.png)

## 二、常用函数


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {数字} 文本颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滚动条 = 界面.找控件("我的滚动条");
//设置背景颜色
滚动条.设置背景颜色($颜色.红色);
```


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滚动条 = 界面.找控件("我的滚动条");
//设置背景颜色
滚动条.设置背景颜色("#1E1F22");
```


### 设置主题颜色(颜色)

> 设置主题颜色

- 参数 : 颜色 {数字} 文本颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滚动条 = 界面.找控件("我的滚动条");
//设置主题颜色
滚动条.设置主题颜色($颜色.红色);
```


### 设置主题颜色(颜色)

> 设置主题颜色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滚动条 = 界面.找控件("我的滚动条");
//设置主题颜色
滚动条.设置主题颜色("#1E1F22");
```


### 标签格式化(回调)

> 设置标签格式化

- 参数 : 回调 {(浮点值)=>{ return "标签"; }} 格式化回调


### 监听变化(回调)

> 监听数值变化
> 
> 注意:只监听由用户手动触发的数值变化,若为编程时设置的数值,则忽略

- 参数 : 回调 {(数值)=>{}}


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滑动条 = 界面.找控件("我的滑动条");
//监听数值变化
滑动条.监听变化((数值)=>{
    //..
});
```


### 获取值()

> 获取当前值

- 返回 : {float} 当前数值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滑动条 = 界面.找控件("我的滑动条");
//获得当前值
定义 当前值 = 滑动条.获取值();
```


### 设置值(数值)

> 设置当前值

- 参数 : 数值 {float} 当前值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滑动条 = 界面.找控件("我的滑动条");
//设置当前值
滑动条.设置值(10);
```


### 设置开始值(开始值)

> 设置开始值

- 参数 : 开始值 {float} 开始值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滑动条 = 界面.找控件("我的滑动条");
//设置开始值
滑动条.设置开始值(0);
```


### 设置进步值(进步值)

> 设置进步值

- 参数 : 进步值 {float} 进步值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滑动条 = 界面.找控件("我的滑动条");
//设置进步值
滑动条.设置进步值(1);
```


### 设置结束值(结束值)

> 设置结束值

- 参数 : 结束值 {float} 结束值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滑动条 = 界面.找控件("我的滑动条");
//设置结束值
滑动条.设置结束值(100);
```


### 设置数据(开始, 结束)

> 设置数据

- 参数 : 开始 {float} 开始值
- 参数 : 结束 {float} 结束值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滑动条 = 界面.找控件("我的滑动条");
//设置数据(开始,结束)
滑动条.设置数据(0,100);
```


### 设置数据(开始, 结束, 当前值)

> 设置数据

- 参数 : 开始 {float} 开始值
- 参数 : 结束 {float} 结束值
- 参数 : 当前值 {float} 当前值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 滑动条 = 界面.找控件("我的滑动条");
//设置数据(开始,结束,当前值)
滑动条.设置数据(0,100,20);
```

---

# 状态栏

- 更新时间:2026-01-30 19:33:13

> 状态栏-statusbar
> 
> 本质上就是一个{MaterialTextView},只不过高度为状态条的高度,此控主要用来占位置,避免手机状态条挡住主要的布局
> 
> 原生类型:{com.google.android.material.textview.MaterialTextView}




状态栏：一般手机界面的最上方的部分就是状态栏。


![](./img/statusbar_example.png)

## 一、常用属性


![](./img/822704913786800.png)

![](./img/823019796005800.png)

![](./img/822979123418600.png)

## 二、常用函数


### 设置颜色(颜色)

> 设置颜色

- 参数 : 颜色 {string} 颜色值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 状态栏 = 界面.找控件("我的状态栏");
//设置颜色
状态栏.设置颜色("#1E1F22");
```

---

# 开关

- 更新时间:2026-01-30 19:33:13

> 开关-switch
> 
> 原生类型:{com.google.android.material.materialswitch.MaterialSwitch}




开关：顾名思义，就是开关的意思，只有打开或者关闭两种状态。


![](./img/823241319415800.png)

## 一、常用属性


![](./img/823661390164300.png)

![](./img/823704126486300.png)

![](./img/823742446042900.png)

![](./img/823778688193600.png)

![](./img/823844386523100.png)

![](./img/823887649088400.png)

![](./img/824262862930600.png)

![](./img/824016785709400.png)

![](./img/824071990244600.png)

![](./img/824213477601000.png)

## 二、常用函数


### 设置选中(状态)

> 设置选中状态

- 参数 : 状态 {boolean} 是否选中


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 开关 = 界面.找控件("我的开关");
//设置选中状态
开关.设置选中(是);
```


### 是选中的()

> 判断选中状态

- 返回 : {布尔值} 是否选中
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 开关 = 界面.找控件("我的开关");
//判断选中状态
如果(开关.是选中的()){
    日志("选中了");
}
```


### 监听选中(回调)

> 监听状态改变

- 参数 : 回调 ((是否选中)=>{}) 回调函数


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 开关 = 界面.找控件("我的开关");
//监听状态改变
开关.监听选中((是否选中)=>{
    //..
});
```


### 设置重力(重力)

> 设置重力

- 参数 : 重力 {String} 例如:"中|下"


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 开关 = 界面.找控件("我的开关");
//设置重力
开关.设置重力("中|下");
```


### 设置文本(文本)

> 设置文本

- 参数 : 文本 {String} 文本内容


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 开关 = 界面.找控件("我的开关");
//设置文本
开关.设置文本("是否开启");
```


### 获取文本()

> 获取文本

- 返回 : {String} 文本内容


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 开关 = 界面.找控件("我的开关");
//获得文本
定义 文本 = 开关.获取文本();
```


### 设置主题颜色(颜色)

> 设置主题颜色

- 参数 : 颜色 {String} 颜色值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 开关 = 界面.找控件("我的开关");
//设置主题颜色
开关.设置主题颜色("#26282E");
```


### 设置文本颜色(颜色)

> 设置文本颜色

- 参数 : 颜色 {String} 颜色值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 开关 = 界面.找控件("我的开关");
//设置文本颜色
开关.设置文本颜色("#26282E");
```

---

# 标签布局

- 更新时间:2026-01-30 19:33:13

> 标签布局-tab
> 
> 原生类型:{com.google.android.material.tabs.TabLayout}




## 一、常用属性

---

# 文本

- 更新时间:2026-01-30 19:33:13

> 文本-text
> 
> 原生类型:{com.google.android.material.textview.MaterialTextView}




## 一、常用属性


## 二、常用函数


### 设置文本(文本内容)

> 设置文本

- 参数 : 文本内容 {string} 文本内容


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 文本 = 界面.找控件("我的文本");
//设置文本
文本.设置文本("新的内容");
```


### 设置颜色(颜色)

> 设置文本颜色

- 参数 : 颜色 {int} 文本颜色值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 文本 = 界面.找控件("我的文本");
//设置文本颜色
文本.设置颜色($颜色.红色);
```


### 设置颜色(颜色)

> 设置文本颜色

- 参数 : 颜色 {string} 文本颜色值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 文本 = 界面.找控件("我的文本");
//设置文本颜色
文本.设置颜色("#1E1F22");
```


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {数字} 文本颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 文本 = 界面.找控件("我的文本");
//设置背景颜色
文本.设置背景颜色($颜色.红色);
```


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 文本 = 界面.找控件("我的文本");
//设置背景颜色
文本.设置背景颜色("#1E1F22");
```


### 设置尺寸(尺寸)

> 设置文本尺寸

- 参数 : 尺寸 {float} 文本尺寸


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 文本 = 界面.找控件("我的文本");
//设置文本尺寸
文本.设置尺寸(18);
```


### 获取文本()

> 获取文本内容

- 返回 : {string} 文本内容


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 文本 = 界面.找控件("我的文本");
//获得文本内容
定义 文本内容 = 文本.获取文本();
```

---

# 工具栏

- 更新时间:2026-01-30 19:33:13

> 工具栏-toolbar
> 
> 原生类型:{com.google.android.material.bottomappbar.BottomAppBar}




### 菜单(回调)

> 监听菜单事件

- 参数 : 回调 {(标题)=>{}} 菜单点击事件


```javascript
//监听菜单事件
工具栏.菜单((标题)=>{
    控制台.日志(标题);
});
```

---

# $ui - 界面交互

- 更新时间:2026-01-30 19:33:14

> UI交互界面




### 界面线程(回调函数)

> 界面线程
> 
> 一般修改界面元素的时候需要用到界面线程，由于本应用已经自动把所有控件操作都放到了界面线程中，所以不需要额外调用。

- 参数 : 回调函数 {()=>{}} 回调函数 
- 版本 : 1.5.8


```javascript
//在界面线程中执行
$界面.界面线程(()=>{
    //在界面线程中执行的代码
});
//或者下面的方式更加直观:先定义要执行的函数
定义 要执行的函数 = 函数(){
    //要执行的内容
}
//然后把这个函数传进去,那么这个函数就会在界面线程中执行
$界面.界面线程(要执行的函数);
```


### 解析布局(xml内容或者路径)

> 解析全屏布局
> 
> 创建一个界面(ui)对象,并且解析布局,最终返回这个界面(ui)对象

- 参数 : xml内容或者路径 {string} xml内容或者xml路径 
- 返回 : {UI} ui对象
- 版本 : 1.5.8


```javascript
定义 我的界面 = $界面.解析布局("./资源/主界面.xml");
```


### 创建底部弹窗(活动对象)

> 显示底部弹窗

- 参数 : 活动对象 {activity} 需要显示底部弹窗的活动对象 
- 返回 : {Sheet} 弹窗对象
- 版本 : 1.5.8


```javascript
//假如已经显示了一个ui了
定义 界面 = $界面.解析界面("主界面.xml");
界面.显示();//显示界面(ui)
//当界面(ui)显示之后就可以获取对应界面的活动对象(activity)了
定义 底部弹窗 = $界面.创建底部弹窗(界面.获得活动对象());//创建目标活动的底部弹窗对象
底部弹窗.解析布局("底部对话框.xml"); //解析底部弹窗(sheet)布局
底部弹窗.找控件("我的按钮"); //绑定底部弹窗(sheet)中的组件事件
底部弹窗.显示(); //显示底部弹窗
```


### 土司(文本)

> 悬浮土司
> 
> 悬浮土司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : 文本 {string} 文本 
- 版本 : 1.5.8


```javascript
$界面.土司("文本");
```


### 土司(文本, 重力)

> 悬浮土司
> 
> 悬浮土司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : 文本 {string} 文本 
- 参数 : 重力 {string} 位置 
- 版本 : 1.5.8


```javascript
$界面.土司("文本","中");
```


### 转px(dp)

> dp转px

- 参数 : dp {数字} dp(虚拟长度单位)
- 返回 : {数字} 转换后的px(像素值)
- 版本 : 1.8.2


```javascript
//获取10dp的真实像素单位
定义 像素 = $界面.转px(10);
```


### 转dp(像素)

> px转dp

- 参数 : 像素 {数字} 要转换的px(像素值)
- 返回 : {数字} 转换后的(dp)虚拟像素单位
- 版本 : 1.8.2


```javascript
//获取10像素的(dp)虚拟单位值
定义 dp = $界面.转dp(10);
```

---

# 视频

- 更新时间:2026-01-30 19:33:13

> 视频-video




### onComplete(callback)

> 视频播放完成回调
> 
> 回调参数含义：mp {MediaPlayer} 视频播放对象

- 参数 : callback {(mp)=>{}} 回调


### onPrepare(callback)

> 视频播放准备好回调
> 
> 回调参数含义：mp {MediaPlayer} 视频播放对象

- 参数 : callback {(mp)=>{}} 回调


### onError(callback)

> 设置视频播放错误的监听器
> 
> 回调参数含义：mp {MediaPlayer} 视频播放对象，what {int} 事件类型，extra {int} 额外信息

- 参数 : callback {(mp, what, extra)=>{return false;}} 回调


### onInfo(callback)

> 设置视频播放信息的监听器（如缓冲开始 / 结束）
> 
> 回调参数含义：mp {MediaPlayer} 视频播放对象，what {int} 事件类型，extra {int} 额外信息

- 参数 : callback {(mp, what, extra)=>{return false;}} 回调


### path(path)

> 设置视频的路径

- 参数 : path {string} 视频的路径


### uri(uri)

> 设置视频的URI

- 参数 : uri {string} 视频的 URI 可以是本地文件或网络视频地址


### start()

> 开始播放


### pause()

> 暂停播放


### stop()

> 停止并释放资源


### resume()

> 恢复之前暂停的视频播放


### suspend()

> 暂停并释放资源


### keepScreen(keep)

> 保持屏幕常亮

- 参数 : keep {boolean} 是否保持屏幕常亮


### seekTo(ms)

> 跳转到指定的时间点

- 参数 : ms {int} 毫秒


### isPlaying()

> 是否正在播放

- 返回 : {boolean} 是否正在播放


### getDur()

> 获取视频的总时长

- 返回 : {int} 视频的总时长（毫秒），返回 -1 表示时长未知


### getCur()

> 获取当前播放位置（毫秒）

- 返回 : {int} 当前播放位置（毫秒）


### canPause()

> 判断视频是否可以暂停

- 返回 : {boolean} 是否可以暂停


### canSeekBackward()

> 判断视频是否可以向后快退

- 返回 : {boolean} 是否可以向后快退


### canSeekForward()

> 判断视频是否可以向前快进

- 返回 : {boolean} 是否可以向前快进


### getBufferPercentage()

> 获取视频缓冲的百分比

- 返回 : {int} 视频缓冲的百分比

---

# $ - 桥梁对象

- 更新时间:2026-01-30 19:33:13

> WebView桥梁对象
> 作为WebView和脚本引擎之间的桥梁,在html中:$符号就是这个桥梁的对象名称,你可以直接通过$对象来调用这里提供的方法




### call(funcName)

> 调用注册函数

- 参数 : funcName {string} 函数名称
- 返回 : {string} 返回值


```javascript
//在js中:注册一个函数
let ui = $ui.layout("./mUi.xml");
let mWeb = ui.id("mWebView");
mWeb.addFunc("mFunc",()=>{
    //获得无障碍权限
    $permit.wza();
    return "";//返回值是一个字符串类型,如果在html中不需要返回值,则不用写这行代码
});
//在html中:调用这个函数
$.call("mFunc");
```


### log(log)

> 调用注册函数
> 
> 此函数只能打印一个普通的文本内容，请注意调用方式

- 参数 : log {string} 日志文本


```javascript
//在html中:
$.log("我是一个文本");
```


### toast(msg)

> 土司提示

- 参数 : msg {string} 信息


```javascript
//在html中:
$.toast("我是一个文本");
```


### alert(msg)

> 对话框提示

- 参数 : msg {string} 信息


```javascript
//在html中:
$.alert("信息");
```


### alert(title, msg)

> 对话框提示

- 参数 : title {string} 标题
- 参数 : msg {string} 信息


```javascript
//在html中:
$.alert("信息","你好啊!");
```


### getClip()

> 获得剪切板

- 返回 : {string} 文字


```javascript
//在html中:
let text = $.getClip();
```


### setClip(text)

> 设置剪切板

- 参数 : text {string} 文字


```javascript
//在html中:
$.setClip("我是来自html中的字符串");
```

---

# 网页

- 更新时间:2026-01-30 19:33:13

> 网页-webview
> 
> 你可以用vant,vue,layui,element-ui等框架编写html界面，在这个控件中加载这个界面，之后就是处理一些交互函数了




### onLoaded(onLoad)

> 设置加载完成回调

- 参数 : onLoad (()=>{}) 回调


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//设置加载完成回调
wv.onLoaded(()=>{
    //一般在控件加载完html之后注册一些交互函数,例如：
    wv.addFunc("getWza",()=>{
        $permit.wza();//获取无障碍权限
    });
    //之后就可以在html中使用:$.call("getWza");调用这个函数了
});
```


### clear()

> 清除网页缓存


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//清除网页缓存
wv.clear();
```


### loadUrl(url)

> 加载url

- 参数 : url url


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//加载url
wv.loadUrl("http://...");
```


### loadHtml(html)

> 加载html字符串

- 参数 : html html字符串


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//加载html字符串
wv.loadHtml(`
<html>
    //这里是html字符串
</html>
`);
```


### loadFile(path)

> 加载html文件

- 参数 : path html文件路径


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//加载html文件
wv.loadFile("./html/index.html");
```


### callJs(functionName, callBack)

> 调用js无参函数


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJs("mFunc",(returnValue)=>{
    //..
});
```


### callJs(functionName)

> 调用js无参函数


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数
wv.callJs("mFunc");
```


### callJsInt(functionName, param, callBack)

> 调用js的整数参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {int} 参数
- 参数 : callBack ((str)=>{}) 回调


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsInt("setFontSize",22,(returnValue)=>{
    //..
});
```


### callJsInt(functionName, param)

> 调用js的整数参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {int} 参数


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数
wv.callJsInt("setFontSize",22);
```


### callJsLong(functionName, param, callBack)

> 调用js的长整数参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {long} 参数
- 参数 : callBack ((str)=>{}) 回调


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsLong("setLength",546894564564849,(returnValue)=>{
    //..
});
```


### callJsLong(functionName, param)

> 调用js的长整数参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {long} 参数


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数
wv.callJsLong("setLength",546894564564849);
```


### callJsDouble(functionName, param, callBack)

> 调用js的浮点数参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {float} 参数
- 参数 : callBack ((str)=>{}) 回调


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsDouble("setVal",3.1415926,(returnValue)=>{
    //..
});
```


### callJsDouble(functionName, param)

> 调用js的浮点数参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {float} 参数


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsDouble("setVal",3.1415926);
```


### callJsFloat(functionName, param, callBack)

> 调用js的浮点数参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {float} 参数
- 参数 : callBack ((str)=>{}) 回调


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsFloat("setVal",3.1415926,(returnValue)=>{
    //..
});
```


### callJsFloat(functionName, param)

> 调用js的浮点数参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {float} 参数


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsFloat("setVal",3.1415926);
```


### callJsChar(functionName, param, callBack)

> 调用js的字符串参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {char} 参数
- 参数 : callBack ((str)=>{}) 回调


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsChar("setChar",'A',(returnValue)=>{
    //..
});
```


### callJsChar(functionName, param)

> 调用js的字符串参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {char} 参数


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsChar("setChar",'A');
```


### callJsBool(functionName, param, callBack)

> 调用js的布尔参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {boolean} 参数
- 参数 : callBack ((str)=>{}) 回调


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsBool("setEnable",true,(returnValue)=>{
    //..
});
```


### callJsBool(functionName, param)

> 调用js的布尔参数函数

- 参数 : functionName {String} js函数名
- 参数 : param {boolean} 参数


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数
wv.callJsBool("setEnable",true);
```


### callJsStr(functionName, param, callBack)

> 调用js的长文本参数函数
> 
> 在传入长文本之前，会把文本进行URL编码，所以在html使用的时候需要使用函数``解码才能得到原本的长文本内容。

- 参数 : functionName {String} js函数名
- 参数 : param {String} 长文本参数
- 参数 : callBack ((str)=>{}) 回调


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数,如果有返回值,那么就会通过returnValue回调获取
wv.callJsStr("setCode","一大堆文字",(returnValue)=>{
    //..
});
//在html中的代码:
function setCode(str){
    //html使用的时候需要使用函数`decodeURIComponent`解码才能得到原本的长文本内容。
    let code =  decodeURIComponent(str);
    $.alert("代码",code);
}
```


### callJsStr(functionName, param)

> 调用js的长文本参数函数
> 
> 在传入长文本之前，会把文本进行URL编码，所以在html使用的时候需要使用函数``解码才能得到原本的长文本内容。

- 参数 : functionName {String} js函数名
- 参数 : param {String} 长文本参数


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//调用js无参函数
//mFunc是html中定义的函数
wv.callJsStr("setCode","一大堆文字");
//在html中的代码:
function setCode(str){
    //html使用的时候需要使用函数`decodeURIComponent`解码才能得到原本的长文本内容。
    let code =  decodeURIComponent(str);
    $.alert("代码",code);
}
```


### addFunc(funcName, callback)

> 注册桥梁函数
> 
> 向桥梁对象$中注册(添加)自定义函数，之后就可以在html中通过$.call(函数名称);来调用啦

- 参数 : funcName {()=>{ return "数据"; }} 回调


```javascript
//解析布局,获得ui对象
let ui = $ui.layout("./mUi.xml");
//获取控件
let wv = ui.id("mWebView");
//设置加载完成回调
wv.onLoaded(()=>{
    //一般在控件加载完html之后注册一些交互函数,例如：
    wv.addFunc("getWza",()=>{
        $permit.wza();//获取无障碍权限
    });
    //之后就可以在html中使用:$.call("getWza");调用这个函数了
});
```

---
