
* [入门](#入门-相识)
  * [HTML标签使用](#HTML标签使用)
  * [HTML中引用](#HTML中引用)
  * [坐标定位](#坐标定位)
  * [SVG的缩放](#SVG的缩放)
* [深入](#深入-相知)
  * [基本形状](#基本形状)
    * [矩形](#矩形)
    * [圆形](#矩形)
    * [椭圆](#矩形)
    * [线条](#矩形)
    * [折线](#矩形)
    * [多边形](#矩形)
    * [路径](#矩形)
  * [填充与边框](#填充与边框)
  * [渐变](#渐变)
  * [图案](#图案)
  * [文字](#文字)
  * [基本变形](#基本变形)
    * [平移](#平移)
    * [旋转](#旋转)
    * [斜切](#斜切)
    * [缩放](#缩放)
    * [matrix](#matrix())
  * [剪切与遮罩](#剪切与遮罩)
  
  
<!-- SVG开始 ---------------------------------------------------------------------------->

# SVG
> &emsp;&emsp;SVG 是一种基于 XML 语法的图像格式，全称是可缩放矢量图（Scalable Vector Graphics）。jpg、png、gif等图像格式都是基于像素处理的，SVG 则是属于对图像的形状描述，所以它本质上是文本文件，体积较小，且不管放大多少倍都不会失真。<br/>
> &emsp;&emsp;SVG也提供了一些元素，用于定义圆形、矩形、简单或复杂的曲线，以及其他形状。一个简单的SVG文档由`<svg>`根元素和基本的形状元素构成。另外还有一个g元素，它用来把若干个基本形状编成一个组。<br/>

<!-- [0] 入门 ---------------------------------------------------------------------------->

## 入门-相识

<!-- [0-1] HTML标签使用 ---------------------------------------------------------------------------->

#### HTML标签使用
```html

    <svg version="1.1"
         baseProfile="full"
         width="300" height="200"
         xmlns="http://www.w3.org/2000/svg">

        <rect width="100%" height="100%" fill="red" />

        <circle cx="150" cy="100" r="80" fill="green" />

        <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">SVG</text>

    </svg>
```

效果：
<p align="center">
<img src="https://github.com/jimwong666/FEstart/blob/master/20190110-canvas%26svg/svg/images/img_1.png" alt="img_1">
</p>
<br/>


**注意：**<br/>
&emsp;&emsp; **1.** SVG的元素和属性必须按标准格式书写，因为XML是区分大小写的（这一点和html不同）<br/>
&emsp;&emsp; **2.** SVG里的属性值必须用引号引起来，就算是数值也必须这样做。
<br/>
  
##
<!-- [0-2] HTML中引用 ---------------------------------------------------------------------------->

#### HTML中引用
```html
    <object data="image.svg" type="image/svg+xml" />
```
```html
    <iframe src="image.svg"></iframe>
```
```html
    <image src="image.svg"></image>
```
而此时“image.svg”是什么文件呢？其实和原来的文件很像~
```xml
    <?xml version="1.0" standalone="no"?>
    <!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
    <svg version="1.1"
         baseProfile="full"
         width="300" height="200"
         xmlns="http://www.w3.org/2000/svg">

        <rect width="100%" height="100%" fill="red" />

        <circle cx="150" cy="100" r="80" fill="green" />

        <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">SVG</text>

    </svg>
```
喏~! 就是这个(xml)~ 最上面多了两行奇怪的东西

##
#### 坐标定位
> &emsp;&emsp;SVG使用的坐标系统或者说网格系统，和Canvas用的差不多（所有计算机绘图都差不多）。这种坐标系统是：以页面的左上角为(0,0)坐标原点，坐标以像素为单位，x轴正方向是向右，y轴正方向是向下。【注意】这和我们小时候所学的坐标系是不一样的。但是在HTML文档中，元素都是用这种方式定位的。

示意图：
<p align="center">
<img src="https://github.com/jimwong666/FEstart/blob/master/20190110-canvas%26svg/svg/images/img_2.png" alt="img_2">
</p>
<br/>

所以我们定义一个矩形
```html
    <rect x="0" y="0" width="100" height="100" />
```
上面的元素定义了一个100*100px的SVG画布，这里1用户单位等同于1屏幕单位。

##  
#### SVG的缩放
> &emsp;&emsp;SVG 文档中的1个像素对应输出设备（比如显示屏）上的1个像素。但是这种情况是可以改变的，否则 SVG 的名字里也不至于会有“Scalable”（可缩放）这个词。如同CSS可以定义字体的绝对大小和相对大小，SVG也可以定义绝对大小同时SVG也能使用相对大小，只需给出数字，不标明单位，输出时就会采用用户的单位。

看个改过的例子：
```html
    <svg version="1.1"
         baseProfile="full"
         width="300" height="200"
         xmlns="http://www.w3.org/2000/svg"
         viewBox="0 0 150 100">

        <rect width="100%" height="100%" fill="red" />

        <circle cx="150" cy="100" r="80" fill="green" />

        <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">SVG</text>

    </svg>
```

这里定义的画布尺寸是300px * 200px。但是，viewBox属性定义了画布上可以显示的区域：从(0,0)点开始，150宽(x) * 100高(y)的区域。这个150 * 100的区域，会放到300 * 200的画布上显示。于是就形成了放大两倍的效果。

用户单位和屏幕单位的映射关系被称为<用户坐标系统>。除了缩放之外，坐标系统还可以旋转、倾斜、翻转。默认的用户坐标系统1用户像素等于设备上的1像素（但是设备上可能会自己定义1像素到底是多大）。

-------------------------------------------------------------------
<!-- [1] 深入 ---------------------------------------------------------------------------->

## 深入-相知
### 基本形状
#### 矩形
```html
    <svg version="1.1"
         baseProfile="full"
         width="300" height="200"
         xmlns="http://www.w3.org/2000/svg">

        <rect x="10" y="10" width="30" height="30"/>
        <rect x="60" y="10" rx="10" ry="10" width="30" height="30"/>

    </svg>
```
> &emsp;&emsp;rect元素会在屏幕上绘制一个矩形 。其实只要6个基本属性就可以控制它在屏幕上的位置和形状。下边的那个图形设置了rx和ry属性用来控制圆角。如果没有设置圆角，则默认为0。

> x
矩形左上角的x位置
y
矩形左上角的y位置
width
矩形的宽度
height
矩形的高度
rx
圆角的x方位的半径
ry
圆角的y方位的半径

##
#### 圆形