# styled_string.h


## Overview

Provides styled string APIs of ArkUI on the native side.

**Library**: libace_ndk.z.so

**File to include**: <arkui/styled_string.h>

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Since**: 12

**Related module**: [ArkUI_NativeModule](_ark_u_i___native_module.md)


## Summary


### Types

| Name| Description| 
| -------- | -------- |
| typedef struct [ArkUI_StyledString](_ark_u_i___native_module.md#arkui_styledstring) [ArkUI_StyledString](_ark_u_i___native_module.md#arkui_styledstring) | Defines a styled string object supported by the text component. | 


### Functions

| Name| Description| 
| -------- | -------- |
| [ArkUI_StyledString](_ark_u_i___native_module.md#arkui_styledstring) \* [OH_ArkUI_StyledString_Create](_ark_u_i___native_module.md#oh_arkui_styledstring_create) (OH_Drawing_TypographyStyle \*style, OH_Drawing_FontCollection \*collection) | Creates an **ArkUI_StyledString** object. | 
| void [OH_ArkUI_StyledString_Destroy](_ark_u_i___native_module.md#oh_arkui_styledstring_destroy) ([ArkUI_StyledString](_ark_u_i___native_module.md#arkui_styledstring) \*handle) | Destroys an **ArkUI_StyledString** object and reclaims the memory occupied by the object. | 
| void [OH_ArkUI_StyledString_PushTextStyle](_ark_u_i___native_module.md#oh_arkui_styledstring_pushtextstyle) ([ArkUI_StyledString](_ark_u_i___native_module.md#arkui_styledstring) \*handle, OH_Drawing_TextStyle \*style) | Pushes a text style to the top of the style stack of a styled string. | 
| void [OH_ArkUI_StyledString_AddText](_ark_u_i___native_module.md#oh_arkui_styledstring_addtext) ([ArkUI_StyledString](_ark_u_i___native_module.md#arkui_styledstring) \*handle, const char \*content) | Adds text for a styled string. | 
| void [OH_ArkUI_StyledString_PopTextStyle](_ark_u_i___native_module.md#oh_arkui_styledstring_poptextstyle) ([ArkUI_StyledString](_ark_u_i___native_module.md#arkui_styledstring) \*handle) | Pops the style at the top of the style stack of a styled string. | 
| OH_Drawing_Typography \* [OH_ArkUI_StyledString_CreateTypography](_ark_u_i___native_module.md#oh_arkui_styledstring_createtypography) ([ArkUI_StyledString](_ark_u_i___native_module.md#arkui_styledstring) \*handle) | Creates an **OH_Drawing_Typography** object based on an **ArkUI_StyledString** object. | 
| void [OH_ArkUI_StyledString_AddPlaceholder](_ark_u_i___native_module.md#oh_arkui_styledstring_addplaceholder) ([ArkUI_StyledString](_ark_u_i___native_module.md#arkui_styledstring) \*handle, OH_Drawing_PlaceholderSpan \*placeholder) | Adds a placeholder. | 
| [ArkUI_StyledString_Descriptor](_ark_u_i___native_module.md#arkui_styledstring_descriptor) \* [OH_ArkUI_StyledString_Descriptor_Create](_ark_u_i___native_module.md#oh_arkui_styledstring_descriptor_create) (void) | Creates an **ArkUI_StyledString_Descriptor** object. | 
| void [OH_ArkUI_StyledString_Descriptor_Destroy](_ark_u_i___native_module.md#oh_arkui_styledstring_descriptor_destroy) ([ArkUI_StyledString_Descriptor](_ark_u_i___native_module.md#arkui_styledstring_descriptor) \*descriptor) | Destroys an **ArkUI_StyledString_Descriptor** object and reclaims the memory occupied by the object. | 
| int32_t [OH_ArkUI_UnmarshallStyledStringDescriptor](_ark_u_i___native_module.md#oh_arkui_unmarshallstyledstringdescriptor) (uint8_t \*buffer, size_t bufferSize, [ArkUI_StyledString_Descriptor](_ark_u_i___native_module.md#arkui_styledstring_descriptor) \*descriptor, size_t \*resultSize) | Unmarshals a byte array containing styled string information into a styled string. | 
| int32_t [OH_ArkUI_MarshallStyledStringDescriptor](_ark_u_i___native_module.md#oh_arkui_marshallstyledstringdescriptor) (uint8_t \*buffer, size_t bufferSize, [ArkUI_StyledString_Descriptor](_ark_u_i___native_module.md#arkui_styledstring_descriptor) \*descriptor) | Marshals the styled string information into a byte array. | 
| const char \* [OH_ArkUI_ConvertToHtml](_ark_u_i___native_module.md#oh_arkui_converttohtml) ([ArkUI_StyledString_Descriptor](_ark_u_i___native_module.md#arkui_styledstring_descriptor) \*descriptor) | Converts styled string information into HTML. | 
