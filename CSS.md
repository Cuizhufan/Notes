CSS

# 行内元素和行内块元素

- 行内元素 inline
  - 不能设置宽高，不能自动换行，同在一行
  - span、input、img、textarea、label、select
- 块级元素block
  - 可以设置宽高，会独占一行
  - p、h1/h2/h3/h4/h5、div、ul、li、table
- inline-block
  - 可以设置宽高，会自动换行

# px,em,rem,vw,vh,rpx等单位的特性

- px

  - 像素

- em

  - 参考物是父元素的font-size，1em=1倍父元素font-size的值

- rem

  - 相对根元素字体大小

- vw

  - 100vw是屏幕总宽度 css新增

- vh

  - 100vh是屏幕总高度

- rpx

  - 750rpx是总宽度，微信小程序解决自适应屏幕尺寸的单位

- vm

  参照窗口的宽度和高度较小的



# doctype标签和meta标签

- doctype

  - 告诉浏览器以什么样的文档规范解析文档，第一种按照浏览器自己的方式解析。叫怪异模式；第二中采用**w3c的标准**解析页面 这叫标准模式。
    如果不写这个声明，各个浏览器就会以自己的方式解析，采用怪异模式，在不同浏览器下就有不同的表现，叫了这个声明，就按照标准模式解析，所有浏览器保持一致。
  - 标准模式和兼容模式
    - 标准模式 ->正常，排版和js运作模式都是以**最高标准**运行
    - 兼容模式->非正常

- meta

  标签是HTML头部的一个辅助性标签，提供了一些元信息（例如针对搜索引擎的页面描述和关键字、定义页面使用的语言等）



# 选择器权重计算

！import>权重计算>权重相同位置靠后>继承样式

1 千分位：声明在行内样式style 得1分

2百分位：包含有id选择器选择器（#）得1分

3十分位：包含有类选择器(.)，属性选择器([属性名])，或者伪类选择器（:hover;  :link;  :focus;  ） 得1分

4 个位：包含标签选择器（p,span）伪元素选择器(:first-letter;first-line;) 得1分

注意：有一些标签自身含有默认得样式 例如 <a>默认颜色是蓝色



```css
div.box h1#title  //权重：0112
#article h1.title  //权重 0111
```

# 伪类和伪元素

伪类：通过选择器找到那些不存在于DOM树中的信息以及不能被常规CSS选择器获取到的信息。如，:active，:hover，:link，:focus等。

伪元素：在DOM树中创建的**虚拟容器**，容器中不包含DOM元素，但是可以包含内容，另外还可以定制样式。如：::first-letter，::first-line，::after，:before等。

区别：伪类弥补了CSS选择器的不足，更方便地获取信息；

而伪元素本质上是创建了一个虚拟容器（元素），我们可以在其中添加内容或样式。伪元素用双冒号::表示；而一个选择器只能同时使用一个伪元素

# flex布局

弹性盒子布局，设置为display:flex 得元素称为容器。

容器属性：

- flex-direction  改变主轴方向
- flex-wrap 是否自动换行
- flex-flow  flex得direction和wrap得结合
- justify-content：主轴上项目的对齐方式
  - `flex-start`（默认值）：左对齐
  - `flex-end`：右对齐
  - `center`： 居中
  - `space-between`：两端对齐，项目之间的间隔都相等。
  - `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
- align-items 交叉轴的对齐方式
  - `flex-start`：交叉轴的起点对齐。
  - `flex-end`：交叉轴的终点对齐。
  - `center`：交叉轴的中点对齐。
  - `baseline`: 项目的第一行文字的基线对齐。
  - `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度
- w3align-content

项目属性：

- `order` 排列顺序

- `flex-grow`放大，默认是0，不变

- `flex-shrink`缩小 默认是0，不变

- `flex-basis` 占主轴的空间，默认auto是项目自身的大小

- `flex`:flex的grow shrink basis的结合，默认是 0 1 auto 

  auto(1 1 auto);none(0 0 auto)

- `align-self` 允许单个项目和其他的对其方式及不同

  

  flex：1表示：1 1 0%

  flex：1===flex:1 1 0  ;//flex：basis为0，会等分剩余空间

  flex：1！==flex:1 1 auto // flex：auto会根据项目自身的大小来计算剩余空间

# 两栏布局

指的是一栏为侧边栏 固定宽度，另一栏是内容，自适应宽度。

实现方法：

1使用flex布局（主流）

父容器设置display:flex，定宽元素设置flex-basis或者width，自适应元素设置flex:1或者flex-grow:1

```css
  .box {
            height: 100px;
            display: flex;
        }
        .left {
            height: 100px;
            width: 300px;
        }
        .right {
            height: 100px;
            flex: 1;    /* 比例设置为1，撑满剩余空间 == flex: 1 1 0%  */
        }

```

2浮动实现

float：left +margin-left：-width

