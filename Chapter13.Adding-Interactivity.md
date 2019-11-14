# Using Links in SVG

直接用`<a xlink:href="...">`包含对应图形标签

```xml
<svg width="200" height="100"
  xmlns="http://www.w3.org/2000/svg"
  xmlns:xlink="http://www.w3.org/1999/xlink">

  <a xlink:href="cat.svg">
    <text x="100" y="30" style="font-size: 12pt;">Cat</text>
  </a>

  <a id="g" xlink:href="http://www.w3.org/SVG/">
    <circle cx="50" cy="70" r="20" style="fill: red;"/>
    <rect x="75" y="50" width="40" height="40" style="fill: green;"/>
    <path d="M120 90, 140 50, 160 90 Z" style="fill: blue;"/>
  </a>
</svg>
```
修改`xlink:href`:
```javascript
g.setAttribute('xlink:href', 'javascript:;'); // clear href
g.addEventListener('click', e => {
  console.log(e.target);
  e.stopPropagation();
  e.preventDefault();
});
```

为svg添加css样式：
```xml
<svg width="200" height="100"
  xmlns="http://www.w3.org/2000/svg"
  xmlns:xlink="http://www.w3.org/1999/xlink">

  <style type="text/css"><![CDATA[
    a.words:hover, a.words:focus {
       text-decoration: underline;
       font-weight:bold;
    }
    a.shapes:hover, a.shapes:focus {
       stroke: #66f;
       stroke-width: 2;
       outline: none; /* over-ride default focus formatting */
    }
    ]]>
  </style>

  <a class="words" xlink:href="cat.svg">
    <text x="100" y="30" style="font-size: 12pt;">Cat</text>
  </a>

  <a class="shapes" xlink:href="http://www.w3.org/SVG/">
    <circle cx="50" cy="70" r="20" style="fill: red;"/>
    <rect x="75" y="50" width="40" height="40" style="fill: green;"/>
    <path d="M120 90, 140 50, 160 90 Z" style="fill: blue;"/>
  </a>
</svg>
```

