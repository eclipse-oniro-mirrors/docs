# @ohos.app.form.formProvider (FormProvider)

The **FormProvider** module provides APIs related to the widget provider. You can use the APIs to update a widget, set the next refresh time for a widget, obtain widget information, and request a widget release.

> **NOTE**
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import formProvider from '@ohos.app.form.formProvider';
```

## setFormNextRefreshTime

setFormNextRefreshTime(formId: string, minute: number, callback: AsyncCallback&lt;void&gt;): void

Sets the next refresh time for a widget. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description                                  |
| ------ | ------ | ---- | ------------------------------------- |
| formId | string | Yes  | Widget ID.                              |
| minute | number | Yes  | Refresh interval, in minutes. The value must be greater than or equal to 5.    |
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |
| 16501001 | The ID of the form to be operated does not exist. |
| 16501002 | The number of forms exceeds upper bound. |
| 16501003 | The form can not be operated by the current application. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formProvider from '@ohos.application.formProvider';
var formId = '12400633174999288';
try {
  formProvider.setFormNextRefreshTime(formId, 5, (error) => {
    if (error) {
      console.log('formProvider setFormNextRefreshTime, error:' + JSON.stringify(error));
      return;
    }
    console.log(`formProvider setFormNextRefreshTime success`);
  });
} catch (error) {
    console.log('error' + JSON.stringify(error))
}
```

## setFormNextRefreshTime

setFormNextRefreshTime(formId: string, minute: number): Promise&lt;void&gt;

Sets the next refresh time for a widget. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description                                  |
| ------ | ------ | ---- | ------------------------------------- |
| formId | string | Yes  | Widget ID.                              |
| minute | number | Yes  | Refresh interval, in minutes. The value must be greater than or equal to 5.    |

**Return value**

| Type         | Description                             |
| ------------- | ---------------------------------- |
| Promise\<void> | Promise that returns no value.     |

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |
| 16501001 | The ID of the form to be operated does not exist. |
| 16501002 | The number of forms exceeds upper bound. |
| 16501003 | The form can not be operated by the current application. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formProvider from '@ohos.application.formProvider';
var formId = '12400633174999288';
try {
  formProvider.setFormNextRefreshTime(formId, 5).then(() => {
  console.log('formProvider setFormNextRefreshTime success');
  }).catch((error) => {
    console.log('formProvider setFormNextRefreshTime, error:' + JSON.stringify(error));
  });
} catch (error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}
```

## updateForm

updateForm(formId: string, formBindingData: formBindingData.FormBindingData,callback: AsyncCallback&lt;void&gt;): void

Updates a widget. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type                                                                   | Mandatory| Description            |
| ------ | ---------------------------------------------------------------------- | ---- | ---------------- |
| formId | string                                                                 | Yes  | ID of the widget to update.|
| formBindingData.FormBindingData | [FormBindingData](js-apis-app-form-formBindingData.md#formbindingdata) | Yes  | Data to be used for the update.   |
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |
| 16501001 | The ID of the form to be operated does not exist. |
| 16501003 | The form can not be operated by the current application. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formBindingData from '@ohos.app.form.formBindingData';
import formProvider from '@ohos.application.formProvider';

var formId = '12400633174999288';
try {
  let obj = formBindingData.createFormBindingData({temperature:'22c', time:'22:00'});
  formProvider.updateForm(formId, obj, (error) => {
    if (error) {
      console.log('formProvider updateForm, error:' + JSON.stringify(error));
      return;
    }
    console.log(`formProvider updateForm success`);
  });
} catch (error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}
```

## updateForm

updateForm(formId: string, formBindingData: formBindingData.FormBindingData): Promise&lt;void&gt;

