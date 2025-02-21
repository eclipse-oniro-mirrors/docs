# @ohos.app.form.FormExtensionAbility (FormExtensionAbility)

The **FormExtensionAbility** module provides lifecycle callbacks invoked when a widget is created, destroyed, or updated.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';
```

## Attributes

**System capability**: SystemCapability.Ability.Form

| Name   | Type                                                        | Readable| Writable| Description                                                        |
| ------- | ------------------------------------------------------------ | ---- | ---- | ------------------------------------------------------------ |
| context | [FormExtensionContext](js-apis-inner-application-formExtensionContext.md) | Yes  | No  | Context of the FormExtensionAbility. This context is inherited from [ExtensionContext](../apis-ability-kit/js-apis-inner-application-extensionContext.md).|

## onAddForm

onAddForm(want: Want): formBindingData.FormBindingData

Called to notify the widget provider that a **Form** instance (widget) is being created.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type                                  | Mandatory| Description                                                        |
| ------ | -------------------------------------- | ---- | ------------------------------------------------------------ |
| want   | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | Yes  | Want information related to the FormExtensionAbility, including the widget ID, name, and style. The information must be managed as persistent data to facilitate subsequent widget update and deletion.|

**Return value**

| Type                                                        | Description                                                       |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [formBindingData.FormBindingData](js-apis-app-form-formBindingData.md#formbindingdata) | A **formBindingData.FormBindingData** object containing the data to be displayed on the widget.|

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';
import formBindingData from '@ohos.app.form.formBindingData';
import Want from '@ohos.app.ability.Want';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onAddForm(want: Want) {
    console.log(`FormExtensionAbility onAddForm, want: ${want.abilityName}`);
    let dataObj1: Record<string, string> = {
      'temperature': '11c',
      'time': '11:00'
    };

    let obj1: formBindingData.FormBindingData = formBindingData.createFormBindingData(dataObj1);
    return obj1;
  }
}
```

## onCastToNormalForm

onCastToNormalForm(formId: string): void

Called to notify the widget provider that a temporary widget is being converted to a normal one.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type  | Mandatory| Description                    |
| ------ | ------ | ---- | ------------------------ |
| formId | string | Yes  | ID of the widget that requests to be converted to a normal one.|

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onCastToNormalForm(formId: string) {
    console.log(`FormExtensionAbility onCastToNormalForm, formId: ${formId}`);
  }
};
```

## onUpdateForm

onUpdateForm(formId: string): void

Called to notify the widget provider that a widget is being updated. After obtaining the latest data, your application should call [updateForm](js-apis-app-form-formProvider.md#updateform) of **formProvider** to update the widget data.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| formId | string | Yes  | ID of the widget that requests to be updated.|

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';
import formBindingData from '@ohos.app.form.formBindingData';
import formProvider from '@ohos.app.form.formProvider';
import Base from '@ohos.base';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onUpdateForm(formId: string) {
    console.log(`FormExtensionAbility onUpdateForm, formId: ${formId}`);
    let param: Record<string, string> = {
      'temperature': '22c',
      'time': '22:00'
    }
    let obj2: formBindingData.FormBindingData = formBindingData.createFormBindingData(param);
    formProvider.updateForm(formId, obj2).then(() => {
      console.log(`FormExtensionAbility context updateForm`);
    }).catch((error: Base.BusinessError) => {
      console.error(`FormExtensionAbility context updateForm failed, data: ${error}`);
    });
  }
};
```

## onChangeFormVisibility

onChangeFormVisibility(newStatus: Record\<string, number>): void

Called to notify the widget provider that the widget visibility status is being changed.

This API is valid only for system applications when **formVisibleNotify** is set to **true**.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name | Type  | Mandatory| Description                  |
| ------- | ------ | ---- | ---------------------- |
| newStatus  | Record\<string, number> | Yes  | ID and visibility status of the widget to be changed.|

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';
import formBindingData from '@ohos.app.form.formBindingData';
import formProvider from '@ohos.app.form.formProvider';
import Base from '@ohos.base';

