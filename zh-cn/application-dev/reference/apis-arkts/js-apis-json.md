# @ohos.util.json (JSON解析与生成)

本模块提供了将JSON文本转换为JSON对象或值，以及将对象转换为JSON文本等功能。

>**说明：**
>
>本模块首批接口从API version 12开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import { JSON } from '@kit.ArkTS';
```

## Transformer

type Transformer = (this: Object, key: string, value: Object) => Object | undefined | null

用于转换结果函数的类型。<br>
作为[JSON.parse](#jsonparse)函数的参数时，对象的每个成员将会调用此函数，允许在解析过程中对数据进行自定义处理或转换。<br>
作为[JSON.stringify](#jsonstringify-1)函数的参数时，序列化时，每个属性都会经过该函数的转换处理。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型   | 必填 | 说明            |
| ------ | ------ | ---- | --------------- |
| this   | Object | 是 | 在解析的键值对所属的对象。|
| key  | string | 是 | 属性名。|
| value  | Object | 是 | 在解析的键值对的值。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Object \| undefined \| null | 返回修改后的对象或undefined或null。|

## BigIntMode

定义处理BigInt的模式。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.Utils.Lang

| 名称 | 值| 说明            |
| ------ | ------ | --------------- |
| DEFAULT   | 0 |不支持BigInt。|
| PARSE_AS_BIGINT   | 1 |当整数小于-(2^53-1)或大于(2^53-1)时，解析为BigInt。|
| ALWAYS_PARSE_AS_BIGINT   | 2 |所有整数都解析为BigInt。|

## ParseOptions

解析的选项，可定义处理BigInt的模式。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.Utils.Lang

| 名称 | 类型| 必填 |说明            |
| ------ | ------ | ---- | --------------- |
| bigIntMode   | [BigIntMode](#bigintmode) | 是 |定义处理BigInt的模式。|

## JSON.parse

parse(text: string, reviver?: Transformer, options?: ParseOptions): Object | null

解析JSON字符串生成ArkTS对象或null。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型   | 必填 | 说明            |
| ------ | ------ | ---- | --------------- |
| text   | string | 是 | 有效的JSON字符串。|
| reviver  | [Transformer](#transformer) | 否 | 转换函数，传入该参数，可以用来修改解析生成的原始值。默认值是undefined。|
| options   | [ParseOptions](#parseoptions) | 否 | 解析的配置，传入该参数，可以用来控制解析生成的类型。默认值是undefined。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Object \| null | 返回ArkTS对象或null。当入参是null时，返回null。|

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |

**示例：**
<!--code_no_check-->
```ts
// /entry/src/main/ets/pages/test.ts
export function reviverFunc(key, value) {
  if (key === "age") {
    return value + 1;
  }
  return value;
}
```

<!--code_no_check-->
```ts
import { JSON } from '@kit.ArkTS';
import { reviverFunc } from './test';

let jsonText = '{"name": "John", "age": 30, "city": "ChongQing"}';
let obj = JSON.parse(jsonText);
console.info((obj as object)?.["name"]);
// 打印结果：John
const jsonTextStr = '{"name": "John", "age": 30}';
let objRst = JSON.parse(jsonTextStr, reviverFunc);
console.info((objRst as object)?.["age"]);
// 打印结果：31
let options: JSON.ParseOptions = {
  bigIntMode: JSON.BigIntMode.PARSE_AS_BIGINT,
}
let numberText = '{"largeNumber":112233445566778899}';
let numberObj = JSON.parse(numberText,(key: string, value: Object | undefined | null): Object | undefined | null => {
  if(key === "largeNumber") return value;
  return value;
},options) as Object;

console.info((numberObj as object)?.["largeNumber"]);
// 打印结果: 112233445566778899
```

```ts
import { JSON } from '@kit.ArkTS';

/*
 * 反序列化包含嵌套引号的JSON字符串场景
 * */

interface Info {
  name: string;
  age: number;
}

interface TestObj {
  info: Info;
}

interface TestStr {
  info: string;
}

// 该JSON字符串中存在嵌套引号的情况，破坏了JSON的结构，将无法正常反序列化。
// let jsonStr = `{"info": "{"name": "zhangsan", "age": 18}"}`;

