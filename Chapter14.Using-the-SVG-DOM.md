# Determining the Value of Element Attributes 确定元素的属性值
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



# SVG Interface Methods SVG接口方法

# Constructing SVG with ECMAScript/JavaScript 使用ECMAScript/JavaScript创建SVG

# Animation via Scripting 使用脚本控制动画

# Using JavaScript Libraries 使用JavaScript库
类似jQuery的API风格。参见README中的SVG库及其文档。

# Event Handling in Snap Snap中的事件处理
略。[Snap.js Docs](http://snapsvg.io/docs/)

## Clicking Objects
略。

## Dragging Objects
略。