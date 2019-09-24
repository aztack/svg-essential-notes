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

# Repeated Action

# Animating Complex Attributes

# Specifying Multiple Values

# Timing of Multistage Animations

# The \<set> Element

# The \<animateTransform> Element

# The \<animateMotion> Element

# Specifying Key Points and Times for Motion

# Animating SVG with CSS
## Animation Properties
## Setting Animation Key Frames
## Animating Movement with CSS

参考：
- [SVG1.1 Animation Spec](https://www.w3.org/TR/SVG11/animate.html)
- [SMIL Animation Spec](https://www.w3.org/TR/2001/REC-smil-animation-20010904/)
- [Can I Use 'SMIL'](https://caniuse.com/#search=SMIL)