// 以下提供两种方式解决该场景问题：
// 方法1：避免出现嵌套的操作，将原始JSON字符串的"{"name": "zhangsan", "age": 18}"转化为{"name": "zhangsan", "age": 18}。
let jsonStr = `{"info": {"name": "zhangsan", "age": 18}}`;
let obj1  = JSON.parse(jsonStr) as TestObj;
console.info(JSON.stringify(obj1)); //{"info":{"name":"zhangsan","age":18}}
// 获取JSON字符串中的name信息
console.info(obj1.info.name); // zhangsan

// 方法2：将JSON字符串中嵌套的引号进行双重转义，恢复JSON的正常结构。
jsonStr = `{"info": "{\\"name\\": \\"zhangsan\\", \\"age\\": 18}"}`;
let obj2 = JSON.parse(jsonStr) as TestStr;;
console.info(JSON.stringify(obj2)); // {"info":"{\"name\": \"zhangsan\", \"age\": 18}"}
// 获取JSON字符串中的name信息
let obj3 = JSON.parse(obj2.info) as Info;
console.info(obj3.name); // zhangsan
```

## JSON.stringify

stringify(value: Object, replacer?: (number | string)[] | null, space?: string | number): string

该方法将一个ArkTS对象或数组转换为JSON字符串，支持线性容器的转换，不支持非线性容器。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | ArkTS对象或数组。支持线性容器的转换，不支持非线性容器。|
| replacer | number[] \| string[] \| null | 否 | 当参数是数组时，只有包含在这个数组中的属性名才会被序列化到最终的JSON字符串中；当参数为null或者未提供时，则对象所有的属性都会被序列化。默认值是undefined。|
| space | string \| number | 否 | 指定缩进用的空格或字符串，用于美化输出。当参数是数字时表示缩进空格数；当参数是字符串时表示缩进字符；无参数则无缩进。默认值是空字符串。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 转换后的JSON字符串。|

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |

**示例：**
<!--code_no_check-->
```ts
// /entry/src/main/ets/pages/test.ts
export let exportObj = {1: "John", 2: 30, 3: "New York"};
```

<!--code_no_check-->
```ts
import { JSON } from '@kit.ArkTS';
import { exportObj } from './test';

let arr = [1, 2];
let rstArrStr = JSON.stringify(exportObj, arr);
console.info(rstArrStr);
// 打印结果："{"1":"John","2":30}"
interface Person {
  name: string;
  age: number;
  city: string;
}
let inputObj = {"name": "John", "age": 30, "city": "ChongQing"} as Person;
let rstStr = JSON.stringify(inputObj, ["name"]);
console.info(rstStr);
// 打印结果："{"name":"John"}"
let rstStrSpace = JSON.stringify(inputObj, ["name"], '  ');
console.info(rstStrSpace);
// 打印结果：
/*
"{
  "name": "John"
}"
*/
let rstStrStar = JSON.stringify(inputObj, ["name"], '&&');
console.info(rstStrStar);
// 打印结果：
/*
"{
&&"name": "John"
}"
*/
```


## JSON.stringify

stringify(value: Object, replacer?: Transformer, space?: string | number): string

该方法将一个ArkTS对象或数组转换为JSON字符串，支持线性容器的转换，不支持非线性容器。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | ArkTS对象或数组，支持线性容器的转换，不支持非线性容器。|
| replacer | [Transformer](#transformer) | 否 | 在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理。默认值是undefined。|
| space | string \| number | 否 | 指定缩进用的空格或字符串或空字符串，用于美化输出。当参数是数字时表示有多少个空格；当参数是字符串时，该字符串被当作空格；当参数没有提供时，将没有空格。默认值是空字符串。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 转换后的JSON字符串。|

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |

**示例：**
```ts
// /entry/src/main/ets/pages/test.ts
export function replacer(key: string, value: Object): Object {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value;
}
```

<!--code_no_check-->
```ts
import { JSON } from '@kit.ArkTS';
import { replacer } from './test';

