# @ohos.util (util工具函数)

该模块主要提供常用的工具函数，实现字符串编解码（[TextEncoder](#textencoder)，[TextDecoder](#textdecoder)）、有理数运算（[RationalNumber<sup>8+</sup>](#rationalnumber8)）、缓冲区管理（[LRUCache<sup>9+</sup>](#lrucache9)）、范围判断（[ScopeHelper<sup>9+</sup>](#scopehelper9)）、Base64编解码（[Base64Helper<sup>9+</sup>](#base64helper9)）、内置对象类型检查（[types<sup>8+</sup>](#types8)、对方法进行插桩和替换（[Aspect<sup>11+</sup>](#aspect11)）等功能。

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import util from '@ohos.util';
```
## util.format<sup>9+</sup>

format(format: string,  ...args: Object[]): string

通过式样化字符串对输入的内容按特定格式输出。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名  | 类型     | 必填 | 说明           |
| ------- | -------- | ---- | -------------- |
| format  | string   | 是   | 格式化字符串，可以包含零个或多个占位符，用于指定要插入的参数的位置和格式。 |
| ...args | Object[] | 否   | 替换format参数中占位符的数据，此参数缺失时，默认返回第一个参数。|

**返回值：**

| 类型   | 说明              |
| ------ | -----------------|
| string | 格式化后的字符串。 |


**格式说明符：**

| 格式说明符 | 说明                          |
| ------ | -------------------------------- |
| %s     | 将参数转换为字符串，用于除Object，BigInt和-0之外的所有值。|
| %d     | 将参数作为十进制整数进行格式化输出，用于除Symbol和BigInt之外的所有值。|
| %i     | 将字符串转换为十进制整数，用于除BigInt和Symbol之外的所有值。|
| %f     | 将字符串转换为浮点数，用于除Bigint和Symbol之外的所有值。|
| %j     | 将JavaScript对象转换为JSON字符串进行格式化输出。|
| %o     | 用于将JavaScript对象进行格式化输出，将对象转换为字符串表示，但不包含对象的原型链信息。|
| %O     | 用于将JavaScript对象进行格式化输出，将对象转换为字符串表示。|
| %c     | 只在浏览器环境中有效。其余环境不会产生样式效果。|
| %%     | 转义百分号的特殊格式化占位符。|

**示例：**

```ts
import util from '@ohos.util';

interface utilAddresstype {
  city: string;
  country: string;
}
interface utilPersontype {
  name: string;
  age: number;
  address: utilAddresstype;
}

let name = 'John';
let age = 20;
let formattedString = util.format('My name is %s and I am %s years old', name, age);
console.info(formattedString);
// 输出结果：My name is John and I am 20 years old
let num = 10.5;
formattedString = util.format('The number is %d', num);
console.info(formattedString);
// 输出结果：The number is 10.5
num = 100.5;
formattedString = util.format('The number is %i', num);
console.info(formattedString);
// 输出结果：The number is 100
const pi = 3.141592653;
formattedString = util.format('The value of pi is %f', pi);
console.info(formattedString);
// 输出结果：The value of pi is 3.141592653
const obj: Record<string,number | string> = { "name": 'John', "age": 20 };
formattedString = util.format('The object is %j', obj);
console.info(formattedString);
// 输出结果：The object is {"name":"John","age":20}
const person: utilPersontype = {
  name: 'John',
  age: 20,
  address: {
    city: 'New York',
    country: 'USA'
  }
};
console.info(util.format('Formatted object using %%O: %O', person));
console.info(util.format('Formatted object using %%o: %o', person));
/*
输出结果：
Formatted object using %O: { name: 'John',
  age: 20,
  address:
  { city: 'New York',
    country: 'USA' } }
Formatted object using %o: { name: 'John',
  age: 20,
  address:
  { city: 'New York',
    country: 'USA' } }
*/
const percentage = 80;
let arg = 'homework';
formattedString = util.format('John finished %d%% of the %s', percentage, arg);
console.info(formattedString);
// 输出结果：John finished 80% of the homework
```

## util.errnoToString<sup>9+</sup>

errnoToString(errno: number): string

获取系统错误码对应的详细信息。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型   | 必填 | 说明                       |
| ------ | ------ | ---- | -------------------------- |
| errno  | number | 是   | 系统发生错误产生的错误码。 |

**返回值：**

| 类型   | 说明                   |
| ------ | ---------------------- |
| string | 错误码对应的详细信息。 |

**示例：**

```ts
let errnum = -1; // -1 : a system error number
let result = util.errnoToString(errnum);
console.info("result = " + result);
```

**部分错误码及信息示例：**

| 错误码 | 信息                              |
| ------ | -------------------------------- |
| -1     | operation not permitted          |
| -2     | no such file or directory        |
| -3     | no such process                  |
| -4     | interrupted system call          |
| -5     | i/o error                        |
| -11    | resource temporarily unavailable |
| -12    | not enough memory                |
| -13    | permission denied                |
| -100   | network is down                  |

## util.callbackWrapper

callbackWrapper(original: Function): (err: Object, value: Object )=&gt;void

对异步函数进行回调化处理，回调中第一个参数将是拒绝原因（如果 Promise 已解决，则为 null），第二个参数将是已解决的值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| original | Function | 是 | 异步函数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Function | 返回一个回调函数，该函数第一个参数err是拒绝原因（如果&nbsp;Promise&nbsp;已解决，则为&nbsp;null），第二个参数value是已解决的值。 |

**示例：**

```ts
async function fn() {
  return 'hello world';
}
let cb = util.callbackWrapper(fn);
cb(1, (err : Object, ret : string) => {
  if (err) throw new Error;
  console.info(ret);
});
```

## util.promisify<sup>9+</sup>

promisify(original: (err: Object, value: Object) =&gt; void): Function

对异步函数处理并返回一个promise的函数。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| original | Function | 是 | 回调函数中第一个参数err是拒绝原因（如果&nbsp;Promise&nbsp;已解决，则为&nbsp;null），第二个参数value是已解决的值。  |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Function | 返回一个&nbsp;Promise&nbsp;的函数。 |

**示例：**

```ts
async function fn() {
  return 'hello world';
}
const addCall = util.promisify(util.callbackWrapper(fn));
(async () => {
  try {
    let res: string = await addCall();
    console.info(res);
  } catch (err) {
    console.info(err);
  }
})();
```

## util.generateRandomUUID<sup>9+</sup>

generateRandomUUID(entropyCache?: boolean): string

使用加密安全随机数生成器生成随机的RFC 4122版本4的string类型UUID。调用此函数会生成两个UUID，其中一个UUID进行缓存，一个UUID用于输出，首次调用时，参数是true或false无区别；下次调用时，如果参数是true，依旧缓存上次UUID，并生成新的UUID；如果参数是false，将生成两个UUID，其中一个UUID进行缓存，一个UUID进行输出。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| entropyCache | boolean | 否 | 是否使用已缓存的UUID， 默认true。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 表示此UUID的字符串。 |

**示例：**

```ts
let uuid = util.generateRandomUUID(true);
console.info("RFC 4122 Version 4 UUID:" + uuid);
// 输出随机生成的UUID
```

## util.generateRandomBinaryUUID<sup>9+</sup>

generateRandomBinaryUUID(entropyCache?: boolean): Uint8Array

使用加密安全随机数生成器生成随机的RFC 4122版本4的Uint8Array类型UUID。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| entropyCache | boolean | 否 | 是否使用已缓存的UUID， 默认true。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 表示此UUID的Uint8Array值。 |

**示例：**

```ts
let uuid = util.generateRandomBinaryUUID(true);
console.info(JSON.stringify(uuid));
// 输出：
// 138,188,43,243,62,254,70,119,130,20,235,222,199,164,140,150
```

## util.parseUUID<sup>9+</sup>

parseUUID(uuid: string): Uint8Array

将generateRandomUUID生成的string类型UUID转换为generateRandomBinaryUUID生成的Uint8Array类型UUID，如RFC 4122版本4中所述。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| uuid | string | 是 | UUID字符串。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回表示此UUID的Uint8Array，如果解析失败，则抛出SyntaxError。 |

**示例：**

```ts
let uuid = util.parseUUID("84bdf796-66cc-4655-9b89-d6218d100f9c");
console.info(JSON.stringify(uuid));
// 输出：
// 132,189,247,150,102,204,70,85,155,137,214,33,141,16,15,156
```

## util.printf<sup>(deprecated)</sup>

printf(format: string,  ...args: Object[]): string

通过式样化字符串对输入的内容按特定格式输出。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃，建议使用[util.format<sup>9+</sup>](#utilformat9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| format | string | 是 | 式样化字符串。 |
| ...args | Object[] | 否 | 替换式样化字符串通配符的数据，此参数缺失时，默认返回第一个参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 按特定格式式样化后的字符串。 |

**示例：**

```ts
let res = util.printf("%s", "hello world!");
console.info(res);
```


## util.getErrorString<sup>(deprecated)</sup>

getErrorString(errno: number): string

获取系统错误码对应的详细信息。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃，建议使用[util.errnoToString<sup>9+</sup>](#utilerrnotostring9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| errno | number | 是 | 系统发生错误产生的错误码。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 错误码对应的详细信息。 |

**示例：**

```ts
let errnum = -1; // -1 : a system error number
let result = util.getErrorString(errnum);
console.info("result = " + result);
```

## util.promiseWrapper<sup>(deprecated)</sup>

promiseWrapper(original: (err: Object, value: Object) =&gt; void): Object

对异步函数处理并返回一个promise的版本。

> **说明：**
>
> 此接口不可用，建议使用[util.promisify<sup>9+</sup>](#utilpromisify9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| original | Function | 是 | 异步函数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Function | 采用遵循常见的错误优先的回调风格的函数（也就是将&nbsp;(err,&nbsp;value)&nbsp;=&gt;&nbsp;...&nbsp;回调作为最后一个参数），并返回一个返回&nbsp;promise&nbsp;的版本。 |


## TextDecoderOptions<sup>11+</sup>

**系统能力：** SystemCapability.Utils.Lang

解码相关选项参数，存在两个属性fatal和ignoreBOM。

| 名称      | 类型 | 必填 | 说明               |
| --------- | -------- | ---- | ------------------ |
| fatal     | boolean  | 否   | 是否显示致命错误，默认值是false。 |
| ignoreBOM | boolean  | 否   | 是否忽略BOM标记，默认值是false。  |


## DecodeWithStreamOptions<sup>11+</sup>

**系统能力：** SystemCapability.Utils.Lang

解码是否跟随附加数据块相关选项参数。

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| stream | boolean | 否 | 在随后的decodeWithStream()调用中是否跟随附加数据块。如果以块的形式处理数据，则设置为true；如果处理最后的数据块或数据未分块，则设置为false。默认为false。 |


## Aspect<sup>11+</sup>

Aspect类用于封装提供切面能力（Aspect Oriented Programming，简写AOP）的接口，这些接口可以用来对类方法进行前后插桩或者替换实现。

### addBefore<sup>11+</sup>

static addBefore(targetClass: Object, methodName: string, isStatic: boolean, before: Function): void

在指定的类对象的原方法执行前插入一个函数。addBefore接口执行完成后，都会先执行插入的函数逻辑，再执行指定类对象的原方法。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名    | 类型    | 必填 | 说明                                   |
| -------- | ------- | ---- | -------------------------------------|
| targetClass  | Object   | 是   | 指定的类对象。                    |
| methodName   | string   | 是   | 指定的方法名。                    |
| isStatic     | boolean  | 是   | 指定的原方法是否为静态方法，true表示静态方法，false表示实例方法。      |
| before       | Function | 是   | 要插入的函数对象。函数有参数，则第一个参数是this对象（若isStatic为true，则为类对象即targetClass；若isStatic为false，则为调用方法的实例对象），其余参数是原方法的参数。函数也可以无参数，无参时不做处理。 |

**示例：**

```ts
class MyClass {
  msg: string = 'msg000';
  foo(arg: string): string {
    console.info('foo arg is ' + arg);
    return this.msg;
  }

  static data: string = 'data000';
  static bar(arg: string): string {
    console.info('bar arg is ' + arg);
	return MyClass.data;
  }
}

let asp = new MyClass();
let result = asp.foo('123');
// 输出结果：foo arg is 123
console.info('result is ' + result);
// 输出结果：result is msg000
console.info('asp.msg is ' + asp.msg);
// 输出结果：asp.msg is msg000

util.Aspect.addBefore(MyClass, 'foo', false, (instance: MyClass, arg: string) => {
  console.info('arg is ' + arg);
  instance.msg = 'msg111';
  console.info('msg is changed to ' + instance.msg)
});

result = asp.foo('123');
// 输出结果：arg is 123
// 输出结果：msg is changed to msg111
// 输出结果：foo arg is 123
console.info('result is ' + result);
// 输出结果：result is msg111
console.info('asp.msg is ' + asp.msg);
// 输出结果：asp.msg is msg111


let res = MyClass.bar('456');
// 输出结果：bar arg is 456
console.info('res is ' + res);
// 输出结果：res is data000
console.info('MyClass.data is ' + MyClass.data);
// 输出结果：MyClass.data is data000

util.Aspect.addBefore(MyClass, 'bar', true, (target: Object, arg: string) => {
  console.info('arg is ' + arg);
  let newVal = 'data111';
  Reflect.set(target, 'data', newVal);
  console.info('data is changed to ' + newVal);
});

res = MyClass.bar('456');
// 输出结果：arg is 456
// 输出结果：data is changed to data111
// 输出结果：bar arg is 456
console.info('res is ' + res);
// 输出结果：res is data111
console.info('MyClass.data is ' + MyClass.data);
// 输出结果：MyClass.data is data111
```

### addAfter<sup>11+</sup>

static addAfter(targetClass: Object, methodName: string, isStatic: boolean, after: Function): void

在指定的类方法执行后插入一段逻辑。最终返回值是插入函数执行后的返回值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名    | 类型    | 必填 | 说明                                   |
| -------- | ------- | ---- | -------------------------------------|
| targetClass  | Object   | 是   | 指定的类对象。                    |
| methodName   | string   | 是   | 指定的原方法名。                   |
| isStatic     | boolean  | 是   | 指定的原方法是否为静态方法，true表示静态方法，false表示实例方法。      |
| after        | Function | 是   | 要插入的函数。函数有参数时，则第一个参数是this对象（若isStatic为true，则为类对象即targetClass；若isStatic为false，则为调用方法的实例对象），第二个参数是原方法的返回值（如果原方法没有返回值，则为undefined），其余参数是原方法的参数。函数也可以无参，无参时不做处理。  |

**示例：**

```ts
class MyClass {
  msg: string = 'msg000';
  foo(arg: string): string {
    console.info('foo arg is ' + arg);
    return this.msg;
  }
}

let asp = new MyClass();
let result = asp.foo('123');
// 输出结果：foo arg is 123
console.info('result is ' + result);
// 输出结果：result is msg000
console.info('asp.msg is ' + asp.msg);
// 输出结果：asp.msg is msg000

util.Aspect.addAfter(MyClass, 'foo', false, (instance: MyClass, ret: string, arg: string): string => {
  console.info('arg is ' + arg);
  console.info('ret is ' + ret);
  instance.msg = 'msg111';
  console.info('msg is changed to ' + instance.msg);
  return 'msg222';
});

result = asp.foo('123');
// 输出结果：foo arg is 123
// 输出结果：arg is 123
// 输出结果：ret is msg000
// 输出结果：msg is changed to msg111
console.info('result is ' + result);
// 输出结果：result is msg222
console.info('asp.msg is ' + asp.msg);
// 输出结果：asp.msg is msg111

// 前后插桩的例子
class AroundTest {
  foo(arg: string) {
    console.info('execute foo with arg ' + arg);
  }
}
util.Aspect.addBefore(AroundTest, 'foo', false, () => {
  console.info('execute before');
});
util.Aspect.addAfter(AroundTest, 'foo', false, () => {
  console.info('execute after');
});

(new AroundTest()).foo('hello');
// 输出结果：execute before
// 输出结果：execute foo with arg hello
// 输出结果：execute after
```

### replace<sup>11+</sup>

static replace(targetClass: Object, methodName: string, isStatic: boolean, instead: Function) : void

将指定的类方法的原方法替换为另一个函数。replace接口执行完成后，调用指定的类方法时，只会执行替换后的逻辑。最终返回值为替换函数执行完毕的返回值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名    | 类型    | 必填 | 说明                                   |
| -------- | ------- | ---- | -------------------------------------|
| targetClass  | Object   | 是   | 指定的类对象。                    |
| methodName   | string   | 是   | 指定的原方法名。                  |
| isStatic     | boolean  | 是   | 指定的原方法是否为静态方法，true表示静态方法，false表示实例方法。       |
| instead      | Function | 是   | 要用来替换原方法的函数。函数有参数时，则第一个参数是this对象（若isStatic为true，则为类对象即targetClass；若isStatic为false，则为调用方法的实例对象），其余参数是原方法的参数。函数也可以无参，无参时不做处理。   |

**示例：**

```ts
class MyClass {
  msg: string = 'msg000';
  foo(arg: string): string {
    console.info('foo arg is ' + arg);
    return this.msg;
  }
}

let asp = new MyClass();
let result = asp.foo('123');
// 输出结果：foo arg is 123
console.info('result is ' + result);
// 输出结果：result is msg000
console.info('asp.msg is ' + asp.msg);
// 输出结果：asp.msg is msg000

util.Aspect.replace(MyClass, 'foo', false, (instance: MyClass, arg: string): string => {
  console.info('execute instead')
  console.info('arg is ' + arg);
  instance.msg = 'msg111';
  console.info('msg is changed to ' + instance.msg);
  return 'msg222';
});

result = asp.foo('123');
// 输出结果：execute instead
// 输出结果：arg is 123
// 输出结果：msg is changed to msg111
console.info('result is ' + result);
// 输出结果：result is msg222
console.info('asp.msg is ' + asp.msg);
// 输出结果：asp.msg is msg111
```

## TextDecoder

TextDecoder用于将字节数组解码为字符串，可以处理多种编码格式，包括utf-8、utf-16le/be、iso-8859和windows-1251等不同的编码格式。

### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Utils.Lang。

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| encoding | string | 是 | 否 | 编码格式。<br/>-&nbsp;支持格式：utf-8、ibm866、iso-8859-2、iso-8859-3、iso-8859-4、iso-8859-5、iso-8859-6、iso-8859-7、iso-8859-8、iso-8859-8-i、iso-8859-10、iso-8859-13、iso-8859-14、iso-8859-15、koi8-r、koi8-u、macintosh、windows-874、windows-1250、windows-1251、windows-1252、windows-1253、windows-1254、windows-1255、windows-1256、windows-1257、windows-1258、x-mac-cyrillic、gbk、gb18030、big5、euc-jp、iso-2022-jp、shift_jis、euc-kr、utf-16be、utf-16le。 |
| fatal | boolean | 是 | 否 | 是否显示致命错误。 |
| ignoreBOM | boolean | 是 | 否 | 是否忽略BOM（byte&nbsp;order&nbsp;marker）标记，默认值为false&nbsp;，表示解码结果包含BOM标记。 |

### constructor<sup>9+</sup>

constructor()

TextDecoder的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

```ts
let result = new util.TextDecoder();
let retStr = result.encoding;
```
### create<sup>9+</sup>

static create(encoding?: string, options?: TextDecoderOptions): TextDecoder

替代有参构造功能。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型   | 必填 | 说明                                             |
| -------- | ------ | ---- | ------------------------------------------------ |
| encoding | string | 否   | 编码格式，默认值是'utf-8'。                      |
| options  | [TextDecoderOptions](#textdecoderoptions11) | 否   | 解码相关选项参数，存在两个属性fatal和ignoreBOM。|

**示例：**

```ts
let textDecoderOptions: util.TextDecoderOptions = {
  fatal: false,
  ignoreBOM : true
}
let result = util.TextDecoder.create('utf-8', textDecoderOptions)
let retStr = result.encoding
```

### decodeWithStream<sup>9+</sup>

decodeWithStream(input: Uint8Array, options?: DecodeWithStreamOptions): string

通过输入参数解码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| input | Uint8Array | 是 | 符合格式需要解码的数组。 |
| options | [DecodeWithStreamOptions](#decodewithstreamoptions11) | 否 | 解码相关选项参数。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 解码后的数据。 |

**示例：**

```ts
let textDecoderOptions: util.TextDecoderOptions = {
  fatal: false,
  ignoreBOM : true
}
let decodeWithStreamOptions: util.DecodeWithStreamOptions = {
  stream: false
}
let textDecoder = util.TextDecoder.create('utf-8', textDecoderOptions);
let result = new Uint8Array(6);
result[0] = 0xEF;
result[1] = 0xBB;
result[2] = 0xBF;
result[3] = 0x61;
result[4] = 0x62;
result[5] = 0x63;
console.info("input num:");
let retStr = textDecoder.decodeWithStream(result , decodeWithStreamOptions);
console.info("retStr = " + retStr);
```

### constructor<sup>(deprecated)</sup>

constructor(encoding?: string, options?: { fatal?: boolean; ignoreBOM?: boolean })

TextDecoder的构造函数。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃，建议使用[create<sup>9+</sup>](#create9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| encoding | string | 否 | 编码格式，默认值是'utf-8'。 |
| options | object | 否 | 解码相关选项参数，存在两个属性fatal和ignoreBOM。 |

  **表1** options

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| fatal | boolean | 否 | 是否显示致命错误，默认值是false。 |
| ignoreBOM | boolean | 否 | 是否忽略BOM标记，默认值是false。 |

**示例：**

```ts
let textDecoder = new util.TextDecoder("utf-8",{ignoreBOM: true});
```

### decode<sup>(deprecated)</sup>

decode(input: Uint8Array, options?: { stream?: false }): string

通过输入参数解码后输出对应文本。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃，建议使用[decodeWithStream<sup>9+</sup>](#decodewithstream9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| input | Uint8Array | 是 | 符合格式需要解码的数组。 |
| options | object | 否 | 解码相关选项参数。 |

**表2** options

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| stream | boolean | 否 | 在随后的decode()调用中是否跟随附加数据块。如果以块的形式处理数据，则设置为true；如果处理最后的数据块或数据未分块，则设置为false。默认为false。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 解码后的数据。 |

**示例：**

```ts
let textDecoder = new util.TextDecoder("utf-8",{ignoreBOM: true});
let result = new Uint8Array(6);
result[0] = 0xEF;
result[1] = 0xBB;
result[2] = 0xBF;
result[3] = 0x61;
result[4] = 0x62;
result[5] = 0x63;
console.info("input num:");
let retStr = textDecoder.decode( result , {stream: false});
console.info("retStr = " + retStr);
```

## EncodeIntoUint8ArrayInfo<sup>11+</sup>

**系统能力：** SystemCapability.Utils.Lang

编码后的文本。

| 名称      | 类型 | 可读  |可写  | 说明               |
| --------- | -------- | -------- |-------- |------------------ |
| read     | number  | 是 | 否 |表示已读取的字符数。 |
| written | number   | 是 |否 |表示已写入的字节数。  |


## TextEncoder

TextEncoder用于将字符串编码为字节数组，支持多种编码格式。
需要注意的是，在使用TextEncoder进行编码时，不同编码格式下字符所占的字节数是不同的，在使用TextEncoder时需要明确指定要使用的编码格式，以确保编码结果正确。

### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Utils.Lang。

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| encoding | string | 是 | 否 | 编码格式，默认值是'utf-8'。 |


### constructor

constructor()

TextEncoder的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

```ts
let textEncoder = new util.TextEncoder();
```

### constructor<sup>9+</sup>

constructor(encoding?: string)

TextEncoder的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ----- | ---- | ---- | ---- |
| encoding | string | 否 | 编码格式，默认值为'utf-8'。 |

**示例：**

```ts
let textEncoder = new util.TextEncoder("utf-8");
```

### encodeInto<sup>9+</sup>

encodeInto(input?: string): Uint8Array

通过输入参数编码后输出Uint8Array对象。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| input  | string | 否   | 需要编码的字符串，默认值是空字符串。 |

**返回值：**

| 类型       | 说明               |
| ---------- | ------------------ |
| Uint8Array | 返回编码后的Uint8Array对象。 |

**示例：**

```ts
let textEncoder = new util.TextEncoder();
let buffer = new ArrayBuffer(20);
let result = new Uint8Array(buffer);
result = textEncoder.encodeInto("\uD800¥¥");
```

### encodeIntoUint8Array<sup>9+</sup>

encodeIntoUint8Array(input: string, dest: Uint8Array): EncodeIntoUint8ArrayInfo

对字符串进行编码，将结果写入dest数组。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型       | 必填 | 说明                                                    |
| ------ | ---------- | ---- | ------------------------------------------------------- |
| input  | string     | 是   | 需要编码的字符串。                                      |
| dest   | Uint8Array | 是   | Uint8Array对象实例，用于将生成的UTF-8编码文本放入其中。 |

**返回值：**

| 类型       | 说明               |
| ---------- | ------------------ |
| [EncodeIntoUint8ArrayInfo](#encodeintouint8arrayinfo11) | 返回一个对象，read表示已编码的字符数，write表示编码字符所占用的字节数。 |

**示例：**

```ts
let that = new util.TextEncoder();
let buffer = new ArrayBuffer(4);
let dest = new Uint8Array(buffer);
let result = new Object();
result = that.encodeIntoUint8Array('abcd', dest);
```

### encodeInto<sup>(deprecated)</sup>

encodeInto(input: string, dest: Uint8Array): { read: number; written: number }

放置生成的UTF-8编码文本。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃，建议使用[encodeIntoUint8Array<sup>9+</sup>](#encodeintouint8array9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| input | string | 是 | 需要编码的字符串。 |
| dest | Uint8Array | 是 | Uint8Array对象实例，用于将生成的UTF-8编码文本放入其中。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回编码后的文本。 |

**示例：**

```ts
let that = new util.TextEncoder();
let buffer = new ArrayBuffer(4);
let dest = new Uint8Array(buffer);
let result = new Object();
result = that.encodeInto('abcd', dest);
```

### encode<sup>(deprecated)</sup>

encode(input?: string): Uint8Array

通过输入参数编码后输出对应文本。

> **说明：**
>
> 从API version 7开始支持，从API version 9开始废弃，建议使用[encodeInto<sup>9+</sup>](#encodeinto9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| input | string | 否 | 需要编码的字符串，默认值是空字符串。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回编码后的文本。 |

**示例：**

```ts
let textEncoder = new util.TextEncoder();
let buffer = new ArrayBuffer(20);
let result = new Uint8Array(buffer);
result = textEncoder.encode("\uD800¥¥");
```

## RationalNumber<sup>8+</sup>

RationalNumber主要是对有理数进行比较，获取分子分母等方法。例如使用toString()方法可以将有理数转换为字符串形式，使用该类可以方便地进行有理数的各种操作。

### constructor<sup>9+</sup>

constructor()

RationalNumber的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

```ts
let rationalNumber = new util.RationalNumber();
```

### parseRationalNumber<sup>9+</sup>

parseRationalNumber(numerator: number,denominator: number): RationalNumber

用于创建具有给定分子和分母的RationalNumber实例。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名      | 类型   | 必填 | 说明             |
| ----------- | ------ | ---- | ---------------- |
| numerator   | number | 是   | 分子，整数类型。 |
| denominator | number | 是   | 分母，整数类型。 |

**示例：**

```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2);
```

### createRationalFromString<sup>8+</sup>

static createRationalFromString​(rationalString: string): RationalNumber​

基于给定的字符串创建一个RationalNumber对象。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| rationalString | string | 是 | 字符串格式。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Object | 返回RationalNumber对象。 |

**示例：**

```ts
let rational = util.RationalNumber.createRationalFromString("3/4");
```

### compare<sup>9+</sup>

compare​(another: RationalNumber): number​

将当前RationalNumber对象与目标RationalNumber对象进行比较，并返回比较结果。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名  | 类型           | 必填 | 说明               |
| ------- | -------------- | ---- | ------------------ |
| another | [RationalNumber](#rationalnumber8) | 是   | 其他的有理数对象。 |

**返回值：**

| 类型   | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| number | 如果两个对象相等，则返回0；如果给定对象小于当前对象，则返回1；如果给定对象大于当前对象，则返回-1。 |

**示例：**

```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2);
let rational = util.RationalNumber.createRationalFromString("3/4");
let result = rationalNumber.compare(rational);
console.info("result = " + result);
// 输出结果：result = -1
```

### valueOf<sup>8+</sup>

valueOf(): number

以整数形式或者浮点数的形式获取当前RationalNumber对象的值。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回整数或者浮点数的值。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.valueOf();
console.info("result = " + result);
// 输出结果：result = 0.5
```
API 9及以上建议使用以下写法：
```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2);
let result = rationalNumber.valueOf();
console.info("result = " + result);
// 输出结果：result = 0.5
```

