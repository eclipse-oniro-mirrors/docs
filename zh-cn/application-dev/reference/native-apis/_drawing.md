# Drawing


Drawing模块提供包括2D图形渲染、文字绘制和图片显示等功能函数。


提供2D绘制功能。


@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing


**起始版本：**


8


## 汇总


### 文件

| 文件名称                                                     | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [drawing_bitmap.h](drawing__bitmap_8h.md)                    | 文件中定义了与位图相关的功能函数。<br>引用文件：<native_drawing/drawing_bitmap.h> <br>库：libnative_drawing.so                          |
| [drawing_brush.h](drawing__brush_8h.md)                      | 文件中定义了与画刷相关的功能函数。<br>引用文件：<native_drawing/drawing_brush.h> <br>库：libnative_drawing.so                       |
| [drawing_canvas.h](drawing__canvas_8h.md)                    | 文件中定义了与画布相关的功能函数。<br>引用文件：<native_drawing/drawing_canvas.h> <br>库：libnative_drawing.so                          |
| [drawing_color.h](drawing__color_8h.md)                      | 文件中定义了与颜色相关的功能函数。<br>引用文件：<native_drawing/drawing_color.h> <br>库：libnative_drawing.so                           |
| [drawing_font_collection.h](drawing__font__collection_8h.md) | 定义绘制模块中与fontCollection相关的函数。<br>引用文件：<native_drawing/drawing_font_collection.h> <br>库：libnative_drawing.so                   |
| [drawing_path.h](drawing__path_8h.md)                        | 文件中定义了与自定义路径相关的功能函数。<br>引用文件：<native_drawing/drawing_path.h> <br>库：libnative_drawing.so                     |
| [drawing_pen.h](drawing__pen_8h.md)                          | 文件中定义了与画笔相关的功能函数。<br>引用文件：<native_drawing/drawing_pen.h> <br>库：libnative_drawing.so                           |
| [drawing_text_declaration.h](drawing__text__declaration_8h.md) | 提供2d drawing文本相关的数据结构声明。<br>引用文件：<native_drawing/drawing_text_declaration.h> <br>库：libnative_drawing.so                       |
| [drawing_text_typography.h](drawing__text__typography_8h.md) | 定义绘制模块中排版相关的函数。<br>引用文件：<native_drawing/drawing_text_typography.h> <br>库：libnative_drawing.so                               |
| [drawing_types.h](drawing__types_8h.md)                      | 文件中定义了用于绘制2d图形的数据类型，包括画布、画笔、画刷、位图和路径。<br>引用文件：<native_drawing/drawing_types.h> <br>库：libnative_drawing.so |


### 结构体

| 结构体名称                                                   | 描述                                                     |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| [OH_Drawing_BitmapFormat](_o_h___drawing___bitmap_format.md) | 结构体用于描述位图像素的格式，包括颜色类型和透明度类型。 |


### 类型定义