interface Person {
  name: string;
  age: number;
  city: string;
}
let inputObj = {"name": "John", "age": 30, "city": "ChongQing"} as Person;
let rstStr= JSON.stringify(inputObj, replacer);
console.info(rstStr);
// 打印结果："{"name":"JOHN","age":30,"city":"CHONGQING"}"
let rstStrSpace= JSON.stringify(inputObj, replacer, '  ');
console.info(rstStrSpace);
// 打印结果：
/*
"{
  "name": "JOHN",
  "age": 30,
  "city": "CHONGQING"
}"
*/
let rstStrSymbol= JSON.stringify(inputObj, replacer, '@@@');
console.info(rstStrSymbol);
// 打印结果：
/*
"{
@@@"name": "JOHN",
@@@"age": 30,
@@@"city": "CHONGQING"
}"
*/
```

```ts
import { JSON } from '@kit.ArkTS';

/*
 * 序列化BigInt对象场景
 * */
let bigIntObject = BigInt(112233445566778899)

/*
 * 场景1：不使用自定义转换函数，直接序列化BigInt对象。
 * */
console.info(JSON.stringify(bigIntObject)); // 112233445566778896

/*
 * 场景2：使用自定义转换函数，需预处理BigInt对象进行序列化操作。
 * 2.1 自定义函数中直接返回BigInt对象会抛JSCrash
 * 2.2 使用自定义转换函数，将BigInt对象预处理为string对象进行处理。
 * */

// 2.1 错误序列化用法：自定义函数中直接返回BigInt对象
// JSON.stringify(bigIntObject, (key: string, value: Object): Object =>{ return value; });

// 2.2 正确序列化用法：自定义函数中将BigInt对象预处理为string对象
let result: string = JSON.stringify(bigIntObject, (key: string, value: Object): Object => {
  if (typeof value === 'bigint') {
    return value.toString();
  }
  return value;
});
console.info("result:", result); // result: "112233445566778896"
```

```ts
import { JSON } from '@kit.ArkTS';

/*
 * 序列化浮点数number场景
 * */
let floatNumber1 = 10.12345;
let floatNumber2 = 10.00;

// 序列化小数部分不为零的浮点数，可以正常序列化。
let result1 = JSON.stringify(floatNumber1);
console.info(result1); // 10.12345

// 序列化小数部分为零的浮点数，为保持数值的简洁表示，会丢失小数部分的精度。
let result11 = JSON.stringify(floatNumber2);
console.info(result11); // 10

// 以下是防止浮点数精度丢失的方法：
let result2 = JSON.stringify(floatNumber2, (key: string, value: Object): Object => {
  if (typeof value === 'number') {
    // 需要按照业务场景需要，定制所需要的固定精度。
    return value.toFixed(2);
  }
  return value;
});
console.info(result2); // "10.00"
```

## JSON.has

has(obj: object, property: string): boolean

检查ArkTS对象是否包含某种属性，可用于[JSON.parse](#jsonparse)解析JSON字符串之后的相关操作。has接口仅支持最外层为字典形式（即大括号而非中括号包围）的合法json串。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| obj | object | 是 | ArkTS对象。|
| property | string | 是 | 属性名。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 返回ArkTS对象是否包含某种属性结果。true表示包含，false表示不包含。|

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |

**示例：**

```ts
import { JSON } from '@kit.ArkTS';

const jsonText = '{"name": "John", "age": 30, "city": "ChongQing"}';
let inputObj = JSON.parse(jsonText);
let result = JSON.has(inputObj, "name");
console.info("result = " + result);
// 打印结果：result = true
```


## JSON.remove

remove(obj: object, property: string): void

从ArkTS对象中删除某种属性，可用于[JSON.parse](#jsonparse)解析JSON字符串之后的相关操作。remove接口仅支持最外层为字典形式（即大括号而非中括号包围）的合法json串。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| obj | object | 是 | ArkTS对象。|
| property | string | 是 | 属性名。|

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |

**示例：**

```ts
import { JSON } from '@kit.ArkTS';

const jsonText = '{"name": "John", "age": 30, "city": "ChongQing"}';
let inputObj = JSON.parse(jsonText);
JSON.remove(inputObj, "name");
let result = JSON.has(inputObj, "name");
console.info("result = " + result);
// 打印结果：result = false
```