- SVG是在一个无限大的画布上作图

# The Viewport (视口)

`<svg width="?" height="?">` 通过`width`,`height`指定svg元素在文档中的宽高。



> 类比页面中的iframe。iframe在页面中的宽高。然而，iframe内部仍然使用其自身的坐标系统。svg也类似。

> 整个文档显示区域通过`viewBox`指定。其尺寸是指svg内部坐标。相当于一个摄像机。`viewBox`越大，相机离的越远，内容越小。

助记：\<svg> → viewport, viewBox → 相机

注意：改变svg的宽高值和单位并不影响其内部元素的坐标。

> 改变svg的宽高属性，默认情况下浏览器会对svg进行缩放，以便将svg全部显示出来。当svg宽高与内部图像比例不一致时，svg图像会水平或垂直居中，两边留白。另见`preserveAspectRatio`

> svg宽高比与viewBox宽高比一致时完整显示

> 实验：[svg宽高和viewBox](https://jsbin.com/kikicat/edit?html,output)

> 实验：[不同单位宽高的svg](https://jsbin.com/medabag/edit?html,output)

可选单位:em，ex，px，pt，pc，cm，mm, in, 百分比

当svg元素宽高使用百分数时，有两种情况：
1. 外层没有svg时，是相对窗口(window)的宽高。参见下面的“坐标系嵌套”
2. 外层有svg（即嵌套svg）时，是相对外层svg的宽高


# Using Default User Coordinates (默认用户坐标系)

- svg坐标系统是一个纯集合系统：点没有宽高；线没有宽度
- svg坐标系是一个x轴正方向为右，y轴正方向为下的**直角坐标系**

> 由于svg内部相当于根据坐标值绝对定位，所以svg内部变化只会触发重绘，不会触发reflow。
> 有时候甚至不会触发重绘。[Performance impact of SVG/SMIL reflow/repaint?
](https://stackoverflow.com/questions/24622003/performance-impact-of-svg-smil-reflow-repaint)

# Specifying User Coordinates for a Viewport (为视口指定用户坐标系)

[The ‘viewBox’ attribute](https://www.w3.org/TR/SVG2/coords.html#ViewBoxAttribute)

Name|Value|Inital Value | Animatable
---|---|---|----
viewBox	| \[<min-x\>,? \<min-y\>,? \<width\>,? \<height\>] |  As if not specified. | yes

- 没有单位的数字默认单位是像素
- `viewBox`可以用逗号分隔。也可以用空格分隔。没有单位
- `viewBox`的单位取svg宽高
- `viewBox`不能写成`viewbox`，这会导致svg无法显示。参见[SVG's viewBox is set to lowercase](https://github.com/ionic-team/stencil/issues/1847)

# Preserving Aspect Ratio (保持宽高比)

[The ‘preserveAspectRatio’ attribute](https://www.w3.org/TR/SVG2/coords.html#PreserveAspectRatioAttribute)


Name|Value|Inital Value | Animatable
---|---|---|----
preserveAspectRatio	| \<align\> \<meetOrSlice\>?| xMidYMid meet | yes

```
<align> =
    none
    | xMinYMin | xMidYMin | xMaxYMin
    | xMinYMid | xMidYMid | xMaxYMid
    | xMinYMax | xMidYMax | xMaxYMax
<meetOrSlice> = meet | slice
```

- x=横坐标，y纵坐标，Min=沿坐标轴最小值，Max=沿坐标轴最大值，Mid居中
- meet=完整显示
- slice=充满并切割
- none=不保持横纵比，会使图像拉伸

# Nested Systems of Coordinates (坐标系嵌套)
