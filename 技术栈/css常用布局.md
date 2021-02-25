# css常用布局

## 盒子居中

```css
.heard {
  background-color: red;
  height: 100px;
  display: flex;
  justify-content: center; //水平方向
  align-items:center;     //垂直方向
}
.child{
  // align-self:center;// 垂直方向，可取代父级的align-items
  background-color: yellow;
}

```

* 有宽度情况下利用定位解决

```css
.heard {
  background-color: red;
  height: 100px;
  position: relative;
}
.child{
  //align-self:center;
  width: 100px;
  position: absolute;
  left: 50%;
  margin-left: -50px;
  background-color: yellow;
}

```
不知道宽度
* * *
```
.heard {
  background-color: red;
  height: 100px;
  position: relative;
}
.child{
  //align-self:center;
  width: 100px;
  position: absolute;
  margin: auto;
  left: 0;
  top:0;
  bottom:0;
  right: 0;
  
  background-color: yellow;
}
```

* * *

* 不知道宽度
  
```css
.heard {
  background-color: red;
  height: 100px;
  width: 500px;
  position: relative;
}
.child{
  //align-self:center;
  width: 100px;
  height: 20px;
  position: absolute;
  // top:calc(200px);
  top:50%;
  left:50%;
  transform:translate(-50%,-50%);
  background-color: yellow;
}
```

* * *
table-cell宽高是不能使用百分比设置

```css
parent{

display:table-cell;

vertical-align:middle; //文字水平

text-align:center;

}

.child{

display:inline-block;

}
```

***

## 清除浮动？

* 通过伪类

```css
  .clearfix:after{/*伪元素是行内元素 正常浏览器清除浮动方法*/
        content: "";
        display: block;
        height: 0;
        clear:both;
        visibility: hidden;
    }
   .clearfix{ *zoom: 1; } 
```

* 双伪类

```css
// 全浏览器通用的clearfix方案【推荐】
// 引入了zoom以支持IE6/7 
// 同时加入:before以解决现代浏览器上边距折叠的问题 
.clearfix:before,
 .clearfix:after { display: table; content: " "; }
 .clearfix:after { clear: both; } 
.clearfix{ *zoom: 1; }

```

* * *

* 盒子模型有哪两种，区别是什么？
  CSS有个属性为 `box-sizing` 默认属性为`border-box`,IE模型为`content-box`
  盒子组成由`content`、`padding`、`border`、`margin`。
  其中IE的`contetn`的`width`、`height`由`content`、`padding`、`border`组成。
  * `width:content.width+margin-left +margin-right`

  而W3C的`contetn`的`width`、`height`
  * `width:content.width+2x(padding-left+border+margin-left)`
  
* * *

## flex布局 

* 采用flex布局的元素称为容器，在容器里面，统称flex项目,简称“项目”

### 一、容器的属性

容器有以下6种属性

```css
1、flex-direction    //控制项目的排列方向
2、flex-warp        //控制项目的换行
3、flex-flow        //控制项目的排列方向、换行
4、justify-content   //控制项目对齐方式
5、align-items       //控制项目垂直方向的对齐方式
6、align-content     //控制项目多条轴线对齐方式
```

### 1.1 flex-direction row

flex-direction：`row | row-reverse | cloumn |cloumn-reverse`
  
```css
row: 起点在左端 （水平方向，默认值）
row-reverse ：起点在右端
cloumn :起点在上端
cloumn-reverse :起点在下端
```

### 1.2 flex-warp nowarp

`flex-warp : nowarp | warp | warp-reverse`
```
nowarp : (默认值) 不换行
warp: 换行 ，第一行在上面
warp-reverse: 换行，第一行在下面
```

### 1.3 flex-flow row nowarp
flex-flow为flex-direction与flex-warp的集合。
`flex-flow:flex-direction || flex-warp`

### 1.4 justify-content flex-start

`justify-content`为项目在主轴的排序顺序（水平）
`justify-content: flex-start | flex-end | center |space-between | space-around`

* 具体对齐方式与轴的方向有关。下面假设主轴为从左到右
  
```css
flex-start（默认） :  左对齐
flex-end:     右对齐
center:      居中
space-between: 两端对齐，项目间隔之间相等
space-around:   每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
```

### 1.5 align-item flex-start

`align-item`为在交叉轴上如何对齐。(垂直)
`align-item：flex-start | flex-end | center | baseline | stretch`

```css
flex-start:上端（起点）对齐
flex-end:下端（终点）对齐
center:居中
baseline: 项目的第一行文字的基线对齐.
stretch（默认值）:若项目高度没设或者是auto，将沾满整个容器
```

### 1.6 align-content

`align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用
`align-content: flex-start | flex-end | center | space-between | space-around | stretch;`

#### 二、项目属性

```css
1、order :       //项目排序
2、flex-grow:    //项目放大
3、flex-shrink:  

