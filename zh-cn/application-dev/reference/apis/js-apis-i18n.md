# @ohos.i18n (国际化-I18n)

 本模块提供系统相关的或者增强的国际化能力，包括区域管理、电话号码处理、日历等，相关接口为ECMA 402标准中未定义的补充接口。
[Intl模块](js-apis-intl.md)提供了ECMA 402标准定义的基础国际化接口，与本模块共同使用可提供完整地国际化支持能力。 

>  **说明：**
>  - 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
>  - I18N模块包含国际化能力增强接口（未在ECMA 402中定义），包括区域管理、电话号码处理、日历等，国际化基础能力请参考[Intl模块](js-apis-intl.md)。


## 导入模块

```js
import I18n from '@ohos.i18n';
```


## System<sup>9+</sup>

### getDisplayCountry<sup>9+</sup>

static getDisplayCountry(country: string, locale: string, sentenceCase?: boolean): string

获取指定国家的本地化显示文本。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名          | 类型      | 必填   | 说明               |
| ------------ | ------- | ---- | ---------------- |
| country      | string  | 是    | 指定国家。            |
| locale       | string  | 是    | 显示指定国家的区域ID。     |
| sentenceCase | boolean | 否    | 本地化显示文本是否要首字母大写。 |

**返回值：** 

| 类型     | 说明            |
| ------ | ------------- |
| string | 指定国家的本地化显示文本。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```js
  try {
    let displayCountry = I18n.System.getDisplayCountry("zh-CN", "en-GB"); // displayCountry = "China"
  } catch(error) {
    console.error(`call System.getDisplayCountry failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getDisplayLanguage<sup>9+</sup>

static getDisplayLanguage(language: string, locale: string, sentenceCase?: boolean): string

获取指定语言的本地化显示文本。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名          | 类型      | 必填   | 说明               |
| ------------ | ------- | ---- | ---------------- |
| language     | string  | 是    | 指定语言。            |
| locale       | string  | 是    | 显示指定语言的区域ID。     |
| sentenceCase | boolean | 否    | 本地化显示文本是否要首字母大写。 |

**返回值：** 

| 类型     | 说明            |
| ------ | ------------- |
| string | 指定语言的本地化显示文本。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```js
  try {
    let displayLanguage = I18n.System.getDisplayLanguage("zh", "en-GB"); // displayLanguage = Chinese
  } catch(error) {
    console.error(`call System.getDisplayLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemLanguages<sup>9+</sup>

static getSystemLanguages(): Array&lt;string&gt;

