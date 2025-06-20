# oh_file_share.h


## Overview

Provides APIs for persisting permissions, activating or deactivating persistent permissions, and checking the persistent permissions on files or directories based on their URIs.

**Library**: libohfileshare.so

**System capability**: SystemCapability.FileManagement.AppFileService.FolderAuthorization

**Since**: 12

**Related module**: [FileShare](file_share.md)


## Summary


### Structs

| Name| Description| 
| -------- | -------- |
| struct  [FileShare_PolicyErrorResult](_file_share___policy_error_result.md) | Represents the permission policy error result. | 
| struct  [FileShare_PolicyInfo](_file_share___policy_info.md) | Represents the permission policy information. | 


### Types

| Name| Description| 
| -------- | -------- |
| typedef enum [FileShare_OperationMode](file_share.md#fileshare_operationmode-1) [FileShare_OperationMode](file_share.md#fileshare_operationmode) | Defines an enum for the URI operation mode. | 
| typedef enum [FileShare_PolicyErrorCode](file_share.md#fileshare_policyerrorcode-1) [FileShare_PolicyErrorCode](file_share.md#fileshare_policyerrorcode) | Defines an enum for the permission policy error code. | 
| typedef struct [FileShare_PolicyErrorResult](_file_share___policy_error_result.md) [FileShare_PolicyErrorResult](file_share.md#fileshare_policyerrorresult) | Defines a struct for the permission policy error result. | 
| typedef struct [FileShare_PolicyInfo](_file_share___policy_info.md) [FileShare_PolicyInfo](file_share.md#fileshare_policyinfo) | Defines a struct for the permission policy information. | 


### Enums

| Name| Description| 
| -------- | -------- |
| [FileShare_OperationMode](file_share.md#fileshare_operationmode) {<br>READ_MODE = 1 &lt;&lt; 0,<br>WRITE_MODE = 1 &lt;&lt; 1<br>} | Enumerates the URI operation mode.| 
| [FileShare_PolicyErrorCode](file_share.md#enum-description) {<br>PERSISTENCE_FORBIDDEN = 1,<br>INVALID_MODE = 2,<br>INVALID_PATH = 3,<br>PERMISSION_NOT_PERSISTED = 4<br>} | Enumerates the permission policy error code.| 


### Functions

| Name| Description| 
| -------- | -------- |
| [FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode) [OH_FileShare_PersistPermission](file_share.md#oh_fileshare_persistpermission) (const [FileShare_PolicyInfo](_file_share___policy_info.md) \*policies, unsigned int policyNum, [FileShare_PolicyErrorResult](_file_share___policy_error_result.md) \*\*result, unsigned int \*resultNum) | Persists the permissions on files or directories. | 
| [FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode) [OH_FileShare_RevokePermission](file_share.md#oh_fileshare_revokepermission) (const [FileShare_PolicyInfo](_file_share___policy_info.md) \*policies, unsigned int policyNum, [FileShare_PolicyErrorResult](_file_share___policy_error_result.md) \*\*result, unsigned int \*resultNum) | Revokes the permissions from files or directories. | 
| [FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode) [OH_FileShare_ActivatePermission](file_share.md#oh_fileshare_activatepermission) (const [FileShare_PolicyInfo](_file_share___policy_info.md) \*policies, unsigned int policyNum, [FileShare_PolicyErrorResult](_file_share___policy_error_result.md) \*\*result, unsigned int \*resultNum) | Activates the persistent permissions on files or directories. | 
| [FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode) [OH_FileShare_DeactivatePermission](file_share.md#oh_fileshare_deactivatepermission) (const [FileShare_PolicyInfo](_file_share___policy_info.md) \*policies, unsigned int policyNum, [FileShare_PolicyErrorResult](_file_share___policy_error_result.md) \*\*result, unsigned int \*resultNum) | Deactivates the persistent permissions on files or directories. | 
| [FileManagement_ErrCode](_file_i_o.md#filemanagement_errcode) [OH_FileShare_CheckPersistentPermission](file_share.md#oh_fileshare_checkpersistentpermission) (const [FileShare_PolicyInfo](_file_share___policy_info.md) \*policies, unsigned int policyNum, bool \*\*result, unsigned int \*resultNum) | Checks the persistent permissions on files or directories. | 
| void [OH_FileShare_ReleasePolicyErrorResult](file_share.md#oh_fileshare_releasepolicyerrorresult) ([FileShare_PolicyErrorResult](_file_share___policy_error_result.md) \*errorResult, unsigned int resultNum) | Releases the memory, to which **FileShare_PolicyErrorResult** points. | 
