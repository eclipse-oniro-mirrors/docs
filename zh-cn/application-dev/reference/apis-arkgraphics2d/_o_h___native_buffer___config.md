# OH_NativeBuffer_Config


## 概述

OH_NativeBuffer的属性配置，用于申请新的OH_NativeBuffer实例或查询现有实例的相关属性。

\@syscap SystemCapability.Graphic.Graphic2D.NativeBuffer

**起始版本：** 9

**相关模块：**[OH_NativeBuffer](_o_h___native_buffer.md)

**所在头文件：**[native_buffer.h](native__buffer_8h.md)

## 汇总


### 成员变量

| 名称 | 描述 |
| -------- | -------- |
| [width](#width) | 宽度（像素）。 |
| [height](#height) | 高度（像素）。 |
| [format](#format) | 像素格式，具体可参见[OH_NativeBuffer_Format](_o_h___native_buffer.md#oh_nativebuffer_format-1)枚举。 |
| [usage](#usage) | buffer的用途说明，具体可参见[OH_NativeBuffer_Usage](_o_h___native_buffer.md#oh_nativebuffer_usage-1)枚举。 |
| [stride](#stride) | 输出参数。本地窗口缓冲区步幅，单位为Byte。 |


## 结构体成员变量说明


### format

```
int32_t OH_NativeBuffer_Config::format
```

**描述:**

像素格式。


### height

```
int32_t OH_NativeBuffer_Config::height
```

**描述:**

高度（像素）。


### stride

```
int32_t OH_NativeBuffer_Config::stride
```

**描述:**

输出参数。本地窗口缓冲区步幅，单位为Byte。

**起始版本：**

10


### usage

```
int32_t OH_NativeBuffer_Config::usage
```

**描述:**

buffer的用途说明。


### width

```
int32_t OH_NativeBuffer_Config::width
```

**描述:**

宽度（像素）。
