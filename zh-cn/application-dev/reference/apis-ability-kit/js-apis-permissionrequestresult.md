# PermissionRequestResult

权限请求结果对象，在调用[requestPermissionsFromUser](js-apis-abilityAccessCtrl.md#requestpermissionsfromuser9)申请权限时返回此对象表明此次权限申请的结果。

> **说明：**
>
> - 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。  
> - 本模块接口仅可在Stage模型下使用。

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Security.AccessToken

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| permissions | Array&lt;string&gt; | 是 | 否 | 用户传入的权限。|
| authResults | Array&lt;number&gt; | 是 | 否 | 相应请求权限的结果：<br>- -1：未授权，表示权限已设置，无需弹窗，需要用户在"设置"中修改。<br>- 0：已授权。<br>- 2：未授权，表示请求无效，可能原因有：<br>  -未在设置文件中声明目标权限。<br>  -权限名非法。<br>  -部分权限存在特殊申请条件，在申请对应权限时未满足其指定的条件，见[ohos.permission.LOCATION](../../security/AccessToken/permissions-for-all.md#ohospermissionlocation)与[ohos.permission.APPROXIMATELY_LOCATION](../../security/AccessToken/permissions-for-all.md#ohospermissionapproximately_location) |

## 使用说明

通过atManager实例来获取。

**示例：**
示例中context的获取方式请参见[获取UIAbility的上下文信息](../../application-models/uiability-usage.md#获取uiability的上下文信息)。

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';
import common from '@ohos.app.ability.common';

let atManager = abilityAccessCtrl.createAtManager();
try {
  let context: Context = getContext(this) as common.UIAbilityContext;
  atManager.requestPermissionsFromUser(context, ["ohos.permission.CAMERA"]).then((data) => {
      console.info("data:" + JSON.stringify(data));
      console.info("data permissions:" + data.permissions);
      console.info("data authResults:" + data.authResults);
  }).catch((err: BusinessError) => {
      console.info("data:" + JSON.stringify(err));
  })
} catch(err) {
  console.log(`catch err->${JSON.stringify(err)}`);
}
```