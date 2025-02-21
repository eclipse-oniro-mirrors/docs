# @ohos.app.form.formProvider (formProvider)

FormProvider模块提供了卡片提供方相关接口的能力，开发者在开发卡片时，可通过该模块提供接口实现更新卡片、设置卡片更新时间、获取卡片信息、请求发布卡片等。

> **说明：**
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import formProvider from '@ohos.app.form.formProvider';
```

## setFormNextRefreshTime

setFormNextRefreshTime(formId: string, minute: number, callback: AsyncCallback&lt;void&gt;): void

设置指定卡片的下一次更新时间，使用callback异步回调。

**系统能力：** SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明                                   |
| ------ | ------ | ---- | ------------------------------------- |
| formId | string | 是   | 卡片标识。                               |
| minute | number | 是   | 指定多久之后更新。单位分钟，大于等于5。     |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |
| 16501001 | The ID of the form to be operated does not exist. |
| 16501002 | The number of forms exceeds upper bound. |
| 16501003 | The form can not be operated by the current application. |

以上错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[卡片错误码](errorcode-form.md)。

**示例：**

```ts
import Base from '@ohos.base';
import formProvider from '@ohos.app.form.formProvider';

let formId: string = '12400633174999288';
try {
  formProvider.setFormNextRefreshTime(formId, 5, (error: Base.BusinessError) => {
    if (error) {
      console.error(`callback error, code: ${error.code}, message: ${error.message})`);
      return;
    }
    console.log(`formProvider setFormNextRefreshTime success`);
  });
} catch (error) {
  console.error(`catch error, code: ${(error as Base.BusinessError).code}, message: ${(error as Base.BusinessError).message})`);
}
```

## setFormNextRefreshTime

setFormNextRefreshTime(formId: string, minute: number): Promise&lt;void&gt;

设置指定卡片的下一次更新时间，使用Promise异步回调。

**系统能力：** SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明                                   |
| ------ | ------ | ---- | ------------------------------------- |
| formId | string | 是   | 卡片标识。                               |
| minute | number | 是   | 指定多久之后更新。单位分钟，大于等于5。     |

**返回值：**

| 类型          | 说明                              |
| ------------- | ---------------------------------- |
| Promise\<void> | 无返回结果的Promise对象。      |

**错误码：**

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |
| 16501001 | The ID of the form to be operated does not exist. |
| 16501002 | The number of forms exceeds upper bound. |
| 16501003 | The form can not be operated by the current application. |

以上错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[卡片错误码](errorcode-form.md)。

**示例：**

```ts
import Base from '@ohos.base';
import formProvider from '@ohos.app.form.formProvider';

let formId: string = '12400633174999288';
try {
  formProvider.setFormNextRefreshTime(formId, 5).then(() => {
    console.log(`formProvider setFormNextRefreshTime success`);
  }).catch((error: Base.BusinessError) => {
    console.error(`promise error, code: ${error.code}, message: ${error.message})`);
  });
} catch (error) {
  console.error(`catch error, code: ${(error as Base.BusinessError).code}, message: ${(error as Base.BusinessError).message})`);
}
```

## updateForm

updateForm(formId: string, formBindingData: formBindingData.FormBindingData,callback: AsyncCallback&lt;void&gt;): void

更新指定的卡片，使用callback异步回调。

**系统能力：** SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型                                                                    | 必填 | 说明             |
| ------ | ---------------------------------------------------------------------- | ---- | ---------------- |
| formId | string                                                                 | 是   | 请求更新的卡片标识。 |
| formBindingData.FormBindingData | [FormBindingData](js-apis-app-form-formBindingData.md#formbindingdata) | 是   | 用于更新的数据。    |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。 |

**错误码：**

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |
| 16501001 | The ID of the form to be operated does not exist. |
| 16501003 | The form can not be operated by the current application. |

以上错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[卡片错误码](errorcode-form.md)。

**示例：**

```ts
import formBindingData from '@ohos.app.form.formBindingData';
import Base from '@ohos.base';
import formProvider from '@ohos.app.form.formProvider';

let formId: string = '12400633174999288';
try {
  let param: Record<string, string> = {
    'temperature': '22c',
    'time': '22:00'
  }
  let obj: formBindingData.FormBindingData = formBindingData.createFormBindingData(param);
  formProvider.updateForm(formId, obj, (error: Base.BusinessError) => {
    if (error) {
      console.error(`callback error, code: ${error.code}, message: ${error.message})`);
      return;
    }
    console.log(`formProvider updateForm success`);
  });
} catch (error) {
  console.error(`catch error, code: ${(error as Base.BusinessError).code}, message: ${(error as Base.BusinessError).message})`);
}
```

## updateForm

updateForm(formId: string, formBindingData: formBindingData.FormBindingData): Promise&lt;void&gt;

更新指定的卡片，使用Promise异步回调。

**系统能力：** SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型                                                                    | 必填 | 说明             |
| ------ | ---------------------------------------------------------------------- | ---- | ---------------- |
| formId | string                                                                 | 是   | 请求更新的卡片标识。 |
| formBindingData.FormBindingData | [FormBindingData](js-apis-app-form-formBindingData.md#formbindingdata) | 是   | 用于更新的数据。    |

**返回值：**

| 类型           | 说明                                |
| -------------- | ----------------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**错误码：**

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500060 | A service connection error happened, please try again later. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |
| 16501001 | The ID of the form to be operated does not exist. |
| 16501003 | The form can not be operated by the current application. |

以上错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[卡片错误码](errorcode-form.md)。

**示例：**

```ts
import formBindingData from '@ohos.app.form.formBindingData';
import Base from '@ohos.base';
import formProvider from '@ohos.app.form.formProvider';

