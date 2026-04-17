# $ui 布局系统

# 应用条布局

- 更新时间:2026-01-30 19:33:12

> 应用条布局-appbar-layout
> 
> 是布局父类的(XLayout)的子类
> 
> 原生类型:{com.google.android.material.appbar.AppBarLayout}




## 一、常用属性


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {int} 颜色值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获得控件
定义 应用条布局 = 界面.找控件("我的应用条布局");
//设置背景颜色
应用条布局.设置背景颜色($颜色.红色);
```


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {string} 颜色值


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获得控件
定义 应用条布局 = 界面.找控件("我的应用条布局");
//设置背景颜色
应用条布局.设置背景颜色("#000000");
```

---

# UI框架

- 更新时间:2026-01-30 19:33:12



UI框架是基于谷歌[Material 3](https://m3.material.io/)进行拓展，封装了全部控件以及布局。 甚至封装了组件式的控件，可以帮助开发者快速完成界面开发。

与此同时，提供了大量界面模板，你可以在软件示例中找到，也可以在本文档中找到。


![](./img/ui-demo.png)

#### UI框架设计图

UI框架中最大的类是XView类，其余的所有视图都是XView的子类，因此XView类中的所有方法都可以被其子类调用。
其中XLayout是XView的子类，也是所有布局类型的父类，所以XLayout类的所有方法都可以被其子类调用。

例如1：XView类中有'click(点击监听)'方法，这个方法可以监听点击事件，因此所有的子组件都可以调用这个方法监听点击事件。

例如2：XLayout类中有'addView(添加视图)'方法，这个方法可以使得布局动态添加一个子视图，'linear(线性布局)'是XLayout的子类，因此可以调用'addView'方法添加子视图。


![](./img/ui-fragment.png)

---

# 绝对布局

- 更新时间:2026-01-30 19:33:12

> 绝对布局-absolute
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{android.widget.AbsoluteLayout}




## 子控件属性表

被绝对布局包裹的子控件可以使用如下属性：

| 中文名   | 英文名    | 描述                                                         |
|----------|-----------|--------------------------------------------------------------|
| 横轴     | x         | 设置视图在AbsoluteLayout中的横轴（X轴）位置                   |
| 纵轴     | y         | 设置视图在AbsoluteLayout中的纵轴（Y轴）位置                   |
| 解决方向 | resolveDir | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽       | w         | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高       | h         | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |

---

# 卡片布局

- 更新时间:2026-01-30 19:33:12

> 卡片布局-card
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法,但需要注意卡片布局本身是帧布局的子类，因此建议在卡片布局中加入线性布局来使用。
> 
> 原生类型:{com.google.android.material.card.MaterialCardView}




## 一、常用属性


## 二、子控件属性表

被卡片布局包裹的子控件可以使用如下属性：

| 中文名   | 英文名        | 描述                                                         |
|----------|---------------|--------------------------------------------------------------|
| 布局方向 | dir           | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向 | resolveDir    | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽       | w             | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高       | h             | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 布局重力 | layout_gravity | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距   | margin        | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距 | margin_left   | 单独设置视图的左外边距，单位为dp                             |
| 上外边距 | margin_top    | 单独设置视图的上外边距，单位为dp                             |
| 右外边距 | margin_right  | 单独设置视图的右外边距，单位为dp                             |
| 下外边距 | margin_bottom | 单独设置视图的下外边距，单位为dp                             |


## 三、常用函数


### 设置可点击(可点击)

> 设置可点击

- 参数 : 可点击 {布尔值} 是否可点击
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 卡片 = 界面.找控件("我的卡片");
//设置可点击
卡片.设置可点击(是);
```


### 设置涟漪色(颜色)

> 设置涟漪色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 卡片 = 界面.找控件("我的卡片");
//设置涟漪色
卡片.设置涟漪色("#FF0000");
```


### 设置涟漪色(颜色)

> 设置涟漪色

- 参数 : 颜色 {数字} 颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 卡片 = 界面.找控件("我的卡片");
//设置涟漪色
卡片.设置涟漪色($颜色.红色);
```


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {数字} 文本颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 卡片 = 界面.找控件("我的卡片");
//设置背景颜色
卡片.设置背景颜色($颜色.红色);
```


### 设置背景颜色(颜色)

> 设置背景颜色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 卡片 = 界面.找控件("我的卡片");
//设置背景颜色
卡片.设置背景颜色("#1E1F22");
```


### 设置填充色(颜色)

> 设置填充色

- 参数 : 颜色 {数字} 颜色值
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 卡片 = 界面.找控件("我的卡片");
//设置填充色
卡片.设置填充色($颜色.红色);
```


### 设置填充色(颜色)

> 设置填充色

- 参数 : 颜色 {字符串} 颜色字符串
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 卡片 = 界面.找控件("我的卡片");
//设置填充色
卡片.设置填充色("#FF0000");
```


### 设置弧度(弧度)

> 设置弧度

- 参数 : 弧度 {数字} 弧度(单位:dp)
- 版本 : 1.8.2


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取控件
定义 卡片 = 界面.找控件("我的卡片");
//设置弧度
卡片.设置弧度(15);
```

---

# 约束布局

- 更新时间:2026-01-30 19:33:12

> 约束布局-const
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{androidx.constraintlayout.widget.ConstraintLayout}




## 子控件属性表

被约束布局包裹的子控件可以使用如下属性：

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 垂直偏移   | verticalBias    | 设置视图在垂直方向的偏移值，若与水平偏移均设为0.5，可实现居中对齐 |
| 水平偏移   | horizontalBias  | 设置视图在水平方向的偏移值，若与垂直偏移均设为0.5，可实现居中对齐 |
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |

---

# 锚点布局

- 更新时间:2026-01-30 19:33:12

> 锚点布局-coord
> 
> 是布局父类(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{androidx.coordinatorlayout.widget.CoordinatorLayout}




锚点布局，能够实现的效果让人意想不到，你可以理解为：船舶停靠在某个驿站上，一般用anchor属性指定驿站的名字，用anchorLayout指定要前往的驿站。


![](../img/coord_toolbar_fab.png)


```html
<ui>
    <statusbar />
    <!--
    anchor属性是所有控件都有的属性，但是使用anchorLayout属性必须要被coord锚点布局包才可以
    -->
    <coord h="max" w="max">
        <!--
        anchor="linear" 指的是:给线性布局(linear)取一个驿站名称为'linear'
        -->
        <linear anchor="linear" gravity="center" h="max" margin_bottom="75" w="max">
            <text text="Hello World!" />
        </linear>
        <!--
        anchorLayout="linear" 指的是:锚定到名称为'linear'的布局上
        -->
        <toolbar anchor="toolbar" anchorGravity="center|bottom" anchorLayout="linear"
            fabAnim="slide" fabGravity="center" fabMode="out" fabRadius="25" h="75"
            layout_gravity="bottom" w="max">
            <menu icon="ic_search" text="搜搜" />
            <menu icon="ic_set" text="设置" />
            <menu icon="ic_menu" text="菜单" />
        </toolbar>
        <!--
        这里我让(fab)悬浮按钮锚定到(toolbar)工作条的布局上，同时在(toolbar)工作条的布局上设置悬浮按钮的样式，
        然而(toolbar)工作条能够专门和(fab)悬浮按一起联动，实现凹陷的效果。
        -->
        <fab anchorLayout="toolbar" icon="ic_add" iconTint="txt" radius="27" />
    </coord>
</ui>
```


## 一、常用属性


## 二、子控件属性表

被锚点布局约束的子控件可以使用如下属性：

| 中文名       | 英文名          | 描述                                                         |
|--------------|-----------------|--------------------------------------------------------------|
| 布局方向     | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向     | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 行为         | behavior        | 指定视图与其他视图或父布局的交互方式，可选值为“appbar”（应用条，对应AppBarLayout.ScrollingViewBehavior）或“fab”（悬浮按钮，对应ScrollAwareFabBehavior） |
| 参考线       | keyline         | 在CoordinatorLayout中定义参考线，帮助子视图根据参考线定位，单位为dp |
| 锚点视图       | anchorLayout        | 设置锚定的视图，用于让当前视图相对锚定视图进行布局（需为每个视图设置anchor以引用） |
| 锚点重力     | anchorGravity   | 设置当前视图相对于锚点视图的重力方向，通过GravityAdd获取对应的重力值 |
| 避让插入边   | dodgeInsetEdges | 指定视图在遇到系统窗口插入边（如状态栏、导航栏等）时的避让行为，通过GravityAdd获取对应值 |
| 插入边       | insetEdge       | 指定视图哪一侧视为系统窗口插入边的边界，当系统窗口覆盖布局时，视图会调整位置或大小为系统窗口留出空间，通过GravityAdd获取对应值 |
| 宽           | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高           | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 布局重力     | layout_gravity  | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距       | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距     | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距     | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距     | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距     | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |

---

# 抽屉布局

- 更新时间:2026-01-30 19:33:12

> 抽屉布局-drawer
> 
> 是布局父类{XLayout}的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{androidx.drawerlayout.widget.DrawerLayout}




## 子控件属性表

被抽屉布局包裹的子控件可以使用如下属性：

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 布局重力   | layout_gravity  | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |

---

# 流式布局

- 更新时间:2026-01-30 19:33:12

> 流式布局-flow
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{com.google.android.material.internal.FlowLayout}




## 子控件属性表

被流式布局包含的子控件可以使用如下属性：

| 中文名   | 英文名    | 描述                                                         |
|----------|-----------|--------------------------------------------------------------|
| 解决方向 | resolveDir | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽       | w         | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高       | h         | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |

---

# 刷新布局

- 更新时间:2026-01-30 19:33:12

> 刷新布局-flush
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{androidx.swiperefreshlayout.widget.SwipeRefreshLayout}




## 子控件属性表

被下拉刷新布局包含的子控件可以使用如下属性：

| 中文名   | 英文名    | 描述                                                         |
|----------|-----------|--------------------------------------------------------------|
| 解决方向 | resolveDir | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽       | w         | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高       | h         | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |


### 监听刷新(runnable)

> 设置下拉刷新监听

- 参数 : runnable {()=>{}} 刷新时执行的任务


```javascript
//解析布局,获得ui对象
定义 我的界面 = $界面.解析界面("./资源/主界面.xml");
//获取控件
定义 下拉刷新控件 = 我的界面.找控件("我的下拉刷新控件");
//监听下拉刷新
下拉刷新控件.监听刷新(()=>{
    //处理一些事情...
});
```

---

# 帧布局

- 更新时间:2026-01-30 19:33:12

> 帧布局-frame
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{android.widget.FrameLayout}




## 子控件属性表

被帧布局包裹的子控件可以使用如下属性：

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 布局重力   | layout_gravity  | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |

---

# 网格布局

- 更新时间:2026-01-30 19:33:12

> 网格布局-grid
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{android.widget.GridLayout}




## 子控件属性表

被网格布局包裹的子控件可以使用如下属性：

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |

---

# 包含布局

- 更新时间:2026-01-30 19:33:12

> 包含布局-include
> 
> 包含布局主要用于引入其他布局文件，避免单个布局文件过大导致代码臃肿。
> 包含布局的本质就是一个线性布局，所以在使用的时候遵循线性布局的规则即可。
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{android.widget.LinearLayout}

---

# 线性布局

- 更新时间:2026-01-30 19:33:12

> 线性布局-linear
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{android.widget.LinearLayout}




## 子控件属性表

被线性布局包裹的子控件可以使用如下属性：

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 权重       | weight          | 设置视图的权重，通过浮点值指定，用于在LinearLayout中分配剩余空间 |
| 布局重力   | layout_gravity  | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |

---

# 滑动布局

- 更新时间:2026-01-30 19:33:12

> 滑动布局-nested
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{androidx.core.widget.NestedScrollView}




## 子控件属性表

被滑动布局包裹的子控件可以使用如下属性：

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 布局重力   | layout_gravity  | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |


### 监听滚动(callback)

> 监听滚动

- 参数 : callback 滚动回调 


```javascript
定义 界面 = $界面.解析布局("./资源/主界面.xml");//解析界面
界面.显示();//显示界面
//找到滑动控件
定义 滑动控件 = 界面.找控件("我的滑动布局");
//监听混动事件
滑动控件.监听滚动((x,y,视图)=>{
    //处理事情
});
```

---

# 相对布局

- 更新时间:2026-01-30 19:33:12

> 相对布局-relative
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{android.widget.RelativeLayout}




## 子控件属性表

被相对布局包裹的子控件可以使用如下属性：

| 中文名         | 英文名          | 描述                                                         |
|----------------|-----------------|--------------------------------------------------------------|
| 与父布局对齐   | alignWithParent | 布尔值属性，用于指定当对应的参考视图不存在时，当前视图是否与父布局对齐 |
| 布局方向       | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向       | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽             | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高             | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 外边距         | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距       | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距       | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距       | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距       | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |

---

# 滚动布局

- 更新时间:2026-01-30 19:33:12

> 滚动布局-scroll
> 
> 是布局父类的(XLayout)的子类,因此可以使用XLayout的所有方法
> 
> 原生类型:{android.widget.ScrollView}




## 子控件属性表

被滚动布局包裹的子控件可以使用如下属性：

| 中文名     | 英文名          | 描述                                                         |
|------------|-----------------|--------------------------------------------------------------|
| 布局方向   | dir             | 设置子视图的排列方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 解决方向   | resolveDir      | 确定视图应遵循的实际布局方向，可选值为“rtl”（右到左）或“ltr”（左到右） |
| 宽         | w               | 设置视图的宽度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 高         | h               | 设置视图的高度，可选值为“auto”（自动，即WRAP_CONTENT）、“max”（最大，即MATCH_PARENT）或具体整数（单位为dp） |
| 布局重力   | layout_gravity  | 设置视图的布局重力，通过GravityAdd获取对应的重力值             |
| 外边距     | margin          | 设置视图的外边距，可传入单个整数（四边外边距相同）或四个整数（分别对应左、上、右、下外边距），单位为dp |
| 左外边距   | margin_left     | 单独设置视图的左外边距，单位为dp                             |
| 上外边距   | margin_top      | 单独设置视图的上外边距，单位为dp                             |
| 右外边距   | margin_right    | 单独设置视图的右外边距，单位为dp                             |
| 下外边距   | margin_bottom   | 单独设置视图的下外边距，单位为dp                             |


### 监听滚动(callback)

> 监听滚动

- 参数 : callback 滚动回调 


```javascript
定义 界面 = $界面.解析布局("./资源/主界面.xml");//解析界面
界面.显示();//显示界面
//找到滑动控件
定义 滑动控件 = 界面.找控件("我的滑动布局");
//监听混动事件
滑动控件.监听滚动((x,y,视图)=>{
    //处理事情
});
```

---

# 布局父类

- 更新时间:2026-01-30 19:33:13

> 布局父类-XLayout
> 
> 布局父类{XLayout}是属于{XView}的子控件，因此{XView}中的所有方法，布局父类都可以调用。
> 
> 所有布局控件都继承{XLayout}类，一因此可以调用{XLayout}中的方法。
> 
> 为了清晰的了解本软件的UI界面框架结构，我给你画个图:XView->XLayout->XScroll、XLinear、XCard等等
> 
> 这是什么意思呢？例如:XScroll是<scroll>标签、XLinear是<linear>标签、XCard是<card>标签等等我就不一一例举了，这些标签都是XLayout布局类的子类，也就是说这些对象都可以调用XLayout中的方法，而XLayout又是XView的子类，因此也可以调用XView中的所有方法。




### 添加视图(xView)

> 添加子视图

- 参数 : xView {XView} 控件


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取布局控件
定义 布局 = 界面.找控件("我的布局");
//创建一个新的文本控件
定义 文本控件 = $界面.创建("文本").设置文本("新添加的文本");
//添加到布局中
布局.添加视图(文本控件);
```


### 添加视图(view)

> 添加子视图

- 参数 : view {View} 控件


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取布局控件
定义 布局 = 界面.找控件("我的布局");
//创建一个新的原生文本控件
定义 原生文本 = new TextView(活动);
原生文本. setText("原生文本");
//添加到布局中
布局.添加视图(原生文本);
```


### 移除视图(xView)

> 移除子视图

- 参数 : xView {XView} 要移除的控件


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取布局控件
定义 布局 = 界面.找控件("我的布局");
//获取要移除的控件
定义 子控件 = 界面.找控件("子控件");
//从布局中移除
布局.移除视图(子控件);
```


### 移除视图(view)

> 移除子视图

- 参数 : view {View} 要移除的原生控件


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取布局控件
定义 布局 = 界面.找控件("我的布局");
//获取要移除的原生控件
定义 原生控件 = 找到视图(R.id.原生控件);
//从布局中移除
布局.移除视图(原生控件);
```


### 移除视图(index)

> 根据索引移除子视图

- 参数 : index {Integer} 子视图索引


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取布局控件
定义 布局 = 界面.找控件("我的布局");
//移除第一个子视图
布局.移除视图(0);
```


### 移除视图(from, to)

> 批量移除子视图

- 参数 : from {Integer} 起始索引
- 参数 : to {Integer} 结束索引


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取布局控件
定义 布局 = 界面.找控件("我的布局");
//移除从索引1开始的3个子视图
布局.移除视图(1, 3);
```


### 移除所有视图()

> 移除所有子视图


```javascript
//解析布局,获得界面对象
定义 界面 = $界面.解析布局("./资源/主界面.xml");
//获取布局控件
定义 布局 = 界面.找控件("我的布局");
//清空所有子视图
布局.移除所有视图();
```

---

# color-颜色属性对照表

- 更新时间:2026-01-30 19:33:12




### 1. 属性颜色

| 属性值                               | 颜色                                                           |
|-----------------------------------|--------------------------------------------------------------|
| colorPrimary、主题                   | com.google.android.material.R.attr.colorPrimary              |
| colorSurface、背景                   | com.google.android.material.R.attr.colorSurface              |
| colorOnSurface、文本                 | com.google.android.material.R.attr.colorOnSurface            |
| colorOnPrimary、主题主反色              | com.google.android.material.R.attr.colorOnPrimary            |
| colorPrimaryContainer、主题主容器颜色     | com.google.android.material.R.attr.colorPrimaryContainer     |
| colorOnPrimaryContainer、主题主容器反色   | com.google.android.material.R.attr.colorOnPrimaryContainer   |
| colorSecondary、主题次颜色              | com.google.android.material.R.attr.colorSecondary            |
| colorOnSecondary、主题次反色            | com.google.android.material.R.attr.colorOnSecondary          |
| colorSecondaryContainer、主题次容器颜色   | com.google.android.material.R.attr.colorSecondaryContainer   |
| colorOnSecondaryContainer、主题次容器反色 | com.google.android.material.R.attr.colorOnSecondaryContainer |
| colorTertiary                     | com.google.android.material.R.attr.colorTertiary             |
| colorOnTertiary                   | com.google.android.material.R.attr.colorOnTertiary           |
| colorTertiaryContainer            | com.google.android.material.R.attr.colorTertiaryContainer    |
| colorOnTertiaryContainer          | com.google.android.material.R.attr.colorOnTertiaryContainer  |
| colorError、主题错误颜色                 | com.google.android.material.R.attr.colorError                |
| colorOnError、主题错误反色               | com.google.android.material.R.attr.colorOnError              |
| colorErrorContainer、主题错误容器颜色      | com.google.android.material.R.attr.colorErrorContainer       |
| colorOnErrorContainer、主题错误容器反色    | com.google.android.material.R.attr.colorOnErrorContainer     |
| colorOnBackground、主题背景反色          | com.google.android.material.R.attr.colorOnBackground         |
| colorSurfaceVariant、主题中性容器颜色      | com.google.android.material.R.attr.colorSurfaceVariant       |
| colorOnSurfaceVariant、主题中性容器反色    | com.google.android.material.R.attr.colorOnSurfaceVariant     |
| colorOutline、主题中性轮廓颜色             | com.google.android.material.R.attr.colorOutline              |
| colorOutlineVariant、主题中性轮廓反色      | com.google.android.material.R.attr.colorOutlineVariant       |
| colorPrimaryInverse、主题主状态反色       | com.google.android.material.R.attr.colorPrimaryInverse       |

### 2. 名称颜色

| 属性值              | 颜色        |
|------------------|-----------|
| white、白色         | #FFFFFF   |
| black、黑色         | #000000   |
| null、透明、none、空、无 | #00000000 |
| green、绿色         | #57965C   |
| red、红色           | #C94F4F   |
| blue、蓝色          | #3574F0   |
| yellow、黄色        | #C29E4A   |

:::tip 注意
由于脚本支持中文和英文编程，所以颜色属性值可以采用中文，也可以采用英文。

例如：color="red"

等同：颜色="红色"
:::

---

# gravity-重力属性对照表

- 更新时间:2026-01-30 19:33:12



#### 使用方法


```html
<ui>
    <statusbar/>
    <!-- 这里的 gravity 重力值，可以决定子组件(按钮)在布局中的位置 center 表示让按钮居中 -->
    <linear w="max" h="max" gravity="center">
        <button text="按钮"/>
    </linear>
</ui>
```


#### Gravity属性值对照表

| 属性值                                        | 对应的Gravity值                     |
|--------------------------------------------|---------------------------------|
| fill、填充                                    | Gravity.FILL                    |
| fill_h、fill_horizontal、水平填充、横向填充           | Gravity.FILL_HORIZONTAL         |
| fill_v、fill_vertical、垂直填充、竖向填充             | Gravity.FILL_VERTICAL           |
| start、开头、开始、头部                             | Gravity.START                   |
| end、末尾、结束、尾部                               | Gravity.END                     |
| left、左、左边                                  | Gravity.LEFT                    |
| right、右、右边                                 | Gravity.RIGHT                   |
| top、上、上边                                   | Gravity.TOP                     |
| bottom、下、下边、下面                             | Gravity.BOTTOM                  |
| center、中、中心、中间、居中                          | Gravity.CENTER                  |
| center_h、center_horizontal、水平居中、横向居中       | Gravity.CENTER_HORIZONTAL       |
| center_v、center_vertical、垂直居中、竖向居中         | Gravity.CENTER_VERTICAL         |
| display_h、display_horizontal、水平显示裁剪、横向显示裁剪 | Gravity.DISPLAY_CLIP_HORIZONTAL |
| display_v、display_vertical、垂直显示裁剪、竖向显示裁剪   | Gravity.DISPLAY_CLIP_VERTICAL   |
| clip_h、clip_horizontal、水平裁剪、横向裁剪           | Gravity.CLIP_HORIZONTAL         |
| clip_v、clip_vertical、垂直裁剪、竖向裁剪             | Gravity.CLIP_VERTICAL           |

:::tip 注意
由于脚本支持中文和英文编程，所以重力属性值可以采用中文，也可以采用英文。

例如：gravity="center"

等同：重力="中"
:::

---

# 补充文档

- 更新时间:2026-01-30 19:33:12



## [1.gravity-重力 属性对照表](./other/gravity)

## [2.color-颜色 属性对照表](./other/color)

---

# Sheet - 底部弹窗

- 更新时间:2026-01-30 19:33:12

> 底部弹窗




### 解析布局(xml内容或路径)

> 解析布局

- 参数 : xml内容或路径 {string} xml内容或者xml路径
- 返回 : {底部弹窗} 返回自己
- 版本 : 1.5.5


### 获得视图()

> 获取解析后的最大布局

- 返回 : {View} 返回最大布局
- 版本 : 1.5.8


### 找控件(标识)

> 通过标识获取控件

- 参数 : 标识 {string} 控件标识
- 返回 : {XView} 返回控件
- 版本 : 1.5.8


### 显示()

> 显示弹窗

- 版本 : 1.5.8


### 关闭()

> 关闭弹窗

- 版本 : 1.5.8

---

# UI - 界面对象

- 更新时间:2026-01-30 19:33:14

> 界面对象




### 获得视图()

> 获取解析后的最大布局

- 返回 : {View} 返回最大布局
- 版本 : 1.5.8


```javascript
//解析布局
定义 界面 = $界面.解析布局("主界面.xml");
//获取最大视图
定义 最大视图 = 界面.获得视图();
```


### 找控件(标识)

> 通过标识找到组件

- 参数 : 标识 {字符串} 组件标识 
- 返回 : {XView} 控件


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
//获取组件
定义 按钮 = 界面.找控件("按钮");
```


### 界面线程(回调函数)

> 在ui线程中执行

- 参数 : 回调函数 {()=>{}} ui线程回调函数


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
//在ui线程中执行
界面.界面线程(()=>{
    //在ui线程中执行的代码
});
```


### 土司(文本)

> 悬浮土司
> 
> 悬浮土司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : 文本 {字符串} 文本
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
//悬浮土司
界面.土司("文本");
```


### 土司(文本, 重力)

> 悬浮土司
> 
> 悬浮土司是基于悬浮窗来实现的，因此在显示的时候会处于界面顶层。

- 参数 : 文本 {字符串} 文本
- 参数 : 重力 {字符串} 重力
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
//悬浮土司
界面.土司("文本","中间");
```


### 显示()

> 显示界面

- 返回 : {UI} 界面
- 版本 : 1.12


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
//显示界面
界面.显示();
```


### 结束()

> 结束界面


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
//显示界面
界面.显示();
//找一个按钮控件来关闭界面
界面.找控件("关闭按钮").点击事件(函数(){
    //关闭界面
    界面.结束();
});
```


### 获得活动对象()

> 等待获得activity对象
> 
> 注意:如果没有解析界面,那么就直接返回null
> 如果没有显示界面,也会直接返回null
> 如果解析成功并且成功显示,那么就会进入循环中,不断的等待判断activity是否获取成功,如果获取成功,则直接返回activity

- 返回 : {AppCompatActivity} activity
- 版本 : 1.1.2


```javascript
//解析界面
定义 界面 = $界面.解析布局("主界面.xml");
//显示界面
界面.显示();
//显示完界面之后即可等待获取到activity对象
定义 活动对象 = 界面.获得活动对象();
```


### 当活动开始(回调)

> 界面初始时执行

- 参数 : 回调 {(activity)=>{}} 生命周期回调
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动开始((activity)=>{
    //界面初始时执行
});
```


### 当活动恢复(回调)

> 重返界面时执行

- 参数 : 回调 {(activity)=>{}} 生命周期回调
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动恢复((activity)=>{
    //重返界面时执行
});
```


### 当活动暂停(回调)

> 界面暂停时执行

- 参数 : 回调 {(activity)=>{}} 生命周期回调
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动暂停((activity)=>{
    //界面暂停时执行
});
```


### 当活动停止(回调)

> 界面停止时执行

- 参数 : 回调 {(activity)=>{}} 生命周期回调
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动停止((activity)=>{
    //界面停止时执行
});
```


### 当活动销毁(回调)

> 界面销毁时执行

- 参数 : 回调 {(activity)=>{}} 生命周期回调
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动销毁((activity)=>{
    //界面销毁时执行(一般用来释放资源)
});
```


### 当活动重启(回调)

> 重新刷新界面时执行

- 参数 : 回调 {(activity)=>{}} 生命周期回调
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动重启((activity)=>{
    //重新刷新界面时执行
});
```


### 当活动结果(回调)

> 活动结果事件

- 参数 : 回调 {(requestCode,resultCode,intent,activity)=>{}} 活动结果事件
- 版本 : 1.4.9


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当活动结果((requestCode,resultCode,intent,activity)=>{
    //活动结果事件(一般用来申请权限时作为结果回调)
    //回调参数类型:
    //int requestCode
    //int resultCode
    //Intent intent
    //AppCompatActivity activity
});
```


### 当上下文菜单创建(回调)

> 上下文菜单创建事件

- 参数 : 回调 {(menu,view,menuInfo,activity)=>{}} 上下文菜单创建事件
- 版本 : 1.4.9


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当上下文菜单创建((menu,view,menuInfo,activity)=>{
    //上下文菜单创建事件
    //回调函数参数类：
    //ContextMenu menu (其API涉及安卓API，请自行参考安卓文档)
    //View view
    //ContextMenu.ContextMenuInfo menuInfo (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### 当选项菜单创建(回调)

> 选项菜单创建事件

- 参数 : 回调 {(menu,activity)=>{}} 选项菜单创建事件
- 版本 : 1.4.9


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当选项菜单创建((menu,activity)=>{
    //选项菜单创建事件
    //回调函数参数类：
    //Menu menu (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### 当选项菜单面板创建(回调)

> 选项菜单面板创建事件

- 参数 : 回调 {(featureId,menu,activity)=>{}} 选项菜单面板创建事件
- 版本 : 1.4.9


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当选项菜单面板创建((featureId,menu,activity)=>{
    //选项菜单创建事件
    //回调函数参数类：
    //int featureId
    //Menu menu (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### 当选项菜单选中(回调)

> 选项菜单点击事件

- 参数 : 回调 {(item,activity)=>{}} 选项菜单点击事件
- 版本 : 1.4.9


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当选项菜单选中((item,activity)=>{
    //选项菜单创建事件
    //回调函数参数类：
    //MenuItem item (其API涉及安卓API，请自行参考安卓文档)
    //AppCompatActivity activity
});
```


### 当按键按下(回调)

> 按键按下事件

- 参数 : 回调 {(keyCode,event,activity)=>{return false;}}  按键抬起事件
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当按键按下((keyCode,event,activity)=>{
    //当按键按下回调
    //回调参数类型:
    //int keyCode
    //KeyEvent event (其API涉及安卓API，请自行参考安卓文档)
});
```


### 当按键抬起(回调)

> 按键抬起事件

- 参数 : 回调 {(keyCode,event,activity)=>{return false;}}  按键抬起事件
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当按键抬起((keyCode,event,activity)=>{
    //按键抬起回调
    //回调参数类型:
    //int keyCode
    //KeyEvent event (其API涉及安卓API，请自行参考安卓文档)
});
```


### 当按键长按(回调)

> 长按事件

- 参数 : 回调 {(keyCode,event,activity)=>{return false;}}  长按事件
- 版本 : 1.1.2


```javascript
定义 界面 = $界面.解析布局("主界面.xml");
界面.显示();
//周期函数
界面.当按键长按((keyCode,event,activity)=>{
    //按键长按回调
    //回调参数类型:
    //int keyCode
    //KeyEvent event (其API涉及安卓API，请自行参考安卓文档)
});
```


### 设置方向(方向)

> 设置界面显示方向
> 
> 可选值：h(横向)、v(竖向)、auto(自动)、null(默认)

- 参数 : 方向 {字符串} 界面显示方向
- 版本 : 1.8.7


```javascript
//首先获取ui对象
定义 界面 = $界面.解析布局("主界面.xml");
//设置界面显示方向
界面.设置方向("横向");
//当界面显示的时候就会转为横屏
界面.显示();
//参数说明：（以下效果也会因使用户手机系统设置而改变）
//h、横向：进入界面后界面强制横屏
//v、竖向：进入界面后界面强制竖屏
//auto、自动：进入界面后界面随用户手机感应自动切换横竖屏
//null、默认：无任何效果
```

---
