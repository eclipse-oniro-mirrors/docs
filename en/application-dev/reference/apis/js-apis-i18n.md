# @ohos.i18n (Internationalization)

 This module provides system-related or enhanced i18n capabilities, such as locale management, phone number formatting, and calendar, through supplementary i18n APIs that are not defined in ECMA 402.
The [intl](js-apis-intl.md) module provides basic i18n capabilities through the standard i18n APIs defined in ECMA 402. It works with the **i18n** module to provide a complete suite of i18n capabilities.

>  **NOTE**
>  - The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
>  - This module provides system-related or enhanced I18N capabilities, such as locale management, phone number formatting, and calendar, through supplementary I18N APIs that are not defined in ECMA 402. For details about the basic I18N capabilities, see [Intl](js-apis-intl.md).


## Modules to Import

```js
import I18n from '@ohos.i18n';
```


## System<sup>9+</sup>

### getDisplayCountry<sup>9+</sup>

static getDisplayCountry(country: string, locale: string, sentenceCase?: boolean): string

Obtains the localized script for the specified country.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name         | Type     | Mandatory  | Description              |
| ------------ | ------- | ---- | ---------------- |
| country      | string  | Yes   | Specified country.           |
| locale       | string  | Yes   | Locale ID.    |
| sentenceCase | boolean | No   | Whether to use sentence case for the localized script.|

**Return value**

| Type    | Description           |
| ------ | ------------- |
| string | Localized script for the specified country.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```js
  try {
    let displayCountry = I18n.System.getDisplayCountry("zh-CN", "en-GB"); // displayCountry = "China"
  } catch(error) {
    console.error(`call System.getDisplayCountry failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getDisplayLanguage<sup>9+</sup>

static getDisplayLanguage(language: string, locale: string, sentenceCase?: boolean): string

Obtains the localized script for the specified language.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name         | Type     | Mandatory  | Description              |
| ------------ | ------- | ---- | ---------------- |
| language     | string  | Yes   | Specified language.           |
| locale       | string  | Yes   | Locale ID.    |
| sentenceCase | boolean | No   | Whether to use sentence case for the localized script.|

**Return value**

| Type    | Description           |
| ------ | ------------- |
| string | Localized script for the specified language.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```js
  try {
    let displayLanguage = I18n.System.getDisplayLanguage("zh", "en-GB"); // displayLanguage = Chinese
  } catch(error) {
    console.error(`call System.getDisplayLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemLanguages<sup>9+</sup>

static getSystemLanguages(): Array&lt;string&gt;