// According to the ArkTS specification, **Object.keys** and **for..in...** cannot be used in .ets files to obtain the key value of an object. Use the user-defined function **getObjKeys** instead.
// Extract this function to a .ts file and export it. Import this function to the required e.ts file before using it.
function getObjKeys(obj: Object): string[] {
  let keys = Object.keys(obj);
  return keys;
}

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onChangeFormVisibility(newStatus: Record<string, number>) {
    console.log(`FormExtensionAbility onChangeFormVisibility, newStatus: ${newStatus}`);
    let param: Record<string, string> = {
      'temperature': '22c',
      'time': '22:00'
    }
    let obj2: formBindingData.FormBindingData = formBindingData.createFormBindingData(param);

    let keys: string[] = getObjKeys(newStatus);

    for (let i: number = 0; i < keys.length; i++) {
      console.log(`FormExtensionAbility onChangeFormVisibility, key: ${keys[i]}, value= ${newStatus[keys[i]]}`);
      formProvider.updateForm(keys[i], obj2).then(() => {
        console.log(`FormExtensionAbility context updateForm`);
      }).catch((error: Base.BusinessError) => {
        console.error(`Operation updateForm failed. Cause: ${JSON.stringify(error)}`);
      });
    }
  }
};
```

## onFormEvent

onFormEvent(formId: string, message: string): void

Called to instruct the widget provider to process the widget event.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name | Type  | Mandatory| Description                  |
| ------- | ------ | ---- | ---------------------- |
| formId  | string | Yes  | ID of the widget that requests the event.|
| message | string | Yes  | Event message.            |

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onFormEvent(formId: string, message: string) {
    console.log(`FormExtensionAbility onFormEvent, formId: ${formId}, message: ${message}`);
  }
};
```

## onRemoveForm

onRemoveForm(formId: string): void

Called to notify the widget provider that a **Form** instance (widget) is being destroyed.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| formId | string | Yes  | ID of the widget to be destroyed.|

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onRemoveForm(formId: string) {
    console.log(`FormExtensionAbility onRemoveForm, formId: ${formId}`);
  }
};
```

## onConfigurationUpdate

onConfigurationUpdate(newConfig: Configuration): void

Called when the configuration of the environment where the FormExtensionAbility is running is updated. 
This lifecycle callback is triggered only when the configuration is updated while the FormExtensionAbility is alive. If no operation is performed within 5 seconds after a **FormExtensionAbility** instance is created, the instance will be deleted.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| newConfig | [Configuration](../apis-ability-kit/js-apis-application-configuration.md) | Yes| New configuration.|

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';
import { Configuration } from '@ohos.app.ability.Configuration';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onConfigurationUpdate(newConfig: Configuration) {
    // This lifecycle callback is triggered only when the configuration is updated while the FormExtensionAbility is alive.
    // If no operation is performed within 5 seconds after a FormExtensionAbility instance is created, the instance will be deleted.
    console.log(`onConfigurationUpdate, config: ${JSON.stringify(newConfig)}`);
  }
};
```

## onAcquireFormState

onAcquireFormState?(want: Want): formInfo.FormState

Called to notify the widget provider that the widget host is requesting the widget state. By default, the initial widget state is returned. (You can override this API as required.)

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | Yes| Description of the widget state, including the bundle name, ability name, module name, widget name, and widget dimension.|

**Example**

```ts
import FormExtensionAbility from '@ohos.app.form.FormExtensionAbility';
import formInfo from '@ohos.app.form.formInfo';
import Want from '@ohos.app.ability.Want';

export default class MyFormExtensionAbility extends FormExtensionAbility {
  onAcquireFormState(want: Want) {
    console.log(`FormExtensionAbility onAcquireFormState, want: ${want}`);
    return formInfo.FormState.UNKNOWN;
  }
};
```