Updates a widget. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type                                                                   | Mandatory| Description            |
| ------ | ---------------------------------------------------------------------- | ---- | ---------------- |
| formId | string                                                                 | Yes  | ID of the widget to update.|
| formBindingData.FormBindingData | [FormBindingData](js-apis-app-form-formBindingData.md#formbindingdata) | Yes  | Data to be used for the update.   |

**Return value**

| Type          | Description                               |
| -------------- | ----------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |
| 16501001 | The ID of the form to be operated does not exist. |
| 16501003 | The form can not be operated by the current application. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formBindingData from '@ohos.app.form.formBindingData';
import formProvider from '@ohos.application.formProvider';

let formId = '12400633174999288';
let obj = formBindingData.createFormBindingData({ temperature: '22c', time: '22:00' });
try {
  formProvider.updateForm(formId, obj).then(() => {
      console.log('formProvider updateForm success');
  }).catch((error) => {
      console.log('formProvider updateForm, error:' + JSON.stringify(error));
  });
} catch (error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}
```

## getFormsInfo

getFormsInfo(callback: AsyncCallback&lt;Array&lt;formInfo.FormInfo&gt;&gt;): void

Obtains the application's widget information on the device. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| callback | AsyncCallback&lt;Array&lt;[FormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Yes| Callback used to return the information obtained.|

**Error codes**
| Error Code ID| Error Message|
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).


**Example**

```ts
import formProvider from '@ohos.application.formProvider';
try {
  formProvider.getFormsInfo((error, data) => {
    if (error) {
      console.log('formProvider getFormsInfo, error:' + JSON.stringify(error));
      return;
    }
    console.log('formProvider getFormsInfo, data:' + JSON.stringify(data));
  });
} catch (error) {
    console.log(`catch err->${JSON.stringify(error)}`);
}
```
## getFormsInfo

getFormsInfo(filter: formInfo.FormInfoFilter, callback: AsyncCallback&lt;Array&lt;formInfo.FormInfo&gt;&gt;): void

Obtains the application's widget information that meets a filter criterion on the device. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| filter | [formInfo.FormInfoFilter](js-apis-app-form-formInfo.md#forminfofilter) | Yes| Filter criterion.|
| callback | AsyncCallback&lt;Array&lt;[FormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Yes| Callback used to return the information obtained.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formInfo from '@ohos.app.form.formInfo';
import formProvider from '@ohos.application.formProvider';

const filter : formInfo.FormInfoFilter = {
    // get info of forms belong to module entry.
    moduleName : 'entry'
};
try {
  formProvider.getFormsInfo(filter, (error, data) => {
    if (error) {
      console.log('formProvider getFormsInfo, error:' + JSON.stringify(error));
      return;
    }
    console.log('formProvider getFormsInfo, data:' + JSON.stringify(data));
  });
} catch(error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}
```

## getFormsInfo

getFormsInfo(filter?: formInfo.FormInfoFilter): Promise&lt;Array&lt;formInfo.FormInfo&gt;&gt;

Obtains the application's widget information on the device. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| filter | [formInfo.FormInfoFilter](js-apis-app-form-formInfo.md#forminfofilter) | No| Filter criterion.|

**Return value**

| Type         | Description                               |
| :------------ | :---------------------------------- |
| Promise&lt;Array&lt;[FormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Promise used to return the information obtained.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formInfo from '@ohos.app.form.formInfo';
import formProvider from '@ohos.application.formProvider';

const filter : formInfo.FormInfoFilter = {
    // get info of forms belong to module entry.
    moduleName : 'entry'
};
try {
  formProvider.getFormsInfo(filter).then((data) => {
    console.log('formProvider getFormsInfo, data:' + JSON.stringify(data));
  }).catch((error) => {
    console.log('formProvider getFormsInfo, error:' + JSON.stringify(error));
  });
} catch (error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}
```

## requestPublishForm

requestPublishForm(want: Want, formBindingData: formBindingData.FormBindingData, callback: AsyncCallback\<string>): void

Requests to publish a widget carrying data to the widget host (usually the home screen). This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.Form

**System API**: This is a system API.

**Parameters**

| Name| Type                                                                   | Mandatory| Description            |
| ------ | ---------------------------------------------------------------------- | ---- | ---------------- |
| want | [Want](js-apis-application-want.md)                           | Yes  | Request used for publishing. The following fields must be included:<br>Information about the target widget.<br>**abilityName**: ability of the target widget.<br>**parameters**:<br>'ohos.extra.param.key.form_dimension'<br>'ohos.extra.param.key.form_name'<br>'ohos.extra.param.key.module_name' |
| formBindingData.FormBindingData | [FormBindingData](js-apis-app-form-formBindingData.md#formbindingdata) | Yes  | Data used for creating the widget.|
| callback | AsyncCallback&lt;string&gt; | Yes| Callback used to return the widget ID.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 202 | The application is not a system application. |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formBindingData from '@ohos.app.form.formBindingData';
import formProvider from '@ohos.application.formProvider';

let want = {
  abilityName: 'FormAbility',
  parameters: {
    'ohos.extra.param.key.form_dimension': 2,
    'ohos.extra.param.key.form_name': 'widget',
    'ohos.extra.param.key.module_name': 'entry'
  }
};
try {
  let obj = formBindingData.createFormBindingData({temperature:'22c', time:'22:00'});
  formProvider.requestPublishForm(want, obj, (error, data) => {
    if (error) {
      console.log('formProvider requestPublishForm, error: ' + JSON.stringify(error));
      return;
    }
    console.log('formProvider requestPublishForm, form ID is: ' + JSON.stringify(data));
  });
} catch (error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}
```

## requestPublishForm

requestPublishForm(want: Want, callback: AsyncCallback&lt;string&gt;): void

Requests to publish a widget to the widget host (usually the home screen). This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.Form

**System API**: This is a system API.

**Parameters**

| Name  | Type                               | Mandatory| Description                                                        |
| -------- | ----------------------------------- | ---- | ------------------------------------------------------------ |
| want     | [Want](js-apis-application-want.md) | Yes  | Request used for publishing. The following fields must be included:<br>Information about the target widget.<br>**abilityName**: ability of the target widget.<br>**parameters**:<br>'ohos.extra.param.key.form_dimension'<br>'ohos.extra.param.key.form_name'<br>'ohos.extra.param.key.module_name' |
| callback | AsyncCallback&lt;string&gt;         | Yes  |  Callback used to return the widget ID.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 202 | The application is not a system application. |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formProvider from '@ohos.application.formProvider';
let want = {
  abilityName: 'FormAbility',
  parameters: {
    'ohos.extra.param.key.form_dimension': 2,
    'ohos.extra.param.key.form_name': 'widget',
    'ohos.extra.param.key.module_name': 'entry'
  }
};
try {
  formProvider.requestPublishForm(want, (error, data) => {
    if (error) {
      console.log('formProvider requestPublishForm, error: ' + JSON.stringify(error));
      return;
    }
    console.log('formProvider requestPublishForm, form ID is: ' + JSON.stringify(data));
  });
} catch (error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}

```

## requestPublishForm

requestPublishForm(want: Want, formBindingData?: formBindingData.FormBindingData): Promise&lt;string&gt;

Requests to publish a widget to the widget host (usually the home screen). This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.Form

**System API**: This is a system API.

**Parameters**

| Name         | Type                                                        | Mandatory| Description                                                        |
| --------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| want            | [Want](js-apis-application-want.md)                          | Yes  | Request used for publishing. The following fields must be included:<br>Information about the target widget.<br>**abilityName**: ability of the target widget.<br>**parameters**:<br>'ohos.extra.param.key.form_dimension'<br>'ohos.extra.param.key.form_name'<br>'ohos.extra.param.key.module_name' |
| formBindingData.FormBindingData | [FormBindingData](js-apis-app-form-formBindingData.md#formbindingdata) | No  | Data used for creating the widget.                                          |

**Return value**

| Type         | Description                               |
| :------------ | :---------------------------------- |
| Promise&lt;string&gt; | Promise used to return the widget ID.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 202 | The application is not a system application. |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formProvider from '@ohos.application.formProvider';
let want = {
  abilityName: 'FormAbility',
  parameters: {
    'ohos.extra.param.key.form_dimension': 2,
    'ohos.extra.param.key.form_name': 'widget',
    'ohos.extra.param.key.module_name': 'entry'
  }
};
try {
  formProvider.requestPublishForm(want).then((data) => {
    console.log('formProvider requestPublishForm success, form ID is :' + JSON.stringify(data));
  }).catch((error) => {
    console.log('formProvider requestPublishForm, error: ' + JSON.stringify(error));
  });
} catch (error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}
```

## isRequestPublishFormSupported

isRequestPublishFormSupported(callback: AsyncCallback&lt;boolean&gt;): void

Checks whether a widget can be published to the widget host. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name| Type   | Mandatory| Description   |
| ------ | ------ | ---- | ------- |
| callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return whether the widget can be published to the widget host.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 202 | The application is not a system application. |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16501000 | An internal functional error occurred. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formProvider from '@ohos.application.formProvider';
try {
  formProvider.isRequestPublishFormSupported((error, isSupported) => {
  if (error) {
    console.log('formProvider isRequestPublishFormSupported, error:' + JSON.stringify(error));
  } else {
    if (isSupported) {
      var want = {
      abilityName: 'FormAbility',
      parameters: {
        'ohos.extra.param.key.form_dimension': 2,
        'ohos.extra.param.key.form_name': 'widget',
        'ohos.extra.param.key.module_name': 'entry'
      }
      };
      try {
        formProvider.requestPublishForm(want, (error, data) => {
          if (error) {
            console.log('formProvider requestPublishForm, error: ' + JSON.stringify(error));
          } else {
            console.log('formProvider requestPublishForm, form ID is: ' + JSON.stringify(data));
          }
      });
      } catch (error) {
        console.log(`catch err->${JSON.stringify(error)}`);
      }

    }
  }
});
} catch (error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}
```

## isRequestPublishFormSupported

isRequestPublishFormSupported(): Promise&lt;boolean&gt;

Checks whether a widget can be published to the widget host. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Ability.Form

**Return value**

| Type         | Description                               |
| :------------ | :---------------------------------- |
| Promise&lt;boolean&gt; | Promise used to return whether the widget can be published to the widget host.|

**Error codes**

| Error Code ID| Error Message|
| -------- | -------- |
| 202 | The application is not a system application. |
| 16500050 | An IPC connection error happened. |
| 16501000 | An internal functional error occurred. |

For details about the error codes, see [Form Error Codes](../errorcodes/errorcode-form.md).

**Example**

```ts
import formProvider from '@ohos.application.formProvider';
try {
  formProvider.isRequestPublishFormSupported().then((isSupported) => {
    if (isSupported) {
      var want = {
      abilityName: 'FormAbility',
      parameters: {
        'ohos.extra.param.key.form_dimension': 2,
        'ohos.extra.param.key.form_name': 'widget',
        'ohos.extra.param.key.module_name': 'entry'
      }
      };
      try {
        formProvider.requestPublishForm(want).then((data) => {
          console.log('formProvider requestPublishForm success, form ID is :' + JSON.stringify(data));
        }).catch((error) => {
          console.log('formProvider requestPublishForm, error: ' + JSON.stringify(error));
        });
      } catch (error) {
        console.log(`catch err->${JSON.stringify(error)}`);
      }

    }
  }).catch((error) => {
    console.log('formProvider isRequestPublishFormSupported, error:' + JSON.stringify(error));
  });
} catch (error) {
  console.log(`catch err->${JSON.stringify(error)}`);
}
```