### equals<sup>8+</sup>

equals​(obj: Object): boolean

将当前的RationalNumber对象与给定的对象进行比较是否相等。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| obj | Object | 是 | 其他类型对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果给定对象与当前对象相同，则返回true；否则返回false。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let rational = util.RationalNumber.createRationalFromString("3/4");
let result = rationalNumber.equals(rational);
console.info("result = " + result);
// 输出结果：result = false
```
API 9及以上建议使用以下写法：
```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2);
let rational = util.RationalNumber.createRationalFromString("3/4");
let result = rationalNumber.equals(rational);
console.info("result = " + result);
// 输出结果：result = false
```

### getCommonFactor<sup>9+</sup>

getCommonFactor(number1: number,number2: number): number

获取两个指定整数的最大公约数。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名  | 类型   | 必填 | 说明       |
| ------- | ------ | ---- | ---------- |
| number1 | number | 是   | 整数类型。 |
| number2 | number | 是   | 整数类型。 |

**返回值：**

| 类型   | 说明                           |
| ------ | ------------------------------ |
| number | 返回两个给定数字的最大公约数。 |

**示例：**

```ts
let result = util.RationalNumber.getCommonFactor(4,6);
console.info("result = " + result);
// 输出结果：result = 2
```

### getNumerator<sup>8+</sup>

getNumerator​(): number

获取当前RationalNumber对象的分子。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回RationalNumber对象的分子的值。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.getNumerator();
console.info("result = " + result);
// 输出结果：result = 1
```
API 9及以上建议使用以下写法：
```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2);
let result = rationalNumber.getNumerator();
console.info("result = " + result);
// 输出结果：result = 1
```

