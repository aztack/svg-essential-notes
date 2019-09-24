[Basic Shapes](https://www.w3.org/TR/SVG2/shapes.html)

基本形状列表
- [rect 矩形](https://www.w3.org/TR/SVG2/shapes.html#RectElement)
- [circle 圆形](https://www.w3.org/TR/SVG2/shapes.html#CircleElement)
- [ellipse 椭圆形](https://www.w3.org/TR/SVG2/shapes.html#EllipseElement)
- [line 直线](https://www.w3.org/TR/SVG2/shapes.html#LineElement)
- [polyline 折线](https://www.w3.org/TR/SVG2/shapes.html#PolylineElement)
- [polygon 多边形](https://www.w3.org/TR/SVG2/shapes.html#PolygonElement)

基本写法

```html
<line x1="start-x" y1="start-y" x2="end-x" y2="end-y" />
<rect x="left-x" y="top-y" width="width" height="height" rx="raidus-x" ry="radius-y"/>

<circle cx="center-x" cy="center-y" r="radius" />
<elllipse cx="center-x" cy="center-y" rx="x-radius" ry="y-radius" />

<polygon pionts="points-list" />
<polyline points="points-list" />
```

# Lines 直线

> **各种形状默认是没有`stroke`的，需要指定**

# Stroke Characteristics 画笔特性
参考：[Stroke properties](https://www.w3.org/TR/SVG2/painting.html#StrokeProperties)
> stroke可以类比为用钢笔在画布上划线。钢笔先包含几个特性：
- stroke-width
- stroke-color
- stroke-opacity
- stroke-linecap
- stroke-linejoin
- stroke-miterlimit
- stroke-dasharray
- stroke-dashoffset
> **注意这几个属性并不局限于line。所有基本形状和path都适用**

## stroke-width 画笔宽度

> 浏览器渲染svg时默认开启抗锯齿。可以通过设置svg元素的`shape-rendering: crispedges`关闭抗锯齿

> **描边与css的border不同。它是以线为轴，两侧延伸的**

![shape-rendering: crispedges](https://user-images.githubusercontent.com/782871/65401312-e29c4c80-ddf9-11e9-8d6e-5b4cc150ace6.png)

## stroke-color 画笔颜色
略：参考[CSS3 Color Specification](https://www.w3.org/TR/css-color-3/)

## stroke-opacity 画笔不透明度

> stroke-opacity ∈ [0.0, 1.0]

## stroke-dasharray

> The stroke-dasharray property controls the pattern of dashes and gaps used to form the shape of a path's stroke.

> 实验: [line, circle, stroke](https://jsbin.com/pizulum/edit?html,output)

参考：
- [张鑫旭:纯CSS实现帅气的SVG路径描边动画效果](https://www.zhangxinxu.com/wordpress/2014/04/animateion-line-drawing-svg-path-%e5%8a%a8%e7%94%bb-%e8%b7%af%e5%be%84/)
- [张鑫旭:寥寥数行SVG实现圆环loading或倒计时效果](https://www.zhangxinxu.com/wordpress/2015/07/svg-circle-loading/)

# Rectangles 矩形

参考：[Fill properties](https://www.w3.org/TR/SVG2/painting.html#FillProperties)

> `fill`的初始值是`black`，可用于各种[形状](https://www.w3.org/TR/SVG2/shapes.html#TermShapeElement)

- fill-rule: nonzero | evenodd
- fill-opacity: 0-1 或百分比

> \<rect\>通过指定`rx,ry`可以画圆角矩形

# Circles and Ellipses 圆形与椭圆形
略

# The \<polygon\> Element
> 必须偶数个点，用空格或者逗号分隔都可以

polygon的points是`SVGAnimatedPoints`。注意`Animated`

![SVGAnimatedPoints](https://user-images.githubusercontent.com/782871/65404290-82fa6d00-de0a-11e9-848b-a197dfe98730.png)

# The \<polyline\> Element

fill-rule: nonzero | evenodd

# Line Caps and Joins 线帽与线连接

参考[LineCaps](https://www.w3.org/TR/SVG2/painting.html#LineCaps)
参考[LineJoin](https://www.w3.org/TR/SVG2/painting.html#LineJoin)

- stroke-linecap: butt | round | square
- stroke-linejoin: miter | miter-clip | round | bevel | arcs

# Basic Shapes Reference Summary

略

参考：
- [Shapes DOM Interface](https://www.w3.org/TR/SVG2/shapes.html#DOMInterfaces)