| 类型定义名称                                                | 描述                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| [OH_Drawing_FontCollection](#oh_drawing_fontcollection)     | OH_Drawing_FontCollection用于加载字体。                      |
| [OH_Drawing_Typography](#oh_drawing_typography)             | OH_Drawing_Typography用于管理排版的布局和显示等。            |
| [OH_Drawing_TextStyle](#oh_drawing_textstyle)               | OH_Drawing_TextStyle用于管理字体颜色、装饰等。               |
| [OH_Drawing_TypographyStyle](#oh_drawing_typographystyle)   | OH_Drawing_TypographyStyle用于管理排版风格，如文字方向等。   |
| [OH_Drawing_TypographyCreate](#oh_drawing_typographycreate) | OH_Drawing_TypographyCreate用于创建OH_Drawing_Typography。   |
| [OH_Drawing_Canvas](#oh_drawing_canvas)                     | OH_Drawing_Canvas定义为一块矩形的画布，可以结合画笔和画刷在上面绘制各种形状、图片和文字。 |
| [OH_Drawing_Pen](#oh_drawing_pen)                           | OH_Drawing_Pen定义为画笔，画笔用于描述绘制图形轮廓的样式和颜色。 |
| [OH_Drawing_Brush](#oh_drawing_brush)                       | OH_Drawing_Brush定义为画刷，画刷用于描述填充图形的样式和颜色。 |
| [OH_Drawing_Path](#oh_drawing_path)                         | OH_Drawing_Path定义为路径，路径用于自定义设置各种形状。      |
| [OH_Drawing_Bitmap](#oh_drawing_bitmap)                     | OH_Drawing_Bitmap定义为位图，位图是一块内存，内存中包含了描述一张图片的像素数据。 |


### 枚举

| 枚举名称                                                     | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [OH_Drawing_PenLineCapStyle](#oh_drawing_penlinecapstyle) { LINE_FLAT_CAP, LINE_SQUARE_CAP, LINE_ROUND_CAP } | 枚举集合定义了画笔笔帽的样式，即画笔在绘制线段时，在线段头尾端点的样式。 |
| [OH_Drawing_PenLineJoinStyle](#oh_drawing_penlinejoinstyle) { LINE_MITER_JOIN, LINE_ROUND_JOIN, LINE_BEVEL_JOIN } | 枚举集合定义了线条转角的样式，即画笔在绘制折线段时，在折线转角处的样式。 |
| [OH_Drawing_TextDirection](#oh_drawing_textdirection) { TEXT_DIRECTION_RTL, TEXT_DIRECTION_LTR } | 文字方向。                                                   |
| [OH_Drawing_TextAlign](#oh_drawing_textalign) { TEXT_ALIGN_LEFT, TEXT_ALIGN_RIGHT, TEXT_ALIGN_CENTER, TEXT_ALIGN_JUSTIFY,   TEXT_ALIGN_START, TEXT_ALIGN_END } | 文字对齐方式。                                               |
| [OH_Drawing_FontWeight](#oh_drawing_fontweight) {  FONT_WEIGHT_100, FONT_WEIGHT_200, FONT_WEIGHT_300, FONT_WEIGHT_400,   FONT_WEIGHT_500, FONT_WEIGHT_600, FONT_WEIGHT_700, FONT_WEIGHT_800,  FONT_WEIGHT_900  } | 字重。                                                       |
| [OH_Drawing_TextBaseline](#oh_drawing_textbaseline) { TEXT_BASELINE_ALPHABETIC, TEXT_BASELINE_IDEOGRAPHIC } | 基线位置。                                                   |
| [OH_Drawing_TextDecoration](#oh_drawing_textdecoration) { TEXT_DECORATION_NONE = 0x0, TEXT_DECORATION_UNDERLINE = 0x1, TEXT_DECORATION_OVERLINE = 0x2, TEXT_DECORATION_LINE_THROUGH = 0x4 } | 文本装饰。                                                   |
| [OH_Drawing_FontStyle](#oh_drawing_fontstyle) { FONT_STYLE_NORMAL, FONT_STYLE_ITALIC } | 区分字体是否为斜体。                                         |
| [OH_Drawing_ColorFormat](#oh_drawing_colorformat) {  COLOR_FORMAT_UNKNOWN, COLOR_FORMAT_ALPHA_8, COLOR_FORMAT_RGB_565, COLOR_FORMAT_ARGB_4444,   COLOR_FORMAT_RGBA_8888, COLOR_FORMAT_BGRA_8888 } | OH_Drawing_ColorFormat用于描述位图像素的存储格式。           |
| [OH_Drawing_AlphaFormat](#oh_drawing_alphaformat) { ALPHA_FORMAT_UNKNOWN, ALPHA_FORMAT_OPAQUE, ALPHA_FORMAT_PREMUL, ALPHA_FORMAT_UNPREMUL } | OH_Drawing_AlphaFormat用于描述位图像素的透明度分量。         |


### 函数

| 函数名称                                                     | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [OH_Drawing_BitmapCreate](#oh_drawing_bitmapcreate) (void)   | 创建一个位图对象。                                           |
| [OH_Drawing_BitmapDestroy](#oh_drawing_bitmapdestroy) ([OH_Drawing_Bitmap](#oh_drawing_bitmap) \*) | 销毁位图对象并回收该对象占有内存。                           |
| [OH_Drawing_BitmapBuild](#oh_drawing_bitmapbuild) ([OH_Drawing_Bitmap](#oh_drawing_bitmap) \*, const uint32_t width, const uint32_t height, const [OH_Drawing_BitmapFormat](_o_h___drawing___bitmap_format.md) \*) | 初始化位图对象的宽度和高度，并且为该位图设置像素格式。       |
| [OH_Drawing_BitmapGetWidth](#oh_drawing_bitmapgetwidth) ([OH_Drawing_Bitmap](#oh_drawing_bitmap) \*) | 获取指定位图的宽度。                                         |
| [OH_Drawing_BitmapGetHeight](#oh_drawing_bitmapgetheight) ([OH_Drawing_Bitmap](#oh_drawing_bitmap) \*) | 获取指定位图的高度。                                         |
| [OH_Drawing_BitmapGetPixels](#oh_drawing_bitmapgetpixels) ([OH_Drawing_Bitmap](#oh_drawing_bitmap) \*) | 获取指定位图的像素地址，可以通过像素地址获取到位图的像素数据。 |
| [OH_Drawing_BrushCreate](#oh_drawing_brushcreate) (void)     | 创建一个画刷对象。                                           |
| [OH_Drawing_BrushDestroy](#oh_drawing_brushdestroy) ([OH_Drawing_Brush](#oh_drawing_brush) \*) | 销毁画刷对象并回收该对象占有的内存。                         |
| [OH_Drawing_BrushIsAntiAlias](#oh_drawing_brushisantialias) (const [OH_Drawing_Brush](#oh_drawing_brush) \*) | 获取画刷是否设置抗锯齿属性，如果为真则说明画刷会启用抗锯齿功能，在绘制图形时会对图形的边缘像素进行半透明的模糊处理。 |
| [OH_Drawing_BrushSetAntiAlias](#oh_drawing_brushsetantialias) ([OH_Drawing_Brush](#oh_drawing_brush) \*, bool) | 设置画刷的抗锯齿属性，设置为真则画刷在绘制图形时会对图形的边缘像素进行半透明的模糊处理。 |
| [OH_Drawing_BrushGetColor](#oh_drawing_brushgetcolor) (const [OH_Drawing_Brush](#oh_drawing_brush) \*) | 获取画刷的颜色属性，颜色属性描述了画刷填充图形时使用的颜色，用一个32位（ARGB）的变量表示。 |
| [OH_Drawing_BrushSetColor](#oh_drawing_brushsetcolor) ([OH_Drawing_Brush](#oh_drawing_brush) \*, uint32_t color) | 设置画刷的颜色属性，颜色属性描述了画刷填充图形时使用的颜色，用一个32位（ARGB）的变量表示。 |
| [OH_Drawing_CanvasCreate](#oh_drawing_canvascreate) (void)   | 创建一个画布对象。                                           |
| [OH_Drawing_CanvasDestroy](#oh_drawing_canvasdestroy) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*) | 销毁画布对象并回收该对象占有的内存。                         |
| [OH_Drawing_CanvasBind](#oh_drawing_canvasbind) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*, [OH_Drawing_Bitmap](#oh_drawing_bitmap) \*) | 将一个位图对象绑定到画布中，使得画布绘制的内容输出到位图中（即CPU渲染）。 |
| [OH_Drawing_CanvasAttachPen](#oh_drawing_canvasattachpen) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*, const [OH_Drawing_Pen](#oh_drawing_pen) \*) | 设置画笔给画布，画布将会使用设置画笔的样式和颜色去绘制图形形状的轮廓。 |
| [OH_Drawing_CanvasDetachPen](#oh_drawing_canvasdetachpen) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*) | 去除掉画布中的画笔，使用后画布将不去绘制图形形状的轮廓。     |
| [OH_Drawing_CanvasAttachBrush](#oh_drawing_canvasattachbrush) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*, const [OH_Drawing_Brush](#oh_drawing_brush) \*) | 设置画刷给画布，画布将会使用设置的画刷样式和颜色去填充绘制的图形形状。 |
| [OH_Drawing_CanvasDetachBrush](#oh_drawing_canvasdetachbrush) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*) | 去除掉画布中的画刷，使用后画布将不去填充图形形状。           |
| [OH_Drawing_CanvasSave](#oh_drawing_canvassave) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*) | 保存当前画布的状态（画布矩阵）到一个栈顶。                   |
| [OH_Drawing_CanvasRestore](#oh_drawing_canvasrestore) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*) | 恢复保存在栈顶的画布状态（画布矩阵）。                       |
| [OH_Drawing_CanvasDrawLine](#oh_drawing_canvasdrawline) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*, float x1, float y1, float x2, float y2) | 画一条直线段。                                               |
| [OH_Drawing_CanvasDrawPath](#oh_drawing_canvasdrawpath) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*, const [OH_Drawing_Path](#oh_drawing_path) \*) | 画一个自定义路径。                                           |
| [OH_Drawing_CanvasClear](#oh_drawing_canvasclear) ([OH_Drawing_Canvas](#oh_drawing_canvas) \*, uint32_t color) | 使用指定颜色去清空画布。                                     |
| [OH_Drawing_ColorSetArgb](#oh_drawing_colorsetargb) (uint32_t alpha, uint32_t red, uint32_t green, uint32_t blue) | 将4个变量（分别描述透明度、红色、绿色和蓝色）转化为一个描述颜色的32位（ARGB）变量。 |
| [OH_Drawing_CreateFontCollection](#oh_drawing_createfontcollection) (void) | 创建OH_Drawing_FontCollection。                              |
| [OH_Drawing_DestroyFontCollection](#oh_drawing_destroyfontcollection) ([OH_Drawing_FontCollection](#oh_drawing_fontcollection) \*) | 释放被OH_Drawing_FontCollection对象占据的内存。              |
| [OH_Drawing_PathCreate](#oh_drawing_pathcreate) (void)       | 创建一个路径对象。                                           |
| [OH_Drawing_PathDestroy](#oh_drawing_pathdestroy) ([OH_Drawing_Path](#oh_drawing_path) \*) | 销毁路径对象并回收该对象占有的内存。                         |
| [OH_Drawing_PathMoveTo](#oh_drawing_pathmoveto) ([OH_Drawing_Path](#oh_drawing_path) \*, float x, float y) | 设置自定义路径的起始点位置。                                 |
| [OH_Drawing_PathLineTo](#oh_drawing_pathlineto) ([OH_Drawing_Path](#oh_drawing_path) \*, float x, float y) | 添加一条从路径的最后点位置到目标点位置的线段。               |
| [OH_Drawing_PathArcTo](#oh_drawing_patharcto) ([OH_Drawing_Path](#oh_drawing_path) \*, float x1, float y1, float x2, float y2, float startDeg, float sweepDeg) | 给路径添加一段弧线，绘制弧线的方式为角度弧，该方式首先会指定一个矩形边框，矩形边框会包裹椭圆， 然后会指定一个起始角度和扫描度数，从起始角度扫描截取的椭圆周长一部分即为绘制的弧线。另外会默认添加一条从路径的最后点位置到弧线起始点位置的线段。 |
| [OH_Drawing_PathQuadTo](#oh_drawing_pathquadto) ([OH_Drawing_Path](#oh_drawing_path) \*, float ctrlX, float ctrlY, float endX, float endY) | 添加一条从路径最后点位置到目标点位置的二阶贝塞尔圆滑曲线。   |
| [OH_Drawing_PathCubicTo](#oh_drawing_pathcubicto) ([OH_Drawing_Path](#oh_drawing_path) \*, float ctrlX1, float ctrlY1, float ctrlX2, float ctrlY2, float endX, float endY) | 添加一条从路径最后点位置到目标点位置的三阶贝塞尔圆滑曲线。   |
| [OH_Drawing_PathClose](#oh_drawing_pathclose) ([OH_Drawing_Path](#oh_drawing_path) \*) | 闭合路径，会添加一条从路径起点位置到最后点位置的线段。       |
| [OH_Drawing_PathReset](#oh_drawing_pathreset) ([OH_Drawing_Path](#oh_drawing_path) \*) | 重置自定义路径数据。                                         |
| [OH_Drawing_PenCreate](#oh_drawing_pencreate) (void)         | 创建一个画笔对象。                                           |
| [OH_Drawing_PenDestroy](#oh_drawing_pendestroy) ([OH_Drawing_Pen](#oh_drawing_pen) \*) | 销毁画笔对象并回收该对象占有的内存。                         |
| [OH_Drawing_PenIsAntiAlias](#oh_drawing_penisantialias) (const [OH_Drawing_Pen](#oh_drawing_pen) \*) | 获取画笔是否设置抗锯齿属性，如果为真则说明画笔会启用抗锯齿功能，在绘制图形时会对图形的边缘像素进行半透明的模糊处理。 |
| [OH_Drawing_PenSetAntiAlias](#oh_drawing_pensetantialias) ([OH_Drawing_Pen](#oh_drawing_pen) \*, bool) | 设置画笔的抗锯齿属性，设置为真则画笔在绘制图形时会对图形的边缘像素进行半透明的模糊处理。 |
| [OH_Drawing_PenGetColor](#oh_drawing_pengetcolor) (const [OH_Drawing_Pen](#oh_drawing_pen) \*) | 获取画笔的颜色属性，颜色属性描述了画笔绘制图形轮廓时使用的颜色，用一个32位（ARGB）的变量表示。 |
| [OH_Drawing_PenSetColor](#oh_drawing_pensetcolor) ([OH_Drawing_Pen](#oh_drawing_pen) \*, uint32_t color) | 设置画笔的颜色属性，颜色属性描述了画笔绘制图形轮廓时使用的颜色，用一个32位（ARGB）的变量表示。 |
| [OH_Drawing_PenGetWidth](#oh_drawing_pengetwidth) (const [OH_Drawing_Pen](#oh_drawing_pen) \*) | 获取画笔的厚度属性，厚度属性描述了画笔绘制图形轮廓的宽度。   |
| [OH_Drawing_PenSetWidth](#oh_drawing_pensetwidth) ([OH_Drawing_Pen](#oh_drawing_pen) \*, float width) | 设置画笔的厚度属性，厚度属性描述了画笔绘制图形轮廓的宽度。   |
| [OH_Drawing_PenGetMiterLimit](#oh_drawing_pengetmiterlimit) (const [OH_Drawing_Pen](#oh_drawing_pen) \*) | 获取折线尖角的限制值，当画笔绘制一条折线，转角类型设置为尖角时，那么此时该属性用于限制出现尖角的长度范围，如果超出则平角显示，不超出依然为尖角。 |
| [OH_Drawing_PenSetMiterLimit](#oh_drawing_pensetmiterlimit) ([OH_Drawing_Pen](#oh_drawing_pen) \*, float miter) | 设置折线尖角的限制值，当画笔绘制一条折线，转角类型设置为尖角时，那么此时该属性用于限制出现尖角的长度范围，如果超出则平角显示，不超出依然为尖角。 |
| [OH_Drawing_PenGetCap](#oh_drawing_pengetcap) (const [OH_Drawing_Pen](#oh_drawing_pen) \*) | 获取画笔笔帽的样式。                                         |
| [OH_Drawing_PenSetCap](#oh_drawing_pensetcap) ([OH_Drawing_Pen](#oh_drawing_pen) \*, [OH_Drawing_PenLineCapStyle](#oh_drawing_penlinecapstyle)) | 设置画笔笔帽样式。                                           |
| [OH_Drawing_PenGetJoin](#oh_drawing_pengetjoin) (const [OH_Drawing_Pen](#oh_drawing_pen) \*) | 获取画笔绘制折线转角的样式。                                 |
| [OH_Drawing_PenSetJoin](#oh_drawing_pensetjoin) ([OH_Drawing_Pen](#oh_drawing_pen) \*, [OH_Drawing_PenLineJoinStyle](#oh_drawing_penlinejoinstyle)) | 设置画笔绘制转角的样式。                                     |
| [OH_Drawing_CreateTypographyStyle](#oh_drawing_createtypographystyle) (void) | 创建OH_Drawing_TypographyStyle。                             |
| [OH_Drawing_DestroyTypographyStyle](#oh_drawing_destroytypographystyle) ([OH_Drawing_TypographyStyle](#oh_drawing_typographystyle) \*) | 释放被OH_Drawing_TypographyStyle对象占据的内存。             |
| [OH_Drawing_SetTypographyTextDirection](#oh_drawing_settypographytextdirection) ([OH_Drawing_TypographyStyle](#oh_drawing_typographystyle) \*, int) | 设置文本方向。                                               |
| [OH_Drawing_SetTypographyTextAlign](#oh_drawing_settypographytextalign) ([OH_Drawing_TypographyStyle](#oh_drawing_typographystyle) \*, int) | 设置文本对齐方式。                                           |
| [OH_Drawing_SetTypographyTextMaxLines](#oh_drawing_settypographytextmaxlines) ([OH_Drawing_TypographyStyle](#oh_drawing_typographystyle) \*, int) | 设置文本最大行数。                                           |
| [OH_Drawing_CreateTextStyle](#oh_drawing_createtextstyle) (void) | 创建OH_Drawing_TextStyle。                                   |
| [OH_Drawing_DestroyTextStyle](#oh_drawing_destroytextstyle) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*) | 释放被OH_Drawing_TextStyle对象占据的内存。                   |
| [OH_Drawing_SetTextStyleColor](#oh_drawing_settextstylecolor) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, uint32_t) | 设置文本颜色。                                               |
| [OH_Drawing_SetTextStyleFontSize](#oh_drawing_settextstylefontsize) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, double) | 设置字号。                                                   |
| [OH_Drawing_SetTextStyleFontWeight](#oh_drawing_settextstylefontweight) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, int) | 设置字重。                                                   |
| [OH_Drawing_SetTextStyleBaseLine](#oh_drawing_settextstylebaseline) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, int) | 设置字体基线位置。                                           |
| [OH_Drawing_SetTextStyleDecoration](#oh_drawing_settextstyledecoration) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, int) | 设置装饰。                                                   |
| [OH_Drawing_SetTextStyleDecorationColor](#oh_drawing_settextstyledecorationcolor) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, uint32_t) | 设置装饰颜色。                                               |
| [OH_Drawing_SetTextStyleFontHeight](#oh_drawing_settextstylefontheight) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, double) | 设置字体高度。                                               |
| [OH_Drawing_SetTextStyleFontFamilies](#oh_drawing_settextstylefontfamilies) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, int, const char \*fontFamilies[]) | 设置字体类型。                                               |
| [OH_Drawing_SetTextStyleFontStyle](#oh_drawing_settextstylefontstyle) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, int) | 设置字体风格。                                               |
| [OH_Drawing_SetTextStyleLocale](#oh_drawing_settextstylelocale) ([OH_Drawing_TextStyle](#oh_drawing_textstyle) \*, const char \*) | 设置语言区域。                                               |
| [OH_Drawing_CreateTypographyHandler](#oh_drawing_createtypographyhandler) ([OH_Drawing_TypographyStyle](#oh_drawing_typographystyle) \*, [OH_Drawing_FontCollection](#oh_drawing_fontcollection) \*) | 创建指向OH_Drawing_TypographyCreate对象的指针。              |
| [OH_Drawing_DestroyTypographyHandler](#oh_drawing_destroytypographyhandler) ([OH_Drawing_TypographyCreate](#oh_drawing_typographycreate) \*) | 释放被OH_Drawing_TypographyCreate对象占据的内存。            |
| [OH_Drawing_TypographyHandlerPushTextStyle](#oh_drawing_typographyhandlerpushtextstyle) ([OH_Drawing_TypographyCreate](#oh_drawing_typographycreate) \*, [OH_Drawing_TextStyle](#oh_drawing_textstyle) \*) | 设置排版风格。                                               |
| [OH_Drawing_TypographyHandlerAddText](#oh_drawing_typographyhandleraddtext) ([OH_Drawing_TypographyCreate](#oh_drawing_typographycreate) \*, const char \*) | 设置文本内容。                                               |
| [OH_Drawing_TypographyHandlerPopTextStyle](#oh_drawing_typographyhandlerpoptextstyle) ([OH_Drawing_TypographyCreate](#oh_drawing_typographycreate) \*) | 排版弹出。                                                   |
| [OH_Drawing_CreateTypography](#oh_drawing_createtypography) ([OH_Drawing_TypographyCreate](#oh_drawing_typographycreate) \*) | 创建OH_Drawing_Typography。                                  |
| [OH_Drawing_DestroyTypography](#oh_drawing_destroytypography) ([OH_Drawing_Typography](#oh_drawing_typography) \*) | 释放OH_Drawing_Typography对象占据的内存。                    |
| [OH_Drawing_TypographyLayout](#oh_drawing_typographylayout) ([OH_Drawing_Typography](#oh_drawing_typography) \*, double) | 排版布局。                                                   |
| [OH_Drawing_TypographyPaint](#oh_drawing_typographypaint) ([OH_Drawing_Typography](#oh_drawing_typography) \*, [OH_Drawing_Canvas](#oh_drawing_canvas) \*, double, double) | 显示文本。                                                   |
| [OH_Drawing_TypographyGetMaxWidth](#oh_drawing_typographygetmaxwidth) ([OH_Drawing_Typography](#oh_drawing_typography) *) | 获取最大宽度。                                               |
| [OH_Drawing_TypographyGetHeight](#oh_drawing_typographygetheight) ([OH_Drawing_Typography](#oh_drawing_typography) *) | 获取高度。                                                   |
| [OH_Drawing_TypographyGetLongestLine](#oh_drawing_typographygetlongestline) ([OH_Drawing_Typography](#oh_drawing_typography) *) | 获取最长行的宽度，建议实际使用时将返回值向上取整。                                                 |
| [OH_Drawing_TypographyGetMinIntrinsicWidth](#oh_drawing_typographygetminintrinsicwidth) ([OH_Drawing_Typography](#oh_drawing_typography) *) | 获取最小固有宽度。                                           |
| [OH_Drawing_TypographyGetMaxIntrinsicWidth](#oh_drawing_typographygetmaxintrinsicwidth) ([OH_Drawing_Typography](#oh_drawing_typography) *) | 获取最大固有宽度。                                           |
| [OH_Drawing_TypographyGetAlphabeticBaseline](#oh_drawing_typographygetalphabeticbaseline)([OH_Drawing_Typography](#oh_drawing_typography) *) | 获取字母文字基线。                                           |
| [OH_Drawing_TypographyGetIdeographicBaseline](#oh_drawing_typographygetideographicbaseline) ([OH_Drawing_Typography](#oh_drawing_typography) *) | 获取表意文字基线。                                           |


## 类型定义说明


### OH_Drawing_Bitmap


```
typedef struct OH_Drawing_Bitmap OH_Drawing_Bitmap
```

**描述：**

OH_Drawing_Bitmap定义为位图，位图是一块内存，内存中包含了描述一张图片的像素数据

**起始版本：**

8


### OH_Drawing_Brush


```
typedef struct OH_Drawing_Brush OH_Drawing_Brush
```

**描述：**

OH_Drawing_Brush定义为画刷，画刷用于描述填充图形的样式和颜色

**起始版本：**

8


### OH_Drawing_Canvas


```
typedef struct OH_Drawing_Canvas OH_Drawing_Canvas
```

**描述：**

OH_Drawing_Canvas定义为一块矩形的画布，可以结合画笔和画刷在上面绘制各种形状、图片和文字

**起始版本：**

8


### OH_Drawing_FontCollection


```
typedef struct OH_Drawing_FontCollection OH_Drawing_FontCollection
```

**描述：**

OH_Drawing_FontCollection用于加载字体

**起始版本：**

8


### OH_Drawing_Path


```
typedef struct OH_Drawing_Path OH_Drawing_Path
```

**描述：**

OH_Drawing_Path定义为路径，路径用于自定义设置各种形状

**起始版本：**

8


### OH_Drawing_Pen


```
typedef struct OH_Drawing_Pen OH_Drawing_Pen
```

**描述：**

OH_Drawing_Pen定义为画笔，画笔用于描述绘制图形轮廓的样式和颜色

**起始版本：**

8


### OH_Drawing_TextStyle


```
typedef struct OH_Drawing_TextStyle OH_Drawing_TextStyle
```

**描述：**

OH_Drawing_TextStyle用于管理字体颜色、装饰等

**起始版本：**

8


### OH_Drawing_Typography


```
typedef struct OH_Drawing_Typography OH_Drawing_Typography
```

**描述：**

OH_Drawing_Typography用于管理排版的布局和显示等

**起始版本：**

8


### OH_Drawing_TypographyCreate


```
typedef struct OH_Drawing_TypographyCreate OH_Drawing_TypographyCreate
```

**描述：**

OH_Drawing_TypographyCreate用于创建OH_Drawing_Typography

**起始版本：**

8


### OH_Drawing_TypographyStyle


```
typedef struct OH_Drawing_TypographyStyle OH_Drawing_TypographyStyle
```

**描述：**

OH_Drawing_TypographyStyle用于管理排版风格，如文字方向等

**起始版本：**

8


## 枚举类型说明


### OH_Drawing_AlphaFormat


```
enum OH_Drawing_AlphaFormat
```

**描述：**

OH_Drawing_AlphaFormat用于描述位图像素的透明度分量

| 枚举值                | 描述                                     |
| --------------------- | ---------------------------------------- |
| ALPHA_FORMAT_UNKNOWN  | 未知格式                                 |
| ALPHA_FORMAT_OPAQUE   | 位图无透明度                             |
| ALPHA_FORMAT_PREMUL   | 每个像素的颜色组件由透明度分量预先乘以   |
| ALPHA_FORMAT_UNPREMUL | 每个像素的颜色组件未由透明度分量预先乘以 |

**起始版本：**

8


### OH_Drawing_ColorFormat


```
enum OH_Drawing_ColorFormat
```

**描述：**

OH_Drawing_ColorFormat用于描述位图像素的存储格式

| 枚举值                 | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| COLOR_FORMAT_UNKNOWN   | 未知格式.                                                    |
| COLOR_FORMAT_ALPHA_8   | 每个像素用一个8位的量表示，8个位比特位表示透明度             |
| COLOR_FORMAT_RGB_565   | 每个像素用一个16位的量表示，高位到低位依次是5个比特位表示红，6个比特位表示绿，5个比特位表示蓝 |
| COLOR_FORMAT_ARGB_4444 | 每个像素用一个16位的量表示，高位到低位依次是4个比特位表示透明度，4个比特位表示红，4个比特位表示绿，4个比特位表示蓝 |
| COLOR_FORMAT_RGBA_8888 | 每个像素用一个32位的量表示，高位到低位依次是8个比特位表示透明度，8个比特位表示红，8个比特位表示绿，8个比特位表示蓝 |
| COLOR_FORMAT_BGRA_8888 | 每个像素用一个32位的量表示，高位到低位依次是8个比特位表示蓝，8个比特位表示绿，8个比特位表示红，8个比特位表示透明度 |

**起始版本：**

8


### OH_Drawing_FontStyle


```
enum OH_Drawing_FontStyle
```

**描述：**

区分字体是否为斜体

| 枚举值            | 描述   |
| ----------------- | ------ |
| FONT_STYLE_NORMAL | 非斜体 |
| FONT_STYLE_ITALIC | 斜体   |

**起始版本：**

8


### OH_Drawing_FontWeight


```
enum OH_Drawing_FontWeight
```

**描述：**

字重

| 枚举值          | 描述                 |
| --------------- | -------------------- |
| FONT_WEIGHT_100 | 字重为thin           |
| FONT_WEIGHT_200 | 字重为extra-light    |
| FONT_WEIGHT_300 | 字重为light          |
| FONT_WEIGHT_400 | 字重为normal/regular |
| FONT_WEIGHT_500 | 字重为medium         |
| FONT_WEIGHT_600 | 字重为semi-bold      |
| FONT_WEIGHT_700 | 字重为bold           |
| FONT_WEIGHT_800 | 字重为extra-bold     |
| FONT_WEIGHT_900 | 字重为black          |

**起始版本：**

8


### OH_Drawing_PenLineCapStyle


```
enum OH_Drawing_PenLineCapStyle
```

**描述：**

枚举集合定义了画笔笔帽的样式，即画笔在绘制线段时，在线段头尾端点的样式

| 枚举值          | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| LINE_FLAT_CAP   | 没有笔帽样式，线条头尾端点处横切                             |
| LINE_SQUARE_CAP | 笔帽的样式为方框，线条的头尾端点处多出一个方框，方框宽度和线段一样宽，高度时线段厚度的一半 |
| LINE_ROUND_CAP  | 笔帽的样式为圆弧，线条的头尾端点处多出一个半圆弧，半圆的直径与线段厚度一致 |

**起始版本：**

8


### OH_Drawing_PenLineJoinStyle


```
enum OH_Drawing_PenLineJoinStyle
```

**描述：**

枚举集合定义了线条转角的样式，即画笔在绘制折线段时，在折线转角处的样式

| 枚举值          | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| LINE_MITER_JOIN | 转角类型为尖角，如果折线角度比较小，则尖角会很长，需要使用限制值（miter limit）进行限制 |
| LINE_ROUND_JOIN | 转角类型为圆头                                               |
| LINE_BEVEL_JOIN | 转角类型为平头                                               |

**起始版本：**

8


### OH_Drawing_TextAlign


```
enum OH_Drawing_TextAlign
```

**描述：**

文字对齐方式

| 枚举值             | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| TEXT_ALIGN_LEFT    | 左对齐                                                       |
| TEXT_ALIGN_RIGHT   | 右对齐                                                       |
| TEXT_ALIGN_CENTER  | 居中对齐                                                     |
| TEXT_ALIGN_JUSTIFY | 两端对齐，即紧靠左和右边缘，中间单词空隙由空格填充 最后一行除外 |
| TEXT_ALIGN_START   | 当OH_Drawing_TextDirection是TEXT_DIRECTION_LTR时， TEXT_ALIGN_START和TEXT_ALIGN_LEFT相同； 类似地，当OH_Drawing_TextDirection是TEXT_DIRECTION_RTL时， TEXT_ALIGN_START和TEXT_ALIGN_RIGHT相同。 |
| TEXT_ALIGN_END     | 当OH_Drawing_TextDirection是TEXT_DIRECTION_LTR时， TEXT_ALIGN_END和TEXT_ALIGN_RIGHT相同； 类似地，当OH_Drawing_TextDirection是TEXT_DIRECTION_RTL时， TEXT_ALIGN_END和TEXT_ALIGN_LEFT相同。 |

**起始版本：**

8


### OH_Drawing_TextBaseline


```
enum OH_Drawing_TextBaseline
```

**描述：**

基线位置

| 枚举值                    | 描述                               |
| ------------------------- | ---------------------------------- |
| TEXT_BASELINE_ALPHABETIC  | 用于表音文字，基线在中间偏下的位置 |
| TEXT_BASELINE_IDEOGRAPHIC | 用于表意文字，基线位于底部         |

**起始版本：**

8


### OH_Drawing_TextDecoration


```
enum OH_Drawing_TextDecoration
```

**描述：**

文本装饰

| 枚举值                       | 描述   |
| ---------------------------- | ------ |
| TEXT_DECORATION_NONE         | 无装饰 |
| TEXT_DECORATION_UNDERLINE    | 下划线 |
| TEXT_DECORATION_OVERLINE     | 上划线 |
| TEXT_DECORATION_LINE_THROUGH | 删除线 |

**起始版本：**

8


### OH_Drawing_TextDirection


```
enum OH_Drawing_TextDirection
```

**描述：**

文字方向

| 枚举值             | 描述           |
| ------------------ | -------------- |
| TEXT_DIRECTION_RTL | 方向：从右到左 |
| TEXT_DIRECTION_LTR | 方向：从左到右 |

**起始版本：**

8


## 函数说明


### OH_Drawing_BitmapBuild()


```
void OH_Drawing_BitmapBuild (OH_Drawing_Bitmap * , const uint32_t width, const uint32_t height, const OH_Drawing_BitmapFormat *  )
```

**描述：**

设置初始化位图对象的宽度和高度，并且为该位图设置像素格式

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                                                         | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| OH_Drawing_Bitmap                                            | 参数是一个指向位图对象的指针                                 |
| width                                                        | 参数是位图要初始化设置的宽度                                 |
| height                                                       | 参数是位图要初始化设置的高度                                 |
| [OH_Drawing_BitmapFormat](_o_h___drawing___bitmap_format.md) | 参数是位图要初始化设置的像素格式，包括像素的颜色类型和透明度类型 |

**起始版本：**

8


### OH_Drawing_BitmapCreate()


```
OH_Drawing_Bitmap* OH_Drawing_BitmapCreate (void )
```

**描述：**

创建一个位图对象。

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**返回：**

函数会返回一个指针，指针指向创建的位图对象

**起始版本：**

8


### OH_Drawing_BitmapDestroy()


```
void OH_Drawing_BitmapDestroy (OH_Drawing_Bitmap * )
```

**描述：**

销毁位图对象并回收该对象占有内存。

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Bitmap | 参数是一个指向位图对象的指针 |

**起始版本：**

8


### OH_Drawing_BitmapGetHeight()


```
uint32_t OH_Drawing_BitmapGetHeight (OH_Drawing_Bitmap * )
```

**描述：**

获取指定位图的高度

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Bitmap | 参数是一个指向位图对象的指针 |

**返回：**

函数返回位图的高度

**起始版本：**

8


### OH_Drawing_BitmapGetPixels()


```
void* OH_Drawing_BitmapGetPixels (OH_Drawing_Bitmap * )
```

**描述：**

获取指定位图的像素地址，可以通过像素地址获取到位图的像素数据

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Bitmap | 参数是一个指向位图对象的指针 |

**返回：**

函数返回位图的像素地址

**起始版本：**

8


### OH_Drawing_BitmapGetWidth()


```
uint32_t OH_Drawing_BitmapGetWidth (OH_Drawing_Bitmap * )
```

**描述：**

获取指定位图的宽度

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Bitmap | 参数是一个指向位图对象的指针 |

**返回：**

函数返回位图的宽度

**起始版本：**

8


### OH_Drawing_BrushCreate()


```
OH_Drawing_Brush* OH_Drawing_BrushCreate (void )
```

**描述：**

创建一个画刷对象

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**返回：**

函数会返回一个指针，指针指向创建的画刷对象

**起始版本：**

8


### OH_Drawing_BrushDestroy()


```
void OH_Drawing_BrushDestroy (OH_Drawing_Brush * )
```

**描述：**

销毁画刷对象并回收该对象占有的内存。

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name             | 描述                         |
| ---------------- | ---------------------------- |
| OH_Drawing_Brush | 参数是一个指向画刷对象的指针 |

**起始版本：**

8


### OH_Drawing_BrushGetColor()


```
uint32_t OH_Drawing_BrushGetColor (const OH_Drawing_Brush * )
```

**描述：**

获取画刷的颜色属性，颜色属性描述了画刷填充图形时使用的颜色，用一个32位（ARGB）的变量表示

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name             | 描述                         |
| ---------------- | ---------------------------- |
| OH_Drawing_Brush | 参数是一个指向画刷对象的指针 |

**返回：**

函数返回一个描述颜色的32位（ARGB）变量

**起始版本：**

8


### OH_Drawing_BrushIsAntiAlias()


```
bool OH_Drawing_BrushIsAntiAlias (const OH_Drawing_Brush * )
```

**描述：**

获取画刷是否设置抗锯齿属性，如果为真则说明画刷会启用抗锯齿功能，在绘制图形时会对图形的边缘像素进行半透明的模糊处理

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name             | 描述                         |
| ---------------- | ---------------------------- |
| OH_Drawing_Brush | 参数是一个指向画刷对象的指针 |

**返回：**

函数返回画刷对象是否设置抗锯齿属性，返回真则设置了抗锯齿，返回假则没有设置抗锯齿

**起始版本：**

8


### OH_Drawing_BrushSetAntiAlias()


```
void OH_Drawing_BrushSetAntiAlias (OH_Drawing_Brush * , bool  )
```

**描述：**

设置画刷的抗锯齿属性，设置为真则画刷在绘制图形时会对图形的边缘像素进行半透明的模糊处理

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name             | 描述                                   |
| ---------------- | -------------------------------------- |
| OH_Drawing_Brush | 参数是一个指向画刷对象的指针           |
| bool             | 参数真为抗锯齿，参数假则不做抗锯齿处理 |

**起始版本：**

8


### OH_Drawing_BrushSetColor()


```
void OH_Drawing_BrushSetColor (OH_Drawing_Brush * , uint32_t color )
```

**描述：**

设置画刷的颜色属性，颜色属性描述了画刷填充图形时使用的颜色，用一个32位（ARGB）的变量表示

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name             | 描述                                 |
| ---------------- | ------------------------------------ |
| OH_Drawing_Brush | 参数是一个指向画刷对象的指针         |
| color            | 参数是一个描述颜色的32位（ARGB）变量 |

**起始版本：**

8


### OH_Drawing_CanvasAttachBrush()


```
void OH_Drawing_CanvasAttachBrush (OH_Drawing_Canvas * , const OH_Drawing_Brush *  )
```

**描述：**

设置画刷给画布，画布将会使用设置的画刷样式和颜色去填充绘制的图形形状

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针 |
| OH_Drawing_Brush  | 参数为一个指向画刷对象的指针 |

**起始版本：**

8


### OH_Drawing_CanvasAttachPen()


```
void OH_Drawing_CanvasAttachPen (OH_Drawing_Canvas * , const OH_Drawing_Pen *  )
```

**描述：**

设置画笔给画布，画布将会使用设置画笔的样式和颜色去绘制图形形状的轮廓

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针 |
| OH_Drawing_Pen    | 参数为一个指向画笔对象的指针 |

**起始版本：**

8


### OH_Drawing_CanvasBind()


```
void OH_Drawing_CanvasBind (OH_Drawing_Canvas * , OH_Drawing_Bitmap *  )
```

**描述：**

将一个位图对象绑定到画布中，使得画布绘制的内容输出到位图中（即CPU渲染）

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针 |
| OH_Drawing_Bitmap | 参数为一个指向位图对象的指针 |

**起始版本：**

8


### OH_Drawing_CanvasClear()


```
void OH_Drawing_CanvasClear (OH_Drawing_Canvas * , uint32_t color )
```

**描述：**

使用指定颜色去清空画布

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                                 |
| ----------------- | ------------------------------------ |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针         |
| color             | 参数为一个描述颜色的32位（ARGB）变量 |

**起始版本：**

8


### OH_Drawing_CanvasCreate()


```
OH_Drawing_Canvas* OH_Drawing_CanvasCreate (void )
```

**描述：**

创建一个画布对象

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**返回：**

函数会返回一个指针，指针指向创建的画布对象

**起始版本：**

8


### OH_Drawing_CanvasDestroy()


```
void OH_Drawing_CanvasDestroy (OH_Drawing_Canvas * )
```

**描述：**

销毁画布对象并回收该对象占有的内存

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数是一个指向画布对象的指针 |

**起始版本：**

8


### OH_Drawing_CanvasDetachBrush()


```
void OH_Drawing_CanvasDetachBrush (OH_Drawing_Canvas * )
```

**描述：**

去除掉画布中的画刷，使用后画布将不去填充图形形状

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针 |

**起始版本：**

8


### OH_Drawing_CanvasDetachPen()


```
void OH_Drawing_CanvasDetachPen (OH_Drawing_Canvas * )
```

**描述：**

去除掉画布中的画笔，使用后画布将不去绘制图形形状的轮廓

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针 |

**起始版本：**

8


### OH_Drawing_CanvasDrawLine()


```
void OH_Drawing_CanvasDrawLine (OH_Drawing_Canvas * , float x1, float y1, float x2, float y2 )
```

**描述：**

画一条直线段

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针 |
| x1                | 参数为线段起始点的横坐标     |
| y1                | 参数为线段起始点的纵坐标     |
| x2                | 参数为线段结束点的横坐标     |
| y2                | 参数为线段结束点的纵坐标     |

**起始版本：**

8


### OH_Drawing_CanvasDrawPath()


```
void OH_Drawing_CanvasDrawPath (OH_Drawing_Canvas * , const OH_Drawing_Path *  )
```

**描述：**

画一个自定义路径

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针 |
| OH_Drawing_Path   | 参数为一个指向路径对象的指针 |

**起始版本：**

8


### OH_Drawing_CanvasRestore()


```
void OH_Drawing_CanvasRestore (OH_Drawing_Canvas * )
```

**描述：**

恢复保存在栈顶的画布状态（画布矩阵）

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针 |

**起始版本：**

8


### OH_Drawing_CanvasSave()


```
void OH_Drawing_CanvasSave (OH_Drawing_Canvas * )
```

**描述：**

保存当前画布的状态（画布矩阵）到一个栈顶

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name              | 描述                         |
| ----------------- | ---------------------------- |
| OH_Drawing_Canvas | 参数为一个指向画布对象的指针 |

**起始版本：**

8


### OH_Drawing_ColorSetArgb()


```
uint32_t OH_Drawing_ColorSetArgb (uint32_t alpha, uint32_t red, uint32_t green, uint32_t blue )
```

**描述：**

将4个变量（分别描述透明度、红色、绿色和蓝色）转化为一个描述颜色的32位（ARGB）变量

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name  | 描述                                            |
| ----- | ----------------------------------------------- |
| alpha | 参数为一个描述透明度的变量, 变量范围是0x00~0xFF |
| red   | 参数为一个描述红色的变量, 变量范围是0x00~0xFF   |
| green | 参数为一个描述绿色的变量, 变量范围是0x00~0xFF   |
| blue  | 参数为一个描述蓝色的变量, 变量范围是0x00~0xFF   |

**返回：**

函数返回一个描述颜色的32位（ARGB）变量

**起始版本：**

8


### OH_Drawing_CreateFontCollection()


```
OH_Drawing_FontCollection* OH_Drawing_CreateFontCollection (void )
```

**描述：**

创建OH_Drawing_FontCollection

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**返回：**

指向创建的OH_Drawing_FontCollection对象的指针

**起始版本：**

8


### OH_Drawing_CreateTextStyle()


```
OH_Drawing_TextStyle* OH_Drawing_CreateTextStyle (void )
```

**描述：**

创建OH_Drawing_TextStyle

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**返回：**

指向创建的OH_Drawing_TextStyle对象的指针

**起始版本：**

8


### OH_Drawing_CreateTypography()


```
OH_Drawing_Typography* OH_Drawing_CreateTypography (OH_Drawing_TypographyCreate * )
```

**描述：**

创建OH_Drawing_Typography

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                        | 描述                                      |
| --------------------------- | ----------------------------------------- |
| OH_Drawing_TypographyCreate | 指向OH_Drawing_TypographyCreate对象的指针 |

**返回：**

指向OH_Drawing_Typography对象的指针

**起始版本：**

8


### OH_Drawing_CreateTypographyHandler()


```
OH_Drawing_TypographyCreate* OH_Drawing_CreateTypographyHandler (OH_Drawing_TypographyStyle * , OH_Drawing_FontCollection *  )
```

**描述：**

创建指向OH_Drawing_TypographyCreate对象的指针

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                       | 描述                                 |
| -------------------------- | ------------------------------------ |
| OH_Drawing_TypographyStyle | 指向OH_Drawing_TypographyStyle的指针 |
| OH_Drawing_FontCollection  | 指向OH_Drawing_FontCollection的指针  |

**返回：**

指向新创建的OH_Drawing_TypographyCreate对象的指针

**起始版本：**

8


### OH_Drawing_CreateTypographyStyle()


```
OH_Drawing_TypographyStyle* OH_Drawing_CreateTypographyStyle (void )
```

**描述：**

创建OH_Drawing_TypographyStyle

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**返回：**

指向创建的OH_Drawing_TypographyStyle对象的指针

**起始版本：**

8


### OH_Drawing_DestroyFontCollection()


```
void OH_Drawing_DestroyFontCollection (OH_Drawing_FontCollection * )
```

**描述：**

释放被OH_Drawing_FontCollection对象占据的内存

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                      | 描述                                    |
| ------------------------- | --------------------------------------- |
| OH_Drawing_FontCollection | 指向OH_Drawing_FontCollection对象的指针 |

**起始版本：**

8


### OH_Drawing_DestroyTextStyle()


```
void OH_Drawing_DestroyTextStyle (OH_Drawing_TextStyle * )
```

**描述：**

释放被OH_Drawing_TextStyle对象占据的内存

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |

**起始版本：**

8


### OH_Drawing_DestroyTypography()


```
void OH_Drawing_DestroyTypography (OH_Drawing_Typography * )
```

**描述：**

释放OH_Drawing_Typography对象占据的内存

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |

**起始版本：**

8


### OH_Drawing_DestroyTypographyHandler()


```
void OH_Drawing_DestroyTypographyHandler (OH_Drawing_TypographyCreate * )
```

**描述：**

释放被OH_Drawing_TypographyCreate对象占据的内存

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                        | 描述                                      |
| --------------------------- | ----------------------------------------- |
| OH_Drawing_TypographyCreate | 指向OH_Drawing_TypographyCreate对象的指针 |

**起始版本：**

8


### OH_Drawing_DestroyTypographyStyle()


```
void OH_Drawing_DestroyTypographyStyle (OH_Drawing_TypographyStyle * )
```

**描述：**

释放被OH_Drawing_TypographyStyle对象占据的内存

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                       | 描述                                     |
| -------------------------- | ---------------------------------------- |
| OH_Drawing_TypographyStyle | 指向OH_Drawing_TypographyStyle对象的指针 |

**起始版本：**

8


### OH_Drawing_PathArcTo()


```
void OH_Drawing_PathArcTo (OH_Drawing_Path * , float x1, float y1, float x2, float y2, float startDeg, float sweepDeg )
```

**描述：**

给路径添加一段弧线，绘制弧线的方式为角度弧，该方式首先会指定一个矩形边框，矩形边框会包裹椭圆， 然后会指定一个起始角度和扫描度数，从起始角度扫描截取的椭圆周长一部分即为绘制的弧线。另外会默认添加一条从路径的最后点位置到弧线起始点位置的线段

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name            | 描述                                     |
| --------------- | ---------------------------------------- |
| OH_Drawing_Path | 参数为一个指向路径对象的指针             |
| x1              | 参数为包围椭圆的矩形左上角点位置的横坐标 |
| y1              | 参数为包围椭圆的矩形左上角点位置的纵坐标 |
| x2              | 参数为包围椭圆的矩形右下角点位置的横坐标 |
| y2              | 参数为包围椭圆的矩形右下角点位置的纵坐标 |
| startDeg        | 参数为起始的角度                         |
| sweepDeg        | 参数为扫描的度数                         |

**起始版本：**

8


### OH_Drawing_PathClose()


```
void OH_Drawing_PathClose (OH_Drawing_Path * )
```

**描述：**

函数用于闭合路径，会添加一条从路径起点位置到最后点位置的线段

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name            | 描述                         |
| --------------- | ---------------------------- |
| OH_Drawing_Path | 参数为一个指向路径对象的指针 |

**起始版本：**

8


### OH_Drawing_PathCreate()


```
OH_Drawing_Path* OH_Drawing_PathCreate (void )
```

**描述：**

创建一个路径对象

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**返回：**

函数会返回一个指针，指针指向创建的路径对象

**起始版本：**

8


### OH_Drawing_PathCubicTo()


```
void OH_Drawing_PathCubicTo (OH_Drawing_Path * , float ctrlX1, float ctrlY1, float ctrlX2, float ctrlY2, float endX, float endY )
```

**描述：**

添加一条从路径最后点位置到目标点位置的三阶贝塞尔圆滑曲线

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name            | 描述                           |
| --------------- | ------------------------------ |
| OH_Drawing_Path | 参数为一个指向路径对象的指针   |
| ctrlX1          | 参数为第一个控制点位置的横坐标 |
| ctrlY1          | 参数为第一个控制点位置的纵坐标 |
| ctrlX2          | 参数为第二个控制点位置的横坐标 |
| ctrlY2          | 参数为第二个控制点位置的纵坐标 |
| endX            | 参数为目标点位置的横坐标       |
| endY            | 参数为目标点位置的纵坐标       |

**起始版本：**

8


### OH_Drawing_PathDestroy()


```
void OH_Drawing_PathDestroy (OH_Drawing_Path * )
```

**描述：**

销毁路径对象并回收该对象占有的内存

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name            | 描述                         |
| --------------- | ---------------------------- |
| OH_Drawing_Path | 参数为一个指向路径对象的指针 |

**起始版本：**

8


### OH_Drawing_PathLineTo()


```
void OH_Drawing_PathLineTo (OH_Drawing_Path * , float x, float y )
```

**描述：**

添加一条从路径的最后点位置到目标点位置的线段

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name            | 描述                         |
| --------------- | ---------------------------- |
| OH_Drawing_Path | 参数为一个指向路径对象的指针 |
| x               | 参数为目标点的横坐标         |
| y               | 参数为目标点的纵坐标         |

**起始版本：**

8


### OH_Drawing_PathMoveTo()


```
void OH_Drawing_PathMoveTo (OH_Drawing_Path * , float x, float y )
```

**描述：**

设置自定义路径的起始点位置

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name            | 描述                         |
| --------------- | ---------------------------- |
| OH_Drawing_Path | 参数为一个指向路径对象的指针 |
| x               | 参数为起始点的横坐标         |
| y               | 参数为起始点的纵坐标         |

**起始版本：**

8


### OH_Drawing_PathQuadTo()


```
void OH_Drawing_PathQuadTo (OH_Drawing_Path * , float ctrlX, float ctrlY, float endX, float endY )
```

**描述：**

添加一条从路径最后点位置到目标点位置的二阶贝塞尔圆滑曲线

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name            | 描述                         |
| --------------- | ---------------------------- |
| OH_Drawing_Path | 参数为一个指向路径对象的指针 |
| ctrlX           | 参数为控制点位置的横坐标     |
| ctrlY           | 参数为控制点位置的纵坐标     |
| endX            | 参数为目标点位置的横坐标     |
| endY            | 参数为目标点位置的纵坐标     |

**起始版本：**

8


### OH_Drawing_PathReset()


```
void OH_Drawing_PathReset (OH_Drawing_Path * )
```

**描述：**

重置自定义路径数据

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name            | 描述                         |
| --------------- | ---------------------------- |
| OH_Drawing_Path | 参数为一个指向路径对象的指针 |

**起始版本：**

8


### OH_Drawing_PenCreate()


```
OH_Drawing_Pen* OH_Drawing_PenCreate (void )
```

**描述：**

创建一个画笔对象

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**返回：**

函数会返回一个指针，指针指向创建的画笔对象

**起始版本：**

8


### OH_Drawing_PenDestroy()


```
void OH_Drawing_PenDestroy (OH_Drawing_Pen * )
```

**描述：**

销毁画笔对象并回收该对象占有的内存

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                         |
| -------------- | ---------------------------- |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针 |

**起始版本：**

8


### OH_Drawing_PenGetCap()


```
OH_Drawing_PenLineCapStyle OH_Drawing_PenGetCap (const OH_Drawing_Pen * )
```

**描述：**

获取画笔笔帽的样式

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                         |
| -------------- | ---------------------------- |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针 |

**返回：**

函数返回画笔笔帽样式

**起始版本：**

8


### OH_Drawing_PenGetColor()


```
uint32_t OH_Drawing_PenGetColor (const OH_Drawing_Pen * )
```

**描述：**

获取画笔的颜色属性，颜色属性描述了画笔绘制图形轮廓时使用的颜色，用一个32位（ARGB）的变量表示

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                         |
| -------------- | ---------------------------- |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针 |

**返回：**

函数返回一个描述颜色的32位（ARGB）变量

**起始版本：**

8


### OH_Drawing_PenGetJoin()


```
OH_Drawing_PenLineJoinStyle OH_Drawing_PenGetJoin (const OH_Drawing_Pen * )
```

**描述：**

获取画笔绘制折线转角的样式

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                         |
| -------------- | ---------------------------- |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针 |

**返回：**

函数返回折线转角的样式

**起始版本：**

8


### OH_Drawing_PenGetMiterLimit()


```
float OH_Drawing_PenGetMiterLimit (const OH_Drawing_Pen * )
```

**描述：**

获取折线尖角的限制值，当画笔绘制一条折线，转角类型设置为尖角时，那么此时该属性用于限制出现尖角的长度范围，如果超出则平角显示，不超出依然为尖角

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                         |
| -------------- | ---------------------------- |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针 |

**返回：**

函数返回尖角的限制值

**起始版本：**

8


### OH_Drawing_PenGetWidth()


```
float OH_Drawing_PenGetWidth (const OH_Drawing_Pen * )
```

**描述：**

获取画笔的厚度属性，厚度属性描述了画笔绘制图形轮廓的宽度

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                         |
| -------------- | ---------------------------- |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针 |

**返回：**

函数返回画笔的厚度

**起始版本：**

8


### OH_Drawing_PenIsAntiAlias()


```
bool OH_Drawing_PenIsAntiAlias (const OH_Drawing_Pen * )
```

**描述：**

获取画笔是否设置抗锯齿属性，如果为真则说明画笔会启用抗锯齿功能，在绘制图形时会对图形的边缘像素进行半透明的模糊处理

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                         |
| -------------- | ---------------------------- |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针 |

**返回：**

函数返回画笔对象是否设置抗锯齿属性，返回真则设置了抗锯齿，返回假则没有设置抗锯齿

**起始版本：**

8


### OH_Drawing_PenSetAntiAlias()


```
void OH_Drawing_PenSetAntiAlias (OH_Drawing_Pen * , bool  )
```

**描述：**

设置画笔的抗锯齿属性，设置为真则画笔在绘制图形时会对图形的边缘像素进行半透明的模糊处理

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                                   |
| -------------- | -------------------------------------- |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针           |
| bool           | 参数真为抗锯齿，参数假则不做抗锯齿处理 |

**起始版本：**

8


### OH_Drawing_PenSetCap()


```
void OH_Drawing_PenSetCap (OH_Drawing_Pen * , OH_Drawing_PenLineCapStyle  )
```

**描述：**

设置画笔笔帽样式

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                       | 描述                             |
| -------------------------- | -------------------------------- |
| OH_Drawing_Pen             | 参数是一个指向画笔对象的指针     |
| OH_Drawing_PenLineCapStyle | 参数是一个描述画笔笔帽样式的变量 |

**起始版本：**

8


### OH_Drawing_PenSetColor()


```
void OH_Drawing_PenSetColor (OH_Drawing_Pen * , uint32_t color )
```

**描述：**

设置画笔的颜色属性，颜色属性描述了画笔绘制图形轮廓时使用的颜色，用一个32位（ARGB）的变量表示

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                                 |
| -------------- | ------------------------------------ |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针         |
| color          | 参数是一个描述颜色的32位（ARGB）变量 |

**起始版本：**

8


### OH_Drawing_PenSetJoin()


```
void OH_Drawing_PenSetJoin (OH_Drawing_Pen * , OH_Drawing_PenLineJoinStyle  )
```

**描述：**

设置画笔绘制转角的样式

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                        | 描述                             |
| --------------------------- | -------------------------------- |
| OH_Drawing_Pen              | 参数是一个指向画笔对象的指针     |
| OH_Drawing_PenLineJoinStyle | 参数值一个描述折线转角样式的变量 |

**起始版本：**

8


### OH_Drawing_PenSetMiterLimit()


```
void OH_Drawing_PenSetMiterLimit (OH_Drawing_Pen * , float miter )
```

**描述：**

设置折线尖角的限制值，当画笔绘制一条折线，转角类型设置为尖角时，那么此时该属性用于限制出现尖角的长度范围，如果超出则平角显示，不超出依然为尖角

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                           |
| -------------- | ------------------------------ |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针   |
| miter          | 参数是一个描述尖角限制值的变量 |

**起始版本：**

8


### OH_Drawing_PenSetWidth()


```
void OH_Drawing_PenSetWidth (OH_Drawing_Pen * , float width )
```

**描述：**

设置画笔的厚度属性，厚度属性描述了画笔绘制图形轮廓的宽度

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name           | 描述                         |
| -------------- | ---------------------------- |
| OH_Drawing_Pen | 参数是一个指向画笔对象的指针 |
| width          | 参数是一个描述画笔厚度的变量 |

**起始版本：**

8


### OH_Drawing_SetTextStyleBaseLine()


```
void OH_Drawing_SetTextStyleBaseLine (OH_Drawing_TextStyle * , int  )
```

**描述：**

设置字体基线位置

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| int                  | OH_Drawing_TextBaseline枚举类型    |

**起始版本：**

8


### OH_Drawing_SetTextStyleColor()


```
void OH_Drawing_SetTextStyleColor (OH_Drawing_TextStyle * , uint32_t  )
```

**描述：**

设置文本颜色

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| uint32_t             | 颜色                               |

**起始版本：**

8


### OH_Drawing_SetTextStyleDecoration()


```
void OH_Drawing_SetTextStyleDecoration (OH_Drawing_TextStyle * , int  )
```

**描述：**

设置装饰

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| int                  | OH_Drawing_TextDecoration枚举类型  |

**起始版本：**

8


### OH_Drawing_SetTextStyleDecorationColor()


```
void OH_Drawing_SetTextStyleDecorationColor (OH_Drawing_TextStyle * , uint32_t  )
```

**描述：**

设置装饰颜色

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| uint32_t             | 颜色                               |

**起始版本：**

8


### OH_Drawing_SetTextStyleFontFamilies()


```
void OH_Drawing_SetTextStyleFontFamilies (OH_Drawing_TextStyle * , int , const char * fontFamilies[] )
```

**描述：**

设置字体类型

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| int                  | 字体名称数量                       |
| fontFamilies         | 指向字体类型的指针数组             |

**起始版本：**

8


### OH_Drawing_SetTextStyleFontHeight()


```
void OH_Drawing_SetTextStyleFontHeight (OH_Drawing_TextStyle * , double  )
```

**描述：**

设置字体高度

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| double               | 字体高度                           |

**起始版本：**

8


### OH_Drawing_SetTextStyleFontSize()


```
void OH_Drawing_SetTextStyleFontSize (OH_Drawing_TextStyle * , double  )
```

**描述：**

设置字号

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| double               | 字号                               |

**起始版本：**

8


### OH_Drawing_SetTextStyleFontStyle()


```
void OH_Drawing_SetTextStyleFontStyle (OH_Drawing_TextStyle * , int  )
```

**描述：**

设置字体风格

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| int                  | OH_Drawing_FontStyle枚举类型       |

**起始版本：**

8


### OH_Drawing_SetTextStyleFontWeight()


```
void OH_Drawing_SetTextStyleFontWeight (OH_Drawing_TextStyle * , int  )
```

**描述：**

设置字重

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| int                  | OH_Drawing_FontWeight枚举类型      |

**起始版本：**

8


### OH_Drawing_SetTextStyleLocale()


```
void OH_Drawing_SetTextStyleLocale (OH_Drawing_TextStyle * , const char *  )
```

**描述：**

设置语言区域

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                 | 描述                               |
| -------------------- | ---------------------------------- |
| OH_Drawing_TextStyle | 指向OH_Drawing_TextStyle对象的指针 |
| char                 | 语言区域，数据类型为指向char的指针 |

**起始版本：**

8


### OH_Drawing_SetTypographyTextAlign()


```
void OH_Drawing_SetTypographyTextAlign (OH_Drawing_TypographyStyle * , int  )
```

**描述：**

设置文本对齐方式

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                       | 描述                                     |
| -------------------------- | ---------------------------------------- |
| OH_Drawing_TypographyStyle | 指向OH_Drawing_TypographyStyle对象的指针 |
| int                        | OH_Drawing_TextAlign枚举类型             |

**起始版本：**

8


### OH_Drawing_SetTypographyTextDirection()


```
void OH_Drawing_SetTypographyTextDirection (OH_Drawing_TypographyStyle * , int  )
```

**描述：**

设置文本方向

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                       | 描述                                     |
| -------------------------- | ---------------------------------------- |
| OH_Drawing_TypographyStyle | 指向OH_Drawing_TypographyStyle对象的指针 |
| int                        | OH_Drawing_TextDirection枚举类型         |

**起始版本：**

8


### OH_Drawing_SetTypographyTextMaxLines()


```
void OH_Drawing_SetTypographyTextMaxLines (OH_Drawing_TypographyStyle * , int  )
```

**描述：**

设置文本最大行数

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                       | 描述                                     |
| -------------------------- | ---------------------------------------- |
| OH_Drawing_TypographyStyle | 指向OH_Drawing_TypographyStyle对象的指针 |
| int                        | 最大行数                                 |

**起始版本：**

8

### OH_Drawing_TypographyGetAlphabeticBaseline()

```
double OH_Drawing_TypographyGetAlphabeticBaseline (OH_Drawing_Typography * )
```

**描述:**

获取字母文字基线

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数:**

| 名称                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |

**返回:**

返回字母文字基线

**起始版本：**

9

### OH_Drawing_TypographyGetHeight()

```
double OH_Drawing_TypographyGetHeight (OH_Drawing_Typography * )
```

**描述:**

获取高度

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数:**

| 名称                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |

**返回:**

返回高度

**起始版本：**

9

### OH_Drawing_TypographyGetIdeographicBaseline()

```
double OH_Drawing_TypographyGetIdeographicBaseline (OH_Drawing_Typography * )
```

**描述:**

获取表意文字基线

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数:**

| 名称                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |

**返回:**

返回表意文字基线

**起始版本：**

9

### OH_Drawing_TypographyGetLongestLine()

```
double OH_Drawing_TypographyGetLongestLine (OH_Drawing_Typography * )
```

**描述:**

获取最长行的宽度，建议实际使用时将返回值向上取整。

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数:**

| 名称                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |

**返回:**

返回最长行的宽度。

**起始版本：**

9

### OH_Drawing_TypographyGetMaxIntrinsicWidth()

```
double OH_Drawing_TypographyGetMaxIntrinsicWidth (OH_Drawing_Typography * )
```

**描述:**

获取最大固有宽度

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数:**

| 名称                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |

**返回:**

返回最大固有宽度

**起始版本：**

9

### OH_Drawing_TypographyGetMaxWidth()

```
double OH_Drawing_TypographyGetMaxWidth (OH_Drawing_Typography * )
```

**描述:**

获取最大宽度

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数:**

| 名称                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |

**返回:**

返回最大宽度

**起始版本：**

9

### OH_Drawing_TypographyGetMinIntrinsicWidth()

```
double OH_Drawing_TypographyGetMinIntrinsicWidth (OH_Drawing_Typography * )
```

**描述:**

获取最小固有宽度

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数:**

| 名称                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |

**返回:**

返回最小固有宽度

**起始版本：**

9

### OH_Drawing_TypographyHandlerAddText()


```
void OH_Drawing_TypographyHandlerAddText (OH_Drawing_TypographyCreate * , const char *  )
```

**描述：**

设置文本内容

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                        | 描述                                      |
| --------------------------- | ----------------------------------------- |
| OH_Drawing_TypographyCreate | 指向OH_Drawing_TypographyCreate对象的指针 |
| char                        | 指向文本内容的指针                        |

**起始版本：**

8


### OH_Drawing_TypographyHandlerPopTextStyle()


```
void OH_Drawing_TypographyHandlerPopTextStyle (OH_Drawing_TypographyCreate * )
```

**描述：**

排版弹出

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                        | 描述                                      |
| --------------------------- | ----------------------------------------- |
| OH_Drawing_TypographyCreate | 指向OH_Drawing_TypographyCreate对象的指针 |

**起始版本：**

8


### OH_Drawing_TypographyHandlerPushTextStyle()


```
void OH_Drawing_TypographyHandlerPushTextStyle (OH_Drawing_TypographyCreate * , OH_Drawing_TextStyle *  )
```

**描述：**

设置排版风格

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                        | 描述                                      |
| --------------------------- | ----------------------------------------- |
| OH_Drawing_TypographyCreate | 指向OH_Drawing_TypographyCreate对象的指针 |
| OH_Drawing_TextStyle        | 指向OH_Drawing_TextStyle对象的指针        |

**起始版本：**

8


### OH_Drawing_TypographyLayout()


```
void OH_Drawing_TypographyLayout (OH_Drawing_Typography * , double  )
```

**描述：**

排版布局

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |
| double                | 文本最大宽度                        |

**起始版本：**

8


### OH_Drawing_TypographyPaint()


```
void OH_Drawing_TypographyPaint (OH_Drawing_Typography * , OH_Drawing_Canvas * , double , double  )
```

**描述：**

显示文本

@syscap SystemCapability.Graphic.Graphic2D.NativeDrawing

**参数：**

| Name                  | 描述                                |
| --------------------- | ----------------------------------- |
| OH_Drawing_Typography | 指向OH_Drawing_Typography对象的指针 |
| OH_Drawing_Canvas     | 指向OH_Drawing_Canvas对象的指针     |
| double                | x坐标                               |
| double                | y坐标                               |

**起始版本：**

8