### getDenominator<sup>8+</sup>

getDenominator​(): number

获取当前RationalNumber对象的分母。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回RationalNumber对象的分母的值。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.getDenominator();
console.info("result = " + result);
// 输出结果：result = 2
```
API 9及以上建议使用以下写法：
```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2)
let result = rationalNumber.getDenominator();
console.info("result = " + result);
// 输出结果：result = 2
```

### isZero<sup>8+</sup>

isZero​():boolean

检查当前RationalNumber对象是否为0。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果当前对象表示的值为0，则返回true；否则返回false。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.isZero();
console.info("result = " + result);
// 输出结果：result = false
```
API 9及以上建议使用以下写法：
```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2);
let result = rationalNumber.isZero();
console.info("result = " + result);
// 输出结果：result = false
```

### isNaN<sup>8+</sup>

isNaN​(): boolean

检查当前RationalNumber对象是否表示非数字(NaN)值。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果分母和分子都为0，则返回true；否则返回false。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.isNaN();
console.info("result = " + result);
// 输出结果：result = false
```
API 9及以上建议使用以下写法：
```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2);
let result = rationalNumber.isNaN();
console.info("result = " + result);
// 输出结果：result = false
```

### isFinite<sup>8+</sup>

isFinite​():boolean

检查当前RationalNumber对象是否表示一个有限值。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果分母不为0，则返回true；否则返回false。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.isFinite();
console.info("result = " + result);
// 输出结果：result = true
```
API 9及以上建议使用以下写法：
```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2);
let result = rationalNumber.isFinite();
console.info("result = " + result);
// 输出结果：result = true
```

### toString<sup>8+</sup>

toString​(): string

获取当前RationalNumber对象的字符串表示形式。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 返回Numerator/Denominator格式的字符串，例如3/5，如果当前对象的分子为0，则返回0/1。如果当前对象的分母为0，则返回Infinity。如果当前对象的分子和分母都为0，则返回NaN。|

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.toString();
console.info("result = " + result);
// 输出结果：result = 1/2
```
API 9及以上建议使用以下写法：
```ts
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2);
let result = rationalNumber.toString();
console.info("result = " + result);
// 输出结果：result = 1/2
```

### constructor<sup>(deprecated)</sup>

constructor(numerator: number,denominator: number)

RationalNumber的构造函数。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[parserationalnumber<sup>9+</sup>](#parserationalnumber9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| numerator | number | 是 | 分子，整数类型。 |
| denominator | number | 是 | 分母，整数类型。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
```

### compareTo<sup>(deprecated)</sup>

compareTo​(another: RationalNumber): number​