float：left+overflow：hiden 构建bfc

```css
 <style type="text/css">
      .box {
          height: 100px;
       }
      .left {
          height: 100px;
          width: 300px;
          float: left;
        }
       .right {
          height: 100px;
          margin-left: 300px; /* 方法1：左浮动，右margin*/
          overflow: hidden; /* 方法2：左浮动，右hidden(右边的盒子就变成了一个绝缘的盒子，BFC中治理高度塌陷)*/
        }
    </style>
```

# CSS实现

![](C:\Users\Cuizhufan\Desktop\学习\HTML-CSS-JS\CSS_Interview\css图形.png)

```css
1、一根0.5px的线 scaleY(0.5)
.line{
            margin-top: 100px;
            background-color: black;
            height: 1px;
            transform: scaleY(0.5);
        }
2、实现三角形
使用border边框实现
.sanjiaoxing{
            margin: auto;
            width: 0;
            height: 0;
            border-top: 200px solid red;
            border-left: 100px solid transparent;
            border-right: 100px solid transparent;
           
        }
3、实现题型，三角形基础上加上 width或者height
.tixing{
    width: 50px;
    height: 0px;
    margin: auto;
    border-bottom: 50px solid red;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
}
4、圆形，设置半径
.yuan{
    width: 50px;
    height: 50px;
    margin: auto;
    background-color: red;
    border-radius: 50%;
}
5、实现扇形，三角形基础上设置半径
.shanxing{
    width: 0px;
    height: 0px;
    margin: auto;
    border-top: 200px solid red;
    border-left: 100px solid transparent;
    border-right: 100px solid transparent;
    border-radius: 50%;
}
```

# BFC

Block format context ,块级格式化上下文;

**一块独立渲染区域，内部元素的渲染不会影响边界以外的元素**

形成BFC的常见条件：

1设置浮动：float不是none 比如说：我们对元素设置了float,这样的话元素就形成了BFC
2设置定位：position是absolute或fixed 这时候元素也形成了BFC
3设置overflow ：overflow不是visible 比如说overflow等于hidden/ scroll/inherit/auto……
4display是flex inline-block等

- BFC特性
  - 同一个BFC下margin会重叠
  - 计算BFC高度时会算上浮动元素，解决高度塌陷
  - BFC不会影响到外部元素，外边距重叠可以分别设置bfc
  - BFC内部元素是垂直排列的
  - BFC区域不会与float元素重叠，组织被浮动元素覆盖

# 清除浮动

浮动之后父元素高度塌陷，要清楚浮动

1、利用bfc原理，设置父元素overflow属性，不为visible，构建一个bfc

```css
.fahter{
        width: 400px;
        border: 1px solid deeppink;
        overflow: hidden;
    }
```

2、额外标签 clear:both

在代码中在放一个空的div标签，然后给这个标签设置clear:both来清除浮动对页面的影响。它的优点是简单，方便兼容性好，但是一般情况下不建议使用该方法，因为会造成结构混乱，不利于后期维护

```html
<div style="clear: both"></div>
```

3、通过给父级元素添加伪元素after，达到清除浮动的目的；
　　这种方式也是使用clear: both;的方式达到效果，只是变相的使用了伪类after，使得页面结构更简洁，也是常用的清理浮动的方式。

```css
.father:after{/*伪元素是行内元素 正常浏览器清除浮动方法*/
        content: "";
        display: block;
        height: 0;
        clear:both;
        visibility: hidden;
    }
```

# 居中方法

行内元素：text-align:center,line-hight:盒子高度

1flex弹性布局，flex容器设置属性   justify-content: center;    align-items:center;

2grid栅格布局 父元素display：grid；align-items：center；

3子绝父相，子元素用相对定位，结合transform translate平移，

4子绝父相，设置margin-top，margin-left（已知宽高）

```css
.child{
        width: 100px;
        height: 100px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
    }
.child{
    width: 100px;
            height: 150px;
            position: absolute;
            top: 50%;
            left: 50%;
            margin-top: -75px;
            margin-left: -50px;

}

```

5子绝父相，子元素用相对定位，定位上下左右为0，在设置margin auto

```css
.child{
			width: 100px;
            height: 100px;
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            margin: auto;
}
```

6子绝父相+css函数calc（）动态计算（已知宽高）

```css
#parent6{
            position: relative;
            height: 100px;
            width: 100px;
            margin: 10px auto;
            background-color: black;
            
        }
#child6{    
            position:absolute;
            height: 50px;
            width: 50px;
            left: calc(50% - 25px);
            top: calc(50% - 25px);
            background-color: blue;
        }
```

7父元素使用table-cell，设置text-algin：center，vertical-algin：middle。注意父元素需要用一级display：table包裹，子元素需要设置margin：auto。继承来的margin：0不能居中。

