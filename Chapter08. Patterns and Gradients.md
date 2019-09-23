
[Paint Servers](https://www.w3.org/TR/SVG2/pservers.html), a method which allows the fill or stroke of an object to be defined by a resource found elsewhere. It allows resources to be reused throughout a document. See the section Painting: Filling and Stroking for a general discussion of filling and stroking objects.

> Paint Servers允许使用另外定义的资源来赋予绘图元素的`fill`和`stroke`属性。

SVG defines several types of paint servers:

1. [Gradients](https://www.w3.org/TR/SVG2/pservers.html#Gradients),
    1. [linear gradients](https://www.w3.org/TR/SVG2/pservers.html#LinearGradients)
    2. [radioal gradients](https://www.w3.org/TR/SVG2/pservers.html#RadialGradients)
2. [Patterns](https://www.w3.org/TR/SVG2/pservers.html#Patterns)


# Patterns 图案

```html
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

# Gradients 渐变

## The linearGradient element
## The radialGradient element

# Transforming Patterns and Gradients