获取系统支持的语言列表。语言的详细说明参见[实例化Locale对象](../../internationalization/intl-guidelines.md#开发步骤)。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型                  | 说明           |
| ------------------- | ------------ |
| Array&lt;string&gt; | 系统支持的语言ID列表。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```js
  try {
    let systemLanguages = I18n.System.getSystemLanguages(); // [ "en-Latn-US", "zh-Hans" ]
  } catch(error) {
    console.error(`call System.getSystemLanguages failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemCountries<sup>9+</sup>

static getSystemCountries(language: string): Array&lt;string&gt;

获取针对输入语言系统支持的国家或地区列表。国家或地区的详细说明参见[实例化Locale对象](../../internationalization/intl-guidelines.md#开发步骤)。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名      | 类型     | 必填   | 说明    |
| -------- | ------ | ---- | ----- |
| language | string | 是    | 语言ID。 |

**返回值：** 

| 类型                  | 说明           |
| ------------------- | ------------ |
| Array&lt;string&gt; | 系统支持的区域ID列表。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```js
  try {
    let systemCountries = I18n.System.getSystemCountries('zh'); // systemCountries = [ "ZW", "YT", "YE", ..., "ER", "CN", "DE" ]，共计240个国家或地区
  } catch(error) {
    console.error(`call System.getSystemCountries failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### isSuggested<sup>9+</sup>

static isSuggested(language: string, region?: string): boolean

判断当前语言和地区是否匹配。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名      | 类型     | 必填   | 说明            |
| -------- | ------ | ---- | ------------- |
| language | string | 是    | 合法的语言ID，例如zh。 |
| region   | string | 否    | 合法的地区ID，例如CN  |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true，表示当前语言和地区匹配；返回false，表示当前语言和地区不匹配。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid|

**示例：** 
  ```js
  try {
    let res = I18n.System.isSuggested('zh', 'CN');  // res = true
  } catch(error) {
    console.error(`call System.isSuggested failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemLanguage<sup>9+</sup>

static getSystemLanguage(): string

获取系统语言。语言的详细说明参见[实例化Locale对象](../../internationalization/intl-guidelines.md#开发步骤)。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明      |
| ------ | ------- |
| string | 系统语言ID。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 |param value not valid |

**示例：** 
  ```js
  try {
    let systemLanguage = I18n.System.getSystemLanguage();  // systemLanguage为当前系统语言
  } catch(error) {
    console.error(`call System.getSystemLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### setSystemLanguage<sup>9+</sup>

static setSystemLanguage(language: string): void

设置系统语言。当前调用该接口不支持系统界面语言的实时刷新。

此接口为系统接口。

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名      | 类型     | 必填   | 说明    |
| -------- | ------ | ---- | ----- |
| language | string | 是    | 语言ID。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid|

**示例：** 
  ```js
  try {
    I18n.System.setSystemLanguage('zh'); // 设置系统当前语言为 "zh"
  } catch(error) {
    console.error(`call System.setSystemLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemRegion<sup>9+</sup>

static getSystemRegion(): string

获取系统地区。地区的详细说明参见[实例化Locale对象](../../internationalization/intl-guidelines.md#开发步骤)。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明      |
| ------ | ------- |
| string | 系统地区ID。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```js
  try {
    let systemRegion = I18n.System.getSystemRegion(); // 获取系统当前地区设置
  } catch(error) {
    console.error(`call System.getSystemRegion failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### setSystemRegion<sup>9+</sup>

static setSystemRegion(region: string): void

设置系统区域。

此接口为系统接口。

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明    |
| ------ | ------ | ---- | ----- |
| region | string | 是    | 地区ID。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid|

**示例：** 
  ```js
  try {
    I18n.System.setSystemRegion('CN');  // 设置系统当前地区为 "CN"
  } catch(error) {
    console.error(`call System.setSystemRegion failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemLocale<sup>9+</sup>

static getSystemLocale(): string

获取系统区域。区域的详细说明参见[实例化Locale对象](../../internationalization/intl-guidelines.md#开发步骤)。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明      |
| ------ | ------- |
| string | 系统区域ID。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```js
  try {
    let systemLocale = I18n.System.getSystemLocale();  // 获取系统当前Locale
  } catch(error) {
    console.error(`call System.getSystemLocale failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### setSystemLocale<sup>9+</sup>

static setSystemLocale(locale: string): void

设置系统Locale。

此接口为系统接口。 

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明              |
| ------ | ------ | ---- | --------------- |
| locale | string | 是    | 指定区域ID，例如zh-CN。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid|

**示例：** 
  ```js
  try {
    I18n.System.setSystemLocale('zh-CN');  // 设置系统当前Locale为 "zh-CN"
  } catch(error) {
    console.error(`call System.setSystemLocale failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### is24HourClock<sup>9+</sup>

static is24HourClock(): boolean

判断系统时间是否为24小时制。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true，表示系统24小时开关开启；返回false，表示系统24小时开关关闭。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid|

**示例：** 
  ```js
  try {
    let is24HourClock = I18n.System.is24HourClock();  // 系统24小时开关是否开启
  } catch(error) {
    console.error(`call System.is24HourClock failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### set24HourClock<sup>9+</sup>

static set24HourClock(option: boolean): void

修改系统时间的24小时制设置。

此接口为系统接口。

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型      | 必填   | 说明                                       |
| ------ | ------- | ---- | ---------------------------------------- |
| option | boolean | 是    | option为true，表示开启系统24小时制开关；返回false，表示关闭系统24小时开关。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid|

**示例：** 
  ```js
  // 将系统时间设置为24小时制
  try {
    I18n.System.set24HourClock(true);
  } catch(error) {
    console.error(`call System.set24HourClock failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### addPreferredLanguage<sup>9+</sup>

static addPreferredLanguage(language: string, index?: number): void

在系统偏好语言列表中的指定位置添加偏好语言。

此接口为系统接口。

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名      | 类型     | 必填   | 说明         |
| -------- | ------ | ---- | ---------- |
| language | string | 是    | 待添加的偏好语言。  |
| index    | number | 否    | 偏好语言的添加位置。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid|

**示例：** 
  ```js
  // 将语言zh-CN添加到系统偏好语言列表中
  let language = 'zh-CN';
  let index = 0;
  try {
    I18n.System.addPreferredLanguage(language, index); // 将zh-CN添加到系统偏好语言列表的第1位
  } catch(error) {
    console.error(`call System.addPreferredLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### removePreferredLanguage<sup>9+</sup>

static removePreferredLanguage(index: number): void

删除系统偏好语言列表中指定位置的偏好语言。

此接口为系统接口。

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名   | 类型     | 必填   | 说明                    |
| ----- | ------ | ---- | --------------------- |
| index | number | 是    | 待删除偏好语言在系统偏好语言列表中的位置。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```js
  // 删除系统偏好语言列表中的第一个偏好语言
  let index = 0;
  try {
    I18n.System.removePreferredLanguage(index);
  } catch(error) {
    console.error(`call System.removePreferredLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getPreferredLanguageList<sup>9+</sup>

static getPreferredLanguageList(): Array&lt;string&gt;

获取系统偏好语言列表。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型                  | 说明        |
| ------------------- | --------- |
| Array&lt;string&gt; | 系统偏好语言列表。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid|

**示例：** 
  ```js
  try {
    let preferredLanguageList = I18n.System.getPreferredLanguageList(); // 获取系统当前偏好语言列表
  } catch(error) {
    console.error(`call System.getPreferredLanguageList failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getFirstPreferredLanguage<sup>9+</sup>

static getFirstPreferredLanguage(): string

获取偏好语言列表中的第一个偏好语言。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明             |
| ------ | -------------- |
| string | 偏好语言列表中的第一个语言。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```js
  try {
    let firstPreferredLanguage = I18n.System.getFirstPreferredLanguage();  // 获取系统当前偏好语言列表中的第一个偏好语言
  } catch(error) {
    console.error(`call System.getFirstPreferredLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getAppPreferredLanguage<sup>9+</sup>

static getAppPreferredLanguage(): string

获取应用的偏好语言。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明       |
| ------ | -------- |
| string | 应用的偏好语言。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```js
  try {
    let appPreferredLanguage = I18n.System.getAppPreferredLanguage(); // 获取应用偏好语言
  } catch(error) {
    console.error(`call System.getAppPreferredLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### setUsingLocalDigit<sup>9+</sup>

static setUsingLocalDigit(flag: boolean): void

设置系统是否使用本地数字。

此接口为系统接口。

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型      | 必填   | 说明                              |
| ---- | ------- | ---- | ------------------------------- |
| flag | boolean | 是    | true表示打开本地数字开关，false表示关闭本地数字开关。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 |param value not valid |

**示例：** 
  ```ts
  try {
    I18n.System.setUsingLocalDigit(true); // 打开本地化数字开关
  } catch(error) {
    console.error(`call System.setUsingLocalDigit failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getUsingLocalDigit<sup>9+</sup>

static getUsingLocalDigit(): boolean

判断系统是否使用本地数字。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | true表示系统当前已打开本地数字开关，false表示系统当前未打开本地数字开关。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.i18n错误码](../errorcodes/errorcode-i18n.md)。

| 错误码ID  | 错误信息                   |
| ------ | ---------------------- |
| 890001 | param value not valid |

**示例：** 
  ```ts
  try {
    let status = I18n.System.getUsingLocalDigit();  // 判断本地化数字开关是否打开
  } catch(error) {
    console.error(`call System.getUsingLocalDigit failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```


## I18n.isRTL<sup>7+</sup>

isRTL(locale: string): boolean

获取是否为从右至左显示语言。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| locale | string | 是    | 指定区域ID。 |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | true表示该locale从右至左显示语言；false表示该locale从左至右显示语言。 |

**示例：** 
  ```js
  I18n.isRTL("zh-CN");// 中文不是RTL语言，返回false
  I18n.isRTL("ar-EG");// 阿语是RTL语言，返回true
  ```


## I18n.getCalendar<sup>8+</sup>

getCalendar(locale: string, type? : string): Calendar

获取日历对象。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明                                       |
| ------ | ------ | ---- | ---------------------------------------- |
| locale | string | 是    | 合法的locale值，例如zh-Hans-CN。                 |
| type   | string | 否    | 合法的日历类型，目前合法的类型有buddhist,&nbsp;chinese,&nbsp;coptic,&nbsp;ethiopic,&nbsp;hebrew,&nbsp;gregory,&nbsp;indian,&nbsp;islamic_civil,&nbsp;islamic_tbla,&nbsp;islamic_umalqura,&nbsp;japanese,&nbsp;persian。当type没有给出时，采用区域默认的日历类型。 |

**返回值：** 

| 类型                     | 说明    |
| ---------------------- | ----- |
| [Calendar](#calendar8) | 日历对象。 |

**示例：** 
  ```js
  I18n.getCalendar("zh-Hans", "chinese"); // 获取中国农历日历对象
  ```


## Calendar<sup>8+</sup>


### setTime<sup>8+</sup>

setTime(date: Date): void

设置日历对象内部的时间日期。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型   | 必填   | 说明                |
| ---- | ---- | ---- | ----------------- |
| date | Date | 是    | 将要设置的日历对象的内部时间日期。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("en-US", "gregory");
  let date = new Date(2021, 10, 7, 8, 0, 0, 0);
  calendar.setTime(date);
  ```


### setTime<sup>8+</sup>

setTime(time: number): void

设置日历对象内部的时间日期, time为从1970.1.1 00:00:00 GMT逝去的毫秒数。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明                                       |
| ---- | ------ | ---- | ---------------------------------------- |
| time | number | 是    | time为从1970.1.1&nbsp;00:00:00&nbsp;GMT逝去的毫秒数。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("en-US", "gregory");
  calendar.setTime(10540800000);
  ```


### set<sup>8+</sup>

set(year: number, month: number, date:number, hour?: number, minute?: number, second?: number): void

设置日历对象的年、月、日、时、分、秒。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明     |
| ------ | ------ | ---- | ------ |
| year   | number | 是    | 设置的年。  |
| month  | number | 是    | 设置的月。  |
| date   | number | 是    | 设置的日。  |
| hour   | number | 否    | 设置的小时。 |
| minute | number | 否    | 设置的分钟。 |
| second | number | 否    | 设置的秒。  |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.set(2021, 10, 1, 8, 0, 0); // set time to 2021.10.1 08:00:00
  ```


### setTimeZone<sup>8+</sup>

setTimeZone(timezone: string): void

设置日历对象的时区。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名      | 类型     | 必填   | 说明                        |
| -------- | ------ | ---- | ------------------------- |
| timezone | string | 是    | 设置的时区id，如“Asia/Shanghai”。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.setTimeZone("Asia/Shanghai");
  ```


### getTimeZone<sup>8+</sup>

getTimeZone(): string

获取日历对象的时区。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明         |
| ------ | ---------- |
| string | 日历对象的时区id。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.setTimeZone("Asia/Shanghai");
  let timezone = calendar.getTimeZone(); // timezone = "Asia/Shanghai"
  ```


### getFirstDayOfWeek<sup>8+</sup>

getFirstDayOfWeek(): number

获取日历对象的一周起始日。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明                    |
| ------ | --------------------- |
| number | 获取一周的起始日，1代表周日，7代表周六。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("en-US", "gregory");
  let firstDayOfWeek = calendar.getFirstDayOfWeek(); // firstDayOfWeek = 1
  ```


### setFirstDayOfWeek<sup>8+</sup>

setFirstDayOfWeek(value: number): void

设置每一周的起始日。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名   | 类型     | 必填   | 说明                    |
| ----- | ------ | ---- | --------------------- |
| value | number | 是    | 设置一周的起始日，1代表周日，7代表周六。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.setFirstDayOfWeek(3);
  let firstDayOfWeek = calendar.getFirstDayOfWeek(); // firstDayOfWeek = 3
  ```


### getMinimalDaysInFirstWeek<sup>8+</sup>

getMinimalDaysInFirstWeek(): number

获取一年中第一周的最小天数。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明           |
| ------ | ------------ |
| number | 一年中第一周的最小天数。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  let minimalDaysInFirstWeek = calendar.getMinimalDaysInFirstWeek(); // minimalDaysInFirstWeek = 1
  ```


### setMinimalDaysInFirstWeek<sup>8+</sup>

setMinimalDaysInFirstWeek(value: number): void

设置一年中第一周的最小天数。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名   | 类型     | 必填   | 说明           |
| ----- | ------ | ---- | ------------ |
| value | number | 是    | 一年中第一周的最小天数。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.setMinimalDaysInFirstWeek(3);
  let minimalDaysInFirstWeek = calendar.getMinimalDaysInFirstWeek(); // minimalDaysInFirstWeek = 3
  ```


### get<sup>8+</sup>

get(field: string): number

获取日历对象中与field相关联的值。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名   | 类型     | 必填   | 说明                                       |
| ----- | ------ | ---- | ---------------------------------------- |
| field | string | 是    | 通过field来获取日历对象相应的值。目前支持的field值有&nbsp;era,&nbsp;year,&nbsp;month,&nbsp;week_of_year,&nbsp;week_of_month,&nbsp;date,&nbsp;day_of_year,&nbsp;day_of_week,&nbsp;day_of_week_in_month,&nbsp;hour,&nbsp;hour_of_day,&nbsp;minute,&nbsp;second,&nbsp;millisecond,&nbsp;zone_offset,&nbsp;dst_offset,&nbsp;year_woy,&nbsp;dow_local,&nbsp;extended_year,&nbsp;julian_day,&nbsp;milliseconds_in_day,&nbsp;is_leap_month。 |

**返回值：** 

| 类型     | 说明                                       |
| ------ | ---------------------------------------- |
| number | 与field相关联的值，如当前Calendar对象的内部日期的年份为1990，get("year")返回1990。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.set(2021, 10, 1, 8, 0, 0); // set time to 2021.10.1 08:00:00
  let hourOfDay = calendar.get("hour_of_day"); // hourOfDay = 8
  ```


### getDisplayName<sup>8+</sup>

getDisplayName(locale: string): string

获取日历对象在locale所指定的区域的名字。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明                                       |
| ------ | ------ | ---- | ---------------------------------------- |
| locale | string | 是    | locale指定获取哪个区域下该calendar的名字，如buddhist在en-US上显示的名称为“Buddhist&nbsp;Calendar”。 |

**返回值：** 

| 类型     | 说明                  |
| ------ | ------------------- |
| string | 日历在locale所指示的区域的名字。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("en-US", "buddhist");
  let calendarName = calendar.getDisplayName("zh"); // calendarName = "佛历"
  ```


### isWeekend<sup>8+</sup>

isWeekend(date?: Date): boolean

判断给定的日期是否在日历中是周末。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型   | 必填   | 说明                                       |
| ---- | ---- | ---- | ---------------------------------------- |
| date | Date | 否    | 判断日期在日历中是否是周末。如果不传日期参数，则判断当前日期是否为周末。 |

**返回值：** 

| 类型      | 说明                                  |
| ------- | ----------------------------------- |
| boolean | 当所判断的日期为周末时，返回&nbsp;true，否则返回false。 |

**示例：** 
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.set(2021, 11, 11, 8, 0, 0); // set time to 2021.11.11 08:00:00
  calendar.isWeekend(); // false
  let date = new Date(2011, 11, 6, 9, 0, 0);
  calendar.isWeekend(date); // true
  ```


## PhoneNumberFormat<sup>8+</sup>


### constructor<sup>8+</sup>

constructor(country: string, options?: PhoneNumberFormatOptions)

创建电话号码格式化对象。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名     | 类型                                       | 必填   | 说明               |
| ------- | ---------------------------------------- | ---- | ---------------- |
| country | string                                   | 是    | 表示电话号码所属国家或地区代码。 |
| options | [PhoneNumberFormatOptions](#phonenumberformatoptions9) | 否    | 电话号码格式化对象的相关选项。  |

**示例：** 
  ```js
  let phoneNumberFormat= new I18n.PhoneNumberFormat("CN", {"type": "E164"});
  ```


### isValidNumber<sup>8+</sup>

isValidNumber(number: string): boolean

判断传入的电话号码格式是否正确。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明        |
| ------ | ------ | ---- | --------- |
| number | string | 是    | 待判断的电话号码。 |

**返回值：** 

| 类型      | 说明                                    |
| ------- | ------------------------------------- |
| boolean | 返回true表示电话号码的格式正确，返回false表示电话号码的格式错误。 |

**示例：** 
  ```js
  let phonenumberfmt = new I18n.PhoneNumberFormat("CN");
  let isValidNumber = phonenumberfmt.isValidNumber("158****2312"); // isValidNumber = true
  ```


### format<sup>8+</sup>

format(number: string): string

对电话号码进行格式化。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明         |
| ------ | ------ | ---- | ---------- |
| number | string | 是    | 待格式化的电话号码。 |

**返回值：** 

| 类型     | 说明         |
| ------ | ---------- |
| string | 格式化后的电话号码。 |

**示例：**
  ```ts
  let phonenumberfmt: I18n.PhoneNumberFormat = new I18n.PhoneNumberFormat("CN");
  let formattedPhoneNumber: string = phonenumberfmt.format("158****2312"); // formattedPhoneNumber = "158 **** 2312"
  ```


### getLocationName<sup>9+</sup>

getLocationName(number: string, locale: string): string

获取电话号码归属地。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明   |
| ------ | ------ | ---- | ---- |
| number | string | 是    | 电话号码 |
| locale | string | 是    | 区域ID |

**返回值：** 

| 类型     | 说明       |
| ------ | -------- |
| string | 电话号码归属地。 |

**示例：**
  ```ts
  let phonenumberfmt: I18n.PhoneNumberFormat = new I18n.PhoneNumberFormat("CN");
  let locationName: string = phonenumberfmt.getLocationName("158****2345", "zh-CN"); // locationName = "广东省湛江市"
  ```


## PhoneNumberFormatOptions<sup>9+</sup>

表示电话号码格式化对象可设置的属性。

**系统能力**：SystemCapability.Global.I18n

| 名称   | 类型     | 可读   | 可写   | 说明                                       |
| ---- | ------ | ---- | ---- | ---------------------------------------- |
| type | string | 是    | 是    | 表示对电话号码格式化的类型，取值范围："E164",&nbsp;"INTERNATIONAL",&nbsp;"NATIONAL",&nbsp;"RFC3966"。 |


## UnitInfo<sup>8+</sup>

度量衡单位信息。

**系统能力**：SystemCapability.Global.I18n

| 名称            | 类型     | 可读   | 可写   | 说明                                       |
| ------------- | ------ | ---- | ---- | ---------------------------------------- |
| unit          | string | 是    | 是    | 单位的名称，如："meter",&nbsp;"inch",&nbsp;"cup"等。 |
| measureSystem | string | 是    | 是    | 单位的度量体系，取值包括："SI",&nbsp;"US",&nbsp;"UK"。 |


## getInstance<sup>8+</sup>

getInstance(locale?:string): IndexUtil

创建并返回IndexUtil对象。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明                           |
| ------ | ------ | ---- | ---------------------------- |
| locale | string | 否    | 包含区域设置信息的字符串，包括语言以及可选的脚本和区域。 |

**返回值：** 

| 类型                       | 说明                    |
| ------------------------ | --------------------- |
| [IndexUtil](#indexutil8) | locale对应的IndexUtil对象。 |

**示例：** 
  ```js
  let indexUtil = I18n.getInstance("zh-CN");
  ```


## IndexUtil<sup>8+</sup>


### getIndexList<sup>8+</sup>

getIndexList(): Array&lt;string&gt;

获取当前locale对应的索引列表。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型                  | 说明                 |
| ------------------- | ------------------ |
| Array&lt;string&gt; | 返回当前locale对应的索引列表。 |

**示例：** 
  ```js
  let indexUtil = I18n.getInstance("zh-CN");
  // indexList = [ "...", "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N",
  //              "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z", "..." ]
  let indexList = indexUtil.getIndexList();
  ```


### addLocale<sup>8+</sup>

addLocale(locale: string): void

将新的locale对应的索引加入当前索引列表。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明                           |
| ------ | ------ | ---- | ---------------------------- |
| locale | string | 是    | 包含区域设置信息的字符串，包括语言以及可选的脚本和区域。 |

**示例：** 
  ```js
  let indexUtil = I18n.getInstance("zh-CN");
  indexUtil.addLocale("en-US");
  ```


### getIndex<sup>8+</sup>

getIndex(text: string): string

获取text对应的索引。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明           |
| ---- | ------ | ---- | ------------ |
| text | string | 是    | 待计算索引值的输入文本。 |

**返回值：** 

| 类型     | 说明          |
| ------ | ----------- |
| string | 输入文本对应的索引值。 |

**示例：** 
  ```js
  let indexUtil = I18n.getInstance("zh-CN");
  let index = indexUtil.getIndex("hi");  // index = "H"
  ```


## I18n.getLineInstance<sup>8+</sup>

getLineInstance(locale: string): BreakIterator

获取一个用于断句的[BreakIterator](#breakiterator8)对象。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明                                       |
| ------ | ------ | ---- | ---------------------------------------- |
| locale | string | 是    | 合法的locale值，例如zh-Hans-CN。生成的[BreakIterator](#breakiterator8)将按照locale所指定的区域的规则来进行断句。 |

**返回值：** 

| 类型                               | 说明          |
| -------------------------------- | ----------- |
| [BreakIterator](#breakiterator8) | 用于进行断句的处理器。 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  ```


## BreakIterator<sup>8+</sup>


### setLineBreakText<sup>8+</sup>

setLineBreakText(text: string): void

设置[BreakIterator](#breakiterator8)要处理的文本。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明                      |
| ---- | ------ | ---- | ----------------------- |
| text | string | 是    | 指定BreakIterator进行断句的文本。 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit."); // 设置短句文本
  ```


### getLineBreakText<sup>8+</sup>

getLineBreakText(): string

获取[BreakIterator](#breakiterator8)当前处理的文本。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明                     |
| ------ | ---------------------- |
| string | BreakIterator对象正在处理的文本 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let breakText = iterator.getLineBreakText(); // breakText = "Apple is my favorite fruit."
  ```


### current<sup>8+</sup>

current(): number

获取[BreakIterator](#breakiterator8)对象在当前处理的文本中的位置。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明                          |
| ------ | --------------------------- |
| number | BreakIterator在当前所处理的文本中的位置。 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let currentPos = iterator.current(); // currentPos = 0
  ```


### first<sup>8+</sup>

first(): number

将[BreakIterator](#breakiterator8)对象设置到第一个可断句的分割点。第一个分割点总是被处理的文本的起始位置。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明                |
| ------ | ----------------- |
| number | 被处理文本的第一个分割点的偏移量。 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let firstPos = iterator.first(); // firstPos = 0
  ```


### last<sup>8+</sup>

last(): number

将[BreakIterator](#breakiterator8)对象的位置设置到最后一个可断句的分割点。最后一个分割点总是被处理文本末尾的下一个位置。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明                 |
| ------ | ------------------ |
| number | 被处理的文本的最后一个分割点的偏移量 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let lastPos = iterator.last(); // lastPos = 27
  ```


### next<sup>8+</sup>

next(index?: number): number

如果index给出，并且index是一个正数将[BreakIterator](#breakiterator8)向后移动number个可断句的分割点，如果n是一个负数，向前移动相应个分割点。若index没有给出，则相当于index = 1。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名   | 类型     | 必填   | 说明                                       |
| ----- | ------ | ---- | ---------------------------------------- |
| index | number | 否    | [BreakIterator](#breakiterator8)将要移动的分割点数，正数代表向后移动，负数代表向前移动。若index没有给出，则按照index=1处理。 |

**返回值：** 

| 类型     | 说明                                       |
| ------ | ---------------------------------------- |
| number | 返回移动了index个分割点后，当前[BreakIterator](#breakiterator8)在文本中的位置。若移动index个分割点后超出了所处理的文本的长度范围，返回-1。 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let pos = iterator.first(); // pos = 0
  pos = iterator.next(); // pos = 6
  pos = iterator.next(10); // pos = -1
  ```


### previous<sup>8+</sup>

previous(): number

将[BreakIterator](#breakiterator8)移动到前一个分割点处。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明                                       |
| ------ | ---------------------------------------- |
| number | 返回移动到前一个分割点后，当前[BreakIterator](#breakiterator8)在文本中的位置。若移动index个分割点后超出了所处理的文本的长度范围，返回-1。 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let pos = iterator.first(); // pos = 0
  pos = iterator.next(3); // pos = 12
  pos = iterator.previous(); // pos = 9
  ```


### following<sup>8+</sup>

following(offset: number): number

将[BreakIterator](#breakiterator8)设置到由offset指定的位置的后面一个分割点。返回移动后[BreakIterator](#breakiterator8)的位置。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明                                       |
| ------ | ------ | ---- | ---------------------------------------- |
| offset | number | 是    | 将[BreakIterator](#breakiterator8)对象的位置设置到由offset所指定的位置的下一个分割点。 |

**返回值：** 

| 类型     | 说明                                       |
| ------ | ---------------------------------------- |
| number | 返回[BreakIterator](#breakiterator8)移动后的位置，如果由offset所指定的位置的下一个分割点超出了文本的范围则返回-1。 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let pos = iterator.following(0); // pos = 6
  pos = iterator.following(100); // pos = -1
  pos = iterator.current(); // pos = 27
  ```


### isBoundary<sup>8+</sup>

isBoundary(offset: number): boolean

如果offset所指定的文本位置是一个分割点，那么返回true，否则返回false。如果返回true, 将[BreakIterator](#breakiterator8)对象设置到offset所指定的位置, 否则相当于调用[following](#following8)(offset)。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明          |
| ------ | ------ | ---- | ----------- |
| offset | number | 是    | 指定需要进行判断的位置 |

**返回值：** 

| 类型      | 说明                              |
| ------- | ------------------------------- |
| boolean | 如果是一个分割点返回true,&nbsp;否则返回false。 |

**示例：** 
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let isBoundary = iterator.isBoundary(0); // isBoundary = true;
  isBoundary = iterator.isBoundary(5); // isBoundary = false;
  ```


## I18n.getTimeZone<sup>7+</sup>

getTimeZone(zoneID?: string): TimeZone

获取时区ID对应的时区对象。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明    |
| ------ | ------ | ---- | ----- |
| zondID | string | 否    | 时区ID。 |

**返回值：** 

| 类型       | 说明           |
| -------- | ------------ |
| TimeZone | 时区ID对应的时区对象。 |

**示例：** 
  ```js
  let timezone = I18n.getTimeZone();
  ```


## TimeZone


### getID

getID(): string

获取时区对象的ID。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明           |
| ------ | ------------ |
| string | 时区对象对应的时区ID。 |

**示例：** 
  ```js
  let timezone = I18n.getTimeZone();
  let timezoneID = timezone.getID(); // timezoneID = "Asia/Shanghai"
  ```


### getDisplayName

getDisplayName(locale?: string, isDST?: boolean): string

获取时区的本地化表示。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型      | 必填   | 说明                   |
| ------ | ------- | ---- | -------------------- |
| locale | string  | 否    | 区域ID。                |
| isDST  | boolean | 否    | 表示获取时区对象的表示时是否考虑夏令时。 |

**返回值：** 

| 类型     | 说明            |
| ------ | ------------- |
| string | 时区对象在指定区域的表示。 |

**示例：** 
  ```js
  let timezone = I18n.getTimeZone();
  let timezoneName = timezone.getDisplayName("zh-CN", false); // timezoneName = "中国标准时间"
  ```


### getRawOffset

getRawOffset(): number

获取时区对象表示的时区与UTC时区的偏差。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明                  |
| ------ | ------------------- |
| number | 时区对象表示的时区与UTC时区的偏差。 |

**示例：** 
  ```js
  let timezone = I18n.getTimeZone();
  let offset = timezone.getRawOffset(); // offset = 28800000
  ```


### getOffset

getOffset(date?: number): number

获取某一时刻时区对象表示的时区与UTC时区的偏差。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明                      |
| ------ | ----------------------- |
| number | 某一时刻时区对象表示的时区与UTC时区的偏差。 |

**示例：** 
  ```js
  let timezone = I18n.getTimeZone();
  let offset = timezone.getOffset(1234567890); // offset = 28800000
  ```


### getAvailableIDs<sup>9+</sup>

static getAvailableIDs(): Array&lt;string&gt;

获取系统支持的时区ID。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型                  | 说明          |
| ------------------- | ----------- |
| Array&lt;string&gt; | 系统支持的时区ID列表 |

**示例：** 
  ```ts
  // ids = ["America/Adak", "America/Anchorage", "America/Bogota", "America/Denver", "America/Los_Angeles", "America/Montevideo", "America/Santiago", "America/Sao_Paulo", "Asia/Ashgabat", "Asia/Hovd", "Asia/Jerusalem", "Asia/Magadan", "Asia/Omsk", "Asia/Shanghai", "Asia/Tokyo", "Asia/Yerevan", "Atlantic/Cape_Verde", "Australia/Lord_Howe", "Europe/Dublin", "Europe/London", "Europe/Moscow", "Pacific/Auckland", "Pacific/Easter", "Pacific/Pago-Pago"], 当前共支持24个时区
  let ids = I18n.TimeZone.getAvailableIDs();
  ```


### getAvailableZoneCityIDs<sup>9+</sup>

static getAvailableZoneCityIDs(): Array&lt;string&gt;

获取系统支持的时区城市ID。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型                  | 说明            |
| ------------------- | ------------- |
| Array&lt;string&gt; | 系统支持的时区城市ID列表 |

**示例：** 
  ```ts
  // cityIDs = ["Auckland", "Magadan", "Lord Howe Island", "Tokyo", "Shanghai", "Hovd", "Omsk", "Ashgabat", "Yerevan", "Moscow", "Tel Aviv", "Dublin", "London", "Praia", "Montevideo", "Brasília", "Santiago", "Bogotá", "Easter Island", "Salt Lake City", "Los Angeles", "Anchorage", "Adak", "Pago Pago"]，当前共支持24个时区城市
  let cityIDs = I18n.TimeZone.getAvailableZoneCityIDs();
  ```


### getCityDisplayName<sup>9+</sup>

static getCityDisplayName(cityID: string, locale: string): string

获取某时区城市在locale下的本地化显示。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明     |
| ------ | ------ | ---- | ------ |
| cityID | string | 是    | 时区城市ID |
| locale | string | 是    | 区域ID   |

**返回值：** 

| 类型     | 说明                 |
| ------ | ------------------ |
| string | 时区城市在locale下的本地化显示 |

**示例：** 
  ```ts
  let displayName = I18n.TimeZone.getCityDisplayName("Shanghai", "zh-CN"); // displayName = "上海(中国)"
  ```


### getTimezoneFromCity<sup>9+</sup>

static getTimezoneFromCity(cityID: string): TimeZone

创建某时区城市对应的时区对象。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明     |
| ------ | ------ | ---- | ------ |
| cityID | string | 是    | 时区城市ID |

**返回值：** 

| 类型       | 说明          |
| -------- | ----------- |
| TimeZone | 时区城市对应的时区对象 |

**示例：** 
  ```ts
  let timezone = I18n.TimeZone.getTimezoneFromCity("Shanghai");
  ```


## Transliterator<sup>9+</sup>


### getAvailableIDs<sup>9+</sup>

static getAvailableIDs(): string[]

获取音译支持的ID列表。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型       | 说明         |
| -------- | ---------- |
| string[] | 音译支持的ID列表。 |

**示例：** 
  ```ts
  // ids共支持671个。每一个id由使用中划线分割的两部分组成，格式为 source-destination。例如ids = ["Han-Latin","Latin-ASCII", "Amharic-Latin/BGN","Accents-Any", ...]，Han-Latin表示汉语转为译拉丁文，Amharic-Latin表示阿姆哈拉语转为拉丁文。
  // 更多使用信息可以参考ISO-15924。
  let ids = I18n.Transliterator.getAvailableIDs();
  ```


### getInstance<sup>9+</sup>

static getInstance(id: string): Transliterator

创建音译对象。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明       |
| ---- | ------ | ---- | -------- |
| id   | string | 是    | 音译支持的ID。 |

**返回值：** 

| 类型                                 | 说明    |
| ---------------------------------- | ----- |
| [Transliterator](#transliterator9) | 音译对象。 |

**示例：** 
  ```ts
  let transliterator = I18n.Transliterator.getInstance("Any-Latn");
  ```


### transform<sup>9+</sup>

transform(text: string): string

将输入字符串从源格式转换为目标格式。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明     |
| ---- | ------ | ---- | ------ |
| text | string | 是    | 输入字符串。 |

**返回值：** 

| 类型     | 说明       |
| ------ | -------- |
| string | 转换后的字符串。 |

**示例：** 
  ```ts
  let transliterator = I18n.Transliterator.getInstance("Any-Latn");
  let res = transliterator.transform("中国"); // res = "zhōng guó"
  ```


## Unicode<sup>9+</sup>


### isDigit<sup>9+</sup>

static isDigit(char: string): boolean

判断字符串char是否是数字。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                   |
| ------- | ------------------------------------ |
| boolean | 返回true表示输入的字符是数字，返回false表示输入的字符不是数字。 |

**示例：** 
  ```js
  let isdigit = I18n.Unicode.isDigit("1");  // isdigit = true
  ```


### isSpaceChar<sup>9+</sup>

static isSpaceChar(char: string): boolean

判断字符串char是否是空格符。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                     |
| ------- | -------------------------------------- |
| boolean | 返回true表示输入的字符是空格符，返回false表示输入的字符不是空格符。 |

**示例：** 
  ```js
  let isspacechar = I18n.Unicode.isSpaceChar("a");  // isspacechar = false
  ```


### isWhitespace<sup>9+</sup>

static isWhitespace(char: string): boolean

判断字符串char是否是空白符。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                     |
| ------- | -------------------------------------- |
| boolean | 返回true表示输入的字符是空白符，返回false表示输入的字符不是空白符。 |

**示例：** 
  ```js
  let iswhitespace = I18n.Unicode.isWhitespace("a");  // iswhitespace = false
  ```


### isRTL<sup>9+</sup>

static isRTL(char: string): boolean

判断字符串char是否是从右到左语言的字符。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true表示输入的字符是从右到左语言的字符，返回false表示输入的字符不是从右到左语言的字符。 |

**示例：** 
  ```js
  let isrtl = I18n.Unicode.isRTL("a");  // isrtl = false
  ```


### isIdeograph<sup>9+</sup>

static isIdeograph(char: string): boolean

判断字符串char是否是表意文字。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true表示输入的字符是表意文字，返回false表示输入的字符不是表意文字。 |

**示例：** 
  ```js
  let isideograph = I18n.Unicode.isIdeograph("a");  // isideograph = false
  ```


### isLetter<sup>9+</sup>

static isLetter(char: string): boolean

判断字符串char是否是字母。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                   |
| ------- | ------------------------------------ |
| boolean | 返回true表示输入的字符是字母，返回false表示输入的字符不是字母。 |

**示例：** 
  ```js
  let isletter = I18n.Unicode.isLetter("a");  // isletter = true
  ```


### isLowerCase<sup>9+</sup>

static isLowerCase(char: string): boolean

判断字符串char是否是小写字母。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true表示输入的字符是小写字母，返回false表示输入的字符不是小写字母。 |

**示例：** 
  ```js
  let islowercase = I18n.Unicode.isLowerCase("a");  // islowercase = true
  ```


### isUpperCase<sup>9+</sup>

static isUpperCase(char: string): boolean

判断字符串char是否是大写字母。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true表示输入的字符是大写字母，返回false表示输入的字符不是大写字母。 |

**示例：** 
  ```js
  let isuppercase = I18n.Unicode.isUpperCase("a");  // isuppercase = false
  ```


### getType<sup>9+</sup>

static getType(char: string): string

获取输入字符串的一般类别值。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型     | 说明          |
| ------ | ----------- |
| string | 输入字符的一般类别值。 |

**示例：** 
  ```js
  let type = I18n.Unicode.getType("a"); // type = "U_LOWERCASE_LETTER"
  ```


## I18NUtil<sup>9+</sup>


### unitConvert<sup>9+</sup>

static unitConvert(fromUnit: UnitInfo, toUnit: UnitInfo, value: number, locale: string, style?: string): string

将fromUnit的单位转换为toUnit的单位，并根据区域与风格进行格式化。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名      | 类型                     | 必填   | 说明                                       |
| -------- | ---------------------- | ---- | ---------------------------------------- |
| fromUnit | [UnitInfo](#unitinfo8) | 是    | 要被转换的单位。                                 |
| toUnit   | [UnitInfo](#unitinfo8) | 是    | 要转换为的单位。                                 |
| value    | number                 | 是    | 要被转换的单位的数量值。                             |
| locale   | string                 | 是    | 格式化时使用的区域参数，如：zh-Hans-CN。                |
| style    | string                 | 否    | 格式化使用的风格，取值包括："long",&nbsp;"short",&nbsp;"narrow"。 |

**返回值：** 

| 类型     | 说明                      |
| ------ | ----------------------- |
| string | 按照toUnit的单位格式化后，得到的字符串。 |

**示例：** 
  ```js
  let res = I18n.I18NUtil.unitConvert({unit: "cup", measureSystem: "US"}, {unit: "liter", measureSystem: "SI"}, 1000, "en-US", "long"); // res = 236.588 liters
  ```


### getDateOrder<sup>9+</sup>

static getDateOrder(locale: string): string

获取某一区域的日期的年、月、日排列顺序。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型     | 必填   | 说明                        |
| ------ | ------ | ---- | ------------------------- |
| locale | string | 是    | 格式化时使用的区域参数，如：zh-Hans-CN。 |

**返回值：** 

| 类型     | 说明                  |
| ------ | ------------------- |
| string | 返回某一区域的日期的年、月、日排列顺序 |

**示例：** 
  ```js
  let order = I18n.I18NUtil.getDateOrder("zh-CN");  // order = "y-L-d"
  ```


## I18n.getDisplayCountry<sup>(deprecated)</sup>

getDisplayCountry(country: string, locale: string, sentenceCase?: boolean): string

获取指定国家的本地化显示文本。

从API version 9开始不再维护，建议使用[System.getDisplayCountry](#getdisplaycountry9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名          | 类型      | 必填   | 说明               |
| ------------ | ------- | ---- | ---------------- |
| country      | string  | 是    | 指定国家。            |
| locale       | string  | 是    | 显示指定国家的区域ID。     |
| sentenceCase | boolean | 否    | 本地化显示文本是否要首字母大写。 |

**返回值：** 

| 类型     | 说明            |
| ------ | ------------- |
| string | 指定国家的本地化显示文本。 |

**示例：** 
  ```js
  let countryName = I18n.getDisplayCountry("zh-CN", "en-GB", true); // countryName = true
  countryName = I18n.getDisplayCountry("zh-CN", "en-GB"); // countryName = true
  ```


## I18n.getDisplayLanguage<sup>(deprecated)</sup>

getDisplayLanguage(language: string, locale: string, sentenceCase?: boolean): string

获取指定语言的本地化显示文本。

从API version 9开始不再维护，建议使用[System.getDisplayLanguage](#getdisplaylanguage9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名          | 类型      | 必填   | 说明               |
| ------------ | ------- | ---- | ---------------- |
| language     | string  | 是    | 指定语言。            |
| locale       | string  | 是    | 显示指定语言的区域ID。     |
| sentenceCase | boolean | 否    | 本地化显示文本是否要首字母大写。 |

**返回值：** 

| 类型     | 说明            |
| ------ | ------------- |
| string | 指定语言的本地化显示文本。 |

**示例：** 
  ```js
  let languageName = I18n.getDisplayLanguage("zh", "en-GB", true); // languageName = "Chinese"
  languageName = I18n.getDisplayLanguage("zh", "en-GB"); // languageName = "Chinese"
  ```


## I18n.getSystemLanguage<sup>(deprecated)</sup>

getSystemLanguage(): string

获取系统语言。

从API version 9开始不再维护，建议使用[System.getSystemLanguage](#getsystemlanguage9)代替。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明      |
| ------ | ------- |
| string | 系统语言ID。 |

**示例：** 
  ```js
  let systemLanguage = I18n.getSystemLanguage(); // 返回当前系统语言
  ```


## I18n.getSystemRegion<sup>(deprecated)</sup>

getSystemRegion(): string

获取系统地区。

从API version 9开始不再维护，建议使用[System.getSystemRegion](#getsystemregion9)代替。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明      |
| ------ | ------- |
| string | 系统地区ID。 |

**示例：** 
  ```js
  let region = I18n.getSystemRegion(); // 返回当前系统地区
  ```


## I18n.getSystemLocale<sup>(deprecated)</sup>

getSystemLocale(): string

获取系统区域。

从API version 9开始不再维护，建议使用[System.getSystemLocale](#getsystemlocale9)代替。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明      |
| ------ | ------- |
| string | 系统区域ID。 |

**示例：** 
  ```js
  let locale = I18n.getSystemLocale(); // 返回系统Locale
  ```


## I18n.is24HourClock<sup>(deprecated)</sup>

is24HourClock(): boolean

判断系统时间是否为24小时制。

从API version 9开始不再维护，建议使用[System.is24HourClock](#is24hourclock9)代替。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true，表示系统24小时开关开启；返回false，表示系统24小时开关关闭。 |

**示例：** 
  ```js
  let is24HourClock = I18n.is24HourClock();
  ```


## I18n.set24HourClock<sup>(deprecated)</sup>

set24HourClock(option: boolean): boolean

修改系统时间的24小时制设置。

从API version 9开始不再维护，建议使用[System.set24HourClock](#set24hourclock9)代替。

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名    | 类型      | 必填   | 说明                                       |
| ------ | ------- | ---- | ---------------------------------------- |
| option | boolean | 是    | option为true，表示开启系统24小时制开关；返回false，表示关闭系统24小时开关。 |

**返回值：** 

| 类型      | 说明                            |
| ------- | ----------------------------- |
| boolean | 返回true，表示修改成功；返回false，表示修改失败。 |

**示例：** 
  ```js
  // 将系统时间设置为24小时制
  let success = I18n.set24HourClock(true);
  ```


## I18n.addPreferredLanguage<sup>(deprecated)</sup>

addPreferredLanguage(language: string, index?: number): boolean

在系统偏好语言列表中的指定位置添加偏好语言。

从API version 8开始支持，从API version 9开始不再维护，建议使用[System.addPreferredLanguage](#addpreferredlanguage9)代替。

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名      | 类型     | 必填   | 说明         |
| -------- | ------ | ---- | ---------- |
| language | string | 是    | 待添加的偏好语言。  |
| index    | number | 否    | 偏好语言的添加位置。 |

**返回值：** 

| 类型      | 说明                            |
| ------- | ----------------------------- |
| boolean | 返回true，表示添加成功；返回false，表示添加失败。 |

**示例：** 
  ```js
  // 将语言zh-CN添加到系统偏好语言列表中
  let language = 'zh-CN';
  let index = 0;
  let success = I18n.addPreferredLanguage(language, index);
  ```


## I18n.removePreferredLanguage<sup>(deprecated)</sup>

removePreferredLanguage(index: number): boolean

删除系统偏好语言列表中指定位置的偏好语言。

从API version 8开始支持，从API version 9开始不再维护，建议使用[System.removePreferredLanguage](#removepreferredlanguage9)代替。

**需要权限**：ohos.permission.UPDATE_CONFIGURATION

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名   | 类型     | 必填   | 说明                    |
| ----- | ------ | ---- | --------------------- |
| index | number | 是    | 待删除偏好语言在系统偏好语言列表中的位置。 |

**返回值：** 

| 类型      | 说明                            |
| ------- | ----------------------------- |
| boolean | 返回true，表示删除成功；返回false，表示删除失败。 |

**示例：** 
  ```js
  // 删除系统偏好语言列表中的第一个偏好语言
  let index = 0;
  let success = I18n.removePreferredLanguage(index);
  ```


## I18n.getPreferredLanguageList<sup>(deprecated)</sup>

getPreferredLanguageList(): Array&lt;string&gt;

获取系统偏好语言列表。

从API version 8开始支持，从API version 9开始不再维护，建议使用[System.getPreferredLanguageList](#getpreferredlanguagelist9)代替。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型                  | 说明        |
| ------------------- | --------- |
| Array&lt;string&gt; | 系统偏好语言列表。 |

**示例：** 
  ```js
  let preferredLanguageList = I18n.getPreferredLanguageList(); // 获取系统偏好语言列表
  ```


## I18n.getFirstPreferredLanguage<sup>(deprecated)</sup>

getFirstPreferredLanguage(): string

获取偏好语言列表中的第一个偏好语言。

从API version 8开始支持，从API version 9开始不再维护，建议使用[System.getFirstPreferredLanguage](#getfirstpreferredlanguage9)代替。

**系统能力**：SystemCapability.Global.I18n

**返回值：** 

| 类型     | 说明             |
| ------ | -------------- |
| string | 偏好语言列表中的第一个语言。 |

**示例：** 
  ```js
  let firstPreferredLanguage = I18n.getFirstPreferredLanguage();
  ```


## Util<sup>(deprecated)</sup>


### unitConvert<sup>(deprecated)</sup>

static unitConvert(fromUnit: UnitInfo, toUnit: UnitInfo, value: number, locale: string, style?: string): string

将fromUnit的单位转换为toUnit的单位，并根据区域与风格进行格式化。

从API version 8开始支持，从API version 9开始不再维护，建议使用[unitConvert](#unitconvert9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名      | 类型                     | 必填   | 说明                                       |
| -------- | ---------------------- | ---- | ---------------------------------------- |
| fromUnit | [UnitInfo](#unitinfo8) | 是    | 要被转换的单位。                                 |
| toUnit   | [UnitInfo](#unitinfo8) | 是    | 要转换为的单位。                                 |
| value    | number                 | 是    | 要被转换的单位的数量值。                             |
| locale   | string                 | 是    | 格式化时使用的区域参数，如：zh-Hans-CN。                |
| style    | string                 | 否    | 格式化使用的风格，取值包括："long",&nbsp;"short",&nbsp;"narrow"。 |

**返回值：** 

| 类型     | 说明                      |
| ------ | ----------------------- |
| string | 按照toUnit的单位格式化后，得到的字符串。 |


## Character<sup>(deprecated)</sup>


### isDigit<sup>(deprecated)</sup>

static isDigit(char: string): boolean

判断字符串char是否是数字。

从API version 8开始支持，从API version 9开始不再维护，建议使用[isDigit](#isdigit9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                   |
| ------- | ------------------------------------ |
| boolean | 返回true表示输入的字符是数字，返回false表示输入的字符不是数字。 |


### isSpaceChar<sup>(deprecated)</sup>

static isSpaceChar(char: string): boolean

判断字符串char是否是空格符。

从API version 8开始支持，从API version 9开始不再维护，建议使用[isSpaceChar](#isspacechar9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                     |
| ------- | -------------------------------------- |
| boolean | 返回true表示输入的字符是空格符，返回false表示输入的字符不是空格符。 |


### isWhitespace<sup>(deprecated)</sup>

static isWhitespace(char: string): boolean

判断字符串char是否是空白符。

从API version 8开始支持，从API version 9开始不再维护，建议使用[isWhitespace](#iswhitespace9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                     |
| ------- | -------------------------------------- |
| boolean | 返回true表示输入的字符是空白符，返回false表示输入的字符不是空白符。 |


### isRTL<sup>(deprecated)</sup>

static isRTL(char: string): boolean

判断字符串char是否是从右到左语言的字符。

从API version 8开始支持，从API version 9开始不再维护，建议使用[isRTL](#isrtl9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true表示输入的字符是从右到左语言的字符，返回false表示输入的字符不是从右到左语言的字符。 |


### isIdeograph<sup>(deprecated)</sup>

static isIdeograph(char: string): boolean

判断字符串char是否是表意文字。

从API version 8开始支持，从API version 9开始不再维护，建议使用[isIdeograph](#isideograph9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true表示输入的字符是表意文字，返回false表示输入的字符不是表意文字。 |


### isLetter<sup>(deprecated)</sup>

static isLetter(char: string): boolean

判断字符串char是否是字母。

从API version 8开始支持，从API version 9开始不再维护，建议使用[isLetter](#isletter9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                   |
| ------- | ------------------------------------ |
| boolean | 返回true表示输入的字符是字母，返回false表示输入的字符不是字母。 |


### isLowerCase<sup>(deprecated)</sup>

static isLowerCase(char: string): boolean

判断字符串char是否是小写字母。

从API version 8开始支持，从API version 9开始不再维护，建议使用[isLowerCase](#islowercase9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true表示输入的字符是小写字母，返回false表示输入的字符不是小写字母。 |


### isUpperCase<sup>(deprecated)</sup>

static isUpperCase(char: string): boolean

判断字符串char是否是大写字母。

从API version 8开始支持，从API version 9开始不再维护，建议使用[isUpperCase](#isuppercase9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型      | 说明                                       |
| ------- | ---------------------------------------- |
| boolean | 返回true表示输入的字符是大写字母，返回false表示输入的字符不是大写字母。 |


### getType<sup>(deprecated)</sup>

static getType(char: string): string

获取输入字符串的一般类别值。

从API version 8开始支持，从API version 9开始不再维护，建议使用[getType](#gettype9)代替。

**系统能力**：SystemCapability.Global.I18n

**参数：** 

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| char | string | 是    | 输入字符。 |

**返回值：** 

| 类型     | 说明          |
| ------ | ----------- |
| string | 输入字符的一般类别值。 |
