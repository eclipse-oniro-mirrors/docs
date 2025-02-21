# SVG标签说明

SVG(Scalable Vector Graphics)是可缩放矢量图形，它是一种基于XML(可扩展标记语言)的图形格式，用于描述二维图形和图像。Image组件支持的SVG矢量图涉及的元素和属性范围受限，为SVG1.1规范的部分功能。相关的元素和属性请参考如下描述：

## 基础形状

基础形状标签包括：\<rect\>、\<circle\>、\<ellipse\>、\<line\>、\<polyline\>、\<polygon\>、\<path\>

>  **说明：**
>
>  基础标签支持通用属性
>  id、fill、fill-rule、fill-opacity、stroke、stroke-dasharray、stroke-dashoffset、stroke-opacity、stroke-width、stroke-linecap、stroke-linejoin、stroke-miterlimit、opacity、transform、clip-path、clip-rule

| 元素 | 说明 | 特有属性 |
| :-------- | :-------- | :-------- |
| \<rect\> | 矩形 | x: x轴方向偏移分量； <br>y: y轴方向偏移分量；<br>width: 宽度； <br>height: 高度；<br>rx: 圆角x轴半径； <br>ry: 圆角y轴半径|
| \<circle\> | 圆形 | cx: 圆心x轴坐标；<br> cy: 圆心y轴坐标；<br> r: 圆形半径 |  |
| \<ellipse\> | 椭圆 | cx: x轴坐标；<br> cy: y轴坐标；<br> rx: x轴半径；<br> ry: y轴半径<br> |  |
| \<line\> | 线 | x1: 起点x轴坐标；<br> y1: 起点y轴坐标；<br> x2: 终点x轴坐标；<br> y2: 终点y轴坐标 |  |
| \<polyline\> | 折线 | points: 顶点坐标 |  |
| \<polygon\> | 多边形 | points：顶点坐标 |  |
| \<path\> | 路径 | d：路径 |  |

## 图形效果

### 滤镜

滤镜标签包括：\<filter\>、\<feOffset\>、\<feGaussianBlur\>、\<feBlend\>、\<feComposite\>、\<feColorMatrix\>、\<feFlood\>，其中\<filter\>定义滤镜范围，其它标签定义滤镜效果。

| 元素 | 说明 | 特有属性 |
| :-------- | :-------- | :-------- |
| \<filter\> | 定义滤镜 | x: 滤镜区域x轴偏移分量，默认值为0； <br>y：滤镜区域y轴偏移分量，默认值为0； <br>width: 滤镜区域宽； <br>height: 滤镜区域高|
| \<feOffset\> | 定义沿x、y方向偏移距离 | in: 滤镜原始输入（仅支持SourceGraphic、SourceAlpha、其它滤镜效果的result）;<br> result: 经过滤镜处理之后的输出，可以作为下一个滤镜的输入, dx, dy |
| \<feGaussianBlur\> | 定义高斯模糊效果 | in: 滤镜原始输入（仅支持SourceGraphic、SourceAlpha、其它滤镜效果的result）;<br> result: 经过滤镜处理之后的输出，可以作为下一个滤镜的输入, edgemode, stddeviation|
| \<feBlend\> | 定义两张输入图像混合模式 | in: 滤镜原始输入（仅支持SourceGraphic、SourceAlpha、其它滤镜效果的result）;<br> result: 经过滤镜处理之后的输出，可以作为下一个滤镜的输入；<br>in2：第二图源（仅支持SourceGraphic、SourceAlpha、其它滤镜效果的result）, mode |
| \<feComposite\> | 定义两张输入图像合成方式，<br>算法：result = k1 * in * in2 + k2 * in + k3 * in2 + k4 | in：滤镜原始输入（仅支持SourceGraphic、SourceAlpha、其它滤镜效果的result）<br>in2：第二图源（仅支持SourceGraphic、SourceAlpha、其它滤镜效果的result）, operator( over \| in \| out \| atop \| xor \| lighter \| arithmetic ), k1, k2, k3, k4 |  |
| \<feColorMatrix\> | 基于转换矩阵对颜色进行变换 | in: 滤镜原始输入（仅支持SourceGraphic、SourceAlpha、其它滤镜效果的result）；<br> result: 经过滤镜处理之后的输出，可以作为下一个滤镜的输入；<br>type ( matrix \| saturate \| hueRotate)、 values |
| \<feFlood\> | 定义填充颜色和透明度 | in: 滤镜原始输入（仅支持SourceGraphic、SourceAlpha、其它滤镜效果的result）；<br> result: 经过滤镜处理之后的输出，可以作为下一个滤镜的输入；flood-color、flood-opacity |

