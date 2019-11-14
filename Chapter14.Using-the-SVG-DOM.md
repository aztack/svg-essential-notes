# Determining the Value of Element Attributes (确定元素的属性值)
SVG元素相关属性都包含两个子属性：`baseVal`和`animVal`。后者只读。
当元素产生动画之后会更新。无论如何设置的属性单位，这两个属性始终存储`user units`（角度单位为“度”)。
这两个属性还包含在不同单位之间转换的方法。

SVG单位类型：

![image](https://user-images.githubusercontent.com/782871/65815642-c72fa800-e224-11e9-8be1-04ee211fa32a.png)

[SVGLength.idl](https://chromium.googlesource.com/chromium/blink/+/refs/heads/master/Source/core/svg/SVGLength.idl)

```idl
[
  ...
] interface SVGLength {
  // Length Unit Types
  const unsigned short SVG_LENGTHTYPE_UNKNOWN    = 0;
  const unsigned short SVG_LENGTHTYPE_NUMBER     = 1;
  const unsigned short SVG_LENGTHTYPE_PERCENTAGE = 2;
  const unsigned short SVG_LENGTHTYPE_EMS        = 3;
  const unsigned short SVG_LENGTHTYPE_EXS        = 4;
  const unsigned short SVG_LENGTHTYPE_PX         = 5;
  const unsigned short SVG_LENGTHTYPE_CM         = 6;
  const unsigned short SVG_LENGTHTYPE_MM         = 7;
  const unsigned short SVG_LENGTHTYPE_IN         = 8;
  const unsigned short SVG_LENGTHTYPE_PT         = 9;
  const unsigned short SVG_LENGTHTYPE_PC         = 10;
    ...
};
```



# SVG Interface Methods (SVG接口方法)
这节介绍了一些SVG相关的接口、元素的方法。
对SVG接口、类、类方法的使用和熟悉是一个相对长期的过程和有技巧的事情。
这里就不罗列接口了。
从[Blink的SVG源码](https://chromium.googlesource.com/chromium/blink/+/refs/heads/master/Source/core/svg/)中可以查看SVG相关的所有接口和方法。
然后在SVG规范中搜索相关接口、方法，再结合规范中的例子理解。理解有难度再Google相关教程、代码片段综合起来理解。并将代码和技巧积累起来。

# Constructing SVG with ECMAScript/JavaScript (使用ECMAScript/JavaScript创建SVG)

书中举了个用JavaScript创建一个表盘的例子。
整个编码过程和用JavaScript创建、操作HTML DOM差不多。
要注意的是:

svg中内嵌script标签的type：
```html
<svg>
  <script type="application/ecmascript"> <![CDATA[
    代码
  // ]]>
  </script>
</svg>
```

创建元素需要用带NS版本的方法：
```js
const svg = document.getElementById('svg');
document.createElementNS(svg.namespaceURI, 'circle');
```

在进行大量 DOM 操作之前暂停 SVG 更新绘制可以提升在某些 阅读器中的性能:
```js
svgElement.suspendRedraw(1000);
//...操作svg
svgElement.unsuspendRedrawAll();
```

# Animation via Scripting (使用脚本控制动画)

使用`requestAnimationFrame`来做动画。自己根据时间戳来控制动画。
`<animationTransform>`可能有潜在问题（未验证）

# Using JavaScript Libraries (使用JavaScript库)
类似jQuery的API风格。参见README中的SVG库及其文档。

# Event Handling in Snap (Snap中的事件处理)
略。[Snap.js Docs](http://snapsvg.io/docs/)

## Clicking Objects
略。

## Dragging Objects
略。