# CustomizeData

The **CustomizeData** module provides custom metadata.

> **NOTE**
>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## CustomizeData<sup>(deprecated)</sup>

> This API is deprecated since API version 9. You are advised to use [Metadata](js-apis-bundleManager-metadata.md) instead.

**System capability**: SystemCapability.BundleManager.BundleFramework

| Name              | Type  | Readable| Writable| Description            |
| ------------------ | ------ | ---- | ---- | ---------------- |
| name               | string | Yes  | Yes  | Key that identifies a data element.|
| value              | string | Yes  | Yes  | Value of the data element.  |
| extra<sup>8+</sup> | string | Yes  | Yes  | Custom format of the data element. The value is an index to the resource that identifies the data.      |