let formId: string = '12400633174999288';
let param: Record<string, string> = {
  'temperature': '22c',
  'time': '22:00'
}
let obj: formBindingData.FormBindingData = formBindingData.createFormBindingData(param);
try {
  formProvider.updateForm(formId, obj).then(() => {
    console.log(`formProvider updateForm success`);
  }).catch((error: Base.BusinessError) => {
    console.error(`promise error, code: ${(error as Base.BusinessError).code}, message: ${(error as Base.BusinessError).message})`);
  });
} catch (error) {
  console.error(`catch error, code: ${(error as Base.BusinessError).code}, message: ${(error as Base.BusinessError).message})`);
}
```

## getFormsInfo

getFormsInfo(callback: AsyncCallback&lt;Array&lt;formInfo.FormInfo&gt;&gt;): void

获取设备上当前应用程序的卡片信息，使用callback异步回调。

**系统能力：** SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| callback | AsyncCallback&lt;Array&lt;[formInfo.FormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | 是 | 回调函数。返回查询到的卡片信息。 |

**错误码：**
| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |

以上错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[卡片错误码](errorcode-form.md)。


**示例：**

```ts
import Base from '@ohos.base';
import formProvider from '@ohos.app.form.formProvider';

try {
  formProvider.getFormsInfo((error, data) => {
    if (error) {
      console.error(`callback error, code: ${error.code}, message: ${error.message})`);
      return;
    }
    console.log(`formProvider getFormsInfo, data: ${JSON.stringify(data)}`);
  });
} catch (error) {
  console.error(`catch error, code: ${(error as Base.BusinessError).code}, message: ${(error as Base.BusinessError).message})`);
}
```
## getFormsInfo

getFormsInfo(filter: formInfo.FormInfoFilter, callback: AsyncCallback&lt;Array&lt;formInfo.FormInfo&gt;&gt;): void

获取设备上当前应用程序的卡片信息，并筛选符合条件的信息，使用callback异步回调。

**系统能力：** SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| filter | [formInfo.FormInfoFilter](js-apis-app-form-formInfo.md#forminfofilter) | 是 | 卡片信息过滤器。 |
| callback | AsyncCallback&lt;Array&lt;[formInfo.FormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | 是 | 回调函数。返回查询到符合条件的卡片信息。 |

**错误码：**

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |

以上错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[卡片错误码](errorcode-form.md)。

**示例：**

```ts
import Base from '@ohos.base';
import formInfo from '@ohos.app.form.formInfo';
import formProvider from '@ohos.app.form.formProvider';

const filter: formInfo.FormInfoFilter = {
  // get info of forms belong to module entry.
  moduleName: 'entry'
};
try {
  formProvider.getFormsInfo(filter, (error, data) => {
    if (error) {
      console.error(`callback error, code: ${error.code}, message: ${error.message})`);
      return;
    }
    console.log(`formProvider getFormsInfo, data: ${JSON.stringify(data)}`);
  });
} catch (error) {
  console.error(`catch error, code: ${(error as Base.BusinessError).code}, message: ${(error as Base.BusinessError).message})`);
}
```

## getFormsInfo

getFormsInfo(filter?: formInfo.FormInfoFilter): Promise&lt;Array&lt;formInfo.FormInfo&gt;&gt;

获取设备上当前应用程序的卡片信息，使用Promise异步回调。

**系统能力：** SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| filter | [formInfo.FormInfoFilter](js-apis-app-form-formInfo.md#forminfofilter) | 否 | 卡片信息过滤器, 默认为空，不进行过滤。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;Array&lt;[formInfo.FormInfo](js-apis-app-form-formInfo.md)&gt;&gt; | Promise对象。返回查询到符合条件的卡片信息。 |

**错误码：**

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | If the input parameter is not valid parameter. |
| 16500050 | An IPC connection error happened. |
| 16500100 | Failed to obtain the configuration information. |
| 16501000 | An internal functional error occurred. |

以上错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[卡片错误码](errorcode-form.md)。

**示例：**

```ts
import formInfo from '@ohos.app.form.formInfo';
import Base from '@ohos.base';
import formProvider from '@ohos.app.form.formProvider';

const filter: formInfo.FormInfoFilter = {
  // get info of forms belong to module entry.
  moduleName: 'entry'
};
try {
  formProvider.getFormsInfo(filter).then((data: formInfo.FormInfo[]) => {
    console.log(`formProvider getFormsInfo, data: ${JSON.stringify(data)}`);
  }).catch((error: Base.BusinessError) => {
    console.error(`promise error, code: ${error.code}, message: ${error.message})`);
  });
} catch (error) {
  console.error(`catch error, code: ${(error as Base.BusinessError).code}, message: ${(error as Base.BusinessError).message})`);
}
```

