# @ohos.app.form.formBindingData (formBindingData)

The **FormBindingData** module provides APIs for widget data binding. You can use the APIs to create a **FormBindingData** object and obtain related information.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import formBindingData from '@ohos.app.form.formBindingData';
```

## FormBindingData

Describes a **FormBindingData** object.

**System capability**: SystemCapability.Ability.Form

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| data | Object | Yes| Data to be displayed on the JS widget. The value can be an object containing multiple key-value pairs or a string in JSON format.|

## createFormBindingData

createFormBindingData(obj?: Object | string): FormBindingData

Creates a **FormBindingData** object.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type          | Mandatory| Description                                                        |
| ------ | -------------- | ---- | ------------------------------------------------------------ |
| obj    | Object\|string | No  | Data to be displayed on the JS widget. The value can be an object containing multiple key-value pairs or a string in JSON format. The image data is identified by **'formImages'**, and the content is multiple key-value pairs, each of which consists of an image identifier and image file descriptor. The final format is {'formImages': {'key1': fd1, 'key2': fd2}}.|


**Return value**

| Type                               | Description                                   |
| ----------------------------------- | --------------------------------------- |
| [FormBindingData](#formbindingdata) | **FormBindingData** object created based on the passed data.|


**Example**

```ts
import formBindingData from '@ohos.app.form.formBindingData';
import fs from '@ohos.file.fs';

try {
  let fd = fs.openSync('/path/to/form.png');
  let obj = {
    'temperature': '21°',
    'formImages': { 'image': fd }
  };
  formBindingData.createFormBindingData(obj);
} catch (error) {
  console.error(`catch error, code: ${error.code}, message: ${error.message}`);
}
```
