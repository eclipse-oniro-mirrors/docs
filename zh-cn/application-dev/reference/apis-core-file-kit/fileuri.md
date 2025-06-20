# FileUri


## 概述

文件统一资源标识符（File Uniform Resource Identifier）。

支持fileuri与路径path的转换、有效性校验、以及指向的变换（指向的文件或路径）。

该类主要用于 uri 格式验证和 uri 转换处理。 且uri用于应用间文件分享场景，将应用沙箱路径按照固定关系转换为uri;

调用者需保证所有接口入参的有效性，接口按照固定规则转换输出结果，并不检查其是否存在。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 12


## 汇总


### 文件

| 名称 | 描述 | 
| -------- | -------- |
| [oh_file_uri.h](oh__file__uri_8h.md) | 提供uri和路径path之间的相互转换，目录uri获取，以及uri的有效性校验的方法。  | 


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| [FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode)[OH_FileUri_GetUriFromPath](#oh_fileuri_geturifrompath) (const char \*path, unsigned int length, char \*\*result) | 通过传入的路径path生成应用自己的uri；<br/>将path转uri时，路径中的中文及非数字字母的特殊字符将会被编译成对应的ASCII码，拼接在uri中。 | 
| [FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode)[OH_FileUri_GetPathFromUri](#oh_fileuri_getpathfromuri) (const char \*uri, unsigned int length, char \*\*result) | 将uri转换成对应的沙箱路径path。<br/>1、uri转path过程中会将uri中存在的ASCII码进行解码后拼接在原处，非系统接口生成的uri中可能存在ASCII码解析范围之外的字符， 导致字符串无法正常拼接； 2、转换处理为系统约定的字符串替换规则（规则随系统演进可能会发生变化），转换过程中不进行路径校验操作，无法保证转换结果的一定可以访问。 | 
| [FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode)[OH_FileUri_GetFullDirectoryUri](#oh_fileuri_getfulldirectoryuri) (const char \*uri, unsigned int length, char \*\*result) | 获取所在路径uri。uri指向文件则返回所在路径的uri，uri指向目录则不处理直接返回原串；<br/>uri指向的文件不存在或属性获取失败则返回空串。 | 
| bool [OH_FileUri_IsValidUri](#oh_fileuri_isvaliduri) (const char \*uri, unsigned int length) | 判断传入的uri的格式是否正确。仅校验uri是否满足系统定义的格式规范，不校验uri的有效性。  | 
| [FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode)[OH_FileUri_GetFileName](#oh_fileuri_getfilename) (const char \*uri, unsigned int length, char \*\*result) | 通过传入的uri获取到对应的文件名称。（如果文件名中存在ASCII码将会被解码处理后拼接在原处）。  | 


## 函数说明


### OH_FileUri_GetFullDirectoryUri()

```
FileManagement_ErrCode OH_FileUri_GetFullDirectoryUri (const char * uri, unsigned int length, char ** result )
```
**描述**
获取所在路径uri。uri指向文件则返回所在路径的uri，uri指向目录则不处理直接返回原串；

uri指向的文件不存在或属性获取失败则返回空串。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| uri | 表示要获取目录的uri的原始uri。  | 
| length | 表示原始uri的字节长度。  | 
| result | 表示获取到的目录uri，需要使用standard library标准库的free()方法释放申请的资源。  | 

**返回：**

返回特定的错误码值，详细信息可以查看[FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode)。


### OH_FileUri_GetPathFromUri()

```
FileManagement_ErrCode OH_FileUri_GetPathFromUri (const char * uri, unsigned int length, char ** result )
```
**描述**
将uri转换成对应的沙箱路径path。

1、uri转path过程中会将uri中存在的ASCII码进行解码后拼接在原处，非系统接口生成的uri中可能存在ASCII码解析范围之外的字符，导致字符串无法正常拼接；2、转换处理为系统约定的字符串替换规则（规则随系统演进可能会发生变化），转换过程中不进行路径校验操作，无法保证转换结果的一定可以访问。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| uri | 表示要转换的uri。 | 
| length | 表示要转换uri的字节长度。 | 
| result | 表示转换后的路径path。需要使用standard library标准库的free()方法释放申请的资源。 | 

**返回：**

返回特定的错误码值，详细信息可以查看[FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode)。


### OH_FileUri_GetUriFromPath()

```
FileManagement_ErrCode OH_FileUri_GetUriFromPath (const char * path, unsigned int length, char ** result )
```
**描述**
通过传入的路径path生成应用自己的uri；

将path转uri时，路径中的中文及非数字字母的特殊字符将会被编译成对应的ASCII码，拼接在uri中。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| path | 表示要转换的路径。  | 
| length | 表示要转换路径的字节长度。  | 
| result | 表示转换后的uri, 需要使用standard library标准库的free()方法释放申请的资源。  | 

**返回：**

返回特定的错误码值，详细信息可以查看[FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode)。


### OH_FileUri_IsValidUri()

```
bool OH_FileUri_IsValidUri (const char * uri, unsigned int length )
```
**描述**
判断传入的uri的格式是否正确。仅校验uri是否满足系统定义的格式规范，不校验uri的有效性。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 12

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| uri | 表示需要校验的uri。  | 
| length | 需要校验uri的字节长度。  | 

**返回：**

true: 传入uri是有效的uri；false: 传入的uri是无效的uri。

### OH_FileUri_GetFileName()

```
FileManagement_ErrCode OH_FileUri_GetFileName (const char * uri, unsigned int length, char ** result )
```

**描述**

通过传入的uri获取到对应的文件名称。（如果文件名中存在ASCII码将会被解码处理后拼接在原处）。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 13

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| uri | 传入的uri。  | 
| length | 表示传入uri的字节长度。  | 
| result | 表示转换后的名称。需要使用standard library标准库的free()方法释放申请的资源。  | 

**返回**：

返回特定的错误码值，详细信息可以查看[FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode)。