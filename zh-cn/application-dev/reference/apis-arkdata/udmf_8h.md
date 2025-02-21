# udmf.h


## 概述

提供访问统一数据管理框架数据的接口、数据结构、枚举类型。

**引用文件：**&lt;database/udmf/udmf.h&gt;

**库：** libudmf.so

**系统能力：** SystemCapability.DistributedDataManager.UDMF.Core

**起始版本：** 12

**相关模块：**[UDMF](_u_d_m_f.md)


## 汇总


### 宏定义

| 名称 | 描述 | 
| -------- | -------- |
| [UDMF_KEY_BUFFER_LEN](_u_d_m_f.md#udmf_key_buffer_len)&nbsp;&nbsp;&nbsp;(512) | 统一数据对象唯一标识符最小空间长度。 | 


### 类型定义

| 名称 | 描述 | 
| -------- | -------- |
| typedef enum [Udmf_Intention](_u_d_m_f.md#udmf_intention) [Udmf_Intention](_u_d_m_f.md#udmf_intention) | 描述UDMF数据通路枚举类型。 | 
| typedef enum [Udmf_ShareOption](_u_d_m_f.md#udmf_shareoption) [Udmf_ShareOption](_u_d_m_f.md#udmf_shareoption) | UDMF支持的设备内使用范围类型枚举。 | 
| typedef struct [OH_UdmfData](_u_d_m_f.md#oh_udmfdata) [OH_UdmfData](_u_d_m_f.md#oh_udmfdata) | 定义统一数据对象数据结构。 | 
| typedef struct [OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) [OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) | 定义统一数据对象中记录数据的数据结构，称为数据记录。 | 
| typedef struct [OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) [OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) | 定义统一数据对象中数据记录的属性结构。 | 


### 枚举

| 名称 | 描述 | 
| -------- | -------- |
| [Udmf_Intention](_u_d_m_f.md#udmf_intention) { UDMF_INTENTION_DRAG, UDMF_INTENTION_PASTEBOARD } | 描述UDMF数据通路枚举类型。 | 
| [Udmf_ShareOption](_u_d_m_f.md#udmf_shareoption) { SHARE_OPTIONS_INVALID, SHARE_OPTIONS_IN_APP, SHARE_OPTIONS_CROSS_APP } | UDMF支持的设备内使用范围类型枚举。 | 


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| [OH_UdmfData](_u_d_m_f.md#oh_udmfdata) \* [OH_UdmfData_Create](_u_d_m_f.md#oh_udmfdata_create) () | 创建统一数据对象[OH_UdmfData](_u_d_m_f.md#oh_udmfdata)指针及实例对象。 | 
| void [OH_UdmfData_Destroy](_u_d_m_f.md#oh_udmfdata_destroy) ([OH_UdmfData](_u_d_m_f.md#oh_udmfdata) \*pThis) | 销毁统一数据对象[OH_UdmfData](_u_d_m_f.md#oh_udmfdata)指针指向的实例对象。 | 
| int [OH_UdmfData_AddRecord](_u_d_m_f.md#oh_udmfdata_addrecord) ([OH_UdmfData](_u_d_m_f.md#oh_udmfdata) \*pThis, [OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*record) | 添加一个数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)到统一数据对象[OH_UdmfData](_u_d_m_f.md#oh_udmfdata)中。 | 
| bool [OH_UdmfData_HasType](_u_d_m_f.md#oh_udmfdata_hastype) ([OH_UdmfData](_u_d_m_f.md#oh_udmfdata) \*pThis, const char \*type) | 检查统一数据对象[OH_UdmfData](_u_d_m_f.md#oh_udmfdata)中是否存在指定类型。 | 
| char \*\* [OH_UdmfData_GetTypes](_u_d_m_f.md#oh_udmfdata_gettypes) ([OH_UdmfData](_u_d_m_f.md#oh_udmfdata) \*pThis, unsigned int \*count) | 获取统一数据对象[OH_UdmfData](_u_d_m_f.md#oh_udmfdata)中包含的所有类型结果集。 | 
| [OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*\* [OH_UdmfData_GetRecords](_u_d_m_f.md#oh_udmfdata_getrecords) ([OH_UdmfData](_u_d_m_f.md#oh_udmfdata) \*pThis, unsigned int \*count) | 获取统一数据对象[OH_UdmfData](_u_d_m_f.md#oh_udmfdata)中包含的所有记录结果集。 | 
| [OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \* [OH_UdmfRecord_Create](_u_d_m_f.md#oh_udmfrecord_create) () | 创建统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)指针及实例对象。 | 
| void [OH_UdmfRecord_Destroy](_u_d_m_f.md#oh_udmfrecord_destroy) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis) | 销毁统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)指针指向的实例对象。 | 
| int [OH_UdmfRecord_AddGeneralEntry](_u_d_m_f.md#oh_udmfrecord_addgeneralentry) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, const char \*typeId, unsigned char \*entry, unsigned int count) | 添加用户自定义的通用数据至统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中。对于已定义UDS的类型（比如PlainText、Link、Pixelmap等）不可使用该接口。 | 
| int [OH_UdmfRecord_AddPlainText](_u_d_m_f.md#oh_udmfrecord_addplaintext) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) \*plainText) | 增加纯文本类型[OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext)数据至统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中。 | 
| int [OH_UdmfRecord_AddHyperlink](_u_d_m_f.md#oh_udmfrecord_addhyperlink) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) \*hyperlink) | 增加超链接类型[OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink)数据至统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中。 | 
| int [OH_UdmfRecord_AddHtml](_u_d_m_f.md#oh_udmfrecord_addhtml) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) \*html) | 增加超文本标记语言类型[OH_UdsHtml](_u_d_m_f.md#oh_udshtml)数据至统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中。 | 
| int [OH_UdmfRecord_AddAppItem](_u_d_m_f.md#oh_udmfrecord_addappitem) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*appItem) | 增加桌面图标类型[OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem)数据至统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中。 | 
| char \*\* [OH_UdmfRecord_GetTypes](_u_d_m_f.md#oh_udmfrecord_gettypes) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, unsigned int \*count) | 获取统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中所有类型的结果集。 | 
| int [OH_UdmfRecord_GetGeneralEntry](_u_d_m_f.md#oh_udmfrecord_getgeneralentry) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, const char \*typeId, unsigned char \*\*entry, unsigned int \*count) | 获取统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中的特定类型的数据结果集。 | 
| int [OH_UdmfRecord_GetPlainText](_u_d_m_f.md#oh_udmfrecord_getplaintext) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) \*plainText) | 从统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中获取纯文本类型[OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext)数据。 | 
| int [OH_UdmfRecord_GetHyperlink](_u_d_m_f.md#oh_udmfrecord_gethyperlink) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) \*hyperlink) | 从统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中获取超链接类型[OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink)数据。 | 
| int [OH_UdmfRecord_GetHtml](_u_d_m_f.md#oh_udmfrecord_gethtml) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) \*html) | 从统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中获取超文本标记语言类型[OH_UdsHtml](_u_d_m_f.md#oh_udshtml)数据。 | 
| int [OH_UdmfRecord_GetAppItem](_u_d_m_f.md#oh_udmfrecord_getappitem) ([OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord) \*pThis, [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*appItem) | 从统一数据记录[OH_UdmfRecord](_u_d_m_f.md#oh_udmfrecord)中获取桌面图标类型[OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem)数据。 | 
| [OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \* [OH_UdmfProperty_Create](_u_d_m_f.md#oh_udmfproperty_create) ([OH_UdmfData](_u_d_m_f.md#oh_udmfdata) \*unifiedData) | 创建统一数据对象中数据记录属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)指针及实例对象。 | 
| void [OH_UdmfProperty_Destroy](_u_d_m_f.md#oh_udmfproperty_destroy) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis) | 销毁数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)指针指向的实例对象。 | 
| const char \* [OH_UdmfProperty_GetTag](_u_d_m_f.md#oh_udmfproperty_gettag) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis) | 从数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)中获取用户自定义标签值。 | 
| int64_t [OH_UdmfProperty_GetTimestamp](_u_d_m_f.md#oh_udmfproperty_gettimestamp) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis) | 从数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)中获取时间戳。 | 
| [Udmf_ShareOption](_u_d_m_f.md#udmf_shareoption)[OH_UdmfProperty_GetShareOption](_u_d_m_f.md#oh_udmfproperty_getshareoption) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis) | 从数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)中获取设备内适用范围属性。 | 
| int [OH_UdmfProperty_GetExtrasIntParam](_u_d_m_f.md#oh_udmfproperty_getextrasintparam) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis, const char \*key, int defaultValue) | 从数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)中获取自定义的附加整型参数。 | 
| const char \* [OH_UdmfProperty_GetExtrasStringParam](_u_d_m_f.md#oh_udmfproperty_getextrasstringparam) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis, const char \*key) | 从数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)中获取自定义的附加字符串参数。 | 
| int [OH_UdmfProperty_SetTag](_u_d_m_f.md#oh_udmfproperty_settag) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis, const char \*tag) | 设置数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)的自定义标签值。 | 
| int [OH_UdmfProperty_SetShareOption](_u_d_m_f.md#oh_udmfproperty_setshareoption) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis, [Udmf_ShareOption](_u_d_m_f.md#udmf_shareoption) option) | 设置数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)的设备内适用范围OH_Udmf_ShareOption参数。 | 
| int [OH_UdmfProperty_SetExtrasIntParam](_u_d_m_f.md#oh_udmfproperty_setextrasintparam) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis, const char \*key, int param) | 设置数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)的附加整型参数。 | 
| int [OH_UdmfProperty_SetExtrasStringParam](_u_d_m_f.md#oh_udmfproperty_setextrasstringparam) ([OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty) \*pThis, const char \*key, const char \*param) | 设置数据属性[OH_UdmfProperty](_u_d_m_f.md#oh_udmfproperty)的附加字符串参数。 | 
| int [OH_Udmf_GetUnifiedData](_u_d_m_f.md#oh_udmf_getunifieddata) (const char \*key, [Udmf_Intention](_u_d_m_f.md#udmf_intention) intention, [OH_UdmfData](_u_d_m_f.md#oh_udmfdata) \*unifiedData) | 从统一数据管理框架数据库中获取统一数据对象[OH_UdmfData](_u_d_m_f.md#oh_udmfdata)数据。 | 
| int [OH_Udmf_SetUnifiedData](_u_d_m_f.md#oh_udmf_setunifieddata) ([Udmf_Intention](_u_d_m_f.md#udmf_intention) intention, [OH_UdmfData](_u_d_m_f.md#oh_udmfdata) \*unifiedData, char \*key, unsigned int keyLen) | 从统一数据管理框架数据库中写入统一数据对象[OH_UdmfData](_u_d_m_f.md#oh_udmfdata)数据。 | 