关于[CDATA](https://www.w3.org/TR/REC-xml/#sec-cdata-sect)：
> 术语 CDATA 指的是不应由 XML 解析器进行解析的文本数据（Unparsed Character Data）。
在 XML 元素中，"<" 和 "&" 是非法的。
"<" 会产生错误，因为解析器会把该字符解释为新元素的开始。
"&" 也会产生错误，因为解析器会把该字符解释为字符实体的开始。
某些文本，比如 JavaScript 代码，包含大量 "<" 或 "&" 字符。为了避免错误，可以将脚本代码定义为 CDATA。
CDATA 部分中的所有内容都会被解析器忽略。
CDATA 部分由 "\<![CDATA[" 开始，由 "]]>" 结束

# Controlling CSS Animations
和普通DOM的CSS动画一样

# User-Triggered SMIL Animation
\<animateTransform>的`begin`,`end`可以以`elementId.eventName + offset`的形式设置触发条件。
这属于『声明式动画』。下节介绍使用脚本控制动画。
```xml
<svg width="200" height="100"
  xmlns="http://www.w3.org/2000/svg"
  xmlns:xlink="http://www.w3.org/1999/xlink">
  <g id="button">
    <rect x="10" y="10" width="40" height="20" rx="4" ry="4"
      style="fill: #ddd;"/>
    <text x="30" y="25"
      style="text-anchor: middle; font-size: 8pt">Start</text>
  </g>

  <g transform="translate(100, 60)">
    <path d="M-25 -15, 0 -15, 25 15, -25 15 Z"
      style="stroke: gray; fill: #699;">

      <animateTransform id="trapezoid" attributeName="transform"
        type="rotate" from="0" to="360"
        begin="button.click"
        dur="6s"/>
    </path>
  </g>
</svg>
```
# Scripting SVG
下面的例子中有一个\<title>标签。和HTML中类似。
```xml
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.0//EN"
    "http://www.w3.org/TR/2001/REC-SVG-20010904/DTD/svg10.dtd">

<svg width="300" height="100" viewBox="0 0 300 100"
  xmlns="http://www.w3.org/2000/svg"
  xmlns:xlink="http://www.w3.org/1999/xlink">

  <title>Accessing Content in SVG</title>

  <rect id="rectangle" x="10" y="20" width="30" height="40"
    style="stroke:gray; fill: #ff9; stroke-width:3"/>
  <text  id="output" x="10" y="80" style="font-size:9pt"></text>

  <script type="application/ecmascript"><![CDATA[
    var txt = document.getElementById("output");
    var r = document.getElementById("rectangle");
    var msg =  r.getAttribute("x") + ", " +
      r.getAttribute("y") + " " +
      r.style.getPropertyValue("stroke") + " " +
      r.style.getPropertyValue("fill");
    r.setAttribute("height", "30");
    txt.textContent= msg;
    ]]></script>
</svg>
```

插曲：体会 [`style.setProperty(name, value, priority)`](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration/setProperty)和`style[name] = value`中name的不同:

```javascript
 el.style.setProperty('background-color', 'red', 'important' /* undefined or "" */);
 el.style['backgroundColor'] = 'red';
```

## Events: An Overview (Event:概览)

[SVG Events](https://www.w3.org/TR/SVG/interact.html#SVGEvents)与`UI Events`的关系：

> The SVG DOM is compatible with all interfaces defined in, and all the event types from, UI Events, and the event types defined in `[Clipboard API and events](https://www.w3.org/TR/clipboard-apis/)` ([uievents](https://www.w3.org/TR/SVG/refs.html#ref-uievents), [clipboard-apis](https://www.w3.org/TR/SVG/refs.html#ref-clipboard-apis)).
>
> All elements in the SVG namespace support event attributes for these events; matching IDL properties are included in the base SVGElement interface via the GlobalEventHandlers and DocumentAndElementEventHandlers mixins, respectively.

SVG DOM兼容UI Events中的所有接口和事件类型。SVG Namespace下的所有元素都支持这些事件的属性；匹配的IDL属性通过混入`GlobalEventHandlers`和`DocumentAndElementEventHandlers`包含在基类`SVGElement`中。

在`typescript/lib/lib.dom.d.ts`中我们可找到相关定义：
![image](https://user-images.githubusercontent.com/782871/65750881-f74f4c00-e13b-11e9-9f3f-e6b3063a75c5.png)
- [SVGElement](https://github.com/microsoft/TypeScript/blob/master/lib/lib.dom.d.ts#L13136)
- [GlobalEventHandlers](https://github.com/microsoft/TypeScript/blob/master/lib/lib.dom.d.ts#L5836)
- [DocumentAndElementEventHandlers](https://github.com/microsoft/TypeScript/blob/master/lib/lib.dom.d.ts#L4963)

其中`SVG animation elements`支持额外的几个事件：

- [beginEvent](https://www.w3.org/TR/SVG/interact.html#BeginEvent)
- [endEvent](https://www.w3.org/TR/SVG/interact.html#EndEvent)
- [repeatEvent](https://www.w3.org/TR/SVG/interact.html#RepeatEvent)

[The ‘pointer-events’ property](https://www.w3.org/TR/SVG/interact.html#PointerEventsProp)

- bounding-box
- visiblePainted
- visibleFill
- visibleStroke
- visible
- painted
- fill
- stroke
- all
- none <-- 这就是面试中常问到的那个如何让元素不响应鼠标、指针事件的值

## Listening for and Responding to Events
略

## Changing Attributes of Multiple Objects
略

## Dragging Objects
透明元素不响应pointer事件。可以将`pointer-events`设置为`visible`使透明元素也响应。

## Interacting with an HTML Page

应用外部svg资源
```xml
<object id="externalShirt" data="shirt_interact.svg" type="image/svg+xml">
  <p>你的浏览器不支持SVG</p>
</object>
```
## Creating New Elements


创建SVG节点：
```javascript
  const r = document.createElementNS("http://www.w3.org/2000/svg", 'rect');
  r.setAttributeNS(null, 'width', 100);
  r.setAttributeNS(null, 'height', 100);
  console.log(r.width); // => SVGAnimatedLength {baseVal: SVGLength, animVal: SVGLength}
  console.log(r.getAttributeNS(null, 'width')); // => "100"
```
其中`createElementNS`,`setAttributeNS`和`getAttributeNS`都是[`Namespace awared methods`](https://developer.mozilla.org/en-US/docs/Web/SVG/Namespaces_Crash_Course#Scripting_in_namespaced_XML)。

> Namespaces affect not only markup, but also scripting. If you write scripts for namespaced XML such as SVG, read on. The DOM Level 1 recommendation was created before the original Namespaces in XML recommendation was released; therefore, DOM1 isn't namespace aware. This causes problems for namespaced XML such as SVG. To resolve these problems, DOM Level 2 Core added namespace aware equivalents of all the applicable DOM Level 1 methods. When scripting SVG, it is important to use the namespace aware methods. The table below lists the DOM1 methods that shouldn't be used in SVG, along with their equivalent DOM2 counterparts that should be used instead.

> DOM1的创建早于XML的Namespaces。所以DOM1中的相关方法是不涉及Namespace的。DOM2中为相关方法添加了NS版本：

DOM1 | DOM2
---|---
createAttribute | createAttributeNS
createElement | createElementNS
getAttributeNode | getAttributeNodeNS
getAttribute | getAttributeNS
getElementsByTagName | getElementsByTagNameNS
getNamedItem | getNamedItemNS
hasAttribute | hasAttributeNS
removeAttribute | removeAttributeNS
removeNamedItem | removeNamedItemNS
setAttribute | setAttributeNS
setAttributeNode | setAttributeNodeNS
setNamedItem | setNamedItemNS

但是！
> The first argument for all the DOM2 namespace aware methods must be the namespace name (also known as the namespace URI) of the element or attribute in question. For SVG elements this is 'http://www.w3.org/2000/svg'. However, note carefully: the Namespaces in XML 1.1 recommendation states that the namespace name for attributes without a prefix does not have a value. In other words, although the attributes belong to the namespace of the tag, you do not use the tag's namespace name. Instead, you must use null as the namespace name for unqualified (prefixless) attributes.

> 虽然DOM2中的这些方法要求第一个是namespace URI(对于svg就是http://www.w3.org/2000/svg)。而 XML1.1中要求无前缀的属性不要指定第一个参数。此时第一个参数**必须**传`null`。就像上面代码中写的那样。

另一个需要注意的是：在HTML文档中，`document.constructor === HTMLDocument`。
而在SVG文档中，`document.constructor === XMLDocument`。
二者都需要通过`document.createElementNS`来创建SVG节点。

关于`getSVGDocument`

分别有三个接口定义了`getSVGDocument`：
- [HTMLObjectElement.getSVGDocument](https://github.com/microsoft/TypeScript/blob/master/lib/lib.dom.d.ts#L8011)
- [HTMLEmbedElement.getSVGDocument](https://github.com/microsoft/TypeScript/blob/master/lib/lib.dom.d.ts#L6709)
- [HTMLIFrameElement.getSVGDocument](https://github.com/microsoft/TypeScript/blob/master/lib/lib.dom.d.ts#L7121)