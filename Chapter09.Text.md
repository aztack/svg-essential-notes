# Text Terminology 文本相关术语

- Character 字符：a byte or bytes with a numeric value according to Unicode Standard 内存中的一个或多个字节，在Unicode中代表具体含义
- Glyph 符号: 字符的具象形态
- Font 字体：略
- Baseline，ascent and descent 基线、上坡线、下坡线：见下图
- Cap-height，ex-height 大写字母高度、x高度：见下图

一图以蔽之：

![image](https://user-images.githubusercontent.com/782871/66727121-b790a000-ee6f-11e9-8315-5c3916640bef.png)


# Simple Attributes and Properties of the \<text> Element 文字元素的基本属性

简单例子：path是辅助线。注意它的画线和text的x、y坐标的关系：
```xml
<svg width="500" height="500" viewBox="0 0 500 500" style="font-size:32px">
  <path d="M 20 30, 20 120
    M 10 30, 100 30
    M 10 70, 100 70
    M 10 110, 110 110"
        stroke-width="0.5" style="stroke:gray;" />
  <text x="20" y="30" style="stroke:red;fill:red;">Simplest Text</text>
  <text x="20" y="70" style="stroke:green;fill:green">Outlined/filled</text>
  <text x="20" y="110" style="stroke:blue;stroke-width:0.5;fill:none">Outlined only</text>
</svg>
```
![image](https://user-images.githubusercontent.com/782871/66727425-a21c7580-ee71-11e9-97af-75b3941884f3.png)

在svg标签上可以指定`font-size`来控制默认字体大小。
但是无法指定`color`来控制文字颜色。文字颜色通过描边和填充一起控制，并且需要分别指定。
不指定则默认是黑色。

以下样式与CSS相同，可以在样式中指定：
`font-family`,`font-size`,`font-weight`,`font-style`,`text-decoration`,`word-spacing`,`letter-spacing`等等。

# Text Alignment 文本对齐

`text-anchor: [start | middle | end]`

```xml
<svg width="500" height="500" viewBox="0 0 500 500" style="font-size:32px">
  <path d="M 120.5 30, 120.5 120
            M 110 30.5, 200 30.5
            M 110 70.5, 200 70.5
            M 110 110.5, 210 110.5"
        stroke-width="0.5" style="stroke:gray;" />
  <text x="120" y="30" style="stroke:red;fill:red;text-anchor:start">Kpfx</text>
  <text x="120" y="70" style="stroke:green;fill:green;text-anchor:middle">Kpfx</text>
  <text x="120" y="110" style="stroke:blue;stroke-width:0.5;text-anchor:end;fill:none">Kpfx</text>
</svg>
```

![image](https://user-images.githubusercontent.com/782871/66727662-389d6680-ee73-11e9-8763-fc004ee33528.png)

# [The \<tspan> Element \<tspan>元素](https://www.w3.org/TR/SVG2/text.html#TSpanNotes)
由于文本内容是千变万化的。当你想为其中一部分文字设置不同的样式时，需要将这部分文字单独用text标签括起来。此时就需要设置文本的`x`,`y`坐标。但是文本内容是变化的，你无法确定。

此时引入`<tspan>`标签。类比HTML中的`<span>`标签。

tspan属性 | 含义 | 举例
---|---|---
x | 横坐标 | x="10"
y | 纵坐标 | y="100"
dx | 横坐标增量 | dx="10" dx="10 -10 10"
dy | 纵坐标增量 | yx="10" yx="10 -10 10"
rotate | 旋转 | rotate="90 -90"

# Settting `textLength` 设置文本长度

可以通过设置`text`的`textLength`属性来设置文本的最大宽度。当内容超出或小于宽度时浏览器自动适应。

tspan属性 | 含义 | 举例
---|---|---
textLength | 文本宽度 | textLength="100"
lengthAdjust | 文本调整方式 | lengthAdjust=[spacing | spacingAndGlyphs]

```svg
<svg width="100%" height="500">
  <text x="10" y="30" style="font-size:12pt;">Switch among 
    <tspan style="font-style:italic" dy="10">italic</tspan>, normal, and
    <tspan style="font-weight:bold; baseline-shift:super;">bold</tspan> ext. 
  </text>
  <text x="10" y="60" style="font-size:24px">
    W<tspan dy="10">a</tspan><tspan dy="-10">v</tspan><tspan dy="10">e</tspan>
  </text>
  <text x="10" y="100" style="font-size:24px">
    <tspan dy="0 10 -10 10">Wave</tspan>
  </text>
  <text x="10" y="140" style="font-size:24px">
    <tspan rotate="90 0 90 0">Wave</tspan>
  </text>
  <text x="10" y="180" textLength="200" lengthAdjust="spacing" style="font-size:24px">
    Short words
  </text>
  <text x="10" y="200" textLength="200" lengthAdjust="spacingAndGlyphs" style="font-size:24px">
    Short words
  </text>
  <text x="10" y="200" style="font-size:24px" writing-mode="tb">
     Short words
  </text>
  <text x="50" y="200" style="font-size:24px;transform-origin: 50px 200px;" transform="rotate(90)">
    Short words
  </text>
</svg>
```
![image](https://user-images.githubusercontent.com/782871/67135702-fd25e200-f24e-11e9-9762-b554faec57be.png)


# Vertical Text 纵向文本

可以通过svg的`transform:rotate(90)`将文本旋转。
还可以通过将书写方式改变改为`top-bottom`来旋转文本。
见上面svg的最后两个text

# Internationalization and Text 国际化和文本

同时设置`direction:rtl`和`unicode-bidi: bidi-override`将文本从右往左显示。
渲染坐标不变，文本将向左扩展。

参考：
- [The switch Element](https://www.w3.org/TR/SVG2/struct.html#SwitchElement)
- [SystemLanguage](https://www.w3.org/TR/SVG2/struct.html#ConditionalProcessingSystemLanguageAttribute)

> The `switch` element evaluates the `requiredExtensions` and `systemLanguage` attributes on its direct child elements in order, and then processes and renders __*the first child for which these attributes evaluate to true*__. All others will be bypassed and therefore not rendered. If the child element is a container element such as a ‘g’, then the entire subtree is either processed/rendered or bypassed/not rendered.

```svg
<svg width="100%" height="500">
  <text x=200 y=20 style="direction:rtl;unicode-bidi:bidi-override;">世界大同Hello World!</text>
</svg>
 ```

 ![image](https://user-images.githubusercontent.com/782871/67139148-560d6e80-f27f-11e9-822e-1772e687bf6d.png)

```svg
<svg width="100%" height="500">
  <switch>
    <text x=100 y=40 systemLanguage="zh-CN"
      style="direction:rtl;unicode-bidi:bidi-override;">世界你好!</text>
    <text x=100 y=40 systemLanguage="en">Hello World!</text>
  </switch>
</svg>
```
简体中文系统下英文部分没有显示：

![image](https://user-images.githubusercontent.com/782871/67139259-b650e000-f280-11e9-822c-c81e442ece79.png)

# Text Path 文本路径

在SVG中文本需要指定坐标才能显示。文字默认沿着水平方向从左到右排列。
通过改变direction和unicode-bidi可以让文字从右到左排列。
不仅如此，文字还可以沿着给定的曲线排列：

```svg
<svg width="400" height="200">
  <defs>
    <!-- 1.创建曲线 -->
    <path id="curvepath"
      d="M30 40 C 50 10, 70 10, 120 40 S 150 0, 200 40"
      style="stroke: gray; fill: none;"/>
  </defs>
  <g>
    <!-- 参考线 -->
    <use xlink:href="#curvepath"/>
  </g>
  <text style="font-family: 'Liberation Sans'; font-size: 10pt;">
    <!-- 2.用<textPath>包围文字，通过xlink:href引用第一步中的曲线 -->
    <textPath xlink:href="#curvepath">Following a cubic Bézier curve.</textPath>
  </text>
</svg>
```
![image](https://user-images.githubusercontent.com/782871/67153644-a0462c80-f31f-11e9-893f-52fd1ae0894f.png)

你还可以设置文字起始位置`<textPath startOffset="50%">`。

在`<textPath>中放置<animate>可以为文字路径增加动画`

```svg
<text style="font-family: 'Liberation Sans'; font-size: 10pt;">
    <!-- 2.用<textPath>包围文字，通过xlink:href引用第一步中的曲线 -->
    <textPath id="text-path" startOffset="10%" xlink:href="#curvepath">
      Following a cubic Bézier curve.
      <animate attributeName="startOffset" keyTimes="0;1" values="0;100%" dur="5s" repeatCount="indefinite" />
    </textPath>
  </text>
```
![animate-startOffset](https://user-images.githubusercontent.com/782871/67153847-552e1880-f323-11e9-9709-a9b17ebed5e6.gif)

# 9.9 Whitespace and Text 空白和文本

参考：[The xml:space attribute](https://www.w3.org/TR/SVG2/struct.html#WhitespaceProcessingXMLSpaceAttribute)

> Deprecated XML attribute to specify whether white space is preserved in character data. The only possible values are the strings 'default' and 'preserve', without white space. Refer to the Extensible Markup Language (XML) 1.0 Recommendation [xml] and to the discussion white space handling in SVG.

>New content should use the white-space property instead.

这个属性已经废弃。建议使用`white-space`。

参考: 
- [Text Element](https://www.w3.org/TR/SVG2/text.html#TextElement)
- [SVG Text properties adaptions](https://www.w3.org/TR/SVG2/text.html#TextPropertiesAdaptions)