```

### 2.1 order  0

`order`为项目排列顺序。数值越小，排在前面越前。默认为0
`order:<integer>`

### 2.2 flex-grow 0

`flex-grow`定义项目的放大比例，默认为0，即如果存在剩余空间，不放大。
`flex-grow: <number>`
若项目的`flex-grow` 的属性值为1时，将会平分剩余空间。若其中有个为2的时候，平分的空间比1的多一倍

### 2.3 flex-shrink (缩小) 1

`flex-shrink` 定义项目的缩放，默认为`1`，即若空间不足，则项目将等比例缩小。
若为0时，空间不足也不缩小。
`flex-shrink: <number>`

### 2.4 flex-basis auto

`flex-basis`定义项目在分配多余空间之前所占据的空间（主轴空间，水平方向）。
默认为`auto`,即为项目本身占据的空间。
`flex-basis: <number> | auto`

### 2.5 flex (0,1,auto)

`flex`定义为`flex-grow`、`flex-shrink`、`flex-basis`的集合体。`flex-shrink`、`flex-basis`为可选项。
`flex : none  | [flex-grow,flex-shrink,flex-basis]`
有快捷键`auto` :`1，1，auto`
有快捷键`none`:`0,0,auto`

### 2.6 align-self auto(垂直方向)

`align-self` 运行自身与其他项目不一样的对齐方式，会覆盖掉`align-items`,
`align-self：flex-start | flex-end | center | stretch | baseline`

```css
flex-start: 起点对齐（上端）
flex-end:   终点对齐（下端）
center:     居中
baseline:   第行一个文字的基线
stretch:    项目整个高度


```

## calc用法

calc动态计算长度单位，运算符前后都需要保留一个空格，例如：
`width: calc(100% - 10px)；`

## @media 

@media查询，可以针对不同的媒体类型定不同的样式。可以在不同的屏幕运用不同的样式，即响应式.

``` js
<meta name="viewport" content="width=device-width, height=device-height,initial-scale=1, maximum-scale=1, user-scalable=no">
```

```css
1、device-width:     当前设备宽度
2、device-height:    当前设备高度
3、initial-scale:    初始缩放
4、maximum-scale:    用户缩放最大的比例
5、user-scaleable:   用户是否可以手动缩放
```

### 一、方法

* 1.1、head标签引入

 `<link rel="stylesheet" href="styleB.css" media="screen and (max-width: 800px)"> `

* 1.2、css引入
  
 浏览器宽度大于等于500px且小于等于900px时使用样式

```css
@media screen and (min-width:500px ) and (max-width:900px){
color:#fff
}

```

若为IE浏览器:
`<meta http-equiv="X-UA-Compatible" content="IE=edge">`

### 二、@media参数用法

```css
1、width:            //浏览器当前可视宽度
2、height:           //浏览器当前可视高度
3、device-width:     //设备屏幕宽度
4、device-heght:     //设备屏幕高度
5、orientation: portrait（竖屏） | landscape（横屏）
...
```

* * *

## css优先级

内联样式(1000) > ID样式（100）> 类样式（10）> 标签样式（1）
！important 为最高级，用于改变内联也改不了的样式（不推荐）

## less用法

变量用@

```css
@width:10px;
.test1{
background-color:#fff
}
.children {
width:@width
.test1();
}

.test{
color:red;

}
```

* sass用法
变量用$

```css
$width:10px;
.test1{
width:$width
}

```

### 两者区别：less vs sass

1、变量的不同 ，前者用@，后者用$
2、安装环境不一样，前者基于JavaScript,是需要引入Less.js来处理代码输出css到浏览器,后者需要安装`Ruby`环境。
3、处理机制不一样，前者是客户端，后者是服务端。

* * *

## 如何让一个子盒子固定在父盒子的右下方

* 可用flex布局原理解决，`justify-content、align-items`
* 用`margin，position，right、bottom`
* 或者计算详细的值，用定位解决
* 或填充`div`,使得自己在下方

* * *

## 区分px,em,rem,vw,vh,rpx

### 1.1 em 相对于当前对象内文本的字体尺寸

* 一般为16px，若父级修改，则em相对应的修改。em 会层层继承父元素的字体大小
* 1em=16px;font-size:20px,1em=20px
  
### 1.2 rem单位是相对于字体大小的html元素，也称为根元素。

```css
html {
  font-size: 10px; /* 不建议设置 font-size: 62.5%; 在 IE 9-11 上有偏差，具体表现为 1rem = 9.93px。 */
}
```

rem是相对于根元素（html）的字体大小，而em是相对于其父元素的字体大小

### 1.3 rpx 

rpx 是微信小程序解决自适应屏幕尺寸的尺寸单位。微信小程序规定屏幕的宽度为750rpx。例如：
屏幕宽度为375px，把它分为750rpx后， 1rpx = 0.5px = 1物理像素。

### 1.4 vw,vh 可利用其作于响应式

vw,视窗的可视宽度
vh,视窗的可视高度

## 如何隐藏盒子

display：none
opacity:0
overflow:hidden
宽度，高度为0

## 定位

position：relative | absolute | fixed

## object-fit

上传头像变形问题（图像）

```css
object-fit:fill  填充满但不保证原比例
         :contain 保持原比例，但不一定可以填充满，可能会空白
         :cover 覆盖，保持原比例，但是内容尺寸一定比容器大
         :none 原有尺寸比例。同时保持替换内容原始尺寸大小
         :scale-down  像依次设置了none或contain, 最终呈现的是尺寸比较小的那个
```
