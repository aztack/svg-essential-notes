
[Paint Servers](https://www.w3.org/TR/SVG2/pservers.html), a method which allows the fill or stroke of an object to be defined by a resource found elsewhere. It allows resources to be reused throughout a document. See the section Painting: Filling and Stroking for a general discussion of filling and stroking objects.

> Paint Servers允许使用另外定义的资源来赋予绘图元素的`fill`和`stroke`属性。

SVG defines several types of paint servers:

1. [Gradients](https://www.w3.org/TR/SVG2/pservers.html#Gradients),
    1. [linear gradients](https://www.w3.org/TR/SVG2/pservers.html#LinearGradients)
    2. [radioal gradients](https://www.w3.org/TR/SVG2/pservers.html#RadialGradients)
2. [Patterns](https://www.w3.org/TR/SVG2/pservers.html#Patterns)


# Patterns (图案)

```xml
<svg width="" height="">
  <defs>
    <pattern id="id" x="0" y="0" width="" height="" patternUnits="">
      ....
    </pattern>
  </defs>
</svg>
```

## patternUnits

patternUnits = userSpaceOnUse | objectBoundingBox

实验：[patternUnits](https://jsbin.com/xibemuy/edit?html,css,output)

## patternContentUnits

## Nested Patterns

```xml
<svg>
  <defs>
    <pattern id="p1"></pattern>
    <pattern id="p2">
      <circle style="fill: url(#p1)" />
    </pattern>
  </defs>
  <rect style="fill: url(#p2)" />
</svg>
```

# Gradients (渐变)

## The linearGradient element


```xml
<!-- 默认水平渐变 -->
<svg>
  <defs>
    <linearGradient id="g1">
      <stop offset="0" stop-color="red" />
      <stop offset="1" stop-color="green" />
    </linearGradient>

    <!-- 引用g1并设置渐变方向为水平从左到右。gradientUnits默认是objectBoundingBox -->
    <linearGradient id="g1-rl" xlink:href="#g1"
      radientUnits="objectBoundingBox"
      spreadMethod="pad"
      x1="100%" y1="0%" x2="0%" y2="0%" />
  </defs>
</svg>
```
[Stop Color Properties](https://www.w3.org/TR/SVG2/pservers.html#StopColorProperties)
- stop-color
- stop-opacity

spreadMethod = pad | reflect | repeat

```css
<!-- 默认垂直渐变  -->
.g1 {
  background-image: linear-gradient(0deg, red 0%, green 100%);
}
```

```idl
[Exposed=Window]
interface SVGStopElement : SVGElement {
  [SameObject] readonly attribute SVGAnimatedNumber offset;
};
```

## The radialGradient element

[Radial gradients](https://www.w3.org/TR/SVG2/pservers.html#RadialGradients)

```xml
<svg>
 <defs>
  <radialGradient id="r1" cx="0%" cy="0%" r="141%">
    <stop offset="0%" stop-color="#f96" />
    <stop offset="50%" stop-color="#9c9" />
    <stop offset="100%" stop-color="#909" />
  </radialGradient>
 </defs>
</svg>
```
> 注意：141%= 1.414* 100% = sqr(2) * 100%
> 这个半径才能正好覆盖一个正方形

# Transforming Patterns and Gradients (变换图案与渐变)

[gradientTransform](https://www.w3.org/TR/SVG2/pservers.html#RadialGradientElementGradientTransformAttribute)
、[patternTransform](https://www.w3.org/TR/SVG2/pservers.html#PatternElementPatternTransformAttribute)

```xml
<linearGradient id="skewed-r" gradientTransform="skewX(10)" xlink:href="#r1">
</linearGradient>

<pattern id="skewed-pattern" patternTransform="skewX(15)" xlink:href="#p1>
</pattern>
```

参考：
- [Gradient, Stop, Pattern DOM Interface](https://www.w3.org/TR/SVG2/pservers.html#DOMInterfaces)