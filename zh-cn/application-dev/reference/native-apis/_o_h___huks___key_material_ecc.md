# OH_Huks_KeyMaterialEcc


## 概述

定义Ecc密钥的结构体类型。

 **起始版本：**
9

**相关模块:**

[HuksTypeApi](_huks_type_api.md)


## 汇总


### 成员变量

  | 名称 | 描述 | 
| -------- | -------- |
| [keyAlg](#keyalg) | 密钥的算法类型。  | 
| [keySize](#keysize) | 密钥的长度。  | 
| [xSize](#xsize) | x值的长度。  | 
| [ySize](#ysize) | y值的长度。  | 
| [zSize](#zsize) | z值的长度。  | 


## 结构体成员变量说明


### keyAlg

  
```
enum OH_Huks_KeyAlg OH_Huks_KeyMaterialEcc::keyAlg
```
**描述:**
密钥的算法类型。


### keySize

  
```
uint32_t OH_Huks_KeyMaterialEcc::keySize
```
**描述:**
密钥的长度。


### xSize

  
```
uint32_t OH_Huks_KeyMaterialEcc::xSize
```
**描述:**
x值的长度。


### ySize

  
```
uint32_t OH_Huks_KeyMaterialEcc::ySize
```
**描述:**
y值的长度。


### zSize

  
```
uint32_t OH_Huks_KeyMaterialEcc::zSize
```
**描述:**
z值的长度。
