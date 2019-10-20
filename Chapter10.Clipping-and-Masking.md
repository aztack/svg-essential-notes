[Cliping and Masking](https://www.w3.org/TR/SVG2/render.html#ClippingAndMasking)

Cliping和Masking有自己的Module
[Masking Spec](https://www.w3.org/TR/css-masking-1/)

- 裁剪元素\<ClipPath>内部可以放置若干个基本形状和文本、图片、路径
- \<clipPath>放在\<defs>内部
- 然后再其他元素通过css的`clip-path:url(#clipId)`

clip-path可以想象成一个异形viewport

# Cliping to a Path

```svg

```

# Masking
> Where the mask is opaque, the pixels of the masked object are opaque.
Where the mask is translucent, so is the object, and the transparent parts of the mask
make the corresponding parts of the masked object invisible.

蒙版将其内部的透明信息传递给应用蒙版的对象：透明的部分使对象对应部分完全不可见。完全不透明的部分使对象对应部分完全可见。半透明同理。

这个被传递的“透明信息”并不是rgba中的a的值。
而是通过一个[相对亮度](https://en.wikipedia.org/wiki/Relative_luminance)公式计算的：

```
0.2125 * red value + 0.7154 * green value + 0.0721 * blue value) * opacity value
```

rgb也参与了计算，并且根据颜色的冷暖程度给了不同的权重。
绿色0.7154最高，红色0.2125次之，蓝色0.0721最低。这三者的值乘以权重系数之后再乘以透明度a的值得到最终的透明名度。


参考：[亮度函数](https://en.wikipedia.org/wiki/Luminosity_function)

TOOD: 这3个系数怎么来的？

# Case Study: Making a Graphic