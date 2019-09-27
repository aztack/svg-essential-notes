本章中的多数内容在Photoshop这类图像处理软件中都能找到对应工具

[Filter Effects Module Level 1](https://www.w3.org/TR/filter-effects/)
滤镜效果是一个单独的Module。滤镜标签的前缀`fe`=`filter effect`

[Compositing and Blending Level 1](https://www.w3.org/TR/compositing-1/#ltblendmodegt)也独立出来了单独的Module

[Filter Functions](https://www.w3.org/TR/filter-effects/#filter-functions)

```
<filter-function> = <blur()> | <brightness()> | <contrast()> | <drop-shadow()> |
<grayscale()> | <hue-rotate()> | <invert()> | <opacity()> | <sepia()> | <saturate()>
```

[Filter Effect DOM Interfaces](https://www.w3.org/TR/filter-effects/#DOMInterfaces)

<details><summary>Click</summary><p><ul>
<li>Interface SVGFilterElement</li>
<li>Interface SVGFilterPrimitiveStandardAttributes</li>
<li>Interface SVGFEBlendElement</li>
<li>Interface SVGFEColorMatrixElement</li>
<li>Interface SVGFEComponentTransferElement</li>
<li>Interface SVGComponentTransferFunctionElement</li>
<li>Interface SVGFEFuncRElement</li>
<li>Interface SVGFEFuncGElement</li>
<li>Interface SVGFEFuncBElement</li>
<li>Interface SVGFEFuncAElement</li>
<li>Interface SVGFECompositeElement</li>
<li>Interface SVGFEConvolveMatrixElement</li>
<li>Interface SVGFEDiffuseLightingElement</li>
<li>Interface SVGFEDistantLightElement</li>
<li>Interface SVGFEPointLightElement</li>
<li>Interface SVGFESpotLightElement</li>
<li>Interface SVGFEDisplacementMapElement</li>
<li>Interface SVGFEDropShadowElement</li>
<li>Interface SVGFEFloodElement</li>
<li>Interface SVGFEGaussianBlurElement</li>
<li>Interface SVGFEImageElement</li>
<li>Interface SVGFEMergeElement</li>
<li>Interface SVGFEMergeNodeElement</li>
<li>Interface SVGFEMorphologyElement</li>
<li>Interface SVGFEOffsetElement</li>
<li>Interface SVGFESpecularLightingElement</li>
<li>Interface SVGFETileElement</li>
<li>Interface SVGFETurbulenceElement</li>
</ul></p></details>

# How Filters Work 滤镜的工作原理
Filter primitives can be assembled to achieve a particular filter effect.
> SVG滤镜是通过将一组滤镜基元（filter primitives）组合起来达到某种滤镜效果。

# Creating a Drop Shadow
[Filter primitive <feDropShadow>](https://www.w3.org/TR/filter-effects/#feDropShadowElement)
## Establishing the Filter's Bounds
## Using <feGaussianBlur> for a Drop Shadow
[Filter primitive <feGaussianBlur>](https://www.w3.org/TR/filter-effects/#feGaussianBlurElement)
## Stroing, Chaning, and Merging Filter Results

# Creating a Glowing Filters
## The <feColorMatrix> Element
[Filter primitive <feColorMatrix>](https://www.w3.org/TR/filter-effects/#feColorMatrixElement)
## More About the <feColorMatrix> Element

# The <feImage> Filter
[Filter primitive <feImage>](https://www.w3.org/TR/filter-effects/#feImageElement)

[Filter primitive <feMerge>](https://www.w3.org/TR/filter-effects/#feMergeElement)

这个滤镜允许使用任意jpg、png、svg作为输入源

```xml
<svg>
  <defs>
    <filter ...>
      <feImage xlink:href="a.jpg" result="a" />
      <feMerge>
        <feMergeNode in="a" />
        <feMergeNode in="SourceGraphic" />
      </feMerge>
    </filter>
  </defs>
</svg>
```

# The \<feComponentTransfer> Filter 分量变换器
[Filter primitive feComponentTransfer](https://www.w3.org/TR/filter-effects/#feComponentTransferElement)
```xml
<svg>
  <defs>
    <filter ...>
      <feComponentTransfer in="sky" result="sky">
        <feFuncR type="linear" slope="1.5" intercept="0.2" />
        <feFuncG type="linear" slope="1.5" intercept="0.2" />
        <feFuncB type="linear" slope="3" intercept="0" />
      </feComponentTransfer>
    </filter>
  </defs>
</svg>
```

# The \<feComposite\> Filter
[Filter primitive <feComposite>](https://www.w3.org/TR/filter-effects/#feCompositeElement)

将两个源以operator指定的方式叠加起来

operator = "over | in | out | atop | xor | lighter | arithmetic"

# The \<feBlend\> Filters
[Filter primitive <feBlend>](https://www.w3.org/TR/filter-effects/#feBlendElement)

类似Photoshop中的图层叠加方式
[Compositing and Blending Level 1](https://www.w3.org/TR/compositing-1/#ltblendmodegt)

# The \<feFlood\> and \<feTitle\> Filters
[Filter primitive <feFlood>](https://www.w3.org/TR/filter-effects/#feFloodElement)

类似Photoshop的填充：可以填充纯色和图案

# Lighting Effects
## Diffuse Lighting
[Filter primitive <feDiffuseLighting>](https://www.w3.org/TR/filter-effects/#feDiffuseLightingElement)
## Specular Lighting
[Filter primitive <feSpecularLighting>](https://www.w3.org/TR/filter-effects/#feSpecularLightingElement)

# Accessing the Background
SVG1.1: [Accessing the background image](https://www.w3.org/TR/SVG11/filters.html#AccessingBackgroundImage)

# The \<feMorphology\> Element
[Filter primitive <feMorphology>](https://www.w3.org/TR/filter-effects/#feMorphologyElement)

# The \<feConvolveMatrix\> Element
[Filter primitive <feConvolveMatrix>](https://www.w3.org/TR/filter-effects/#feConvolveMatrixElement)

这个滤镜允许我们生成诸如模糊、锐化、浮雕和斜切这样的效果。它的原理是合并像素和它邻近的像素，生成结果像素值。

# The \<feDisplacementMap\> Element
[Filter primitive <feDisplacementMap>](https://www.w3.org/TR/filter-effects/#feDisplacementMapElement)

Photoshop中类似操作。可以制作将某个图案贴合在某个表面的效果。并不是直接叠加，而是根据图片通道信息对图案像素进行一定位移以达到逼真效果。

![image](https://user-images.githubusercontent.com/782871/65491690-236f9080-dee2-11e9-9134-0f95d1703915.png)

参考：[SVG Filter Effects: Conforming Text to Surface Texture with <feDisplacementMap>](https://tympanus.net/codrops/2019/02/12/svg-filter-effects-conforming-text-to-surface-texture-with-fedisplacementmap/)

# The \<feTurbulence\> Element
[Filter primitive <feTurbulence>](https://www.w3.org/TR/filter-effects/#feTurbulenceElement)
允许我们通过使用由 Ken Perlin 开发的方程，生成大理石、云彩等人 工纹理效果。这个方程被称作 [Perlin noise](https://en.wikipedia.org/wiki/Perlin_noise)

# Filter Reference Summary

参考：
- [Light source elements and properties](https://www.w3.org/TR/filter-effects/#LightSourceDefinitions)
    - [Light source feDistantLight](https://www.w3.org/TR/filter-effects/#feDistantLightElement)
    - [Light source fePointLight](https://www.w3.org/TR/filter-effects/#fePointLightElement)
    - [Light source feSpotLight](https://www.w3.org/TR/filter-effects/#feSpotLightElement)