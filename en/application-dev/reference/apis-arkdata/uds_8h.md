# uds.h


## Overview

Defines the APIs and structs related to the uniform data structs.

**File to include**: &lt;database/udmf/uds.h&gt;

**Library**: libudmf.so

**System capability**: SystemCapability.DistributedDataManager.UDMF.Core

**Since**: 12

**Related module**: [UDMF](_u_d_m_f.md)


## Summary


### Types

| Name| Description| 
| -------- | -------- |
| typedef struct [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) | Defines a struct for the uniform data of the plain text type.| 
| typedef struct [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) | Defines a struct for the uniform data of the hyperlink type.| 
| typedef struct [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) | Defines a struct for the uniform data of the Hypertext Markup Language (HTML) type.| 
| typedef struct [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) | Defines a struct for the uniform data of the home screen icon type.| 
| typedef struct [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) | Defines a struct for the uniform data of the file URI type.| 
| typedef struct [OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) [OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) | Defines a struct for the uniform data of the pixel map type.| 
| typedef struct [OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) [OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) | Defines a struct for the uniform data of the ArrayBuffer type.| 
| typedef struct [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) | Defines a struct for the uniform data of the content widget type.| 

### Functions

| Name| Description| 
| -------- | -------- |
| [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) \* [OH_UdsPlainText_Create](_u_d_m_f.md#oh_udsplaintext_create) () | Creates an [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) instance and a pointer to it. If this pointer is no longer required, use [OH_UdsPlainText_Destroy](_u_d_m_f.md#oh_udsplaintext_destroy) to destroy it. Otherwise, memory leaks may occur.| 
| void [OH_UdsPlainText_Destroy](_u_d_m_f.md#oh_udsplaintext_destroy) ([OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) \*pThis) | Destroys an [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) instance.| 
| const char \* [OH_UdsPlainText_GetType](_u_d_m_f.md#oh_udsplaintext_gettype) ([OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) \*pThis) | Obtains the type ID from an [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) instance.| 
| const char \* [OH_UdsPlainText_GetContent](_u_d_m_f.md#oh_udsplaintext_getcontent) ([OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) \*pThis) | Obtains the plaintext from an [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) instance.| 
| const char \* [OH_UdsPlainText_GetAbstract](_u_d_m_f.md#oh_udsplaintext_getabstract) ([OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) \*pThis) | Obtains the abstract from an [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) instance.| 
| int [OH_UdsPlainText_SetContent](_u_d_m_f.md#oh_udsplaintext_setcontent) ([OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) \*pThis, const char \*content) | Sets the plaintext content for an [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) instance.| 
| int [OH_UdsPlainText_SetAbstract](_u_d_m_f.md#oh_udsplaintext_setabstract) ([OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) \*pThis, const char \*abstract) | Sets the abstract for an [OH_UdsPlainText](_u_d_m_f.md#oh_udsplaintext) instance.| 
| [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) \* [OH_UdsHyperlink_Create](_u_d_m_f.md#oh_udshyperlink_create) () | Creates an [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) instance and a pointer to it. If this pointer is no longer required, use [OH_UdsHyperlink_Destroy](_u_d_m_f.md#oh_udshyperlink_destroy) to destroy it. Otherwise, memory leaks may occur.| 
| void [OH_UdsHyperlink_Destroy](_u_d_m_f.md#oh_udshyperlink_destroy) ([OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) \*pThis) | Destroys an [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) instance.| 
| const char \* [OH_UdsHyperlink_GetType](_u_d_m_f.md#oh_udshyperlink_gettype) ([OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) \*pThis) | Obtains the type ID from an [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) instance.| 
| const char \* [OH_UdsHyperlink_GetUrl](_u_d_m_f.md#oh_udshyperlink_geturl) ([OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) \*pThis) | Obtains the URL from an [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) instance.| 
| const char \* [OH_UdsHyperlink_GetDescription](_u_d_m_f.md#oh_udshyperlink_getdescription) ([OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) \*pThis) | Obtains the description from an [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) instance.| 
| int [OH_UdsHyperlink_SetUrl](_u_d_m_f.md#oh_udshyperlink_seturl) ([OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) \*pThis, const char \*url) | Sets the URL for an [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) instance.| 
| int [OH_UdsHyperlink_SetDescription](_u_d_m_f.md#oh_udshyperlink_setdescription) ([OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) \*pThis, const char \*description) | Sets the description for an [OH_UdsHyperlink](_u_d_m_f.md#oh_udshyperlink) instance.| 
| [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) \* [OH_UdsHtml_Create](_u_d_m_f.md#oh_udshtml_create) () | Creates an [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) instance and a pointer to it. If this pointer is no longer required, use [OH_UdsHtml_Destroy](_u_d_m_f.md#oh_udshtml_destroy) to destroy it. Otherwise, memory leaks may occur.| 
| void [OH_UdsHtml_Destroy](_u_d_m_f.md#oh_udshtml_destroy) ([OH_UdsHtml](_u_d_m_f.md#oh_udshtml) \*pThis) | Destroys an [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) instance.| 
| const char \* [OH_UdsHtml_GetType](_u_d_m_f.md#oh_udshtml_gettype) ([OH_UdsHtml](_u_d_m_f.md#oh_udshtml) \*pThis) | Obtains the type ID from an [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) instance.| 
| const char \* [OH_UdsHtml_GetContent](_u_d_m_f.md#oh_udshtml_getcontent) ([OH_UdsHtml](_u_d_m_f.md#oh_udshtml) \*pThis) | Obtains the HTML content from an [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) instance.| 
| const char \* [OH_UdsHtml_GetPlainContent](_u_d_m_f.md#oh_udshtml_getplaincontent) ([OH_UdsHtml](_u_d_m_f.md#oh_udshtml) \*pThis) | Obtains the plaintext from an [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) instance.| 
| int [OH_UdsHtml_SetContent](_u_d_m_f.md#oh_udshtml_setcontent) ([OH_UdsHtml](_u_d_m_f.md#oh_udshtml) \*pThis, const char \*content) | Sets the HTML content for an [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) instance.| 
| int [OH_UdsHtml_SetPlainContent](_u_d_m_f.md#oh_udshtml_setplaincontent) ([OH_UdsHtml](_u_d_m_f.md#oh_udshtml) \*pThis, const char \*plainContent) | Sets the plaintext for an [OH_UdsHtml](_u_d_m_f.md#oh_udshtml) instance.| 
| [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \* [OH_UdsAppItem_Create](_u_d_m_f.md#oh_udsappitem_create) () | Creates an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance and a pointer to it. If this pointer is no longer required, use [OH_UdsAppItem_Destroy](_u_d_m_f.md#oh_udsappitem_destroy) to destroy it. Otherwise, memory leaks may occur.| 
| void [OH_UdsAppItem_Destroy](_u_d_m_f.md#oh_udsappitem_destroy) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis) | Destroys an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| const char \* [OH_UdsAppItem_GetType](_u_d_m_f.md#oh_udsappitem_gettype) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis) | Obtains the type ID from an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| const char \* [OH_UdsAppItem_GetId](_u_d_m_f.md#oh_udsappitem_getid) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis) | Obtains the application ID from an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| const char \* [OH_UdsAppItem_GetName](_u_d_m_f.md#oh_udsappitem_getname) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis) | Obtains the application name from an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| const char \* [OH_UdsAppItem_GetIconId](_u_d_m_f.md#oh_udsappitem_geticonid) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis) | Obtains the application icon ID from an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| const char \* [OH_UdsAppItem_GetLabelId](_u_d_m_f.md#oh_udsappitem_getlabelid) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis) | Obtains the application label ID from an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| const char \* [OH_UdsAppItem_GetBundleName](_u_d_m_f.md#oh_udsappitem_getbundlename) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis) | Obtains the bundle name from an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| const char \* [OH_UdsAppItem_GetAbilityName](_u_d_m_f.md#oh_udsappitem_getabilityname) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis) | Obtain the ability name from an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| int [OH_UdsAppItem_SetId](_u_d_m_f.md#oh_udsappitem_setid) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis, const char \*appId) | Sets the application ID for an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| int [OH_UdsAppItem_SetName](_u_d_m_f.md#oh_udsappitem_setname) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis, const char \*appName) | Sets the application name for an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| int [OH_UdsAppItem_SetIconId](_u_d_m_f.md#oh_udsappitem_seticonid) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis, const char \*appIconId) | Sets the application icon ID for an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| int [OH_UdsAppItem_SetLabelId](_u_d_m_f.md#oh_udsappitem_setlabelid) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis, const char \*appLabelId) | Sets the application label ID for an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| int [OH_UdsAppItem_SetBundleName](_u_d_m_f.md#oh_udsappitem_setbundlename) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis, const char \*bundleName) | Sets the bundle name for an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| int [OH_UdsAppItem_SetAbilityName](_u_d_m_f.md#oh_udsappitem_setabilityname) ([OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) \*pThis, const char \*abilityName) | Sets the ability name for an [OH_UdsAppItem](_u_d_m_f.md#oh_udsappitem) instance.| 
| [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) \* [OH_UdsFileUri_Create](_u_d_m_f.md#oh_udsfileuri_create) () | Creates an [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) instance and a pointer to it. If this pointer is no longer required, use [OH_UdsFileUri_Destroy](_u_d_m_f.md#oh_udsfileuri_destroy) to destroy it. Otherwise, memory leaks may occur.| 
| void [OH_UdsFileUri_Destroy](_u_d_m_f.md#oh_udsfileuri_destroy) ([OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) \*pThis) | Destroys an [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) instance.| 
| const char \* [OH_UdsFileUri_GetType](_u_d_m_f.md#oh_udsfileuri_gettype) ([OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) \*pThis) | Obtains the type ID from an [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) instance.| 
| const char \* [OH_UdsFileUri_GetFileUri](_u_d_m_f.md#oh_udsfileuri_getfileuri) ([OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) \*pThis) | Obtains the file URI from an [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) instance.| 
| const char \* [OH_UdsFileUri_GetFileType](_u_d_m_f.md#oh_udsfileuri_getfiletype) ([OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) \*pThis) | Obtains the file type from an [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) instance.| 
| int [OH_UdsFileUri_SetFileUri](_u_d_m_f.md#oh_udsfileuri_setfileuri) ([OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) \*pThis, const char \*fileUri) | Sets the URI information for an [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) instance.| 
| int [OH_UdsFileUri_SetFileType](_u_d_m_f.md#oh_udsfileuri_setfiletype) ([OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) \*pThis, const char \*fileType) | Sets the file type for an [OH_UdsFileUri](_u_d_m_f.md#oh_udsfileuri) instance.| 
| [OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) \* [OH_UdsPixelMap_Create](_u_d_m_f.md#oh_udspixelmap_create) () | Creates an [OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) instance and a pointer to it. If this pointer is no longer required, use [OH_UdsPixelMap_Destroy](_u_d_m_f.md#oh_udspixelmap_destroy) to destroy it. Otherwise, memory leaks may occur.| 
| void [OH_UdsPixelMap_Destroy](_u_d_m_f.md#oh_udspixelmap_destroy) ([OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) \*pThis) | Destroys an [OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) instance.| 
| const char \* [OH_UdsPixelMap_GetType](_u_d_m_f.md#oh_udspixelmap_gettype) ([OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) \*pThis) | Obtains the type ID from an [OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) instance.| 
| void [OH_UdsPixelMap_GetPixelMap](_u_d_m_f.md#oh_udspixelmap_getpixelmap) ([OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) \*pThis, OH_PixelmapNative \*pixelmapNative) | Obtains the pointer to the **OH_PixelmapNative** instance from an [OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) instance.| 
| int [OH_UdsPixelMap_SetPixelMap](_u_d_m_f.md#oh_udspixelmap_setpixelmap) ([OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) \*pThis, OH_PixelmapNative \*pixelmapNative) | Sets the pixel map content for an [OH_UdsPixelMap](_u_d_m_f.md#oh_udspixelmap) instance.| 
| [OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) \* [OH_UdsArrayBuffer_Create](_u_d_m_f.md#oh_udsarraybuffer_create) () | Creates an [OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) instance and a pointer to it. If this pointer is no longer required, use [OH_UdsArrayBuffer_Destroy](_u_d_m_f.md#oh_udsarraybuffer_destroy) to destroy it. Otherwise, memory leaks may occur.| 
| int [OH_UdsArrayBuffer_Destroy](_u_d_m_f.md#oh_udsarraybuffer_destroy) ([OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) \*buffer) | Destroys an [OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) instance.| 
| int [OH_UdsArrayBuffer_SetData](_u_d_m_f.md#oh_udsarraybuffer_setdata) ([OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) \*buffer, unsigned char \*data, unsigned int len) | Sets data for an [OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) instance.| 
| int [OH_UdsArrayBuffer_GetData](_u_d_m_f.md#oh_udsarraybuffer_getdata) ([OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) \*buffer, unsigned char \*\*data, unsigned int \*len) | Obtains the custom ArrayBuffer from an [OH_UdsArrayBuffer](_u_d_m_f.md#oh_udsarraybuffer) instance.| 
| [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \* [OH_UdsContentForm_Create](_u_d_m_f.md#oh_udscontentform_create) () | Creates an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance and a pointer to it.| 
| void [OH_UdsContentForm_Destroy](_u_d_m_f.md#oh_udscontentform_destroy) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis) | Destroys an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| const char \* [OH_UdsContentForm_GetType](_u_d_m_f.md#oh_udscontentform_gettype) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis) | Obtains the type ID from an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| int [OH_UdsContentForm_GetThumbData](_u_d_m_f.md#oh_udscontentform_getthumbdata) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis, unsigned char \*\*thumbData, unsigned int \*len) | Obtains image data from an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| const char \* [OH_UdsContentForm_GetDescription](_u_d_m_f.md#oh_udscontentform_getdescription) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis) | Obtains the description from an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| const char \* [OH_UdsContentForm_GetTitle](_u_d_m_f.md#oh_udscontentform_gettitle) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis) | Obtains the title from an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| int [OH_UdsContentForm_GetAppIcon](_u_d_m_f.md#oh_udscontentform_getappicon) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis, unsigned char \*\*appIcon, unsigned int \*len) | Obtains the application icon data from an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| const char \* [OH_UdsContentForm_GetAppName](_u_d_m_f.md#oh_udscontentform_getappname) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis) | Obtains the application name from an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| const char \* [OH_UdsContentForm_GetLinkUri](_u_d_m_f.md#oh_udscontentform_getlinkuri) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis) | Obtains the hyperlink information from an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| int [OH_UdsContentForm_SetThumbData](_u_d_m_f.md#oh_udscontentform_setthumbdata) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis, const unsigned char \*thumbData, unsigned int len) | Sets the image data for an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| int [OH_UdsContentForm_SetDescription](_u_d_m_f.md#oh_udscontentform_setdescription) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis, const char \*description) | Sets the description for an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| int [OH_UdsContentForm_SetTitle](_u_d_m_f.md#oh_udscontentform_settitle) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis, const char \*title) | Sets the title for an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| int [OH_UdsContentForm_SetAppIcon](_u_d_m_f.md#oh_udscontentform_setappicon) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis, const unsigned char \*appIcon, unsigned int len) | Sets the application icon data for an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| int [OH_UdsContentForm_SetAppName](_u_d_m_f.md#oh_udscontentform_setappname) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis, const char \*appName) | Sets the application name for an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
| int [OH_UdsContentForm_SetLinkUri](_u_d_m_f.md#oh_udscontentform_setlinkuri) ([OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) \*pThis, const char \*linkUri) | Sets the hyperlink data for an [OH_UdsContentForm](_u_d_m_f.md#oh_udscontentform) instance.| 