Obtains the list of system languages. For details about languages, see [Instantiating the Locale Object](../../internationalization/intl-guidelines.md#how-to-develop).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type                 | Description          |
| ------------------- | ------------ |
| Array&lt;string&gt; | List of the IDs of system languages.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```js
  try {
    let systemLanguages = I18n.System.getSystemLanguages(); // [ "en-Latn-US", "zh-Hans" ]
  } catch(error) {
    console.error(`call System.getSystemLanguages failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemCountries<sup>9+</sup>

static getSystemCountries(language: string): Array&lt;string&gt;

Obtains the list of countries and regions supported for the specified language. For details about countries or regions, see [Instantiating the Locale Object](../../internationalization/intl-guidelines.md#how-to-develop).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name     | Type    | Mandatory  | Description   |
| -------- | ------ | ---- | ----- |
| language | string | Yes   | Language ID.|

**Return value**

| Type                 | Description          |
| ------------------- | ------------ |
| Array&lt;string&gt; | List of the IDs of the countries and regions supported for the specified language.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```js
  try {
    let systemCountries = I18n.System.getSystemCountries('zh'); // systemCountries = [ "ZW", "YT", "YE", ..., "ER", "CN", "DE" ], 240 countries or regions in total
  } catch(error) {
    console.error(`call System.getSystemCountries failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### isSuggested<sup>9+</sup>

static isSuggested(language: string, region?: string): boolean

Checks whether the system language matches the specified region.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name     | Type    | Mandatory  | Description           |
| -------- | ------ | ---- | ------------- |
| language | string | Yes   | Valid language ID, for example, **zh**.|
| region   | string | No   | Valid region ID, for example, **CN**. |

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the system language matches the specified region, and the value **false** indicates the opposite.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid|

**Example**
  ```js
  try {
    let res = I18n.System.isSuggested('zh', 'CN');  // res = true
  } catch(error) {
    console.error(`call System.isSuggested failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemLanguage<sup>9+</sup>

static getSystemLanguage(): string

Obtains the system language. For details about languages, see [Instantiating the Locale Object](../../internationalization/intl-guidelines.md#how-to-develop).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description     |
| ------ | ------- |
| string | System language ID.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 |param value not valid |

**Example**
  ```js
  try {
    let systemLanguage = I18n.System.getSystemLanguage(); // systemLanguage indicates the current system language.
  } catch(error) {
    console.error(`call System.getSystemLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### setSystemLanguage<sup>9+</sup>

static setSystemLanguage(language: string): void

Sets the system language. Currently, this API does not support real-time updating of the system language.

This is a system API.

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name     | Type    | Mandatory  | Description   |
| -------- | ------ | ---- | ----- |
| language | string | Yes   | Language ID.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid|

**Example**
  ```js
  try {
    I18n.System.setSystemLanguage('zh'); // Set the current system language to zh.
  } catch(error) {
    console.error(`call System.setSystemLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemRegion<sup>9+</sup>

static getSystemRegion(): string

Obtains the system region. For details about system regions, see [Instantiating the Locale Object](../../internationalization/intl-guidelines.md#how-to-develop).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description     |
| ------ | ------- |
| string | System region ID.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```js
  try {
    let systemRegion = I18n.System.getSystemRegion(); // Obtain the current system region.
  } catch(error) {
    console.error(`call System.getSystemRegion failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### setSystemRegion<sup>9+</sup>

static setSystemRegion(region: string): void

Sets the system region.

This is a system API.

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description   |
| ------ | ------ | ---- | ----- |
| region | string | Yes   | System region ID.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid|

**Example**
  ```js
  try {
    I18n.System.setSystemRegion('CN'); // Set the current system region to CN.
  } catch(error) {
    console.error(`call System.setSystemRegion failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getSystemLocale<sup>9+</sup>

static getSystemLocale(): string

Obtains the system locale. For details about system locales, see [Instantiating the Locale Object](../../internationalization/intl-guidelines.md#how-to-develop).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description     |
| ------ | ------- |
| string | System locale ID.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```js
  try {
    let systemLocale = I18n.System.getSystemLocale(); // Obtain the current system locale.
  } catch(error) {
    console.error(`call System.getSystemLocale failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### setSystemLocale<sup>9+</sup>

static setSystemLocale(locale: string): void

Sets the system locale.

This is a system API.

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description             |
| ------ | ------ | ---- | --------------- |
| locale | string | Yes   | System locale ID, for example, **zh-CN**.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid|

**Example**
  ```js
  try {
    I18n.System.setSystemLocale('zh-CN'); // Set the current system locale to zh-CN.
  } catch(error) {
    console.error(`call System.setSystemLocale failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### is24HourClock<sup>9+</sup>

static is24HourClock(): boolean

Checks whether the 24-hour clock is used.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the 24-hour clock is used, and the value **false** indicates the opposite.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid|

**Example**
  ```js
  try {
    let is24HourClock = I18n.System.is24HourClock(); // Check whether the 24-hour clock is enabled.
  } catch(error) {
    console.error(`call System.is24HourClock failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### set24HourClock<sup>9+</sup>

static set24HourClock(option: boolean): void

Sets the 24-hour clock.

This is a system API.

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type     | Mandatory  | Description                                      |
| ------ | ------- | ---- | ---------------------------------------- |
| option | boolean | Yes   | Whether to enable the 24-hour clock. The value **true** means to enable the 24-hour clock, and the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid|

**Example**
  ```js
  // Set the system time to the 24-hour clock.
  try {
    I18n.System.set24HourClock(true);
  } catch(error) {
    console.error(`call System.set24HourClock failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### addPreferredLanguage<sup>9+</sup>

static addPreferredLanguage(language: string, index?: number): void

Adds a preferred language to the specified position on the preferred language list.

This is a system API.

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name     | Type    | Mandatory  | Description        |
| -------- | ------ | ---- | ---------- |
| language | string | Yes   | Preferred language to add. |
| index    | number | No   | Position to which the preferred language is added.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid|

**Example**
  ```js
  // Add zh-CN to the preferred language list.
  let language = 'zh-CN';
  let index = 0;
  try {
    I18n.System.addPreferredLanguage(language, index); // Add zh-CN to the first place in the preferred language list.
  } catch(error) {
    console.error(`call System.addPreferredLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### removePreferredLanguage<sup>9+</sup>

static removePreferredLanguage(index: number): void

Deletes a preferred language from the specified position on the preferred language list.

This is a system API.

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name  | Type    | Mandatory  | Description                   |
| ----- | ------ | ---- | --------------------- |
| index | number | Yes   | Position of the preferred language to delete.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```js
  // Delete the first preferred language from the preferred language list.
  let index = 0;
  try {
    I18n.System.removePreferredLanguage(index);
  } catch(error) {
    console.error(`call System.removePreferredLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getPreferredLanguageList<sup>9+</sup>

static getPreferredLanguageList(): Array&lt;string&gt;

Obtains the list of preferred languages.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type                 | Description       |
| ------------------- | --------- |
| Array&lt;string&gt; | List of preferred languages.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid|

**Example**
  ```js
  try {
    let preferredLanguageList = I18n.System.getPreferredLanguageList(); // Obtain the current preferred language list.
  } catch(error) {
    console.error(`call System.getPreferredLanguageList failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getFirstPreferredLanguage<sup>9+</sup>

static getFirstPreferredLanguage(): string

Obtains the first language in the preferred language list.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description            |
| ------ | -------------- |
| string | First language in the preferred language list.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```js
  try {
    let firstPreferredLanguage = I18n.System.getFirstPreferredLanguage(); // Obtain the first language in the preferred language list.
  } catch(error) {
    console.error(`call System.getFirstPreferredLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getAppPreferredLanguage<sup>9+</sup>

static getAppPreferredLanguage(): string

Obtains the preferred language of an application.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description      |
| ------ | -------- |
| string | Preferred language of the application.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```js
  try {
    let appPreferredLanguage = I18n.System.getAppPreferredLanguage(); // Obtain the preferred language of an application.
  } catch(error) {
    console.error(`call System.getAppPreferredLanguage failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### setUsingLocalDigit<sup>9+</sup>

static setUsingLocalDigit(flag: boolean): void

Specifies whether to enable use of local digits.

This is a system API.

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type     | Mandatory  | Description                             |
| ---- | ------- | ---- | ------------------------------- |
| flag | boolean | Yes   | Whether to turn on the local digit switch. The value **true** means to turn on the local digit switch, and the value **false** indicates the opposite.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 |param value not valid |

**Example**
  ```ts
  try {
    I18n.System.setUsingLocalDigit(true); // Enable the local digit switch.
  } catch(error) {
    console.error(`call System.setUsingLocalDigit failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```

### getUsingLocalDigit<sup>9+</sup>

static getUsingLocalDigit(): boolean

Checks whether use of local digits is enabled.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the local digit switch is turned on, and the value **false** indicates the opposite.|

**Error codes**

For details about the error codes, see [I18N Error Codes](../errorcodes/errorcode-i18n.md).

| ID | Error Message                  |
| ------ | ---------------------- |
| 890001 | param value not valid |

**Example**
  ```ts
  try {
    let status = I18n.System.getUsingLocalDigit(); // Check whether the local digit switch is enabled.
  } catch(error) {
    console.error(`call System.getUsingLocalDigit failed, error code: ${error.code}, message: ${error.message}.`);
  }
  ```


## I18n.isRTL<sup>7+</sup>

isRTL(locale: string): boolean

Checks whether the localized script for the specified language is displayed from right to left.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description     |
| ------ | ------ | ---- | ------- |
| locale | string | Yes   | Locale ID.|

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the localized script is displayed from right to left, and the value **false** indicates the opposite.|

**Example**
  ```js
  i18n.isRTL("zh-CN");// Since Chinese is not written from right to left, false is returned.
  i18n.isRTL("ar-EG");// Since Arabic is written from right to left, true is returned.
  ```


## I18n.getCalendar<sup>8+</sup>

getCalendar(locale: string, type? : string): Calendar

Obtains a **Calendar** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description                                      |
| ------ | ------ | ---- | ---------------------------------------- |
| locale | string | Yes   | Valid locale value, for example, **zh-Hans-CN**.                |
| type   | string | No   | Valid calendar type. Currently, the valid types are as follows: **buddhist**, **chinese**, **coptic**, **ethiopic**, **hebrew**, **gregory**, **indian**, **islamic\_civil**, **islamic\_tbla**, **islamic\_umalqura**, **japanese**, and **persian**. If this parameter is left unspecified, the default calendar type of the specified locale is used.|

**Return value**

| Type                    | Description   |
| ---------------------- | ----- |
| [Calendar](#calendar8) | **Calendar** object.|

**Example**
  ```js
  I18n.getCalendar("zh-Hans", "chinese"); // Obtain the Calendar object for the Chinese lunar calendar.
  ```


## Calendar<sup>8+</sup>


### setTime<sup>8+</sup>

setTime(date: Date): void

Sets the date for this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type  | Mandatory  | Description               |
| ---- | ---- | ---- | ----------------- |
| date | Date | Yes   | Date to be set for the **Calendar** object.|

**Example**
  ```js
  let calendar = I18n.getCalendar("en-US", "gregory");
  let date = new Date(2021, 10, 7, 8, 0, 0, 0);
  calendar.setTime(date);
  ```


### setTime<sup>8+</sup>

setTime(time: number): void

Sets the date and time for this **Calendar** object. The value is represented by the number of milliseconds that have elapsed since the Unix epoch (00:00:00 UTC on January 1, 1970).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description                                      |
| ---- | ------ | ---- | ---------------------------------------- |
| time | number | Yes   | Number of milliseconds that have elapsed since the Unix epoch.|

**Example**
  ```js
  let calendar = I18n.getCalendar("en-US", "gregory");
  calendar.setTime(10540800000);
  ```


### set<sup>8+</sup>

set(year: number, month: number, date:number, hour?: number, minute?: number, second?: number): void

Sets the year, month, day, hour, minute, and second for this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description    |
| ------ | ------ | ---- | ------ |
| year   | number | Yes   | Year to set. |
| month  | number | Yes   | Month to set. |
| date   | number | Yes   | Day to set. |
| hour   | number | No   | Hour to set.|
| minute | number | No   | Minute to set.|
| second | number | No   | Second to set. |

**Example**
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.set(2021, 10, 1, 8, 0, 0); // set time to 2021.10.1 08:00:00
  ```


### setTimeZone<sup>8+</sup>

setTimeZone(timezone: string): void

Sets the time zone of this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name     | Type    | Mandatory  | Description                       |
| -------- | ------ | ---- | ------------------------- |
| timezone | string | Yes   | Time zone, for example, **Asia/Shanghai**.|

**Example**
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.setTimeZone("Asia/Shanghai");
  ```


### getTimeZone<sup>8+</sup>

getTimeZone(): string

Obtains the time zone of this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description        |
| ------ | ---------- |
| string | Time zone of the **Calendar** object.|

**Example**
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.setTimeZone("Asia/Shanghai");
  let timezone = calendar.getTimeZone(); // timezone = "Asia/Shanghai"
  ```


### getFirstDayOfWeek<sup>8+</sup>

getFirstDayOfWeek(): number

Obtains the start day of a week for this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description                   |
| ------ | --------------------- |
| number | Start day of a week. The value **1** indicates Sunday, and the value **7** indicates Saturday.|

**Example**
  ```js
  let calendar = I18n.getCalendar("en-US", "gregory");
  let firstDayOfWeek = calendar.getFirstDayOfWeek(); // firstDayOfWeek = 1
  ```


### setFirstDayOfWeek<sup>8+</sup>

setFirstDayOfWeek(value: number): void

Sets the start day of a week for this **Calendar** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name  | Type    | Mandatory  | Description                   |
| ----- | ------ | ---- | --------------------- |
| value | number | Yes   | Start day of a week. The value **1** indicates Sunday, and the value **7** indicates Saturday.|

**Example**
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.setFirstDayOfWeek(3);
  let firstDayOfWeek = calendar.getFirstDayOfWeek(); // firstDayOfWeek = 3
  ```


### getMinimalDaysInFirstWeek<sup>8+</sup>

getMinimalDaysInFirstWeek(): number

Obtains the minimum number of days in the first week of a year.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description          |
| ------ | ------------ |
| number | Minimum number of days in the first week of a year.|

**Example**
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  let minimalDaysInFirstWeek = calendar.getMinimalDaysInFirstWeek(); // minimalDaysInFirstWeek = 1
  ```


### setMinimalDaysInFirstWeek<sup>8+</sup>

setMinimalDaysInFirstWeek(value: number): void

Sets the minimum number of days in the first week of a year.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name  | Type    | Mandatory  | Description          |
| ----- | ------ | ---- | ------------ |
| value | number | Yes   | Minimum number of days in the first week of a year.|

**Example**
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.setMinimalDaysInFirstWeek(3);
  let minimalDaysInFirstWeek = calendar.getMinimalDaysInFirstWeek(); // minimalDaysInFirstWeek = 3
  ```


### get<sup>8+</sup>

get(field: string): number

Obtains the value of the specified field in the **Calendar** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name  | Type    | Mandatory  | Description                                      |
| ----- | ------ | ---- | ---------------------------------------- |
| field | string | Yes   | Value of the specified field in the **Calendar** object. Currently, a valid field can be any of the following: **era**, **year**, **month**, **week\_of\_year**, **week\_of\_month**, **date**, **day\_of\_year**, **day\_of\_week**, **day\_of\_week\_in\_month**, **hour**, **hour\_of\_day**, **minute**, **second**, **millisecond**, **zone\_offset**, **dst\_offset**, **year\_woy**, **dow\_local**, **extended\_year**, **julian\_day**, **milliseconds\_in\_day**, **is\_leap\_month**.|

**Return value**

| Type    | Description                                      |
| ------ | ---------------------------------------- |
| number | Value of the specified field. For example, if the year in the internal date of this **Calendar** object is **1990**, the **get("year")** function will return **1990**.|

**Example**
  ```js
  let calendar = I18n.getCalendar("zh-Hans");
  calendar.set(2021, 10, 1, 8, 0, 0); // set time to 2021.10.1 08:00:00
  let hourOfDay = calendar.get("hour_of_day"); // hourOfDay = 8
  ```


### getDisplayName<sup>8+</sup>

getDisplayName(locale: string): string

Obtains the **Calendar** object name displayed for the specified locale.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description                                      |
| ------ | ------ | ---- | ---------------------------------------- |
| locale | string | Yes   | Locale for which the name of the **Calendar** object is displayed. For example, if **locale** is **en-US**, the name of the Buddhist calendar will be **Buddhist Calendar**.|

**Return value**

| Type    | Description                 |
| ------ | ------------------- |
| string | Displayed name of the **Calendar** object for the specified locale.|

**Example**
  ```js
  let calendar = I18n.getCalendar("en-US", "buddhist");
  let calendarName = calendar.getDisplayName("zh"); // calendarName = "Buddhist Calendar"
  ```


### isWeekend<sup>8+</sup>

isWeekend(date?: Date): boolean

Checks whether the specified date in this **Calendar** object is a weekend.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type  | Mandatory  | Description                                      |
| ---- | ---- | ---- | ---------------------------------------- |
| date | Date | No   | Specified date in this **Calendar** object. If the **date** parameter is not specified, the system checks whether the current date is a weekend.|

**Return value**

| Type     | Description                                 |
| ------- | ----------------------------------- |
| boolean | The value **true** indicates that the date is a weekend, and the value **false** indicates that the date is a weekday.|

**Example**
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

Creates a **PhoneNumberFormat** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name    | Type                                      | Mandatory  | Description              |
| ------- | ---------------------------------------- | ---- | ---------------- |
| country | string                                   | Yes   | Country or region to which the phone number to be formatted belongs.|
| options | [PhoneNumberFormatOptions](#phonenumberformatoptions9) | No   | Options of the **PhoneNumberFormat** object. |

**Example**
  ```js
  let phoneNumberFormat= new I18n.PhoneNumberFormat("CN", {"type": "E164"});
  ```


### isValidNumber<sup>8+</sup>

isValidNumber(number: string): boolean

Checks whether the format of the specified phone number is valid.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description       |
| ------ | ------ | ---- | --------- |
| number | string | Yes   | Phone number to be checked.|

**Return value**

| Type     | Description                                   |
| ------- | ------------------------------------- |
| boolean | The value **true** indicates that the phone number format is valid, and the value **false** indicates the opposite.|

**Example**
  ```js
  let phonenumberfmt = new I18n.PhoneNumberFormat("CN");
  let isValidNumber = phonenumberfmt.isValidNumber("158****2312"); // isValidNumber = true
  ```


### format<sup>8+</sup>

format(number: string): string

Formats a phone number.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description        |
| ------ | ------ | ---- | ---------- |
| number | string | Yes   | Phone number to be formatted.|

**Return value**

| Type    | Description        |
| ------ | ---------- |
| string | Formatted phone number.|

**Example**
  ```ts
  let phonenumberfmt: I18n.PhoneNumberFormat = new I18n.PhoneNumberFormat("CN");
  let formattedPhoneNumber: string = phonenumberfmt.format("158****2312"); // formattedPhoneNumber = "158 **** 2312"
  ```


### getLocationName<sup>9+</sup>

getLocationName(number: string, locale: string): string

Obtains the home location of a phone number.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description  |
| ------ | ------ | ---- | ---- |
| number | string | Yes   | Phone number.|
| locale | string | Yes   | Locale ID.|

**Return value**

| Type    | Description      |
| ------ | -------- |
| string | Home location of the phone number.|

**Example**
  ```ts
  let phonenumberfmt: I18n.PhoneNumberFormat = new I18n.PhoneNumberFormat("CN");
  let locationName: string = phonenumberfmt.getLocationName("158****2345", "zh-CN"); // locationName = "Zhanjiang, Guangdong Province"
  ```


## PhoneNumberFormatOptions<sup>9+</sup>

Defines the options for this PhoneNumberFormat object.

**System capability**: SystemCapability.Global.I18n

| Name  | Type    | Readable  | Writable  | Description                                      |
| ---- | ------ | ---- | ---- | ---------------------------------------- |
| type | string | Yes   | Yes   | Format type of a phone number. The value can be **E164**, **INTERNATIONAL**, **NATIONAL**, or **RFC3966**.|


## UnitInfo<sup>8+</sup>

Defines the measurement unit information.

**System capability**: SystemCapability.Global.I18n

| Name           | Type    | Readable  | Writable  | Description                                      |
| ------------- | ------ | ---- | ---- | ---------------------------------------- |
| unit          | string | Yes   | Yes   | Name of the measurement unit, for example, **meter**, **inch**, or **cup**.|
| measureSystem | string | Yes   | Yes   | Measurement system. The value can be **SI**, **US**, or **UK**.|


## getInstance<sup>8+</sup>

getInstance(locale?:string): IndexUtil

Creates an **IndexUtil** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description                          |
| ------ | ------ | ---- | ---------------------------- |
| locale | string | No   | A string containing locale information, including the language, optional script, and region.|

**Return value**

| Type                      | Description                   |
| ------------------------ | --------------------- |
| [IndexUtil](#indexutil8) | **IndexUtil** object mapping to the **locale** object.|

**Example**
  ```js
  let indexUtil = I18n.getInstance("zh-CN");
  ```


## IndexUtil<sup>8+</sup>


### getIndexList<sup>8+</sup>

getIndexList(): Array&lt;string&gt;

Obtains the index list for this **locale** object.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type                 | Description                |
| ------------------- | ------------------ |
| Array&lt;string&gt; | Index list for the **locale** object.|

**Example**
  ```js
  let indexUtil = I18n.getInstance("zh-CN");
  // indexList = [ "...", "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N",
  //              "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z", "..." ]
  let indexList = indexUtil.getIndexList();
  ```


### addLocale<sup>8+</sup>

addLocale(locale: string): void

Adds the index of the new **locale** object to the index list.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description                          |
| ------ | ------ | ---- | ---------------------------- |
| locale | string | Yes   | A string containing locale information, including the language, optional script, and region.|

**Example**
  ```js
  let indexUtil = I18n.getInstance("zh-CN");
  indexUtil.addLocale("en-US");
  ```


### getIndex<sup>8+</sup>

getIndex(text: string): string

Obtains the index of a **text** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description          |
| ---- | ------ | ---- | ------------ |
| text | string | Yes   | **text** object whose index is to be obtained.|

**Return value**

| Type    | Description         |
| ------ | ----------- |
| string | Index of the **text** object.|

**Example**
  ```js
  let indexUtil = I18n.getInstance("zh-CN");
  let index = indexUtil.getIndex("hi");  // index = "H"
  ```


## I18n.getLineInstance<sup>8+</sup>

getLineInstance(locale: string): BreakIterator

Obtains a [BreakIterator](#breakiterator8) object for text segmentation.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description                                      |
| ------ | ------ | ---- | ---------------------------------------- |
| locale | string | Yes   | Valid locale value, for example, **zh-Hans-CN**. The [BreakIterator](#breakiterator8) object segments text according to the rules of the specified locale.|

**Return value**

| Type                              | Description         |
| -------------------------------- | ----------- |
| [BreakIterator](#breakiterator8) | [BreakIterator](#breakiterator8) object used for text segmentation.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  ```


## BreakIterator<sup>8+</sup>


### setLineBreakText<sup>8+</sup>

setLineBreakText(text: string): void

Sets the text to be processed by the [BreakIterator](#breakiterator8) object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description                     |
| ---- | ------ | ---- | ----------------------- |
| text | string | Yes   | Text to be processed by the **BreakIterator** object.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit ."); // Set a short sentence as the text to be processed by the BreakIterator object.
  ```


### getLineBreakText<sup>8+</sup>

getLineBreakText(): string

Obtains the text being processed by the [BreakIterator](#breakiterator8) object.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description                    |
| ------ | ---------------------- |
| string | Text being processed by the **BreakIterator** object.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let breakText = iterator.getLineBreakText(); // breakText = "Apple is my favorite fruit."
  ```


### current<sup>8+</sup>

current(): number

Obtains the position of the [BreakIterator](#breakiterator8) object in the text being processed.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description                         |
| ------ | --------------------------- |
| number | Position of the **BreakIterator** object in the text being processed.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let currentPos = iterator.current(); // currentPos = 0
  ```


### first<sup>8+</sup>

first(): number

Puts the [BreakIterator](#breakiterator8) object to the first text boundary, which is always at the beginning of the processed text.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description               |
| ------ | ----------------- |
| number | Offset to the first break point of the processed text.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let firstPos = iterator.first(); // firstPos = 0
  ```


### last<sup>8+</sup>

last(): number

Puts the [BreakIterator](#breakiterator8) object to the last text boundary, which is always the next position after the end of the processed text.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description                |
| ------ | ------------------ |
| number | Offset to the last break point of the processed text.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let lastPos = iterator.last(); // lastPos = 27
  ```


### next<sup>8+</sup>

next(index?: number): number

Moves the [BreakIterator](#breakiterator8) object backward by the specified number of text boundaries if the specified index is a positive number. If the index is a negative number, the [BreakIterator](#breakiterator8) object will be moved forward by the corresponding number of text boundaries. If no index is specified, the index will be treated as **1**.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name  | Type    | Mandatory  | Description                                      |
| ----- | ------ | ---- | ---------------------------------------- |
| index | number | No   | Number of text boundaries by which the [BreakIterator](#breakiterator8) object is moved. A positive value indicates that the text boundary is moved backward, and a negative value indicates the opposite. If no index is specified, the index will be treated as **1**.|

**Return value**

| Type    | Description                                      |
| ------ | ---------------------------------------- |
| number | Position of the [BreakIterator](#breakiterator8) object in the text after it is moved by the specified number of text boundaries. The value **-1** is returned if the position of the [BreakIterator](#breakiterator8) object is outside of the processed text after it is moved by the specified number of break points.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let pos = iterator.first(); // pos = 0
  pos = iterator.next(); // pos = 6
  pos = iterator.next(10); // pos = -1
  ```


### previous<sup>8+</sup>

previous(): number

Moves the [BreakIterator](#breakiterator8) object to the previous text boundary.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description                                      |
| ------ | ---------------------------------------- |
| number | Position of the [BreakIterator](#breakiterator8) object in the text after it is moved to the previous text boundary. The value **-1** is returned if the position of the [BreakIterator](#breakiterator8) object is outside of the processed text after it is moved by the specified number of break points.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let pos = iterator.first(); // pos = 0
  pos = iterator.next(3); // pos = 12
  pos = iterator.previous(); // pos = 9
  ```


### following<sup>8+</sup>

following(offset: number): number

Moves the [BreakIterator](#breakiterator8) object to the text boundary after the position specified by the offset. Position of the [BreakIterator](#breakiterator8) object after it is moved to the text boundary after the position specified by the offset.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description                                      |
| ------ | ------ | ---- | ---------------------------------------- |
| offset | number | Yes   | Offset to the position before the text boundary to which the [BreakIterator](#breakiterator8) object is moved.|

**Return value**

| Type    | Description                                      |
| ------ | ---------------------------------------- |
| number | The value **-1** is returned if the text boundary to which the [BreakIterator](#breakiterator8) object is moved is outside of the processed text.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let pos = iterator.following(0); // pos = 6
  pos = iterator.following(100); // pos = -1
  pos = iterator.current(); // pos = 27
  ```


### isBoundary<sup>8+</sup>

isBoundary(offset: number): boolean

Checks whether the position specified by the offset is a text boundary. If **true** is returned, the [BreakIterator](#breakiterator8) object is moved to the position specified by the offset. If **false** is returned, the [BreakIterator](#breakiterator8) object is moved to the text boundary after the position specified by the offset, which is equivalent to calling [following](#following8)(offset).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description         |
| ------ | ------ | ---- | ----------- |
| offset | number | Yes   | Position to check.|

**Return value**

| Type     | Description                             |
| ------- | ------------------------------- |
| boolean | The value **true** indicates that the position specified by the offset is a break point, and the value **false** indicates the opposite.|

**Example**
  ```js
  let iterator = I18n.getLineInstance("en");
  iterator.setLineBreakText("Apple is my favorite fruit.");
  let isBoundary = iterator.isBoundary(0); // isBoundary = true;
  isBoundary = iterator.isBoundary(5); // isBoundary = false;
  ```


## I18n.getTimeZone<sup>7+</sup>

getTimeZone(zoneID?: string): TimeZone

Obtains the **TimeZone** object corresponding to the specified time zone ID.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description   |
| ------ | ------ | ---- | ----- |
| zondID | string | No   | Time zone ID.|

**Return value**

| Type      | Description          |
| -------- | ------------ |
| TimeZone | **TimeZone** object corresponding to the time zone ID.|

**Example**
  ```js
  let timezone = I18n.getTimeZone();
  ```


## TimeZone


### getID

getID(): string

Obtains the ID of the specified **TimeZone** object.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description          |
| ------ | ------------ |
| string | Time zone ID corresponding to the **TimeZone** object.|

**Example**
  ```js
  let timezone = I18n.getTimeZone();
  let timezoneID = timezone.getID(); // timezoneID = "Asia/Shanghai"
  ```


### getDisplayName

getDisplayName(locale?: string, isDST?: boolean): string

Obtains the localized representation of the time zone.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type     | Mandatory  | Description                  |
| ------ | ------- | ---- | -------------------- |
| locale | string  | No   | Locale ID.               |
| isDST  | boolean | No   | Whether to consider DST when obtaining the representation of the **TimeZone** object.|

**Return value**

| Type    | Description           |
| ------ | ------------- |
| string | Representation of the **TimeZone** object in the specified locale.|

**Example**
  ```js
  let timezone = I18n.getTimeZone();
  let timezoneName = timezone.getDisplayName("zh-CN", false); // timezoneName = "China Standard Time"
  ```


### getRawOffset

getRawOffset(): number

Obtains the offset between the time zone represented by a **TimeZone** object and the UTC time zone.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description                 |
| ------ | ------------------- |
| number | Offset between the time zone represented by the **TimeZone** object and the UTC time zone.|

**Example**
  ```js
  let timezone = I18n.getTimeZone();
  let offset = timezone.getRawOffset(); // offset = 28800000
  ```


### getOffset

getOffset(date?: number): number

Obtains the offset between the time zone represented by a **TimeZone** object and the UTC time zone at a certain time point.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description                     |
| ------ | ----------------------- |
| number | Offset between the time zone represented by the **TimeZone** object and the UTC time zone at a certain time point.|

**Example**
  ```js
  let timezone = I18n.getTimeZone();
  let offset = timezone.getOffset(1234567890); // offset = 28800000
  ```


### getAvailableIDs<sup>9+</sup>

static getAvailableIDs(): Array&lt;string&gt;

Obtains the list of time zone IDs supported by the system.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type                 | Description         |
| ------------------- | ----------- |
| Array&lt;string&gt; | List of time zone IDs supported by the system.|

**Example**
  ```ts
  // ids = ["America/Adak", "America/Anchorage", "America/Bogota", "America/Denver", "America/Los_Angeles", "America/Montevideo", "America/Santiago", "America/Sao_Paulo", "Asia/Ashgabat", "Asia/Hovd", "Asia/Jerusalem", "Asia/Magadan", "Asia/Omsk", "Asia/Shanghai", "Asia/Tokyo", "Asia/Yerevan", "Atlantic/Cape_Verde", "Australia/Lord_Howe", "Europe/Dublin", "Europe/London", "Europe/Moscow", "Pacific/Auckland", "Pacific/Easter", "Pacific/Pago-Pago"], 24 time zones supported in total
  let ids = I18n.TimeZone.getAvailableIDs();
  ```


### getAvailableZoneCityIDs<sup>9+</sup>

static getAvailableZoneCityIDs(): Array&lt;string&gt;

Obtains the list of time zone city IDs supported by the system.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type                 | Description           |
| ------------------- | ------------- |
| Array&lt;string&gt; | List of time zone city IDs supported by the system.|

**Example**
  ```ts
  // cityIDs = ["Auckland", "Magadan", "Lord Howe Island", "Tokyo", "Shanghai", "Hovd", "Omsk", "Ashgabat", "Yerevan", "Moscow", "Tel Aviv", "Dublin", "London", "Praia", "Montevideo", "Brasília", "Santiago", "Bogotá", "Easter Island", "Salt Lake City", "Los Angeles", "Anchorage", "Adak", "Pago Pago"], 24 time zone cities supported in total
  let cityIDs = I18n.TimeZone.getAvailableZoneCityIDs();
  ```


### getCityDisplayName<sup>9+</sup>

static getCityDisplayName(cityID: string, locale: string): string

Obtains the localized representation of a time zone city in the specified locale.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description    |
| ------ | ------ | ---- | ------ |
| cityID | string | Yes   | Time zone city ID.|
| locale | string | Yes   | Locale ID.  |

**Return value**

| Type    | Description                |
| ------ | ------------------ |
| string | Localized representation of the time zone city in the specified locale.|

**Example**
  ```ts
  let displayName = I18n.TimeZone.getCityDisplayName("Shanghai", "zh-CN"); // displayName = "Shanghai (China)"
  ```


### getTimezoneFromCity<sup>9+</sup>

static getTimezoneFromCity(cityID: string): TimeZone

Obtains the **TimeZone** object corresponding to the specified time zone city ID.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description    |
| ------ | ------ | ---- | ------ |
| cityID | string | Yes   | Time zone city ID.|

**Return value**

| Type      | Description         |
| -------- | ----------- |
| TimeZone | **TimeZone** object corresponding to the specified time zone city ID.|

**Example**
  ```ts
  let timezone = I18n.TimeZone.getTimezoneFromCity("Shanghai");
  ```


## Transliterator<sup>9+</sup>


### getAvailableIDs<sup>9+</sup>

static getAvailableIDs(): string[]

Obtains a list of IDs supported by the **Transliterator** object.

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type      | Description        |
| -------- | ---------- |
| string[] | List of IDs supported by the **Transliterator** object.|

**Example**
  ```ts
  // A total of 671 IDs are supported. One ID is comprised of two parts separated by a hyphen (-) in the format of source-destination. For example, in **ids = ["Han-Latin","Latin-ASCII", "Amharic-Latin/BGN","Accents-Any", ...]**, **Han-Latin** indicates conversion from Chinese to Latin, and **Amharic-Latin** indicates conversion from Amharic to Latin.
  // For more information, see ISO-15924.
  let ids = I18n.Transliterator.getAvailableIDs();
  ```


### getInstance<sup>9+</sup>

static getInstance(id: string): Transliterator

Creates a **Transliterator** object.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description      |
| ---- | ------ | ---- | -------- |
| id   | string | Yes   | ID supported by the **Transliterator** object.|

**Return value**

| Type                                | Description   |
| ---------------------------------- | ----- |
| [Transliterator](#transliterator9) | **Transliterator** object.|

**Example**
  ```ts
  let transliterator = I18n.Transliterator.getInstance("Any-Latn");
  ```


### transform<sup>9+</sup>

transform(text: string): string

Converts the input string from the source format to the target format.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description    |
| ---- | ------ | ---- | ------ |
| text | string | Yes   | Input string.|

**Return value**

| Type    | Description      |
| ------ | -------- |
| string | Target string.|

**Example**
  ```ts
  let transliterator = I18n.Transliterator.getInstance("Any-Latn");
  let res = transliterator.transform("China"); // res = "zhōng guó"
  ```


## Unicode<sup>9+</sup>


### isDigit<sup>9+</sup>

static isDigit(char: string): boolean

Checks whether the input string is composed of digits.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                  |
| ------- | ------------------------------------ |
| boolean | The value **true** indicates that the input character is a digit, and the value **false** indicates the opposite.|

**Example**
  ```js
  let isdigit = I18n.Unicode.isDigit("1");  // isdigit = true
  ```


### isSpaceChar<sup>9+</sup>

static isSpaceChar(char: string): boolean

Checks whether the input character is a space.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                    |
| ------- | -------------------------------------- |
| boolean | The value **true** indicates that the input character is a space, and the value **false** indicates the opposite.|

**Example**
  ```js
  let isspacechar = I18n.Unicode.isSpaceChar("a");  // isspacechar = false
  ```


### isWhitespace<sup>9+</sup>

static isWhitespace(char: string): boolean

Checks whether the input character is a white space.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                    |
| ------- | -------------------------------------- |
| boolean | The value **true** indicates that the input character is a white space, and the value **false** indicates the opposite.|

**Example**
  ```js
  let iswhitespace = I18n.Unicode.isWhitespace("a");  // iswhitespace = false
  ```


### isRTL<sup>9+</sup>

static isRTL(char: string): boolean

Checks whether the input character is of the right to left (RTL) language.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the input character is of the RTL language, and the value **false** indicates the opposite.|

**Example**
  ```js
  let isrtl = I18n.Unicode.isRTL("a");  // isrtl = false
  ```


### isIdeograph<sup>9+</sup>

static isIdeograph(char: string): boolean

Checks whether the input character is an ideographic character.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the input character is an ideographic character, and the value **false** indicates the opposite.|

**Example**
  ```js
  let isideograph = I18n.Unicode.isIdeograph("a");  // isideograph = false
  ```


### isLetter<sup>9+</sup>

static isLetter(char: string): boolean

Checks whether the input character is a letter.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                  |
| ------- | ------------------------------------ |
| boolean | The value **true** indicates that the input character is a letter, and the value **false** indicates the opposite.|

**Example**
  ```js
  let isletter = I18n.Unicode.isLetter("a");  // isletter = true
  ```


### isLowerCase<sup>9+</sup>

static isLowerCase(char: string): boolean

Checks whether the input character is a lowercase letter.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the input character is a lowercase letter, and the value **false** indicates the opposite.|

**Example**
  ```js
  let islowercase = I18n.Unicode.isLowerCase("a");  // islowercase = true
  ```


### isUpperCase<sup>9+</sup>

static isUpperCase(char: string): boolean

Checks whether the input character is an uppercase letter.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the input character is an uppercase letter, and the value **false** indicates the opposite.|

**Example**
  ```js
  let isuppercase = I18n.Unicode.isUpperCase("a");  // isuppercase = false
  ```


### getType<sup>9+</sup>

static getType(char: string): string

Obtains the type of the input string.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type    | Description         |
| ------ | ----------- |
| string | Type of the input character.|

**Example**
  ```js
  let type = I18n.Unicode.getType("a"); // type = "U_LOWERCASE_LETTER"
  ```


## I18NUtil<sup>9+</sup>


### unitConvert<sup>9+</sup>

static unitConvert(fromUnit: UnitInfo, toUnit: UnitInfo, value: number, locale: string, style?: string): string

Converts one measurement unit into another and formats the unit based on the specified locale and style.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name     | Type                    | Mandatory  | Description                                      |
| -------- | ---------------------- | ---- | ---------------------------------------- |
| fromUnit | [UnitInfo](#unitinfo8) | Yes   | Measurement unit to be converted.                                |
| toUnit   | [UnitInfo](#unitinfo8) | Yes   | Measurement unit to be converted to.                                |
| value    | number                 | Yes   | Value of the measurement unit to be converted.                            |
| locale   | string                 | Yes   | Locale used for formatting, for example, **zh-Hans-CN**.               |
| style    | string                 | No   | Style used for formatting. The value can be **long**, **short**, or **narrow**.|

**Return value**

| Type    | Description                     |
| ------ | ----------------------- |
| string | String obtained after formatting based on the measurement unit specified by **toUnit**.|

**Example**
  ```js
  let res = I18n.I18NUtil.unitConvert({unit: "cup", measureSystem: "US"}, {unit: "liter", measureSystem: "SI"}, 1000, "en-US", "long"); // res = 236.588 liters
  ```


### getDateOrder<sup>9+</sup>

static getDateOrder(locale: string): string

Obtains the sequence of the year, month, and day in the specified locale.

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type    | Mandatory  | Description                       |
| ------ | ------ | ---- | ------------------------- |
| locale | string | Yes   | Locale used for formatting, for example, **zh-Hans-CN**.|

**Return value**

| Type    | Description                 |
| ------ | ------------------- |
| string | Sequence of the year, month, and day.|

**Example**
  ```js
  let order = I18n.I18NUtil.getDateOrder("zh-CN");  // order = "y-L-d"
  ```


## I18n.getDisplayCountry<sup>(deprecated)</sup>

getDisplayCountry(country: string, locale: string, sentenceCase?: boolean): string

Obtains the localized script for the specified country.

This API is deprecated since API version 9. You are advised to use [System.getDisplayCountry](#getdisplaycountry9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name         | Type     | Mandatory  | Description              |
| ------------ | ------- | ---- | ---------------- |
| country      | string  | Yes   | Specified country.           |
| locale       | string  | Yes   | Locale ID.    |
| sentenceCase | boolean | No   | Whether to use sentence case for the localized script.|

**Return value**

| Type    | Description           |
| ------ | ------------- |
| string | Localized script for the specified country.|

**Example**
  ```js
  let countryName = I18n.getDisplayCountry("zh-CN", "en-GB", true); // countryName = true
  countryName = I18n.getDisplayCountry("zh-CN", "en-GB"); // countryName = true
  ```


## I18n.getDisplayLanguage<sup>(deprecated)</sup>

getDisplayLanguage(language: string, locale: string, sentenceCase?: boolean): string

Obtains the localized script for the specified language.

This API is deprecated since API version 9. You are advised to use [System.getDisplayLanguage](#getdisplaylanguage9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name         | Type     | Mandatory  | Description              |
| ------------ | ------- | ---- | ---------------- |
| language     | string  | Yes   | Specified language.           |
| locale       | string  | Yes   | Locale ID.    |
| sentenceCase | boolean | No   | Whether to use sentence case for the localized script.|

**Return value**

| Type    | Description           |
| ------ | ------------- |
| string | Localized script for the specified language.|

**Example**
  ```js
  let languageName = I18n.getDisplayLanguage("zh", "en-GB", true); // languageName = "Chinese"
  languageName = I18n.getDisplayLanguage("zh", "en-GB"); // languageName = "Chinese"
  ```


## I18n.getSystemLanguage<sup>(deprecated)</sup>

getSystemLanguage(): string

Obtains the system language.

This API is deprecated since API version 9. You are advised to use [System.getSystemLanguage](#getsystemlanguage9).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description     |
| ------ | ------- |
| string | System language ID.|

**Example**
  ```js
  let systemLanguage = I18n.getSystemLanguage(); // Obtain the current system language.
  ```


## I18n.getSystemRegion<sup>(deprecated)</sup>

getSystemRegion(): string

Obtains the system region.

This API is deprecated since API version 9. You are advised to use [System.getSystemRegion](#getsystemregion9).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description     |
| ------ | ------- |
| string | System region ID.|

**Example**
  ```js
  let region = I18n.getSystemRegion(); // Obtain the current system region.
  ```


## I18n.getSystemLocale<sup>(deprecated)</sup>

getSystemLocale(): string

Obtains the system locale.

This API is deprecated since API version 9. You are advised to use [System.getSystemLocale](#getsystemlocale9).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description     |
| ------ | ------- |
| string | System locale ID.|

**Example**
  ```js
  let locale = I18n.getSystemLocale (); // Obtain the system locale.
  ```


## I18n.is24HourClock<sup>(deprecated)</sup>

is24HourClock(): boolean

Checks whether the 24-hour clock is used.

This API is deprecated since API version 9. You are advised to use [System.is24HourClock](#is24hourclock9).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the 24-hour clock is used, and the value **false** indicates the opposite.|

**Example**
  ```js
  let is24HourClock = I18n.is24HourClock();
  ```


## I18n.set24HourClock<sup>(deprecated)</sup>

set24HourClock(option: boolean): boolean

Sets the 24-hour clock.

This API is deprecated since API version 9. You are advised to use [System.set24HourClock](#set24hourclock9).

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name   | Type     | Mandatory  | Description                                      |
| ------ | ------- | ---- | ---------------------------------------- |
| option | boolean | Yes   | Whether to enable the 24-hour clock. The value **true** means to enable the 24-hour clock, and the value **false** means the opposite.|

**Return value**

| Type     | Description                           |
| ------- | ----------------------------- |
| boolean | The value **true** indicates that the 24-hour clock is enabled, and the value **false** indicates the opposite.|

**Example**
  ```js
  // Set the system time to the 24-hour clock.
  let success = I18n.set24HourClock(true);
  ```


## I18n.addPreferredLanguage<sup>(deprecated)</sup>

addPreferredLanguage(language: string, index?: number): boolean

Adds a preferred language to the specified position on the preferred language list.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [System.addPreferredLanguage](#addpreferredlanguage9).

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name     | Type    | Mandatory  | Description        |
| -------- | ------ | ---- | ---------- |
| language | string | Yes   | Preferred language to add. |
| index    | number | No   | Position to which the preferred language is added.|

**Return value**

| Type     | Description                           |
| ------- | ----------------------------- |
| boolean | The value **true** indicates that the preferred language is successfully added, and the value **false** indicates the opposite.|

**Example**
  ```js
  // Add zh-CN to the preferred language list.
  let language = 'zh-CN';
  let index = 0;
  let success = I18n.addPreferredLanguage(language, index);
  ```


## I18n.removePreferredLanguage<sup>(deprecated)</sup>

removePreferredLanguage(index: number): boolean

Deletes a preferred language from the specified position on the preferred language list.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [System.removePreferredLanguage](#removepreferredlanguage9).

**Permission required**: ohos.permission.UPDATE_CONFIGURATION

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name  | Type    | Mandatory  | Description                   |
| ----- | ------ | ---- | --------------------- |
| index | number | Yes   | Position of the preferred language to delete.|

**Return value**

| Type     | Description                           |
| ------- | ----------------------------- |
| boolean | The value **true** indicates that the preferred language is deleted, and the value **false** indicates the opposite.|

**Example**
  ```js
  // Delete the first preferred language from the preferred language list.
  let index = 0;
  let success = I18n.removePreferredLanguage(index);
  ```


## I18n.getPreferredLanguageList<sup>(deprecated)</sup>

getPreferredLanguageList(): Array&lt;string&gt;

Obtains the list of preferred languages.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [System.getPreferredLanguageList](#getpreferredlanguagelist9).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type                 | Description       |
| ------------------- | --------- |
| Array&lt;string&gt; | List of preferred languages.|

**Example**
  ```js
  let preferredLanguageList = I18n.getPreferredLanguageList(); // Obtain the preferred language list.
  ```


## I18n.getFirstPreferredLanguage<sup>(deprecated)</sup>

getFirstPreferredLanguage(): string

Obtains the first language in the preferred language list.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [System.getFirstPreferredLanguage](#getfirstpreferredlanguage9).

**System capability**: SystemCapability.Global.I18n

**Return value**

| Type    | Description            |
| ------ | -------------- |
| string | First language in the preferred language list.|

**Example**
  ```js
  let firstPreferredLanguage = I18n.getFirstPreferredLanguage();
  ```


## Util<sup>(deprecated)</sup>


### unitConvert<sup>(deprecated)</sup>

static unitConvert(fromUnit: UnitInfo, toUnit: UnitInfo, value: number, locale: string, style?: string): string

Converts one measurement unit into another and formats the unit based on the specified locale and style.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [unitConvert](#unitconvert9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name     | Type                    | Mandatory  | Description                                      |
| -------- | ---------------------- | ---- | ---------------------------------------- |
| fromUnit | [UnitInfo](#unitinfo8) | Yes   | Measurement unit to be converted.                                |
| toUnit   | [UnitInfo](#unitinfo8) | Yes   | Measurement unit to be converted to.                                |
| value    | number                 | Yes   | Value of the measurement unit to be converted.                            |
| locale   | string                 | Yes   | Locale used for formatting, for example, **zh-Hans-CN**.               |
| style    | string                 | No   | Style used for formatting. The value can be **long**, **short**, or **narrow**.|

**Return value**

| Type    | Description                     |
| ------ | ----------------------- |
| string | string obtained after formatting based on the measurement unit specified by **toUnit**.|


## Character<sup>(deprecated)</sup>


### isDigit<sup>(deprecated)</sup>

static isDigit(char: string): boolean

Checks whether the input string is composed of digits.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [isDigit](#isdigit9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                  |
| ------- | ------------------------------------ |
| boolean | The value **true** indicates that the input character is a digit, and the value **false** indicates the opposite.|


### isSpaceChar<sup>(deprecated)</sup>

static isSpaceChar(char: string): boolean

Checks whether the input character is a space.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [isSpaceChar](#isspacechar9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                    |
| ------- | -------------------------------------- |
| boolean | The value **true** indicates that the input character is a space, and the value **false** indicates the opposite.|


### isWhitespace<sup>(deprecated)</sup>

static isWhitespace(char: string): boolean

Checks whether the input character is a white space.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [isWhitespace](#iswhitespace9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                    |
| ------- | -------------------------------------- |
| boolean | The value **true** indicates that the input character is a white space, and the value **false** indicates the opposite.|


### isRTL<sup>(deprecated)</sup>

static isRTL(char: string): boolean

Checks whether the input character is of the right to left (RTL) language.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [isRTL](#isrtl9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the input character is of the RTL language, and the value **false** indicates the opposite.|


### isIdeograph<sup>(deprecated)</sup>

static isIdeograph(char: string): boolean

Checks whether the input character is an ideographic character.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [isIdeograph](#isideograph9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the input character is an ideographic character, and the value **false** indicates the opposite.|


### isLetter<sup>(deprecated)</sup>

static isLetter(char: string): boolean

Checks whether the input character is a letter.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [isLetter](#isletter9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                  |
| ------- | ------------------------------------ |
| boolean | The value **true** indicates that the input character is a letter, and the value **false** indicates the opposite.|


### isLowerCase<sup>(deprecated)</sup>

static isLowerCase(char: string): boolean

Checks whether the input character is a lowercase letter.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [isLowerCase](#islowercase9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the input character is a lowercase letter, and the value **false** indicates the opposite.|


### isUpperCase<sup>(deprecated)</sup>

static isUpperCase(char: string): boolean

Checks whether the input character is an uppercase letter.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [isUpperCase](#isuppercase9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type     | Description                                      |
| ------- | ---------------------------------------- |
| boolean | The value **true** indicates that the input character is an uppercase letter, and the value **false** indicates the opposite.|


### getType<sup>(deprecated)</sup>

static getType(char: string): string

Obtains the type of the input string.

This API is supported since API version 8 and is deprecated since API version 9. You are advised to use [getType](#gettype9).

**System capability**: SystemCapability.Global.I18n

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| char | string | Yes   | Input character.|

**Return value**

| Type    | Description         |
| ------ | ----------- |
| string | Type of the input character.|