### 遮罩

遮罩标签：\<mask\>
| 元素 | 说明 | 特有属性 |
| :-------- | :-------- | :-------- |
| \<mask\> | 定义遮罩 | x: 遮罩区域x轴偏移分量； <br>y: 遮罩区域y轴偏移分量； <br>width: 遮罩区域宽； <br>height: 遮罩区域高 |

### 裁剪

裁剪标签：\<clippath\>
| 元素 | 说明 | 特有属性 |
| :-------- | :-------- | :-------- |
| \<clippath\> | 定义一条剪切路径 | x: 裁剪区域x轴偏移分量；<br>y: 裁剪区域y轴偏移分量； <br>width: 裁剪区域宽； <br>height: 裁剪区域高 |

### 图案

裁剪标签：\<pattern\>
| 元素 | 说明 | 特有属性 |
| :-------- | :-------- | :-------- |
| \<pattern\> | 定义填充图案 | x: 填充区域x轴偏移分量； <br>y: 填充区域y轴偏移分量； <br>width: 填充区域宽； <br>height: 填充区域高 |

### 渐变色

渐变色相关的标签包括：\<linearGradient\>、\<racialGradient\>、\<stop\>

| 元素 | 说明 | 特有属性 |
| :-------- | :-------- | :-------- |
| \<linearGradient\> | 线性渐变 | x1, y1, x2, y2 |
| \<racialGradient\> | 放射渐变 | fx, fy, cx, cy, r |
| \<stop\> | 色阶 | offset、stop-color |

## 静态图片

图片标签：\<image\>
| 元素 | 说明 | 特有属性 |
| :-------- | :-------- | :-------- |
| \<image\> | 用于图像显示 | x: 图像x轴偏移；<br> y：图像y轴偏移；<br> width: 图像宽；<br> height：图像高；<br> href(支持: jpg、jpeg、png、bmp、webp、heic、base64,不支持svg) |

## 动画

动画标签：\<animate\>、\<animateTransform\>
| 元素 | 说明 | 特有属性 |
| :-------- | :-------- | :-------- |
| \<animate\> | 定义元素属性动画 | attributeName: 定义可动画属性，取值：( cx \| cy \| r \| fill \| stroke \| fill-opacity \| stroke-opacity \| stroke-miterlimit )；<br>begin: 定义动画起始时间；<br> dur: 定义动画持续时间；<br>from: 定义起始值；<br>to: 定义结束值；<br>fill: 定义动画结尾状态；<br> calcMode: 定义插值；<br> keyTimes、values、keySplines  |
| \<animateTransform\> | 定义元素变形动画 | attributeName:  定义可动画属性，取值：transform；<br/>type: 属性定义转换类型取值：( translate \| scale \| rotate \| skewX \| skewY )；<br>begin: 定义动画起始时间；<br> dur: 定义动画持续时间；<br>from: 定义起始值；<br>to: 定义结束值；<br>fill: 定义动画结尾状态；<br> calcMode: 定义插值；<br> keyTimes、values、keySplines |

## 其它

除了标识图形图像效果的标签，还支持分组等标签，分别有：
\<svg\>、\<g\>、\<use\>、\<defs\>

| 元素 | 说明 | 特有属性 | 通用属性 |
| :-------- | :-------- | :-------- | :-------- |
| \<svg\> | 容器，定义个svg片段 | x: x轴偏移分量；<br> y: y轴偏移分量；<br> width: 宽度； <br>height：高度；<br> viewBox：视口| fill、fill-rule、fill-opacity、stroke、stroke-dasharray、stroke-dashoffset、stroke-opacity、stroke-width、stroke-linecap、stroke-linejoin、stroke-miterlimit、transform |
| \<g\> | 分组 | x：x轴偏移分量；<br> y：y轴偏移分量；<br> width: 宽度；<br> height：高度 | fill、fill-rule、fill-opacity、stroke、stroke-dasharray、stroke-dashoffset、stroke-opacity、stroke-width、stroke-linecap、stroke-linejoin、stroke-miterlimit、transform |
| \<use\> | 复用已有元素 | x：x轴偏移分量；<br> y：y轴偏移分量；href: 目标元素 | fill、fill-rule、fill-opacity、stroke、stroke-dasharray、stroke-dashoffset、stroke-opacity、stroke-width、stroke-linecap、stroke-linejoin、stroke-miterlimit、transform |
| \<defs\> | 定义可复用对象 | | |

**说明：** 当前支持的颜色值格式包括：#rrggbb、rgb()、rgba()