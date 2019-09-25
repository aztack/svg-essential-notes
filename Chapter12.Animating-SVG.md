# Animation Basics SVG动画基础

```html
<rect x="10" y="10" width="200" height="20" stroke="black" fill="none">
  <animate attributeName="width" attributeType="XML"
    from="200" to="20" begin="0s" dur="5s" fill="freeze" />
</rect>

<!-- Q: 如何控制开始时间？ -->
<rect x="10" y="10" width="20" height="20"
style="stroke: black; fill: green; style: fill-opacity: 0.25;">
  <!-- 开始时间begin="ns" -->
  <animate attributeName="width" attributeType="XML"
    from="20" to="200" begin="0s" dur="8s" fill="freeze"/>
  <animate attributeName="height" attributeType="XML"
    from="20" to="150" begin="0s" dur="8s" fill="freeze"/>
  <animate attributeName="fill-opacity" attributeType="CSS"
    from="0.25" to="1" begin="0s" dur="3s" fill="freeze"/>
  <animate attributeName="fill-opacity" attributeType="CSS"
    from="1" to="0.25" begin="3s" dur="3s" fill="freeze"/>
</rect>
```

# How Time Is Measured SVG中如何计时？

SVG’s animation clock starts ticking when the SVG has finished loading, and it stops ticking when the user leaves the page
> SVG片段加载结束后开始计时。用户离开页面停止计时。

- begin=开始时间
- dur=时长
- end=结束时间（结束时间可以小于开始时间加时长，此时动画提前结束）
- 默认单位是『秒』

# Synchronizing Animation 同步多个动画

通过引用动画的id加上`.start`或`.end`

```html
<circle cx="60" cy="60" r="30" style="fill: #f9f; stroke: gray;">
  <animate id="c1" attributeName="r" attributeType="XML"
      begin="0s" dur="4s" from="30" to="10" fill="freeze"/>
</circle>
<circle cx="120" cy="60" r="10" style="fill: #9f9; stroke: gray;">
  <animate attributeName="r" attributeType="XML"
      begin="c1.end" dur="4s" from="10" to="30" fill="freeze"/>
</circle>
```
还可以加上偏移量:`id.start+1.25s`

```html
<circle cx="60" cy="60" r="30" style="fill: #f9f; stroke: gray;">
  <animate id="c1" attributeName="r" attributeType="XML"
    begin="0s" dur="4s" from="30" to="10" fill="freeze"/>
</circle>
<circle cx="120" cy="60" r="10" style="fill: #9f9; stroke: gray;">
  <animate attributeName="r" attributeType="XML"
    begin="c1.begin+1.25s" dur="4s" from="10" to="30" fill="freeze"/>
</circle>
```

# Repeated Action 重复动作

```html
<circle cx="60" cy="60" r="30" style="fill: none; stroke: red;">
  <animate attributeName="cx" attributeType="XML"
    begin="0s" dur="5s" repeatCount="2"
    from="60" to="260" fill="freeze"/>
</circle>
<circle cx="260" cy="90" r="30" style="fill: #ccf; stroke: black;">
  <animate attributeName="cx" attributeType="XML"
    begin="0s" dur="5s" repeatDur="8s"
    from="260" to="60" fill="freeze"/>
</circle>
```

repeatCount和repeatDur哪个先到就用哪个。
与上面类似，可以在重复几次后在延时几秒执行下一个动画：

```html
<circle cx="60" cy="60" r="15" style="fill: none; stroke: red;">
  <animate id="circleAnim" attributeName="cx" attributeType="XML"
    begin="0s" dur="5s" repeatCount="3"
    from="60" to="260" fill="freeze"/>
</circle>
<rect x="230" y="80" width="30" height="30" style="fill: #ccf; stroke: black;">
  <animate attributeName="x" attributeType="XML"
    begin="circleAnim.repeat(1)+2.5s" dur="5s"
    from="230" to="30" fill="freeze"/>
</rect>
```

# Animating Complex Attributes 对复杂属性的动画
> 只要可插值的属性都可以做动画。颜色是由数值表示的，自然可以插值做动画。
> 对于不能插值的属性：参见下面的\<set>

下面将`fill`从red变为blue。
```html
<svg width="150" height="100">
  <circle cx="60" cy="60" r="30"
    style="fill: #ff9; stroke: gray; stroke-width: 10;">
    <animate attributeName="fill"
      begin="2s" dur="4s" from="#ff9" to="red" fill="freeze"/>
    <animate attributeName="stroke"
      begin="2s" dur="4s" from="gray" to="blue" fill="freeze"/>
  </circle>
</svg>
```
指定颜色空间
```html
< filter color-interpolation-filters="sRGB | linearRGB" .../>
```

