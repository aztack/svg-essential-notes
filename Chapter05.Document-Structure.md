# Structure and Presetation

# Using style with SVG

# Grouping and Referecing Objects
## \<g> 元素

> container element
An element which can have graphics elements and other container elements as child elements. Specifically: ‘a’, ‘clipPath’, ‘defs’, ‘g’, ‘marker’, ‘mask’, ‘pattern’, ‘svg’, ‘switch’, ‘symbol’ and ‘unknown’.
The ‘g’ element is a container element for grouping together related graphics elements.

## [\<use>元素](https://www.w3.org/TR/SVG2/struct.html#UseElement)

用于元素复用。克隆的元素继承use元素的style属性。
克隆的元素与被克隆元素保持同步，实时反映其变化。

## [\<defs>元素](https://www.w3.org/TR/SVG2/struct.html#DefsElement)

组织g和symbol等元素，不被渲染

## [\<symbol>元素](https://www.w3.org/TR/SVG2/struct.html#SymbolElement)

> The ‘symbol’ element is used to define graphical templates which can be instantiated by a ‘use’ element but which are not rendered directly.

> A ‘symbol’ establishes a nested coordinate system for the graphics it contains. When a symbol is instantiated as the referenced element of a ‘use’ element, it is therefore rendered very similarly to a nested ‘svg’ element.

\<use>克隆被引用的元素。

\<symbol>相当于一个模板。只有在use引用是才初始化。

## \<image>元素

\<image>标签可以引用另外一个svg或者位图