将当前的RationalNumber对象与给定的对象进行比较。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[compare<sup>9+</sup>](#compare9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| another | RationalNumber | 是 | 其他的有理数对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 如果两个对象相等，则返回0；如果给定对象小于当前对象，则返回1；如果给定对象大于当前对象，则返回-1。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let rational = util.RationalNumber.createRationalFromString("3/4");
let result = rationalNumber.compareTo(rational);
```

### getCommonDivisor<sup>(deprecated)</sup>

static getCommonDivisor​(number1: number,number2: number): number

获取两个指定整数的最大公约数。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[getCommonFactor<sup>9+</sup>](#getcommonfactor9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| number1 | number | 是 | 整数类型。 |
| number2 | number | 是 | 整数类型。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回两个给定数字的最大公约数。 |

**示例：**

```ts
let rationalNumber = new util.RationalNumber(1,2);
let result = util.RationalNumber.getCommonDivisor(4,6);
```

## LRUCache<sup>9+</sup>

LRUCache用于在缓存空间不够的时候，将近期最少使用的数据替换为新数据。此设计基于资源访问的考虑：近期访问的数据，可能在不久的将来会再次访问。于是最少访问的数据就是价值最小的数据，是最应该踢出缓存空间的数据。

### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Utils.Lang。

| 名称   | 类型   | 可读 | 可写 | 说明                   |
| ------ | ------ | ---- | ---- | ---------------------- |
| length | number | 是   | 否   | 当前缓冲区中值的总数。 |

**示例：**

```ts
let  pro : util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
pro.put(1,8);
let result = pro.length;
```

### constructor<sup>9+</sup>

constructor(capacity?: number)

默认构造函数用于创建一个新的LruBuffer实例，默认容量为64。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型   | 必填 | 说明                         |
| -------- | ------ | ---- | ---------------------------- |
| capacity | number | 否   | 指示要为缓冲区自定义的容量，默认值为64。 |

**示例：**

```ts
let lrubuffer : util.LRUCache<number, number> = new util.LRUCache();
```


### updateCapacity<sup>9+</sup>

updateCapacity(newCapacity: number): void

将缓冲区容量更新为指定容量，如果newCapacity小于或等于0，则抛出异常。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名      | 类型   | 必填 | 说明                         |
| ----------- | ------ | ---- | ---------------------------- |
| newCapacity | number | 是   | 指示要为缓冲区自定义的容量。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.updateCapacity(100);
```

### toString<sup>9+</sup>

toString(): string

返回对象的字符串表示形式。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型   | 说明                       |
| ------ | -------------------------- |
| string | 返回对象的字符串表示形式。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
pro.get(2);
pro.get(3);
console.info(pro.toString());
// 输出结果：LRUCache[ maxSize = 64, hits = 1, misses = 1, hitRate = 50% ]
// maxSize: 缓存区最大值 hits: 查询值匹配成功的次数 misses: 查询值匹配失败的次数 hitRate: 查询值匹配率
```

### getCapacity<sup>9+</sup>

getCapacity(): number

获取当前缓冲区的容量。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型   | 说明                   |
| ------ | ---------------------- |
| number | 返回当前缓冲区的容量。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
let result = pro.getCapacity();
```

### clear<sup>9+</sup>

clear(): void

从当前缓冲区清除键值对。后续会调用afterRemoval()方法执行后续操作。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
let result = pro.length;
pro.clear();
```

### getCreateCount<sup>9+</sup>

getCreateCount(): number

获取创建对象的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型   | 说明                |
| ------ | -------------------|
| number | 返回创建对象的次数。 |

**示例：**

```ts
// 创建新类ChildLRUCache继承LRUCache，重写createDefault方法，返回一个非undefined的值。
class ChildLRUCache extends util.LRUCache<number, number> {
  constructor() {
    super();
  }

  createDefault(key: number): number {
    return key;
  }
}
let lru = new ChildLRUCache();
lru.put(2,10);
lru.get(3);
lru.get(5);
let res = lru.getCreateCount();
```

### getMissCount<sup>9+</sup>

getMissCount(): number

获取查询值不匹配的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型   | 说明                     |
| ------ | ------------------------ |
| number | 返回查询值不匹配的次数。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
pro.get(2);
let result = pro.getMissCount();
```

### getRemovalCount<sup>9+</sup>

getRemovalCount(): number

获取缓冲区键值对回收的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型   | 说明                       |
| ------ | -------------------------- |
| number | 返回缓冲区键值对回收的次数。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
pro.updateCapacity(2);
pro.put(50,22);
let result = pro.getRemovalCount();
```

### getMatchCount<sup>9+</sup>

getMatchCount(): number

获取查询值匹配成功的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型   | 说明                       |
| ------ | -------------------------- |
| number | 返回查询值匹配成功的次数。 |

**示例：**

  ```ts
  let pro: util.LRUCache<number, number> = new util.LRUCache();
  pro.put(2,10);
  pro.get(2);
  let result = pro.getMatchCount();
  ```

### getPutCount<sup>9+</sup>

getPutCount(): number

获取将值添加到缓冲区的次数。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型   | 说明                         |
| ------ | ---------------------------- |
| number | 返回将值添加到缓冲区的次数。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
let result = pro.getPutCount();
```

### isEmpty<sup>9+</sup>

isEmpty(): boolean

检查当前缓冲区是否为空。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型    | 说明                                     |
| ------- | ---------------------------------------- |
| boolean | 如果当前缓冲区不包含任何值，则返回true。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
let result = pro.isEmpty();
```

### get<sup>9+</sup>

get(key: K): V | undefined

表示要查询的键。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明         |
| ------ | ---- | ---- | ------------ |
| key    | K    | 是   | 要查询的键。 |

**返回值：**

| 类型                     | 说明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| V \| undefined | 如果指定的键存在于缓冲区中，则返回与键关联的值；否则返回undefined。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
let result  = pro.get(2);
```

### put<sup>9+</sup>

put(key: K,value: V): V

将键值对添加到缓冲区。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明                       |
| ------ | ---- | ---- | -------------------------- |
| key    | K    | 是   | 要添加的密钥。             |
| value  | V    | 是   | 指示与要添加的键关联的值。 |

**返回值：**

| 类型 | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| V    | 返回与添加的键关联的值；如果要添加的键已经存在，则返回原始值，如果键或值为空，则抛出此异常。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
let result = pro.put(2,10);
```

### values<sup>9+</sup>

values(): V[]

获取当前缓冲区中所有值从最近访问到最近最少访问的顺序列表 。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型      | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| V&nbsp;[] | 按从最近访问到最近最少访问的顺序返回当前缓冲区中所有值的列表。 |

**示例：**

```ts
let pro: util.LRUCache<number|string,number|string> = new util.LRUCache();
pro.put(2,10);
pro.put(2,"anhu");
pro.put("afaf","grfb");
let result = pro.values();
```

### keys<sup>9+</sup>

keys(): K[]

获取当前缓冲区中所有键从最近访问到最近最少访问的升序列表。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型      | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| K&nbsp;[] | 按升序返回当前缓冲区中所有键的列表，从最近访问到最近最少访问。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
let result = pro.keys();
```

### remove<sup>9+</sup>

remove(key: K): V | undefined

从当前缓冲区中删除指定的键及其关联的值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明           |
| ------ | ---- | ---- | -------------- |
| key    | K    | 是   | 要删除的键值。 |

**返回值：**

| 类型                     | 说明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| V&nbsp;\|&nbsp;undefined | 返回一个包含已删除键值对的Optional对象；如果key不存在，则返回undefined，如果key为null，则抛出异常。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
let result = pro.remove(20);
```

### afterRemoval<sup>9+</sup>

afterRemoval(isEvict: boolean,key: K,value: V,newValue: V): void

删除值后执行后续操作。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型    | 必填 | 说明                                                         |
| -------- | ------- | ---- | ------------------------------------------------------------ |
| isEvict  | boolean | 是   | 因容量不足而调用该方法时，参数值为true，其他情况为false。    |
| key      | K       | 是   | 表示删除的键。                                               |
| value    | V       | 是   | 表示删除的值。                                               |
| newValue | V       | 是   | 如果已调用put方法并且要添加的键已经存在，则参数值是关联的新值。其他情况下参数值为空。 |

**示例：**

```ts
class ChildLRUCache<K, V> extends util.LRUCache<K, V> {
  constructor(capacity?: number) {
    super(capacity);
  }

  afterRemoval(isEvict: boolean, key: K, value: V, newValue: V): void {
    if (isEvict === true) {
      console.info('key: ' + key);
      console.info('value: ' + value);
      console.info('newValue: ' + newValue);
    }
  }
}
let lru: ChildLRUCache<number, number>= new ChildLRUCache(2);
lru.put(1, 1);
lru.put(2, 2);
lru.put(3, 3);
```

### contains<sup>9+</sup>

contains(key: K): boolean

检查当前缓冲区是否包含指定的键。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型   | 必填 | 说明             |
| ------ | ------ | ---- | ---------------- |
| key    | K | 是   | 表示要检查的键。 |

**返回值：**

| 类型    | 说明                                       |
| ------- | ------------------------------------------ |
| boolean | 如果缓冲区包含指定的键，则返回&nbsp;true。 |

**示例：**

```ts
let pro : util.LRUCache<number | object, number> = new util.LRUCache();
pro.put(2,10);
class Lru{
s : string = "";
}
let obj : Lru = {s : "key" };
let result = pro.contains(obj);
```

### createDefault<sup>9+</sup>

createDefault(key: K): V

如果未计算特定键的值，则执行后续操作，参数表示丢失的键，返回与键关联的值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明           |
| ------ | ---- | ---- | -------------- |
| key    | K    | 是   | 表示丢失的键。 |

**返回值：**

| 类型 | 说明               |
| ---- | ------------------ |
| V    | 返回与键关联的值。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
let result = pro.createDefault(50);
```

### entries<sup>9+</sup>

entries(): IterableIterator&lt;[K,V]&gt;

允许迭代包含在这个对象中的所有键值对。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型        | 说明                 |
| ----------- | -------------------- |
| [K,&nbsp;V] | 返回一个可迭代数组。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
pro.put(3,15);
let pair:Iterable<Object[]> = pro.entries();
let arrayValue = Array.from(pair);
for (let value of arrayValue) {
  console.info(value[0]+ ', '+ value[1]);
}
```

### [Symbol.iterator]<sup>9+</sup>

[Symbol.iterator]\(): IterableIterator&lt;[K, V]&gt;

返回一个键值对形式的二维数组。

> **说明：**
>
> 本接口不支持在.ets文件中使用

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型        | 说明                           |
| ----------- | ------------------------------ |
| [K,&nbsp;V] | 返回一个键值对形式的二维数组。 |

**示例：**

```ts
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
pro.put(3,15);
let pair:Iterable<Object[]> = pro[Symbol.iterator]();
let arrayValue = Array.from(pair);
for (let value of arrayValue) {
  console.info(value[0]+ ', '+ value[1]);
}
```

## ScopeComparable<sup>8+</sup>

ScopeComparable类型的值需要实现compareTo方法，确保传入的数据具有可比性。

**系统能力：** SystemCapability.Utils.Lang

### compareTo<sup>8+</sup>

compareTo(other: ScopeComparable): boolean

比较两个值的大小，返回一个布尔值。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明           |
| ------ | ---- | ---- | -------------- |
| other  | [ScopeComparable](#scopecomparable8) | 是  | 表示要比较的值。 |

**返回值：**

| 类型 | 说明               |
| ---- | ------------------ |
| boolean | 调用compareTo的值大于等于传入的值返回true，否则返回false。|

**示例：**

构造新类，实现compareTo方法。后续示例代码中，均以此Temperature类为例。

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}
```

## ScopeType<sup>8+</sup>

用于表示范围中的值的类型。

**系统能力：** SystemCapability.Utils.Lang

| 类型 | 说明 |
| -------- | -------- |
| number | 表示值的类型为数字。 |
| [ScopeComparable](#scopecomparable8) | 表示值的类型为ScopeComparable。|

## ScopeHelper<sup>9+</sup>

ScopeHelper接口用于描述一个字段的有效范围。ScopeHelper实例的构造函数用于创建具有指定下限和上限的对象，并要求这些对象必须具有可比性。

### constructor<sup>9+</sup>

constructor(lowerObj: ScopeType, upperObj: ScopeType)

用于创建指定下限和上限的作用域实例的构造函数，返回一个ScopeHelper对象。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型                     | 必填 | 说明                   |
| -------- | ------------------------ | ---- | ---------------------- |
| lowerObj | [ScopeType](#scopetype8) | 是   | 指定作用域实例的下限。 |
| upperObj | [ScopeType](#scopetype8) | 是   | 指定作用域实例的上限。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
```

### toString<sup>9+</sup>

toString(): string

该字符串化方法返回一个包含当前范围的字符串表示形式。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型   | 说明                                   |
| ------ | -------------------------------------- |
| string | 返回包含当前范围对象的字符串表示形式。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.toString();
```

### intersect<sup>9+</sup>

intersect(range: ScopeHelper): ScopeHelper

获取给定范围和当前范围的交集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型                         | 必填 | 说明               |
| ------ | ---------------------------- | ---- | ------------------ |
| range  | [ScopeHelper](#scopehelper9) | 是   | 传入一个给定范围。 |

**返回值：**

| 类型                           | 说明                           |
| ------------------------------ | ------------------------------ |
| [ScopeHelper](#scopehelper9) | 返回给定范围和当前范围的交集。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
let tempMiDF = new Temperature(35);
let tempMidS = new Temperature(39);
let rangeFir = new util.ScopeHelper(tempMiDF, tempMidS);
range.intersect(rangeFir);
```

### intersect<sup>9+</sup>

intersect(lowerObj:ScopeType,upperObj:ScopeType):ScopeHelper

获取当前范围与给定下限和上限范围的交集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型                     | 必填 | 说明             |
| -------- | ------------------------ | ---- | ---------------- |
| lowerObj | [ScopeType](#scopetype8) | 是   | 给定范围的下限。 |
| upperObj | [ScopeType](#scopetype8) | 是   | 给定范围的上限。 |

**返回值：**

| 类型                         | 说明                                     |
| ---------------------------- | ---------------------------------------- |
| [ScopeHelper](#scopehelper9) | 返回当前范围与给定下限和上限范围的交集。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let tempMidS = new Temperature(39);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.intersect(tempMiDF, tempMidS);
```

### getUpper<sup>9+</sup>

getUpper(): ScopeType

获取当前范围的上限。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型                     | 说明                   |
| ------------------------ | ---------------------- |
| [ScopeType](#scopetype8) | 返回当前范围的上限值。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.getUpper();
```

### getLower<sup>9+</sup>

getLower(): ScopeType

获取当前范围的下限。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型                     | 说明                   |
| ------------------------ | ---------------------- |
| [ScopeType](#scopetype8) | 返回当前范围的下限值。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.getLower();
```

### expand<sup>9+</sup>

expand(lowerObj: ScopeType,upperObj: ScopeType): ScopeHelper

创建并返回包括当前范围和给定下限和上限的并集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名   | 类型                     | 必填 | 说明             |
| -------- | ------------------------ | ---- | ---------------- |
| lowerObj | [ScopeType](#scopetype8) | 是   | 给定范围的下限。 |
| upperObj | [ScopeType](#scopetype8) | 是   | 给定范围的上限。 |

**返回值：**

| 类型                         | 说明                                 |
| ---------------------------- | ------------------------------------ |
| [ScopeHelper](#scopehelper9) | 返回当前范围和给定下限和上限的并集。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let tempMidS = new Temperature(39);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.expand(tempMiDF, tempMidS);
```

### expand<sup>9+</sup>

expand(range: ScopeHelper): ScopeHelper

创建并返回包括当前范围和给定范围的并集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型                         | 必填 | 说明               |
| ------ | ---------------------------- | ---- | ------------------ |
| range  | [ScopeHelper](#scopehelper9) | 是   | 传入一个给定范围。 |

**返回值：**

| 类型                         | 说明                               |
| ---------------------------- | ---------------------------------- |
| [ScopeHelper](#scopehelper9) | 返回包括当前范围和给定范围的并集。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let tempMidS = new Temperature(39);
let range = new util.ScopeHelper(tempLower, tempUpper);
let rangeFir = new util.ScopeHelper(tempMiDF, tempMidS);
let result = range.expand(rangeFir);
```

### expand<sup>9+</sup>

expand(value: ScopeType): ScopeHelper

创建并返回包括当前范围和给定值的并集。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型                     | 必填 | 说明             |
| ------ | ------------------------ | ---- | ---------------- |
| value  | [ScopeType](#scopetype8) | 是   | 传入一个给定值。 |

**返回值：**

| 类型                         | 说明                             |
| ---------------------------- | -------------------------------- |
| [ScopeHelper](#scopehelper9) | 返回包括当前范围和给定值的并集。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.expand(tempMiDF);
```

### contains<sup>9+</sup>

contains(value: ScopeType): boolean

检查给定value是否包含在当前范围内。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型                     | 必填 | 说明             |
| ------ | ------------------------ | ---- | ---------------- |
| value  | [ScopeType](#scopetype8) | 是   | 传入一个给定值。 |

**返回值：**

| 类型    | 说明                                                |
| ------- | --------------------------------------------------- |
| boolean | 如果给定值包含在当前范围内返回true，否则返回false。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.contains(tempMiDF);
```

### contains<sup>9+</sup>

contains(range: ScopeHelper): boolean

检查给定range是否在当前范围内。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型                         | 必填 | 说明               |
| ------ | ---------------------------- | ---- | ------------------ |
| range  | [ScopeHelper](#scopehelper9) | 是   | 传入一个给定范围。 |

**返回值：**

| 类型    | 说明                                                  |
| ------- | ----------------------------------------------------- |
| boolean | 如果给定范围包含在当前范围内返回true，否则返回false。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
let tempLess = new Temperature(20);
let tempMore = new Temperature(45);
let rangeSec = new util.ScopeHelper(tempLess, tempMore);
let result = range.contains(rangeSec);
```

### clamp<sup>9+</sup>

clamp(value: ScopeType): ScopeType

将给定值限定到当前范围内。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型                     | 必填 | 说明           |
| ------ | ------------------------ | ---- | -------------- |
| value  | [ScopeType](#scopetype8) | 是   | 传入的给定值。 |

**返回值：**

| 类型                     | 说明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| [ScopeType](#scopetype8) | 如果传入的value小于下限，则返回lowerObj；如果大于上限值则返回upperObj；如果在当前范围内，则返回value。 |

**示例：**

```ts
class Temperature{
  private readonly _temp: number;
  constructor(value : number) {
    this._temp = value;
  }
  compareTo(value : Temperature ) {
    return this._temp >= value.getTemp();
  }
  getTemp() {
    return this._temp;
  }
  toString() : string {
    return this._temp.toString();
  }
}

let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.clamp(tempMiDF);
```

## Base64Helper<sup>9+</sup>

Base64编码表包含A-Z、a-z、0-9这62个字符，以及"+"和"/"这两个特殊字符。在编码时，将原始数据按3个字节一组进行划分，得到若干个6位的数字，然后使用Base64编码表中对应的字符来表示这些数字。如果最后剩余1或2个字节，则需要使用"="字符进行补齐。

### constructor<sup>9+</sup>

constructor()

Base64Helper的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

  ```ts 
  let base64 = new  util.Base64Helper();
  ```

### encodeSync<sup>9+</sup>

encodeSync(src: Uint8Array): Uint8Array

通过输入参数编码后输出Uint8Array对象。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型       | 必填 | 说明                |
| ------ | ---------- | ---- | ------------------- |
| src    | Uint8Array | 是   | 待编码Uint8Array对象。 |

**返回值：**

| 类型       | 说明                          |
| ---------- | ----------------------------- |
| Uint8Array | 返回编码后的Uint8Array对象。 |

**示例：**

  ```ts
  let that = new util.Base64Helper();
  let array = new Uint8Array([115,49,51]);
  let result = that.encodeSync(array);
  ```


### encodeToStringSync<sup>9+</sup>

encodeToStringSync(src: Uint8Array, options?: Type): string

通过输入参数编码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型       | 必填 | 说明                |
| ------ | ---------- | ---- | ------------------- |
| src    | Uint8Array | 是   | 待编码Uint8Array对象。 |
| options<sup>10+</sup>    | [Type](#type10) | 否   | 从API version 10开始支持该参数，表示对应的编码格式。<br/>此参数可选，可选值为：util.Type.BASIC和util.Type.MIME，默认值为：util.Type.BASIC。<br/>- 当参数取值为util.Type.BASIC时，输出结果包含：64个可打印字符，包括大写字母A-Z、小写字母a-z、数字0-9共62个字符，再加上另外2个'+'和'/'，没有回车符、换行符。<br/>- 当参数取值为util.Type.MIME时，输出结果包含：64个可打印字符，包括大写字母A-Z、小写字母a-z、数字0-9共62个字符，再加上另外2个'+'和'/'，编码输出每一行不超过76个字符，而且每行以'\r\n'符结束。|

**返回值：**

| 类型   | 说明                 |
| ------ | -------------------- |
| string | 返回编码后的字符串。 |

**示例：**

  ```ts
  let that = new util.Base64Helper();
  let array = new Uint8Array([77,97,110,105,115,100,105,115,116,105,110,103,117,105,115,104,101,100,110,111,116,111,110,108,121,98,121,104,105,115,114,101,97,115,111,110,98,117,116,98,121,116,104,105,115,115,105,110,103,117,108,97,114,112,97,115,115,105,111,110,102,114,111,109,111,116,104,101,114,97,110,105,109,97,108,115,119,104,105,99,104,105,115,97,108,117,115,116,111,102,116,104,101,109,105,110,100,101,120,99,101,101,100,115,116,104,101,115,104,111,114,116,118,101,104,101,109,101,110,99,101,111,102,97,110,121,99,97,114,110,97,108,112,108,101,97,115,117,114,101]);
  let result = that.encodeToStringSync(array, util.Type.MIME);
  ```


### decodeSync<sup>9+</sup>

decodeSync(src: Uint8Array | string, options?: Type): Uint8Array

通过输入参数解码后输出对应Uint8Array对象。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型                           | 必填 | 说明                          |
| ------ | ------------------------------ | ---- | ----------------------------- |
| src    | Uint8Array&nbsp;\|&nbsp;string | 是   | 待解码Uint8Array对象或者字符串。 |
| options<sup>10+</sup>    | [Type](#type10) | 否   | 从API version 10开始支持该参数，表示对应的编码格式。<br/>此参数可选，可选值为：util.Type.BASIC和util.Type.MIME，默认值为：util.Type.BASIC。<br/>- 当参数取值为util.Type.BASIC时，表示入参包含：64个可打印字符，包括大写字母A-Z、小写字母a-z、数字0-9共62个字符，再加上另外2个'+'和'/'，没有回车符、换行符。<br/>- 当参数取值为util.Type.MIME时，表示入参包含：64个可打印字符，包括大写字母A-Z、小写字母a-z、数字0-9共62个字符，再加上另外2个'+'和'/'，每一行不超过76个字符，而且每行以'\r\n'符结束。 |

**返回值：**

| 类型       | 说明                          |
| ---------- | ----------------------------- |
| Uint8Array | 返回解码后新分配的Uint8Array对象。 |

**示例：**

  ```ts
  let that = new util.Base64Helper();
  let buff = 'TWFuaXNkaXN0aW5ndWlzaGVkbm90b25seWJ5aGlzcmVhc29uYnV0Ynl0aGlzc2luZ3VsYXJwYXNz\r\naW9uZnJvbW90aGVyYW5pbWFsc3doaWNoaXNhbHVzdG9mdGhlbWluZGV4Y2VlZHN0aGVzaG9ydHZl\r\naGVtZW5jZW9mYW55Y2FybmFscGxlYXN1cmU=\r\n';
  let result = that.decodeSync(buff, util.Type.MIME);
  ```


### encode<sup>9+</sup>

encode(src: Uint8Array): Promise&lt;Uint8Array&gt;

通过输入参数异步编码后输出对应Uint8Array对象。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型       | 必填 | 说明                    |
| ------ | ---------- | ---- | ----------------------- |
| src    | Uint8Array | 是   | 异步编码输入Uint8Array对象。 |

**返回值：**

| 类型                      | 说明                              |
| ------------------------- | --------------------------------- |
| Promise&lt;Uint8Array&gt; | 返回异步编码后新分配的Uint8Array对象。 |

**示例：**

  ```ts
  let that = new util.Base64Helper();
  let array = new Uint8Array([115,49,51]);
  let rarray = new Uint8Array([99,122,69,122]);
  that.encode(array).then(val=>{
    for (let i = 0; i < rarray.length; i++) {
      console.info(val[i].toString());
    }
  })
  ```


### encodeToString<sup>9+</sup>

encodeToString(src: Uint8Array, options?: Type): Promise&lt;string&gt;

通过输入参数异步编码后输出对应文本。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型       | 必填 | 说明                    |
| ------ | ---------- | ---- | ----------------------- |
| src    | Uint8Array | 是   | 异步编码输入Uint8Array对象。 |
| options<sup>10+</sup>    | [Type](#type10) | 否   |  从API version 10开始支持该参数，表示对应的编码格式。<br/>此参数可选，可选值为：util.Type.BASIC和util.Type.MIME，默认值为：util.Type.BASIC。<br/>- 当参数取值为util.Type.BASIC时，输出结果包含：64个可打印字符，包括大写字母A-Z、小写字母a-z、数字0-9共62个字符，再加上另外2个'+'和'/'，没有回车符、换行符。<br/>- 当参数取值为util.Type.MIME时，输出结果包含：64个可打印字符，包括大写字母A-Z、小写字母a-z、数字0-9共62个字符，再加上另外2个'+'和'/'，编码输出每一行不超过76个字符，而且每行以'\r\n'符结束。 |

**返回值：**

| 类型                  | 说明                     |
| --------------------- | ------------------------ |
| Promise&lt;string&gt; | 返回异步编码后的字符串。 |

**示例：**

  ```ts
  let that = new util.Base64Helper();
  let array = new Uint8Array([77,97,110,105,115,100,105,115,116,105,110,103,117,105,115,104,101,100,110,111,116,111,110,108,121,98,121,104,105,115,114,101,97,115,111,110,98,117,116,98,121,116,104,105,115,115,105,110,103,117,108,97,114,112,97,115,115,105,111,110,102,114,111,109,111,116,104,101,114,97,110,105,109,97,108,115,119,104,105,99,104,105,115,97,108,117,115,116,111,102,116,104,101,109,105,110,100,101,120,99,101,101,100,115,116,104,101,115,104,111,114,116,118,101,104,101,109,101,110,99,101,111,102,97,110,121,99,97,114,110,97,108,112,108,101,97,115,117,114,101]);
  that.encodeToString(array, util.Type.MIME).then(val=>{
    // 根据开发者需求进行添加。
  })
  ```


### decode<sup>9+</sup>

decode(src: Uint8Array | string, options?: Type): Promise&lt;Uint8Array&gt;

通过输入参数异步解码后输出对应Uint8Array对象。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型                           | 必填 | 说明                              |
| ------ | ------------------------------ | ---- | --------------------------------- |
| src    | Uint8Array&nbsp;\|&nbsp;string | 是   | 异步解码输入Uint8Array对象或者字符串。 |
| options<sup>10+</sup>    | [Type](#type10) | 否   | 从API version 10开始支持该参数，表示对应的编码格式。<br/>此参数可选，可选值为：util.Type.BASIC和util.Type.MIME，默认值为：util.Type.BASIC。<br/>- 当参数取值为util.Type.BASIC时，表示入参包含：64个可打印字符，包括大写字母A-Z、小写字母a-z、数字0-9共62个字符，再加上另外2个'+'和'/'，没有回车符、换行符。<br/>- 当参数取值为util.Type.MIME时，表示入参包含：64个可打印字符，包括大写字母A-Z、小写字母a-z、数字0-9共62个字符，再加上另外2个'+'和'/'，每一行不超过76个字符，而且每行以'\r\n'符结束。 |

**返回值：**

| 类型                      | 说明                              |
| ------------------------- | --------------------------------- |
| Promise&lt;Uint8Array&gt; | 返回异步解码后新分配的Uint8Array对象。 |

**示例：**

  ```ts
  let that = new util.Base64Helper();
  let array = 'TWFuaXNkaXN0aW5ndWlzaGVkbm90b25seWJ5aGlzcmVhc29uYnV0Ynl0aGlzc2luZ3VsYXJwYXNz\r\naW9uZnJvbW90aGVyYW5pbWFsc3doaWNoaXNhbHVzdG9mdGhlbWluZGV4Y2VlZHN0aGVzaG9ydHZl\r\naGVtZW5jZW9mYW55Y2FybmFscGxlYXN1cmU=\r\n';
  that.decode(array, util.Type.MIME).then(val=>{
    // 根据开发者需求进行添加。
  })
  ```


## Type<sup>10+</sup>

Base64编码格式枚举。

**系统能力：** SystemCapability.Utils.Lang

| 名称   |值| 说明               |
| ----- |---| ----------------- |
| BASIC | 0 | 表示BASIC编码格式。|
| MIME  | 1 | 表示MIME编码格式。 |


## types<sup>8+</sup>

types为不同类型的内置对象提供类型检查，可以避免由于类型错误导致的异常或崩溃。该模块包含了多个工具函数，用于判断JS对象是否属于各种类型例如：ArrayBuffer、Map、Set等。

### constructor<sup>8+</sup>

constructor()

Types的构造函数。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

  ```ts
  let type = new util.types();
  ```


### isAnyArrayBuffer<sup>8+</sup>

isAnyArrayBuffer(value: Object): boolean

检查输入的value是否是ArrayBuffer类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是ArrayBuffer类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isAnyArrayBuffer(new ArrayBuffer(0));
  ```


### isArrayBufferView<sup>8+</sup>

isArrayBufferView(value: Object): boolean

检查输入的value是否是内置ArrayBufferView辅助类型。

ArrayBufferView辅助类型包括：Int8Array、Int16Array、Int32Array、Uint8Array、Uint8ClampedArray、Uint32Array、Float32Array、Float64Array、DataView。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的ArrayBufferView辅助类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isArrayBufferView(new Int8Array([]));
  ```


### isArgumentsObject<sup>8+</sup>

isArgumentsObject(value: Object): boolean

检查输入的value是否是一个arguments对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的arguments类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  function foo() {
      let result = that.isArgumentsObject(arguments);
  }
  let f = foo();
  ```


### isArrayBuffer<sup>8+</sup>

isArrayBuffer(value: Object): boolean

检查输入的value是否是ArrayBuffer类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的ArrayBuffer类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isArrayBuffer(new ArrayBuffer(0));
  ```


### isAsyncFunction<sup>8+</sup>

isAsyncFunction(value: Object): boolean

检查输入的value是否是一个异步函数类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的异步函数类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isAsyncFunction(async () => {});
  ```


### isBooleanObject<sup>8+</sup>

isBooleanObject(value: Object): boolean

检查输入的value是否是一个Boolean对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Boolean对象类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isBooleanObject(new Boolean(true));
  ```


### isBoxedPrimitive<sup>8+</sup>

isBoxedPrimitive(value: Object): boolean

检查输入的value是否是Boolean或Number或String或Symbol对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Boolean或Number或String或Symbol对象类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isBoxedPrimitive(new Boolean(false));
  ```


### isDataView<sup>8+</sup>

isDataView(value: Object): boolean

检查输入的value是否是DataView类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的DataView对象类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  const ab = new ArrayBuffer(20);
  let result = that.isDataView(new DataView(ab));
  ```


### isDate<sup>8+</sup>

isDate(value: Object): boolean

检查输入的value是否是Date类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Date对象类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isDate(new Date());
  ```


### isExternal<sup>8+</sup>

isExternal(value: Object): boolean

检查输入的value是否是native External类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含native&nbsp;External类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isExternal(true);
  ```


### isFloat32Array<sup>8+</sup>

isFloat32Array(value: Object): boolean

检查输入的value是否是Float32Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Float32Array数组类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isFloat32Array(new Float32Array());
  ```


### isFloat64Array<sup>8+</sup>

isFloat64Array(value: Object): boolean

检查输入的value是否是Float64Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Float64Array数组类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isFloat64Array(new Float64Array());
  ```


### isGeneratorFunction<sup>8+</sup>

isGeneratorFunction(value: Object): boolean

检查输入的value是否是generator函数类型。

> **说明：**
>
> 本接口不支持在.ets文件中使用

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的generator函数类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isGeneratorFunction(function* foo() {});
  ```


### isGeneratorObject<sup>8+</sup>

isGeneratorObject(value: Object): boolean

检查输入的value是否是generator对象类型。

> **说明：**
>
> 本接口不支持在.ets文件中使用

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的generator对象类型为true，反之为false。 |

**示例：**

  ```ts
  // 本接口不支持在.ets文件中使用。
  let that = new util.types();
  function* foo() {};
  const generator = foo();
  let result = that.isGeneratorObject(generator);
  ```


### isInt8Array<sup>8+</sup>

isInt8Array(value: Object): boolean

检查输入的value是否是Int8Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Int8Array数组类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isInt8Array(new Int8Array([]));
  ```


### isInt16Array<sup>8+</sup>

isInt16Array(value: Object): boolean

检查输入的value是否是Int16Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Int16Array数组类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isInt16Array(new Int16Array([]));
  ```


### isInt32Array<sup>8+</sup>

isInt32Array(value: Object): boolean

检查输入的value是否是Int32Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Int32Array数组类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isInt32Array(new Int32Array([]));
  ```


### isMap<sup>8+</sup>

isMap(value: Object): boolean

检查输入的value是否是Map类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Map类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isMap(new Map());
  ```


### isMapIterator<sup>8+</sup>

isMapIterator(value: Object): boolean

检查输入的value是否是Map的Iterator类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**


| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Map的Iterator类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  const map : Map<number,number> = new Map();
  let result = that.isMapIterator(map.keys());
  ```


### isNativeError<sup>8+</sup>

isNativeError(value: Object): boolean

检查输入的value是否是Error类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Error类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isNativeError(new TypeError());
  ```


### isNumberObject<sup>8+</sup>

isNumberObject(value: Object): boolean

检查输入的value是否是Number对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Number对象类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isNumberObject(new Number(0));
  ```


### isPromise<sup>8+</sup>

isPromise(value: Object): boolean

检查输入的value是否是Promise类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Promise类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isPromise(Promise.resolve(1));
  ```


### isProxy<sup>8+</sup>

isProxy(value: Object): boolean

检查输入的value是否是Proxy类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Proxy类型为true，反之为false。 |

**示例：**

  ```ts
  class Target{
  }
  let that = new util.types();
  const target : Target = {};
  const proxy = new Proxy(target, target);
  let result = that.isProxy(proxy);
  ```


### isRegExp<sup>8+</sup>

isRegExp(value: Object): boolean

检查输入的value是否是RegExp类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的RegExp类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isRegExp(new RegExp('abc'));
  ```


### isSet<sup>8+</sup>

isSet(value: Object): boolean

检查输入的value是否是Set类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Set类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let set : Set<number> = new Set();
  let result = that.isSet(set);
  ```


### isSetIterator<sup>8+</sup>

isSetIterator(value: Object): boolean

检查输入的value是否是Set的Iterator类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Set的Iterator类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  const set : Set<number> = new Set();
  let result = that.isSetIterator(set.keys());
  ```


### isStringObject<sup>8+</sup>

isStringObject(value: Object): boolean

检查输入的value是否是String对象类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的String对象类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isStringObject(new String('foo'));
  ```


### isSymbolObjec<sup>8+</sup>

isSymbolObject(value: Object): boolean

检查输入的value是否是Symbol对象类型。

> **说明：**
>
> 本接口不支持在.ets文件中使用

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Symbol对象类型为true，反之为false。 |

**示例：**

  ```ts
  // 本接口不支持在.ets文件中使用。
  let that = new util.types();
  const symbols = Symbol('foo');
  let result = that.isSymbolObject(Object(symbols));
  ```


### isTypedArray<sup>8+</sup>

isTypedArray(value: Object): boolean

检查输入的value是否是TypedArray类型的辅助类型。

TypedArray类型的辅助类型，包括Int8Array、Int16Array、Int32Array、Uint8Array、Uint8ClampedArray、Uint16Array、Uint32Array、Float32Array、Float64Array、DataView。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的TypedArray包含的类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isTypedArray(new Float64Array([]));
  ```


### isUint8Array<sup>8+</sup>

isUint8Array(value: Object): boolean

检查输入的value是否是Uint8Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Uint8Array数组类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isUint8Array(new Uint8Array([]));
  ```


### isUint8ClampedArray<sup>8+</sup>

isUint8ClampedArray(value: Object): boolean

检查输入的value是否是Uint8ClampedArray数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Uint8ClampedArray数组类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isUint8ClampedArray(new Uint8ClampedArray([]));
  ```


### isUint16Array<sup>8+</sup>

isUint16Array(value: Object): boolean

检查输入的value是否是Uint16Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Uint16Array数组类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isUint16Array(new Uint16Array([]));
  ```


### isUint32Array<sup>8+</sup>

isUint32Array(value: Object): boolean

检查输入的value是否是Uint32Array数组类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Uint32Array数组类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isUint32Array(new Uint32Array([]));
  ```


### isWeakMap<sup>8+</sup>

isWeakMap(value: Object): boolean

检查输入的value是否是WeakMap类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的WeakMap类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let value : WeakMap<object, number> = new WeakMap();
  let result = that.isWeakMap(value);
  ```


### isWeakSet<sup>8+</sup>

isWeakSet(value: Object): boolean

检查输入的value是否是WeakSet类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的WeakSet类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isWeakSet(new WeakSet());
  ```


### isBigInt64Array<sup>8+</sup>

isBigInt64Array(value: Object): boolean

检查输入的value是否是BigInt64Array类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的BigInt64Array类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isBigInt64Array(new BigInt64Array([]));
  ```


### isBigUint64Array<sup>8+</sup>

isBigUint64Array(value: Object): boolean

检查输入的value是否是BigUint64Array类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的BigUint64Array类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isBigUint64Array(new BigUint64Array([]));
  ```


### isModuleNamespaceObject<sup>8+</sup>

isModuleNamespaceObject(value: Object): boolean

检查输入的value是否是Module Namespace Object类型。

> **说明：**
>
> 本接口不支持在.ets文件中使用

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的Module Namespace Object类型为true，反之为false。 |

**示例：**

  ```ts
  // 本接口不支持在.ets文件中使用。
  import url from '@ohos.url'
  let that = new util.types();
  let result = that.isModuleNamespaceObject(url);
  ```


### isSharedArrayBuffer<sup>8+</sup>

isSharedArrayBuffer(value: Object): boolean

检查输入的value是否是SharedArrayBuffer类型。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | 待检测对象。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 判断的结果，如果是内置包含的SharedArrayBuffer类型为true，反之为false。 |

**示例：**

  ```ts
  let that = new util.types();
  let result = that.isSharedArrayBuffer(new SharedArrayBuffer(0));
  ```

## LruBuffer<sup>(deprecated)</sup>

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache<sup>9+</sup>](#lrucache9)替代。

### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Utils.Lang。

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| length | number | 是 | 否 | 当前缓冲区中值的总数。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number>= new util.LruBuffer();
  pro.put(2,10);
  pro.put(1,8);
  let result = pro.length;
  ```

### constructor<sup>(deprecated)</sup>

constructor(capacity?: number)

默认构造函数用于创建一个新的LruBuffer实例，默认容量为64。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.constructor<sup>9+</sup>](#constructor9-3)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| capacity | number | 否 | 指示要为缓冲区自定义的容量，默认值为64。 |

**示例：**

  ```ts
  let lrubuffer : util.LruBuffer<number,number> = new util.LruBuffer();
  ```

### updateCapacity<sup>(deprecated)</sup>

updateCapacity(newCapacity: number): void

将缓冲区容量更新为指定容量，如果newCapacity小于或等于0，则抛出异常。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.updateCapacity<sup>9+</sup>](#updatecapacity9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| newCapacity | number | 是 | 指示要为缓冲区自定义的容量。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.updateCapacity(100);
  ```

### toString<sup>(deprecated)</sup>

toString(): string

返回对象的字符串表示形式。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.toString<sup>9+</sup>](#tostring9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 返回对象的字符串表示形式。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  pro.get(2);
  pro.remove(20);
  let result = pro.toString();
  ```

### getCapacity<sup>(deprecated)</sup>

getCapacity(): number

获取当前缓冲区的容量。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.getCapacity<sup>9+</sup>](#getcapacity9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回当前缓冲区的容量。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  let result = pro.getCapacity();
  ```

### clear<sup>(deprecated)</sup>

clear(): void

从当前缓冲区清除键值对。后续会调用afterRemoval()方法执行后续操作。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.clear<sup>9+</sup>](#clear9)替代。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.length;
  pro.clear();
  ```

### getCreateCount<sup>(deprecated)</sup>

getCreateCount(): number

获取createDefault()返回值的次数。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.getCreateCount<sup>9+</sup>](#getcreatecount9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回createDefault()返回值的次数。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(1,8);
  let result = pro.getCreateCount();
  ```

### getMissCount<sup>(deprecated)</sup>

getMissCount(): number

获取查询值不匹配的次数。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.getMissCount<sup>9+</sup>](#getmisscount9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回查询值不匹配的次数。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  pro.get(2);
  let result = pro.getMissCount();
  ```

### getRemovalCount<sup>(deprecated)</sup>

getRemovalCount(): number

获取从缓冲区中逐出值的次数。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.getRemovalCount<sup>9+</sup>](#getremovalcount9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回从缓冲区中驱逐的次数。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  pro.updateCapacity(2);
  pro.put(50,22);
  let result = pro.getRemovalCount();
  ```

### getMatchCount<sup>(deprecated)</sup>

getMatchCount(): number

获取查询值匹配成功的次数。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.getMatchCount<sup>9+</sup>](#getmatchcount9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回查询值匹配成功的次数。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  pro.get(2);
  let result = pro.getMatchCount();
  ```

### getPutCount<sup>(deprecated)</sup>

getPutCount(): number

获取将值添加到缓冲区的次数。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.getPutCount<sup>9+</sup>](#getputcount9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回将值添加到缓冲区的次数。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.getPutCount();
  ```

### isEmpty<sup>(deprecated)</sup>

isEmpty(): boolean

检查当前缓冲区是否为空。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.isEmpty<sup>9+</sup>](#isempty9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果当前缓冲区不包含任何值，则返回true。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.isEmpty();
  ```

### get<sup>(deprecated)</sup>

get(key: K): V | undefined

表示要查询的键。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.get<sup>9+</sup>](#get9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 要查询的键。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| V&nbsp;\|&nbsp;undefined | 如果指定的键存在于缓冲区中，则返回与键关联的值；否则返回undefined。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  let result  = pro.get(2);
  ```

### put<sup>(deprecated)</sup>

put(key: K,value: V): V

将键值对添加到缓冲区。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.put<sup>9+</sup>](#put9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 要添加的密钥。 |
| value | V | 是 | 指示与要添加的键关联的值。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| V | 返回与添加的键关联的值；如果要添加的键已经存在，则返回原始值，如果键或值为空，则抛出此异常。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  let result = pro.put(2,10);
  ```

### values<sup>(deprecated)</sup>

values(): V[]

获取当前缓冲区中所有值从最近访问到最近最少访问的顺序列表。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.values<sup>9+</sup>](#values9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| V&nbsp;[] | 按从最近访问到最近最少访问的顺序返回当前缓冲区中所有值的列表。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number|string,number|string> = new util.LruBuffer();
  pro.put(2,10);
  pro.put(2,"anhu");
  pro.put("afaf","grfb");
  let result = pro.values();
  ```

### keys<sup>(deprecated)</sup>

keys(): K[]

获取当前缓冲区中所有键从最近访问到最近最少访问的升序列表。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.keys<sup>9+</sup>](#keys9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| K&nbsp;[] | 按升序返回当前缓冲区中所有键的列表，从最近访问到最近最少访问。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.keys();
  ```

### remove<sup>(deprecated)</sup>

remove(key: K): V | undefined

从当前缓冲区中删除指定的键及其关联的值。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.remove<sup>9+</sup>](#remove9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 要删除的密钥。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| V&nbsp;\|&nbsp;undefined | 返回一个包含已删除键值对的Optional对象；如果key不存在，则返回一个空的Optional对象，如果key为null，则抛出异常。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.remove(20);
  ```

### afterRemoval<sup>(deprecated)</sup>

afterRemoval(isEvict: boolean,key: K,value: V,newValue: V): void

删除值后执行后续操作。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.afterRemoval<sup>9+</sup>](#afterremoval9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| isEvict | boolean | 是 | 因容量不足而调用该方法时，参数值为true，其他情况为false。 |
| key | K | 是 | 表示删除的键。 |
| value | V | 是 | 表示删除的值。 |
| newValue | V | 是 | 如果已调用put方法并且要添加的键已经存在，则参数值是关联的新值。其他情况下参数值为空。 |

**示例：**

```ts
class ChildLruBuffer<K, V> extends util.LruBuffer<K, V> {
  constructor(capacity?: number) {
    super(capacity);
  }

  afterRemoval(isEvict: boolean, key: K, value: V, newValue: V): void {
    if (isEvict === true) {
      console.info('key: ' + key);
      console.info('value: ' + value);
      console.info('newValue: ' + newValue);
    }
  }
}
let lru: ChildLruBuffer<number, number> = new ChildLruBuffer(2);
lru.put(11, 1);
lru.put(22, 2);
lru.put(33, 3);
```

### contains<sup>(deprecated)</sup>

contains(key: K): boolean

检查当前缓冲区是否包含指定的键。


> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.contains<sup>9+</sup>](#contains9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 表示要检查的键。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果缓冲区包含指定的键，则返回&nbsp;true。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.contains(20);
  ```

### createDefault<sup>(deprecated)</sup>

createDefault(key: K): V

如果未计算特定键的值，则执行后续操作，参数表示丢失的键，返回与键关联的值。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.createDefault<sup>9+</sup>](#createdefault9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| key | K | 是 | 表示丢失的键。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| V | 返回与键关联的值。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  let result = pro.createDefault(50);
  ```

### entries<sup>(deprecated)</sup>

entries(): IterableIterator&lt;[K,V]&gt;

允许迭代包含在这个对象中的所有键值对。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.entries<sup>9+</sup>](#entries9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [K,&nbsp;V] | 返回一个可迭代数组。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.entries();
  ```

### [Symbol.iterator]<sup>(deprecated)</sup>

[Symbol.iterator]\(): IterableIterator&lt;[K, V]&gt;

返回一个键值对形式的二维数组。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[LRUCache.Symbol.iterator<sup>9+</sup>](#symboliterator9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [K,&nbsp;V] | 返回一个键值对形式的二维数组。 |

**示例：**

  ```ts
  let pro : util.LruBuffer<number,number> = new util.LruBuffer();
  pro.put(2,10);
  let result = pro[Symbol.iterator]();
  ```

## Scope<sup>(deprecated)</sup>

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper<sup>9+</sup>](#scopehelper9)替代。

### constructor<sup>(deprecated)</sup>

constructor(lowerObj: ScopeType, upperObj: ScopeType)

用于创建指定下限和上限的作用域实例的构造函数，返回一个Scope对象。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.constructor<sup>9+</sup>](#constructor9-4)替代。


**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| lowerObj | [ScopeType](#scopetype8) | 是 | 指定作用域实例的下限。 |
| upperObj | [ScopeType](#scopetype8) | 是 | 指定作用域实例的上限。 |

**示例：**
  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  ```

### toString<sup>(deprecated)</sup>

toString(): string

该字符串化方法返回一个包含当前范围的字符串表示形式。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.toString<sup>9+</sup>](#tostring9-1)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 返回包含当前范围对象的字符串表示形式。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.toString();
  ```

### intersect<sup>(deprecated)</sup>

intersect(range: Scope): Scope

获取给定范围和当前范围的交集。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.intersect<sup>9+</sup>](#intersect9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| range | [Scope](#scopedeprecated) | 是 | 传入一个给定范围。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scopedeprecated) | 返回给定范围和当前范围的交集。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  let tempMiDF = new Temperature(35);
  let tempMidS = new Temperature(39);
  let rangeFir = new util.Scope(tempMiDF, tempMidS);
  let result = range.intersect(rangeFir );
  ```

### intersect<sup>(deprecated)</sup>

intersect(lowerObj:ScopeType,upperObj:ScopeType):Scope

获取当前范围与给定下限和上限范围的交集。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.intersect<sup>9+</sup>](#intersect9-1)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| lowerObj | [ScopeType](#scopetype8) | 是 | 给定范围的下限。 |
| upperObj | [ScopeType](#scopetype8) | 是 | 给定范围的上限。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scopedeprecated) | 返回当前范围与给定下限和上限范围的交集。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let tempMidS = new Temperature(39);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.intersect(tempMiDF, tempMidS);
  ```

### getUpper<sup>(deprecated)</sup>

getUpper(): ScopeType

获取当前范围的上限。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.getUpper<sup>9+</sup>](#getupper9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [ScopeType](#scopetype8) | 返回当前范围的上限值。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.getUpper();
  ```

### getLower<sup>(deprecated)</sup>

getLower(): ScopeType

获取当前范围的下限。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.getLower<sup>9+</sup>](#getlower9)替代。

**系统能力：** SystemCapability.Utils.Lang

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [ScopeType](#scopetype8) | 返回当前范围的下限值。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.getLower();
  ```

### expand<sup>(deprecated)</sup>

expand(lowerObj: ScopeType,upperObj: ScopeType): Scope

创建并返回包括当前范围和给定下限和上限的并集。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.expand<sup>9+</sup>](#expand9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| lowerObj | [ScopeType](#scopetype8) | 是 | 给定范围的下限。 |
| upperObj | [ScopeType](#scopetype8) | 是 | 给定范围的上限。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scopedeprecated) | 返回当前范围和给定下限和上限的并集。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let tempMidS = new Temperature(39);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.expand(tempMiDF, tempMidS);
  ```

### expand<sup>(deprecated)</sup>

expand(range: Scope): Scope

创建并返回包括当前范围和给定范围的并集。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.expand<sup>9+</sup>](#expand9-1)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| range | [Scope](#scopedeprecated) | 是 | 传入一个给定范围。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scopedeprecated) | 返回包括当前范围和给定范围的并集。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let tempMidS = new Temperature(39);
  let range = new util.Scope(tempLower, tempUpper);
  let rangeFir = new util.Scope(tempMiDF, tempMidS);
  let result = range.expand(rangeFir);
  ```

### expand<sup>(deprecated)</sup>

expand(value: ScopeType): Scope

创建并返回包括当前范围和给定值的并集。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.expand<sup>9+</sup>](#expand9-2)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | [ScopeType](#scopetype8) | 是 | 传入一个给定值。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [Scope](#scopedeprecated) | 返回包括当前范围和给定值的并集。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.expand(tempMiDF);
  ```

### contains<sup>(deprecated)</sup>

contains(value: ScopeType): boolean

检查给定value是否包含在当前范围内。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.contains<sup>9+</sup>](#contains9-1)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | [ScopeType](#scopetype8) | 是 | 传入一个给定值。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果给定值包含在当前范围内返回true，否则返回false。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.contains(tempMiDF);
  ```

### contains<sup>(deprecated)</sup>

contains(range: Scope): boolean

检查给定range是否在当前范围内。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.contains<sup>9+</sup>](#contains9-2)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| range | [Scope](#scopedeprecated) | 是 | 传入一个给定范围。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 如果给定范围包含在当前范围内返回true，否则返回false。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  let tempLess = new Temperature(20);
  let tempMore = new Temperature(45);
  let rangeSec = new util.Scope(tempLess, tempMore);
  let result = range.contains(rangeSec);
  ```

### clamp<sup>(deprecated)</sup>


clamp(value: ScopeType): ScopeType

将给定值限定到当前范围内。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[ScopeHelper.clamp<sup>9+</sup>](#clamp9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | [ScopeType](#scopetype8) | 是 | 传入的给定值。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [ScopeType](#scopetype8) | 如果传入的value小于下限，则返回lowerObj；如果大于上限值则返回upperObj；如果在当前范围内，则返回value。 |

**示例：**

  ```ts
  class Temperature{
    private readonly _temp: number;
    constructor(value : number) {
      this._temp = value;
    }
    compareTo(value : Temperature ) {
      return this._temp >= value.getTemp();
    }
    getTemp() {
      return this._temp;
    }
    toString() : string {
      return this._temp.toString();
    }
  }

  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.clamp(tempMiDF);
  ```


## Base64<sup>(deprecated)</sup>

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[Base64Helper<sup>9+</sup>](#base64helper9)替代。

### constructor<sup>(deprecated)</sup>

constructor()

Base64的构造函数。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[Base64Helper.constructor<sup>9+</sup>](#constructor9-5)替代。

**系统能力：** SystemCapability.Utils.Lang

**示例：**

  ```ts
  let base64 = new  util.Base64();
  ```

### encodeSync<sup>(deprecated)</sup>

encodeSync(src: Uint8Array): Uint8Array

通过输入参数编码后输出对应文本。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[Base64Helper.encodeSync<sup>9+</sup>](#encodesync9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array | 是 | 编码输入Uint8数组。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回编码后新分配的Uint8数组。 |

**示例：**

  ```ts
  let that = new util.Base64();
  let array = new Uint8Array([115,49,51]);
  let result = that.encodeSync(array);
  ```

### encodeToStringSync<sup>(deprecated)</sup>

encodeToStringSync(src: Uint8Array): string

通过输入参数编码后输出对应文本。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[Base64Helper.encodeToStringSync<sup>9+</sup>](#encodetostringsync9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array | 是 | 编码输入Uint8数组。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 返回编码后的字符串。 |

**示例：**

  ```ts
  let that = new util.Base64();
  let array = new Uint8Array([115,49,51]);
  let result = that.encodeToStringSync(array);
  ```

### decodeSync<sup>(deprecated)</sup>

decodeSync(src: Uint8Array | string): Uint8Array

通过输入参数解码后输出对应文本。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[Base64Helper.decodeSync<sup>9+</sup>](#decodesync9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array&nbsp;\|&nbsp;string | 是 | 解码输入Uint8数组或者字符串。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回解码后新分配的Uint8数组。 |

**示例：**

  ```ts
  let that = new util.Base64();
  let buff = 'czEz';
  let result = that.decodeSync(buff);
  ```

### encode<sup>(deprecated)</sup>

encode(src: Uint8Array): Promise&lt;Uint8Array&gt;

通过输入参数异步编码后输出对应文本。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[Base64Helper.encode<sup>9+</sup>](#encode9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array | 是 | 异步编码输入Uint8数组。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Uint8Array&gt; | 返回异步编码后新分配的Uint8数组。 |

**示例：**

  ```ts
  let that = new util.Base64();
  let array = new Uint8Array([115,49,51]);
  let rarray = new Uint8Array([99,122,69,122]);
  that.encode(array).then(val=>{    
      for (let i = 0; i < rarray.length; i++) {        
          console.info(val[i].toString())
      }
  })
  ```

### encodeToString<sup>(deprecated)</sup>

encodeToString(src: Uint8Array): Promise&lt;string&gt;

通过输入参数异步编码后输出对应文本。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[Base64Helper.encodeToString<sup>9+</sup>](#encodetostring9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array | 是 | 异步编码输入Uint8数组。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;string&gt; | 返回异步编码后的字符串。 |

**示例：**

  ```ts
  let that = new util.Base64();
  let array = new Uint8Array([115,49,51]);
  that.encodeToString(array).then(val=>{    
      console.info(val)
  })
  ```

### decode<sup>(deprecated)</sup>


decode(src: Uint8Array | string): Promise&lt;Uint8Array&gt;

通过输入参数异步解码后输出对应文本。

> **说明：**
>
> 从API version 8开始支持，从API version 9开始废弃，建议使用[Base64Helper.decode<sup>9+</sup>](#decode9)替代。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| src | Uint8Array&nbsp;\|&nbsp;string | 是 | 异步解码输入Uint8数组或者字符串。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;Uint8Array&gt; | 返回异步解码后新分配的Uint8数组。 |

**示例：**

  ```ts
  let that = new util.Base64();
  let array = new Uint8Array([99,122,69,122]);
  let rarray = new Uint8Array([115,49,51]);
  that.decode(array).then(val=>{    
      for (let i = 0; i < rarray.length; i++) {        
          console.info(val[i].toString());
      }
  })
  ```