# Specifying Multiple Values 指定多个值

通过`values`指定分号分隔的多个值。
> 这几个值等分在插值过程中？是的，见下节

```html
<svg width="100" height="100">
  <circle cx="50" cy="50" r="30"
    style="fill: #ff9; stroke:black;">
    <animate attributeName="fill"
      begin="2s" dur="4s" values="#ff9;#99f;#f99;#9f9"
      fill="freeze"/>
  </circle>
</svg>
```

# Timing of Multistage Animations 多阶段动画的时间设定
[keyTimes = "\<list>"](https://www.w3.org/TR/SVG11/animate.html#KeyTimesAttribute)

[calcMode = "discrete | linear | paced | spline"](https://www.w3.org/TR/SVG11/animate.html#CalcModeAttribute)

[keySplines = "\<list>"](https://www.w3.org/TR/SVG11/animate.html#KeySplinesAttribute)

```html
<animate ... keyTimes="0;.5;1" calcMode="paced | linear | discrete | spline" keySplines="...">
```

# The \<set> Element \<set>元素

下面4.5秒后将文字显示出来

```html
<svg width="150" height="100">
  <circle cx="60" cy="60" r="30" style="fill: #ff9; stroke: gray;">
    <animate id="c1" attributeName="r" attributeType="XML"
      begin="0s" dur="4s" from="30" to="0" fill="freeze"/>
  </circle>

  <text text-anchor="middle" x="60" y="60" style="visibility: hidden;">
    <set attributeName="visibility" attributeType="CSS"
      to="visible" begin="4.5s" dur="1s" fill="freeze"/>
    All gone!
  </text>
</svg>
```

# The \<animateTransform> Element \<animateTransform>元素

\<animate>元素并没有提供旋转、平移、缩放、斜切功能。这些功能都用专门的\<animateTransform>元素来实现。

```html
<g transform="translate(100,60)">
  <rect x="-10" y="-10" width="20" height="20" style="fill: #ff9; stroke: black;">
    <animateTransform attributeType="XML" attributeName="transform"
      type="scale" from="1" to="4 2" begin="0s" dur="4s" fill="freeze"/>
  </rect>
</g>
```

多个\<animateTransform>可以同时使用。注意下面的`additive="sum"`
[Attributes that control whether animations are additive](https://www.w3.org/TR/SVG11/animate.html#AdditionAttributes)
```html
<svg width="200" height="100">
  <g transform="translate(100, 60)">
  <rect x="-10" y="-10" width="20" height="20"
    style="fill: #ff9; stroke: black;">
    <animateTransform attributeName="transform" attributeType="XML"
      type="scale" from="1" to="4 2"
      additive="sum" begin="0s" dur="4s" fill="freeze"/>
    <animateTransform attributeName="transform" attributeType="XML"
      type="rotate" from="0" to="45"
      additive="sum" begin="0s" dur="4s" fill="freeze"/>
  </rect>
  </g>
</svg>
```

# The \<animateMotion> Element \<animateMotion>元素
简单在两点之间移动
```html
<svg width="120" height="100" viewBox="0 0 120 100">
  <g>
    <rect x="0" y="0" width="30" height="30" style="fill: #ccc;"/>
    <circle cx="30" cy="30" r="15" style="fill: #cfc; stroke: green;"/>
    <animateMotion from="0,0" to="60,30" dur="4s" fill="freeze"/>
  </g>
</svg>
```
沿path移动，并垂直曲线。注意`rotate`属性。
```html
<svg width="250" height="250">
  <!-- show the path along which the triangle will move -->
  <path d="M50,125 C 100,25 150,225, 200, 125"
    style="fill: none; stroke: blue;"/>

  <!-- Triangle to be moved along the motion path.
    It is defined with an upright orientation with the base of
    the triangle centered horizontally just above the origin. -->
  <path d="M-10,-3 L10,-3 L0,-25z" style="fill: yellow; stroke: red;" >
    <animateMotion
      path="M50,125 C 100,25 150,225, 200, 125"
      rotate="auto"
      dur="6s" fill="freeze"/>
  </path>
</svg>
```
# Specifying Key Points and Times for Motion 为动作指定关键点和时间
略
# Animating SVG with CSS
## Animation Properties
## Setting Animation Key Frames
## Animating Movement with CSS

参考：
- [SVG1.1 Animation Spec](https://www.w3.org/TR/SVG11/animate.html)
- [SMIL Animation Spec](https://www.w3.org/TR/2001/REC-smil-animation-20010904/)
- [Can I Use 'SMIL'](https://caniuse.com/#search=SMIL)