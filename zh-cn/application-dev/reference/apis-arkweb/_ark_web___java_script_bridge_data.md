# ArkWeb_JavaScriptBridgeData


## 概述

定义JavaScript Bridge数据的基础结构。

**起始版本：** 12

**相关模块：**[Web](_web.md)


## 汇总


### 成员变量

| 名称 | 描述 | 
| -------- | -------- |
| const uint8_t \* [buffer](#buffer) | 指向传输数据的指针。仅支持前端传入String和ArrayBuffer类型，其余类型会被json序列化后，以String类型传递。  | 
| size_t [size](#size) | 传输数据的长度。  | 


## 结构体成员变量说明


### buffer

```
const uint8_t* ArkWeb_JavaScriptBridgeData::buffer
```
**描述：**

指向传输数据的指针。仅支持前端传入String和ArrayBuffer类型，其余类型会被json序列化后，以String类型传递。


### size

```
size_t ArkWeb_JavaScriptBridgeData::size
```
**描述：**

传输数据的长度。
