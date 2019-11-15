[Paths](https://www.w3.org/TR/SVG2/paths.html#PathElement)

[EBNF grammar for path data](https://www.w3.org/TR/SVG2/paths.html#PathDataBNF)
<details><summary>Click</summary><p>

```
svg_path::= wsp* moveto? (moveto drawto_command*)?

drawto_command::=
    moveto
    | closepath
    | lineto
    | horizontal_lineto
    | vertical_lineto
    | curveto
    | smooth_curveto
    | quadratic_bezier_curveto
    | smooth_quadratic_bezier_curveto
    | elliptical_arc

moveto::=
    ( "M" | "m" ) wsp* coordinate_pair_sequence

closepath::=
    ("Z" | "z")

lineto::=
    ("L"|"l") wsp* coordinate_pair_sequence

horizontal_lineto::=
    ("H"|"h") wsp* coordinate_sequence

vertical_lineto::=
    ("V"|"v") wsp* coordinate_sequence

curveto::=
    ("C"|"c") wsp* curveto_coordinate_sequence

curveto_coordinate_sequence::=
    coordinate_pair_triplet
    | (coordinate_pair_triplet comma_wsp? curveto_coordinate_sequence)

smooth_curveto::=
    ("S"|"s") wsp* smooth_curveto_coordinate_sequence

smooth_curveto_coordinate_sequence::=
    coordinate_pair_double
    | (coordinate_pair_double comma_wsp? smooth_curveto_coordinate_sequence)

quadratic_bezier_curveto::=
    ("Q"|"q") wsp* quadratic_bezier_curveto_coordinate_sequence

quadratic_bezier_curveto_coordinate_sequence::=
    coordinate_pair_double
    | (coordinate_pair_double comma_wsp? quadratic_bezier_curveto_coordinate_sequence)

smooth_quadratic_bezier_curveto::=
    ("T"|"t") wsp* coordinate_pair_sequence

elliptical_arc::=
    ( "A" | "a" ) wsp* elliptical_arc_argument_sequence

elliptical_arc_argument_sequence::=
    elliptical_arc_argument
    | (elliptical_arc_argument comma_wsp? elliptical_arc_argument_sequence)

elliptical_arc_argument::=
    number comma_wsp? number comma_wsp? number comma_wsp
    flag comma_wsp? flag comma_wsp? coordinate_pair

coordinate_pair_double::=
    coordinate_pair comma_wsp? coordinate_pair

coordinate_pair_triplet::=
    coordinate_pair comma_wsp? coordinate_pair comma_wsp? coordinate_pair

coordinate_pair_sequence::=
    coordinate_pair | (coordinate_pair comma_wsp? coordinate_pair_sequence)

coordinate_sequence::=
    coordinate | (coordinate comma_wsp? coordinate_sequence)

coordinate_pair::= coordinate comma_wsp? coordinate

coordinate::= sign? number

sign::= "+"|"-"
number ::= ([0-9])+
flag::=("0"|"1")
comma_wsp::=(wsp+ ","? wsp*) | ("," wsp*)
wsp ::= (#x9 | #x20 | #xA | #xC | #xD)
```
</p></details>

<u>**复杂的路径肯定需要专业的矢量绘图软件来绘制。
但是，对于简单的icon可以手工绘制，方便制作动画效果**</u>

- 大写字母后跟绝对坐标
- 小写字母后跟相对坐标
- 坐标之间用逗号或者空格分隔
- <u>**字母与数字之间空格可以省略**</u> [svgo优化path data的部分代码](https://github.com/svg/svgo/blob/master/lib/svgo/tools.js#L77)

从EBNF中可以看到分隔符可以是一下几个

![wsp](https://user-images.githubusercontent.com/782871/65409485-6bc37b80-de1a-11e9-9ea3-1985ea3afef2.png)

分别对应于：

![wsp](https://user-images.githubusercontent.com/782871/65409719-09b74600-de1b-11e9-8599-f2d5ac3d6c93.png)

直线命令

命令 | 参数 | 说明
---|---|---
M m | x y | moveto(x,y)
L l | x y | lineto(x,y)
H h | x | moveto(x, currentY)
V v | y | moveto(currentX, y);

弧线命令
命令 | 参数 | 说明
---|---|---
A a | rx ry x-axis-rotation large-arc seep x y

贝塞尔曲线命令
命令 | 参数 | 说明
---|---|---
T t | x y |
Q q | x1 y1 x y
C c | x1 y1 x2 y2 x y
S s | x2 y2 x y


> All of the basic shapes described in Chapter 4 are really shorthand forms for the more general \<path\> element

> 第四章中介绍的所有基本形状都是\<path\>的简写。
>（所有基本形状都可以写成\<path\>的形式

# moveto, lineto, and closepath
略。

# Relative moveto and lineto 使用相对坐标的moveto和lineto

# Path Shortcuts 路径的快捷写法
略。见上面总结

# Elliptical Arc (椭圆弧)

绘制椭圆弧需要众多参数：

参数 | 说明
---|---
rx | x半径
ry | y半径
x-axis-rotation | x轴旋转角度
large-arc | 大弧为1，小弧为0
sweep | 正角为1，负角为0
x | 终点x
y | 终点y

![image](https://user-images.githubusercontent.com/782871/65411570-c6aba180-de1f-11e9-8541-bf1ce2f60d55.png)


# Converting from Other Arc Formats (从其他弧线格式转换)
略

# Bezier Curves (贝塞尔曲线)
雷诺汽车工程师皮埃尔·雷诺和雪铁龙数学家Paul de Casteljau开发的计算简便的生成曲线的方法。

控制点和曲线 关系的方式:想象一下线是由柔性金属制造的。控制点内部是一个磁铁，与控制点越近， 吸引力越强。

## Quadratic Bézier Curves (二次贝塞尔曲线)

-[贝塞尔曲线原理(实现图真漂亮)](https://www.jianshu.com/p/8f82db9556d2)
-[Animated Bézier Curves](sample/animated-bezier-curve/README.md)



## Cubic Bézier Curves (三次贝塞尔曲线)

# Paths and Filling (路径和填充)

# The \<mark\> element (标记元素)

```xml
<defs>
  <marker id="mStart"
  refX=""
  refY=""
  viewBox=""
  preserveAspectRatio=""
  >...</marker>
</defs>
<path d="..."
  marker-start="url(#mStart)"
  marker-mid="url(#mMid)"
  marker-end="url(#mEnd)"
/>
```

# Marker Miscellanea (标记记录)

```xml
<path d="..."
  marker="url(#mStartMidEnd)"
/>
```

```css
/* 为所有path设置marker */
path {marker: url(#start)}
/* 防止循环引用 */
marker#start path {marker: none}
```