```css
.table{
            display: table;
            height: 100px;
            width: 100px;
            background-color: black;
            margin: 10px auto;
        }
        #parent5{
            display: table-cell;
            text-align: center;
            vertical-align: middle;
        }
        #child5{    
            margin: auto;/* 父元素的text-align会受margin：0影响*/
            height: 50px;
            width: 50px;
            background-color: blue;
        }
```



# 解决margin塌陷问题

构造bfc，用bfc特性

用padding代替margin	

# 显示隐藏

1设置为display:none;的元素将不会再占用页面空间，从渲染树中消失，其占用的空间会被其他元素所占有，从而会引起浏览器的重排和重汇。不继承，父元素设置了 子元素无法显示

2visibility: hidden

不会从渲染树消失，元素仍会占用页面空间但无法点击，因此只会导致浏览器的重汇而不会引起重排。可以被子元素修改取消隐藏

3opacity:0

设置元素透明度opacity属性为0，也可以隐藏页面元素。不会重绘重排。不会从渲染树中消失，可以点击。不继承

# css3新特性

**文字阴影**  text-shadow

**font-face属性：** 定义自己的字体

**圆角（边框半径）：** border-radius 属性用于创建圆角
**边框图片：** border-image: url(border.png) 30 30 round
**盒阴影：** box-shadow: 10px 10px 5px #888888

# css动画

1、transform变换

用于元素旋转 

缩放scale

移动tranlate

倾斜skew等效果

2、transition过渡

允许css属性值在一定的时间区域内平滑的过渡，需要事件的触发，例如单击，获取焦点，失去焦点，只能定义开始状态和结束状态，不能定义中间状态，也就是说只有**两个状态**。

3、animation动画

更加复杂一些，它允许你按照实际需求添加很多的keyframes来创建动画。它可以自动触发，并且可以循环。通过 @keyframes来定义关键帧。from 表示最开始的那一帧，to 表示结束时的那一帧。单独定义keyframes的好处是我们可以复用这些动画。

animation-name ：keyframes的名字来描述动画
animation-duration：持续时间
animation-timing-function ：速率匀速liner
animation-delay：延时播放
animation-direction：播放顺序
animation-iteration-count：播放次数infinite 循环播放

# @import link

@import是CSS提供的语法规则，只有导入样式表的作用；link是HTML提供的标签，不仅可以加载CSS文件，还可以定义RSS、rel连接属性

区别：加载页面时，link标签引入的CSS被同时加载；@import 引入的 CSS 将在页面加载完毕后被加载。

# 常见布局

1、  **静态布局**：所有元素的尺寸一律使用px作为单位，不管浏览器尺寸具体是多少，网页布局始终按照最初写代码时的布局来显示。

2、  **自适应布局**：分别为不同的屏幕分辨率对应不同的静态布局并进行切换。位置会变，大小不变。使用 @media **媒体查询**给不同尺寸和介质的设备切换不同的样式。是为了解决如何才能在不同大小的设备上呈现同样的网页

3、  **流式布局**：页面元素的宽度按照屏幕分辨率进行适配调整，但整体布局不变。代表作**栅栏**、**网格系统**。使用%百分比定义宽度，高度大都是用px来固定住。

4、  **响应式布局**：每个屏幕分辨率下面会有一个布局样式，即元素位置和大小都会变。使用媒体查询+流式布局实现。可以自动识别屏幕宽度、并做出相应调整，布局和展示的内容可能会有所变动。覆盖了自适应，而且涵盖的内容更多。

5、 **弹性布局（flex****）**（rem/em布局）：rem/em区别：rem是相对于根元素的font-size大小而言的，而em是相对于其父元素。使用 em 或 rem 单位进行相对布局，相对%百分比更加灵活，同时可以支持浏览器的字体大小调整和缩放等的正常显示。

**结论：**

1、  pc端，那么静态布局（定宽度）是最好的选择；

2、  移动端，弹性布局（rem+js）是最好的选择，一份css+一份js调节font-size搞定；

3、  如果pc，移动要兼容，**响应式根据媒体查询做不同的布局**。

**1.1**   **响应式和弹性布局之间的对比：**

响应式布局：**改变浏览器宽度，“布局”会随之变化**，不是一成不变的，例如导航栏在大屏幕下是横排，在小屏幕下是竖排，在超小屏幕下隐藏为菜单，也就是说如果有足够的耐心，在每一种屏幕下都应该有合理的布局，完美的效果。

rem布局：改变浏览器宽度，**页面所有元素的高宽都等比例缩放**，也就是大屏幕下导航是横的，小屏幕下还是横的只不过变小了。

# css预处理

sass（3.0版本后更名scss） ：嵌套规则，&引用父选择符，导入功能@import，使用$变量，变量默认值！default，简单运算，@if/@for/@extend继承/@media/@function

作用：清晰，页面结构化，提升可访问性；易于后期维护；易于机器解析；易于搜索引擎SEO优化
