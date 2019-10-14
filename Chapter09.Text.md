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
