# drawing_font.h


## 概述

文件中定义了与字体相关的功能函数。

**引用文件：**&lt;native_drawing/drawing_font.h&gt;

**库：** libnative_drawing.so

**起始版本：** 11

**相关模块：**[Drawing](_drawing.md)


## 汇总


### 结构体

| 名称 | 描述 | 
| -------- | -------- |
| struct  [OH_Drawing_Font_Metrics](_o_h___drawing___font___metrics.md) | 定义字体度量信息的结构体。 | 


### 类型定义

| 名称 | 描述 | 
| -------- | -------- |
| typedef enum [OH_Drawing_FontEdging](_drawing.md#oh_drawing_fontedging)  [OH_Drawing_FontEdging](_drawing.md#oh_drawing_fontedging) | 字型边缘效果类型枚举。 | 
| typedef enum [OH_Drawing_FontHinting](_drawing.md#oh_drawing_fonthinting)  [OH_Drawing_FontHinting](_drawing.md#oh_drawing_fonthinting) | 字型轮廓效果类型枚举。 | 
| typedef struct [OH_Drawing_Font_Metrics](_o_h___drawing___font___metrics.md)  [OH_Drawing_Font_Metrics](_drawing.md#oh_drawing_font_metrics) | 定义字体度量信息的结构体。 | 


### 枚举

| 名称 | 描述 | 
| -------- | -------- |
| [OH_Drawing_FontEdging](_drawing.md#oh_drawing_fontedging) { FONT_EDGING_ALIAS, FONT_EDGING_ANTI_ALIAS, FONT_EDGING_SUBPIXEL_ANTI_ALIAS } | 字型边缘效果类型枚举。 | 
| [OH_Drawing_FontHinting](_drawing.md#oh_drawing_fonthinting) { FONT_HINTING_NONE, FONT_HINTING_SLIGHT, FONT_HINTING_NORMAL, FONT_HINTING_FULL } | 字型轮廓效果类型枚举。 | 


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| [OH_Drawing_ErrorCode](_drawing.md#oh_drawing_errorcode) [OH_Drawing_FontSetThemeFontFollowed](_drawing.md#oh_drawing_fontsetthemefontfollowed) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*font, bool followed) | 设置字型中的字体是否跟随主题字体。设置跟随主题字体后，若系统启用主题字体并且字型未被设置字体，字型会使用该主题字体。 | 
| [OH_Drawing_ErrorCode](_drawing.md#oh_drawing_errorcode) [OH_Drawing_FontIsThemeFontFollowed](_drawing.md#oh_drawing_fontisthemefontfollowed) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*font, bool \*followed) | 获取字型中的字体是否跟随主题字体。默认不跟随主题字体。 | 
| [OH_Drawing_ErrorCode](_drawing.md#oh_drawing_errorcode) [OH_Drawing_FontMeasureSingleCharacter](_drawing.md#oh_drawing_fontmeasuresinglecharacter) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*font, const char \*str, float \*textWidth) | 用于测量单个字符的宽度。当前字型中的字体不支持待测量字符时，退化到使用系统字体测量字符宽度。  | 
| [OH_Drawing_ErrorCode](_drawing.md#oh_drawing_errorcode) [OH_Drawing_FontMeasureText](_drawing.md#oh_drawing_fontmeasuretext) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*font, const void \*text, size_t byteLength, [OH_Drawing_TextEncoding](_drawing.md#oh_drawing_textencoding) encoding, [OH_Drawing_Rect](_drawing.md#oh_drawing_rect) \*bounds, float \*textWidth) | 用于获取文本的宽度和边界框。 | 
| void [OH_Drawing_FontSetBaselineSnap](_drawing.md#oh_drawing_fontsetbaselinesnap) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, bool baselineSnap) | 当前画布矩阵轴对齐时，将字型基线设置为是否与像素对齐。 | 
| bool [OH_Drawing_FontIsBaselineSnap](_drawing.md#oh_drawing_fontisbaselinesnap) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 当前画布矩阵轴对齐时，获取字型基线是否与像素对齐。 | 
| void [OH_Drawing_FontSetEdging](_drawing.md#oh_drawing_fontsetedging) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, [OH_Drawing_FontEdging](_drawing.md#oh_drawing_fontedging)) | 用于设置字型边缘效果。 | 
| [OH_Drawing_FontEdging](_drawing.md#oh_drawing_fontedging) [OH_Drawing_FontGetEdging](_drawing.md#oh_drawing_fontgetedging) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字型边缘效果。 | 
| void [OH_Drawing_FontSetForceAutoHinting](_drawing.md#oh_drawing_fontsetforceautohinting) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, bool isForceAutoHinting) | 用于设置是否自动调整字型轮廓。 | 
| bool [OH_Drawing_FontIsForceAutoHinting](_drawing.md#oh_drawing_fontisforceautohinting) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字型轮廓是否自动调整。 | 
| void [OH_Drawing_FontSetSubpixel](_drawing.md#oh_drawing_fontsetsubpixel) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, bool isSubpixel) | 设置字型是否使用次像素渲染。 | 
| bool [OH_Drawing_FontIsSubpixel](_drawing.md#oh_drawing_fontissubpixel) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字型是否使用次像素渲染。 | 
| [OH_Drawing_Font](_drawing.md#oh_drawing_font) \* [OH_Drawing_FontCreate](_drawing.md#oh_drawing_fontcreate) (void) | 用于创建一个字型对象。 | 
| void [OH_Drawing_FontSetTypeface](_drawing.md#oh_drawing_fontsettypeface) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, [OH_Drawing_Typeface](_drawing.md#oh_drawing_typeface) \*) | 用于给字型设置字体。 | 
| [OH_Drawing_Typeface](_drawing.md#oh_drawing_typeface) \* [OH_Drawing_FontGetTypeface](_drawing.md#oh_drawing_fontgettypeface) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字体对象。 | 
| void [OH_Drawing_FontSetTextSize](_drawing.md#oh_drawing_fontsettextsize) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, float textSize) | 用于给字型设置文字大小。 | 
| float [OH_Drawing_FontGetTextSize](_drawing.md#oh_drawing_fontgettextsize) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字型文字大小。 | 
| int [OH_Drawing_FontCountText](_drawing.md#oh_drawing_fontcounttext) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, const void \*text, size_t byteLength, [OH_Drawing_TextEncoding](_drawing.md#oh_drawing_textencoding) encoding) | 获取文本所表示的字符数量。 | 
| uint32_t [OH_Drawing_FontTextToGlyphs](_drawing.md#oh_drawing_fonttexttoglyphs) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, const void \*text, uint32_t byteLength, [OH_Drawing_TextEncoding](_drawing.md#oh_drawing_textencoding) encoding, uint16_t \*glyphs, int maxGlyphCount) | 用于将文本转换为字形索引。 | 
| void [OH_Drawing_FontGetWidths](_drawing.md#oh_drawing_fontgetwidths) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, const uint16_t \*glyphs, int count, float \*widths) | 用于获取字符串中每个字符的宽度。 | 
| void [OH_Drawing_FontSetLinearText](_drawing.md#oh_drawing_fontsetlineartext) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, bool isLinearText) | 用于设置线性可缩放字型。 | 
| bool [OH_Drawing_FontIsLinearText](_drawing.md#oh_drawing_fontislineartext) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字型是否使用线性缩放。 | 
| void [OH_Drawing_FontSetTextSkewX](_drawing.md#oh_drawing_fontsettextskewx) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, float skewX) | 用于给字型设置文本倾斜。 | 
| float [OH_Drawing_FontGetTextSkewX](_drawing.md#oh_drawing_fontgettextskewx) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字型文本在x轴上的倾斜度。 | 
| void [OH_Drawing_FontSetFakeBoldText](_drawing.md#oh_drawing_fontsetfakeboldtext) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, bool isFakeBoldText) | 用于设置增加描边宽度以近似粗体字体效果。 | 
| bool [OH_Drawing_FontIsFakeBoldText](_drawing.md#oh_drawing_fontisfakeboldtext) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取是否增加笔画宽度以接近粗体字体。 | 
| void [OH_Drawing_FontSetScaleX](_drawing.md#oh_drawing_fontsetscalex) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, float scaleX) | 用于设置字型对象在x轴上的缩放比例。 | 
| float [OH_Drawing_FontGetScaleX](_drawing.md#oh_drawing_fontgetscalex) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字型对象在x轴上的缩放比例。 | 
| void [OH_Drawing_FontSetHinting](_drawing.md#oh_drawing_fontsethinting) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, [OH_Drawing_FontHinting](_drawing.md#oh_drawing_fonthinting)) | 用于设置字型轮廓效果。 | 
| [OH_Drawing_FontHinting](_drawing.md#oh_drawing_fonthinting) [OH_Drawing_FontGetHinting](_drawing.md#oh_drawing_fontgethinting) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字型轮廓效果枚举类型。 | 
| void [OH_Drawing_FontSetEmbeddedBitmaps](_drawing.md#oh_drawing_fontsetembeddedbitmaps) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, bool isEmbeddedBitmaps) | 用于设置字型是否转换成位图处理。 | 
| bool [OH_Drawing_FontIsEmbeddedBitmaps](_drawing.md#oh_drawing_fontisembeddedbitmaps) (const [OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 获取字型是否转换成位图处理。 | 
| void [OH_Drawing_FontDestroy](_drawing.md#oh_drawing_fontdestroy) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*) | 用于销毁字型对象并回收该对象占有的内存。 | 
| float [OH_Drawing_FontGetMetrics](_drawing.md#oh_drawing_fontgetmetrics) ([OH_Drawing_Font](_drawing.md#oh_drawing_font) \*, [OH_Drawing_Font_Metrics](_o_h___drawing___font___metrics.md) \*) | 获取字体度量信息。 | 
