# @ohos.util (util)

The **util** module provides common utility functions, such as [TextEncoder](#textencoder) and [TextDecoder](#textdecoder) for string encoding and decoding, [RationalNumber<sup>8+</sup>](#rationalnumber8) for rational number operations, [LRUCache<sup>9+</sup>](#lrucache9) for cache management, [ScopeHelper<sup>9+</sup>](#scopehelper9) for range determination, [Base64Helper<sup>9+</sup>](#base64helper9) for Base64 encoding and decoding, and [types<sup>8+</sup>](#types8) for built-in object type check.

> **NOTE**
>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```js
import util from '@ohos.util';
```

## util.format<sup>9+</sup>

format(format: string,  ...args: Object[]): string

Formats a string by replacing the placeholders in it.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name | Type    | Mandatory| Description          |
| ------- | -------- | ---- | -------------- |
| format  | string   | Yes  | Format string. This string contains zero or more placeholders, which specify the position and format of the arguments to be inserted.|
| ...args | Object[] | No  | Data used to replace the placeholders in **format**. If **null** is passed in, the first argument is returned by default.|

**Return value**

| Type  | Description             |
| ------ | -----------------|
| string | Formatted string.|


**Format Specifiers**

| Specifier| Description                         |
| ------ | -------------------------------- |
| %s     | Converts a parameter into a string for all values except **Object**, **BigInt**, and **-0**.|
| %d     | Converts a parameter into a decimal integer for all values except **Symbol** and **BigInt**.|
| %i     | Converts a string into a decimal integer for all values except **Symbol** and **BigInt**.|
| %f     | Converts a string into a floating point number for all values except **Symbol** and **BigInt**.|
| %j     | Converts a JavaScript object into a JSON string.|
| %o     | Converts a JavaScript object into a string, without containing the prototype chain information of the object.|
| %O     | Converts a JavaScript object into a string.|
| %c     | Valid only in the browser. It is ignored in other environments.|
| %%     | Placeholder for escaping the percent sign.|

**Example**

```js
let name = 'John';
let age = 20;
let formattedString = util.format('My name is %s and I am %s years old', name, age);
console.log(formattedString);
// Output: My name is John and I am 20 years old
let num = 10.5;
formattedString = util.format('The number is %d', num);
console.log(formattedString);
// Output: The number is 10.5.
num = 100.5;
formattedString = util.format('The number is %i', num);
console.log(formattedString);
// Output: The number is 100.
const pi = 3.141592653;
formattedString = util.format('The value of pi is %f', pi);
console.log(formattedString);
// Output: The value of pi is 3.141592653
const obj = { name: 'John', age: 20 };
formattedString = util.format('The object is %j', obj);
console.log(formattedString);
// Output: The object is {"name":"John","age":20}.
const person = {
  name: 'John',
  age: 20,
  address: {
    city: 'New York',
    country: 'USA'
  }
};
console.log(util.format('Formatted object using %%O: %O', person));
console.log(util.format('Formatted object using %%o: %o', person));
/*
Output:
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
console.log(formattedString);
// Output: John finished 80% of the homework
```

## util.errnoToString<sup>9+</sup>

errnoToString(errno: number): string

Obtains detailed information about a system error code.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| errno  | number | Yes  | Error code generated.|

**Return value**

| Type  | Description                  |
| ------ | ---------------------- |
| string | Detailed information about the error code.|

**Example**

```js
let errnum = -1; // -1 is a system error code.
let result = util.errnoToString(errnum);
console.log("result = " + result);
```

**Some error code and message examples**

| Error Code| Message                             |
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

Calls back an asynchronous function. In the callback, the first parameter indicates the cause of the rejection (the value is **null** if the promise has been resolved), and the second parameter indicates the resolved value.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| original | Function | Yes| Asynchronous function.|

**Return value**

| Type| Description|
| -------- | -------- |
| Function | Callback function, in which the first parameter **err** indicates the cause of the rejection (the value is **null** if the promise has been resolved) and the second parameter **value** indicates the resolved value.|

**Example**

  ```js
async function fn() {
   return 'hello world';
}
let cb = util.callbackWrapper(fn);
cb(1, (err, ret) => {
   if (err) throw err;
   console.log(ret);
});
  ```

## util.promisify<sup>9+</sup>

promisify(original: (err: Object, value: Object) =&gt; void): Function

Processes an asynchronous function and returns a promise.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| original | Function | Yes| Function, in which the first parameter **err** indicates the cause of the rejection (the value is **null** if the promise has been resolved) and the second parameter **value** indicates the resolved value. |

**Return value**

| Type| Description|
| -------- | -------- |
| Function | Promise function.|

**Example**

```js
async function fn() {
  return 'hello world';
}
const addCall = util.promisify(util.callbackWrapper(fn));
(async () => {
  try {
    let res: string = await addCall();
    console.log(res);
  } catch (err) {
    console.log(err);
  }
})();
```

## util.generateRandomUUID<sup>9+</sup>

generateRandomUUID(entropyCache?: boolean): string

Uses a secure random number generator to generate a random universally unique identifier (UUID) of the string type in RFC 4122 version 4.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| entropyCache | boolean | No| Whether a cached UUID can be used. The default value is **true**.|

**Return value**

| Type| Description|
| -------- | -------- |
| string | A string representing the UUID generated.|

**Example**

  ```js
  let uuid = util.generateRandomUUID(true);
  console.log("RFC 4122 Version 4 UUID:" + uuid);
  // Output:
  // RFC 4122 Version 4 UUID:88368f2a-d5db-47d8-a05f-534fab0a0045
  ```

## util.generateRandomBinaryUUID<sup>9+</sup>

generateRandomBinaryUUID(entropyCache?: boolean): Uint8Array

Uses a secure random number generator to generate a random UUID of the Uint8Array type in RFC 4122 version 4.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| entropyCache | boolean | No| Whether a cached UUID can be used. The default value is **true**.|

**Return value**

| Type| Description|
| -------- | -------- |
| Uint8Array | A Uint8Array value representing the UUID generated.|

**Example**

  ```js
  let uuid = util.generateRandomBinaryUUID(true);
  console.log(JSON.stringify(uuid));
  // Output:
  // 138,188,43,243,62,254,70,119,130,20,235,222,199,164,140,150
  ```

## util.parseUUID<sup>9+</sup>

parseUUID(uuid: string): Uint8Array

Converts a UUID of the string type generated by **generateRandomUUID** to a UUID of the Uint8Array type generated by **generateRandomBinaryUUID**, as described in RFC 4122 version 4.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| uuid | string | Yes| A string representing the UUID.|

**Return value**

| Type| Description|
| -------- | -------- |
| Uint8Array | A Uint8Array value representing the UUID parsed. If the parsing fails, **SyntaxError** is thrown.|

**Example**

  ```js
  let uuid = util.parseUUID("84bdf796-66cc-4655-9b89-d6218d100f9c");
  console.log(JSON.stringify(uuid));
  // Output:
  // 132,189,247,150,102,204,70,85,155,137,214,33,141,16,15,156
  ```

## util.printf<sup>(deprecated)</sup>

printf(format: string,  ...args: Object[]): string

Formats a string by replacing the placeholders in it.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [util.format<sup>9+</sup>](#utilformat9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| format | string | Yes| Format string.|
| ...args | Object[] | No| Data used to replace the placeholders in **format**. If **null** is passed in, the first argument is returned by default.|

**Return value**

| Type| Description|
| -------- | -------- |
| string | String containing the formatted values.|

**Example**

  ```js
  let res = util.printf("%s", "hello world!");
  console.log(res);
  ```


## util.getErrorString<sup>(deprecated)</sup>

getErrorString(errno: number): string

Obtains detailed information about a system error code.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [util.errnoToString<sup>9+</sup>](#utilerrnotostring9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| errno | number | Yes| Error code generated.|

**Return value**

| Type| Description|
| -------- | -------- |
| string | Detailed information about the error code.|

**Example**

  ```js
  let errnum = -1; // -1 is a system error code.
  let result = util.getErrorString(errnum);
  console.log("result = " + result);
  ```

## util.promiseWrapper<sup>(deprecated)</sup>

promiseWrapper(original: (err: Object, value: Object) =&gt; void): Object

Processes an asynchronous function and returns a promise.

> **NOTE**
>
> This API is unavailable. You are advised to use [util.promisify<sup>9+</sup>](#utilpromisify9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| original | Function | Yes| Asynchronous function.|

**Return value**

| Type| Description|
| -------- | -------- |
| Function | Function in the error-first style (that is, **(err, value) =>...** is called as the last parameter) and the promise.|


## TextDecoder

Provides APIs to decode byte arrays into strings. It supports multiple formats, including UTF-8, UTF-16LE, UTF-16BE, ISO-8859, and Windows-1251.

### Attributes

**System capability**: SystemCapability.Utils.Lang

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| encoding | string | Yes| No| Encoding format.<br>- Supported formats: utf-8, ibm866, iso-8859-2, iso-8859-3, iso-8859-4, iso-8859-5, iso-8859-6, iso-8859-7, iso-8859-8, iso-8859-8-i, iso-8859-10, iso-8859-13, iso-8859-14, iso-8859-15, koi8-r, koi8-u, macintosh, windows-874, windows-1250, windows-1251, windows-1252, windows-1253, windows-1254, windows-1255, windows-1256, windows-1257, windows-1258, x-mac-cyrilli, gbk, gb18030, big5, euc-jp, iso-2022-jp, shift_jis, euc-kr, utf-16be, utf-16le|
| fatal | boolean | Yes| No| Whether to display fatal errors.|
| ignoreBOM | boolean | Yes| No| Whether to ignore the byte order marker (BOM). The default value is **false**, which indicates that the result contains the BOM.|

### constructor<sup>9+</sup>

constructor()

A constructor used to create a **TextDecoder** object.

**System capability**: SystemCapability.Utils.Lang

**Example**

```js
let result = new util.TextDecoder();
let retStr = result.encoding;
```
### create<sup>9+</sup>

static create(encoding?: string,options?: { fatal?: boolean; ignoreBOM?: boolean }): TextDecoder

Creates a **TextDecoder** object. It provides the same function as the deprecated argument constructor.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name  | Type  | Mandatory| Description                                            |
| -------- | ------ | ---- | ------------------------------------------------ |
| encoding | string | No  | Encoding format. The default format is **'utf-8'**.                     |
| options  | Object | No  | Decoding-related options, which include **fatal** and **ignoreBOM**.|

**Table 1.1** options

| Name     | Type| Mandatory| Description              |
| --------- | -------- | ---- | ------------------ |
| fatal     | boolean  | No  | Whether to display fatal errors. The default value is **false**.|
| ignoreBOM | boolean  | No  | Whether to ignore the BOM. The default value is **false**. |

**Example**

```js
let result = util.TextDecoder.create('utf-8', { ignoreBOM : true })
let retStr = result.encoding
```

### decodeWithStream<sup>9+</sup>

decodeWithStream(input: Uint8Array, options?: { stream?: boolean }): string

Decodes the input content into a string.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| input | Uint8Array | Yes| Uint8Array object to decode.|
| options | Object | No| Decoding-related options.|

**Table 2** options

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| stream | boolean | No| Whether to allow data blocks in subsequent **decodeWithStream()**. If data is processed in blocks, set this parameter to **true**. If this is the last data block to process or data is not divided into blocks, set this parameter to **false**. The default value is **false**.|

**Return value**

| Type| Description|
| -------- | -------- |
| string | String obtained.|

**Example**

  ```js
  let textDecoder = new util.TextDecoder("utf-8",{ignoreBOM: true});
  let result = new Uint8Array(6);
  result[0] = 0xEF;
  result[1] = 0xBB;
  result[2] = 0xBF;
  result[3] = 0x61;
  result[4] = 0x62;
  result[5] = 0x63;
  console.log("input num:");
  let retStr = textDecoder.decodeWithStream( result , {stream: false});
  console.log("retStr = " + retStr);
  ```

### constructor<sup>(deprecated)</sup>

constructor(encoding?: string, options?: { fatal?: boolean; ignoreBOM?: boolean })

A constructor used to create a **TextDecoder** object.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [create<sup>9+</sup>](#create9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| encoding | string | No| Encoding format. The default format is **'utf-8'**.|
| options | Object | No| Decoding-related options, which include **fatal** and **ignoreBOM**.|

  **Table 1** options

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| fatal | boolean | No| Whether to display fatal errors. The default value is **false**.|
| ignoreBOM | boolean | No| Whether to ignore the BOM. The default value is **false**.|

**Example**

  ```js
  let textDecoder = new util.TextDecoder("utf-8",{ignoreBOM: true});
  ```

### decode<sup>(deprecated)</sup>

decode(input: Uint8Array, options?: { stream?: false }): string

Decodes the input content into a string.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [decodeWithStream<sup>9+</sup>](#decodewithstream9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| input | Uint8Array | Yes| Uint8Array object to decode.|
| options | Object | No| Decoding-related options.|

**Table 2** options

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| stream | boolean | No| Whether to allow data blocks in subsequent **decode()**. If data is processed in blocks, set this parameter to **true**. If this is the last data block to process or data is not divided into blocks, set this parameter to **false**. The default value is **false**.|

**Return value**

| Type| Description|
| -------- | -------- |
| string | String obtained.|

**Example**

  ```js
  let textDecoder = new util.TextDecoder("utf-8",{ignoreBOM: true});
  let result = new Uint8Array(6);
  result[0] = 0xEF;
  result[1] = 0xBB;
  result[2] = 0xBF;
  result[3] = 0x61;
  result[4] = 0x62;
  result[5] = 0x63;
  console.log("input num:");
  let retStr = textDecoder.decode( result , {stream: false});
  console.log("retStr = " + retStr);
  ```

## TextEncoder

Provides APIs to encode strings into byte arrays. It supports multiple formats, including UTF-8, UTF-16LE, and UTF-16BE. When **TextEncoder** is used for encoding, the number of bytes occupied by a character varies according to the encoding format. For example, a Chinese character usually occupies three bytes in UTF-8 encoding format but two bytes in UTF-16LE or UTF-16BE encoding format. Therefore, when using **TextEncoder**, you must explicitly specify the encoding format to obtain the required encoding result.

### Attributes

**System capability**: SystemCapability.Utils.Lang

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| encoding | string | Yes| No| Encoding format. The default format is **'utf-8'**.|


### constructor

constructor()

A constructor used to create a **TextEncoder** object.

**System capability**: SystemCapability.Utils.Lang

**Example**

  ```js
  let textEncoder = new util.TextEncoder();
  ```

### constructor<sup>9+</sup>

constructor(encoding?: string)

A constructor used to create a **TextEncoder** object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| ----- | ---- | ---- | ---- |
| encoding | string | No| Encoding format. The default format is **'utf-8'**.|

**Example**

  ```js
  let textEncoder = new util.TextEncoder("utf-8");
  ```

### encodeInto<sup>9+</sup>

encodeInto(input?: string): Uint8Array

Encodes the input content in to a Uint8Array object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| input  | string | No  | String to encode. The default value is an empty string.|

**Return value**

| Type      | Description              |
| ---------- | ------------------ |
| Uint8Array | Uint8Array object obtained.|

**Example**

  ```js
let textEncoder = new util.TextEncoder();
let buffer = new ArrayBuffer(20);
let result = new Uint8Array(buffer);
result = textEncoder.encodeInto("\uD800¥¥");
  ```

### encodeIntoUint8Array<sup>9+</sup>

encodeIntoUint8Array(input: string, dest: Uint8Array, ): { read: number; written: number }

Stores the UTF-8 encoded text.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type      | Mandatory| Description                                                   |
| ------ | ---------- | ---- | ------------------------------------------------------- |
| input  | string     | Yes  | String to encode.                                     |
| dest   | Uint8Array | Yes  | Uint8Array object used to store the UTF-8 encoded text.|

**Return value**

| Type      | Description              |
| ---------- | ------------------ |
| Uint8Array | Uint8Array object obtained.|

**Example**

  ```js
let that = new util.TextEncoder()
let buffer = new ArrayBuffer(4)
let dest = new Uint8Array(buffer)
let result = new Object()
result = that.encodeIntoUint8Array('abcd', dest)
  ```

### encodeInto<sup>(deprecated)</sup>

encodeInto(input: string, dest: Uint8Array, ): { read: number; written: number }

Stores the UTF-8 encoded text.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [encodeIntoUint8Array<sup>9+</sup>](#encodeintouint8array9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| input | string | Yes| String to encode.|
| dest | Uint8Array | Yes| Uint8Array object used to store the UTF-8 encoded text.|

**Return value**

| Type| Description|
| -------- | -------- |
| Uint8Array | Uint8Array object obtained.|

**Example**
  ```js
  let that = new util.TextEncoder()
  let buffer = new ArrayBuffer(4)
  let dest = new Uint8Array(buffer)
  let result = new Object()
  result = that.encodeInto('abcd', dest)
  ```

### encode<sup>(deprecated)</sup>

encode(input?: string): Uint8Array

Encodes the input content in to a Uint8Array object.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [encodeInto<sup>9+</sup>](#encodeinto9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| input | string | No| String to encode. The default value is an empty string.|

**Return value**

| Type| Description|
| -------- | -------- |
| Uint8Array | Uint8Array object obtained.|

**Example**
  ```js
  let textEncoder = new util.TextEncoder();
  let buffer = new ArrayBuffer(20);
  let result = new Uint8Array(buffer);
  result = textEncoder.encode("\uD800¥¥");
  ```

## RationalNumber<sup>8+</sup>

Provides APIs to compare rational numbers and obtain numerators and denominators. For example, the **toString()** API can be used to convert a rational number into a string.

### constructor<sup>9+</sup>

constructor()

A constructor used to create a **RationalNumber** object.

**System capability**: SystemCapability.Utils.Lang

**Example**

```js
let rationalNumber = new util.RationalNumber();
```

### parseRationalNumber<sup>9+</sup>

parseRationalNumber(numerator: number,denominator: number): RationalNumber

Parses a rational number. Previously, this processing is an internal action of the deprecated constructor.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name     | Type  | Mandatory| Description            |
| ----------- | ------ | ---- | ---------------- |
| numerator   | number | Yes  | Numerator, which is an integer.|
| denominator | number | Yes  | Denominator, which is an integer.|

**Example**

```js
let rationalNumber = util.RationalNumber.parseRationalNumber(1,2)
```

### createRationalFromString<sup>8+</sup>

static createRationalFromString​(rationalString: string): RationalNumber​

Creates a **RationalNumber** object based on the given string.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| rationalString | string | Yes| String used to create the **RationalNumber** object.|

**Return value**

| Type| Description|
| -------- | -------- |
| object | **RationalNumber** object created.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let rational = util.RationalNumber.createRationalFromString("3/4");
```

### compare<sup>9+</sup>

compare​(another: RationalNumber): number​

Compares this **RationalNumber** object with a given object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name | Type          | Mandatory| Description              |
| ------- | -------------- | ---- | ------------------ |
| another | RationalNumber | Yes  | Object used to compare with this **RationalNumber** object.|

**Return value**

| Type  | Description                                                        |
| ------ | ------------------------------------------------------------ |
| number | Returns **0** if the two objects are equal; returns **1** if the given object is less than this object; return **-1** if the given object is greater than this object.|

**Example**

  ```js
let rationalNumber = new util.RationalNumber(1,2);
let rational = util.RationalNumber.createRationalFromString("3/4");
let result = rationalNumber.compare(rational);
  ```

### valueOf<sup>8+</sup>

valueOf(): number

Obtains the value of this **RationalNumber** object as an integer or a floating-point number.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| number | An integer or a floating-point number.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.valueOf();
```

### equals<sup>8+</sup>

equals​(obj: Object): boolean

Checks whether this **RationalNumber** object equals the given object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| obj | Object | Yes| Object used to compare with this **RationalNumber** object.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the two objects are equal; returns **false** otherwise.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let rational = util.RationalNumber.createRationalFromString("3/4");
let result = rationalNumber.equals(rational);
```

### getCommonFactor<sup>9+</sup>

getCommonFactor(number1: number,number2: number): number

Obtains the greatest common divisor of two specified integers.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name | Type  | Mandatory| Description      |
| ------- | ------ | ---- | ---------- |
| number1 | number | Yes  | The first integer used to get the greatest common divisor.|
| number2 | number | Yes  | The second integer used to get the greatest common divisor.|

**Return value**

| Type  | Description                          |
| ------ | ------------------------------ |
| number | Greatest common divisor obtained.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let result = util.RationalNumber.getCommonFactor(4,6);
```

### getNumerator<sup>8+</sup>

getNumerator​(): number

Obtains the numerator of this **RationalNumber** object.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| number | Numerator of this **RationalNumber** object.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.getNumerator();
```

### getDenominator<sup>8+</sup>

getDenominator​(): number

Obtains the denominator of this **RationalNumber** object.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| number | Denominator of this **RationalNumber** object.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.getDenominator();
```

### isZero<sup>8+</sup>

isZero​():boolean

Checks whether this **RationalNumber** object is **0**.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the value of this **RationalNumber** object is **0**; returns **false** otherwise.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.isZero();
```

### isNaN<sup>8+</sup>

isNaN​(): boolean

Checks whether this **RationalNumber** object is a Not a Number (NaN).

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if this **RationalNumber** object is a NaN (the denominator and numerator are both **0**); returns **false** otherwise.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.isNaN();
```

### isFinite<sup>8+</sup>

isFinite​():boolean

Checks whether this **RationalNumber** object represents a finite value.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if this **RationalNumber** object represents a finite value (the denominator is not **0**); returns **false** otherwise.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.isFinite();
```

### toString<sup>8+</sup>

toString​(): string

Obtains the string representation of this **RationalNumber** object.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| string | Returns **NaN** if the numerator and denominator of this object are both **0**; returns a string in Numerator/Denominator format otherwise, for example, 3/5.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let result = rationalNumber.toString();
```

### constructor<sup>(deprecated)</sup>

constructor(numerator: number,denominator: number)

A constructor used to create a **RationalNumber** object.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [constructor<sup>9+</sup>](#constructor9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| numerator | number | Yes| Numerator, which is an integer.|
| denominator | number | Yes| Denominator, which is an integer.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
```

### compareTo<sup>(deprecated)</sup>

compareTo​(another: RationalNumber): number​

Compares this **RationalNumber** object with a given object.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [compare<sup>9+</sup>](#compare9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| another | RationalNumber | Yes| Object used to compare with this **RationalNumber** object.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | Returns **0** if the two objects are equal; returns **1** if the given object is less than this object; return **-1** if the given object is greater than this object.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let rational = util.RationalNumber.createRationalFromString("3/4");
let result = rationalNumber.compareTo(rational);
```

### getCommonDivisor<sup>(deprecated)</sup>

static getCommonDivisor​(number1: number,number2: number): number

Obtains the greatest common divisor of two specified integers.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [getCommonFactor<sup>9+</sup>](#getcommonfactor9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| number1 | number | Yes| The first integer used to get the greatest common divisor.|
| number2 | number | Yes| The second integer used to get the greatest common divisor.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | Greatest common divisor obtained.|

**Example**

```js
let rationalNumber = new util.RationalNumber(1,2);
let result = util.RationalNumber.getCommonDivisor(4,6);
```

## LRUCache<sup>9+</sup>

Provides APIs to discard the least recently used data to make rooms for new elements when the cache is full. This class uses the Least Recently Used (LRU) algorithm, which believes that the recently used data may be accessed again in the near future and the least accessed data is the least valuable data and should be removed from the cache.

### Attributes

**System capability**: SystemCapability.Utils.Lang

| Name  | Type  | Readable| Writable| Description                  |
| ------ | ------ | ---- | ---- | ---------------------- |
| length | number | Yes  | No  | Total number of values in this cache.|

**Example**

```js
let pro = new util.LRUCache();
pro.put(2,10);
pro.put(1,8);
let result = pro.length;
```

### constructor<sup>9+</sup>

constructor(capacity?: number)

A constructor used to create a **LruCache** instance. The default capacity of the cache is 64.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name  | Type  | Mandatory| Description                        |
| -------- | ------ | ---- | ---------------------------- |
| capacity | number | No  | New capacity of the cache.|

**Example**

```js
let lrubuffer= new util.LRUCache();
```


### updateCapacity<sup>9+</sup>

updateCapacity(newCapacity: number): void

Changes the cache capacity. If the new capacity is less than or equal to **0**, an exception will be thrown.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name     | Type  | Mandatory| Description                        |
| ----------- | ------ | ---- | ---------------------------- |
| newCapacity | number | Yes  | New capacity of the cache.|

**Example**

```js
let pro = new util.LRUCache();
pro.updateCapacity(100);
```


### toString<sup>9+</sup>

toString(): string

Obtains the string representation of this cache.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type  | Description                      |
| ------ | -------------------------- |
| string | String representation of this cache.|

**Example**

```js
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
pro.get(2);
pro.get(3);
console.log(pro.toString());
// Output: LRUCache[ maxSize = 64, hits = 1, misses = 1, hitRate = 50% ]
// maxSize: maximum size of the cache. hits: number of matched queries. misses: number of mismatched queries. hitRate: matching rate.
```

### getCapacity<sup>9+</sup>

getCapacity(): number

Obtains the capacity of this cache.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type  | Description                  |
| ------ | ---------------------- |
| number | Capacity of the cache.|

**Example**

  ```js
let pro = new util.LRUCache();
let result = pro.getCapacity();
  ```


### clear<sup>9+</sup>

clear(): void

Clears key-value pairs from this cache. The **afterRemoval()** method will be called to perform subsequent operations.

**System capability**: SystemCapability.Utils.Lang

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
let result = pro.length;
pro.clear();
  ```


### getCreateCount<sup>9+</sup>

getCreateCount(): number

Obtains the number of times that an object is created.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type  | Description               |
| ------ | -------------------|
| number | Number of times that objects are created.|

**Example**

```js
// Create the ChildLRUCache class that inherits LRUCache, and override createDefault() to return a non-undefined value.
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

Obtains the number of times that the queried values are mismatched.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type  | Description                    |
| ------ | ------------------------ |
| number | Number of times that the queried values are mismatched.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
pro.get(2);
let result = pro.getMissCount();
  ```


### getRemovalCount<sup>9+</sup>

getRemovalCount(): number

Obtains the number of times that key-value pairs in the cache are recycled.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type  | Description                      |
| ------ | -------------------------- |
| number | Number of times that key-value pairs in the cache are recycled.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
pro.updateCapacity(2);
pro.put(50,22);
let result = pro.getRemovalCount();
  ```


### getMatchCount<sup>9+</sup>

getMatchCount(): number

Obtains the number of times that the queried values are matched.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type  | Description                      |
| ------ | -------------------------- |
| number | Number of times that the queried values are matched.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
pro.get(2);
let result = pro.getMatchCount();
  ```


### getPutCount<sup>9+</sup>

getPutCount(): number

Obtains the number of additions to this cache.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type  | Description                        |
| ------ | ---------------------------- |
| number | Number of additions to the cache.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
let result = pro.getPutCount();
  ```


### isEmpty<sup>9+</sup>

isEmpty(): boolean

Checks whether this cache is empty.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type   | Description                                    |
| ------- | ---------------------------------------- |
| boolean | Returns **true** if the cache does not contain any value.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
let result = pro.isEmpty();
  ```


### get<sup>9+</sup>

get(key: K): V | undefined

Obtains the value of the specified key.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description        |
| ------ | ---- | ---- | ------------ |
| key    | K    | Yes  | Key based on which the value is queried.|

**Return value**

| Type                    | Description                                                        |
| ------------------------ | ------------------------------------------------------------ |
| V \| undefined | Returns the value of the key if a match is found in the cache; returns **undefined** otherwise.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
let result  = pro.get(2);
  ```


### put<sup>9+</sup>

put(key: K,value: V): V

Adds a key-value pair to this cache.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description                      |
| ------ | ---- | ---- | -------------------------- |
| key    | K    | Yes  | Key of the key-value pair to add.            |
| value  | V    | Yes  | Value of the key-value pair to add.|

**Return value**

| Type| Description                                                        |
| ---- | ------------------------------------------------------------ |
| V    | Returns the existing value if the key already exists; returns the value added otherwise; throws an error if **null** is passed in for **key** or **value**.|

**Example**

  ```js
let pro = new util.LRUCache();
let result = pro.put(2,10);
  ```

### values<sup>9+</sup>

values(): V[]

Obtains all values in this cache, listed from the most to the least recently accessed.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type     | Description                                                        |
| --------- | ------------------------------------------------------------ |
| V&nbsp;[] | All values in the cache, listed from the most to the least recently accessed.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
pro.put(2,"anhu");
pro.put("afaf","grfb");
let result = pro.values();
  ```


### keys<sup>9+</sup>

keys(): K[]

Obtains all keys in this cache, listed from the most to the least recently accessed.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type     | Description                                                        |
| --------- | ------------------------------------------------------------ |
| K&nbsp;[] | All keys in the cache, listed from the most to the least recently accessed.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
let result = pro.keys();
  ```


### remove<sup>9+</sup>

remove(key: K): V | undefined

Removes the specified key and its value from this cache.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description          |
| ------ | ---- | ---- | -------------- |
| key    | K    | Yes  | Key to remove.|

**Return value**

| Type                    | Description                                                        |
| ------------------------ | ------------------------------------------------------------ |
| V&nbsp;\|&nbsp;undefined | Returns an **Optional** object containing the removed key-value pair if the key exists in the cache; returns an empty **Optional** object otherwise; throws an error if **null** is passed in for **key**.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
let result = pro.remove(20);
  ```


### afterRemoval<sup>9+</sup>

afterRemoval(isEvict: boolean,key: K,value: V,newValue: V): void

Performs subsequent operations after a value is removed.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name  | Type   | Mandatory| Description                                                        |
| -------- | ------- | ---- | ------------------------------------------------------------ |
| isEvict  | boolean | Yes  | Whether the capacity is insufficient. If the value is **true**, this API is called due to insufficient capacity.   |
| key      | K       | Yes  | Key removed.                                              |
| value    | V       | Yes  | Value removed.                                              |
| newValue | V       | Yes  | New value for the key if the **put()** method is called and the key to be added already exists. In other cases, this parameter is left blank.|

**Example**

```js
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

Checks whether this cache contains the specified key.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type  | Mandatory| Description            |
| ------ | ------ | ---- | ---------------- |
| key    | K | Yes  | Key to check.|

**Return value**

| Type   | Description                                      |
| ------- | ------------------------------------------ |
| boolean | Returns **true** if the cache contains the specified key; returns **false** otherwise.|

**Example**

  ```js
let pro = new util.LRUCache();
pro.put(2,10);
let obj = {1:"key"};
let result = pro.contains(obj);
  ```


### createDefault<sup>9+</sup>

createDefault(key: K): V

Creates a value if the value of the specified key is not available.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description          |
| ------ | ---- | ---- | -------------- |
| key    | K    | Yes  | Key of which the value is missing.|

**Return value**

| Type| Description              |
| ---- | ------------------ |
| V    | Value of the key.|

**Example**

  ```js
let pro = new util.LRUCache();
let result = pro.createDefault(50);
  ```


### entries<sup>9+</sup>

entries(): IterableIterator&lt;[K,V]&gt;

Obtains a new iterator object that contains all key-value pairs in this object.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type       | Description                |
| ----------- | -------------------- |
| [K,&nbsp;V] | Iterable array.|

**Example**

```js
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
pro.put(3,15);
let pair:Iterable<Object[]> = pro.entries();
let arrayValue = Array.from(pair);
for (let value of arrayValue) {
  console.log(value[0]+ ', '+ value[1]);
}
```

### [Symbol.iterator]<sup>9+</sup>

[Symbol.iterator]\(): IterableIterator&lt;[K, V]&gt;

Obtains a two-dimensional array in key-value pairs.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type       | Description                          |
| ----------- | ------------------------------ |
| [K,&nbsp;V] | Two-dimensional array in key-value pairs.|

**Example**

```js
let pro: util.LRUCache<number, number> = new util.LRUCache();
pro.put(2,10);
pro.put(3,15);
let pair:Iterable<Object[]> = pro[Symbol.iterator]();
let arrayValue = Array.from(pair);
for (let value of arrayValue) {
  console.log(value[0]+ ', '+ value[1]);
}
```

## ScopeComparable<sup>8+</sup>

The values of the **ScopeComparable** type are used to implement the **compareTo** method. Therefore, ensure that the input parameters are comparable.

**System capability**: SystemCapability.Utils.Lang

### compareTo<sup>8+</sup>

compareTo(other: ScopeComparable): boolean

Compares two values and returns a Boolean value.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description          |
| ------ | ---- | ---- | -------------- |
| other  | [ScopeComparable](#scopecomparable8) | Yes | The other value to be compared with the current value.|

**Return value**

| Type| Description              |
| ---- | ------------------ |
| boolean | If the current value is greater than or equal to the input value, **true** is returned. Otherwise, **false** is returned.|

**Example**

Create a class to implement the **compareTo** method. The **Temperature** class is used as an example in the following sample code.

```js
class Temperature{
    // If ArkTS is used for development, add the following code:
    // private readonly _temp: Temperature;
    constructor(value) {
       this._temp = value;
    }
    compareTo(value) {
       return this._temp >= value.getTemp();
    }
    getTemp() {
       return this._temp;
    }
    toString() {
       return this._temp.toString();
    }
}
```

## ScopeType<sup>8+</sup>

Defines the type of values in a **Scope** object.

**System capability**: SystemCapability.Utils.Lang

| Type| Description|
| -------- | -------- |
| number | The value type is a number.|
| [ScopeComparable](#scopecomparable8) | The value type is ScopeComparable.|

## ScopeHelper<sup>9+</sup>

Provides APIs to define the valid range of a field. The constructor of this class creates comparable objects with lower and upper limits.

### constructor<sup>9+</sup>

constructor(lowerObj: ScopeType, upperObj: ScopeType)

A constructor used to create a **ScopeHelper** object with the specified upper and lower limits.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name  | Type                    | Mandatory| Description                  |
| -------- | ------------------------ | ---- | ---------------------- |
| lowerObj | [ScopeType](#scopetype8) | Yes  | Lower limit of the **Scope** object.|
| upperObj | [ScopeType](#scopetype8) | Yes  | Upper limit of the **Scope** object.|

**Example**

  ```js
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
  ```


### toString<sup>9+</sup>

toString(): string

Obtains a string representation that contains this **Scope**.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type  | Description                                  |
| ------ | -------------------------------------- |
| string | String representation containing the **Scope**.|

**Example**

  ```js
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.toString();
  ```


### intersect<sup>9+</sup>

intersect(range: ScopeHelper): ScopeHelper

Obtains the intersection of this **Scope** and the given **Scope**.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type                        | Mandatory| Description              |
| ------ | ---------------------------- | ---- | ------------------ |
| range  | [ScopeHelper](#scopehelper9) | Yes  | **Scope** specified.|

**Return value**

| Type                          | Description                          |
| ------------------------------ | ------------------------------ |
| [ScopeHelper](#scopehelper9) | Intersection of this **Scope** and the given **Scope**.|

**Example**

  ```js
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

Obtains the intersection of this **Scope** and the given lower and upper limits.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name  | Type                    | Mandatory| Description            |
| -------- | ------------------------ | ---- | ---------------- |
| lowerObj | [ScopeType](#scopetype8) | Yes  | Lower limit.|
| upperObj | [ScopeType](#scopetype8) | Yes  | Upper limit.|

**Return value**

| Type                        | Description                                    |
| ---------------------------- | ---------------------------------------- |
| [ScopeHelper](#scopehelper9) | Intersection of this **Scope** and the given lower and upper limits.|

**Example**

  ```js
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let tempMidS = new Temperature(39);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.intersect(tempMiDF, tempMidS);
  ```


### getUpper<sup>9+</sup>

getUpper(): ScopeType

Obtains the upper limit of this **Scope**.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type                    | Description                  |
| ------------------------ | ---------------------- |
| [ScopeType](#scopetype8) | Upper limit of this **Scope**.|

**Example**

  ```js
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.getUpper();
  ```


### getLower<sup>9+</sup>

getLower(): ScopeType

Obtains the lower limit of this **Scope**.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type                    | Description                  |
| ------------------------ | ---------------------- |
| [ScopeType](#scopetype8) | Lower limit of this **Scope**.|

**Example**

  ```js
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.getLower();
  ```


### expand<sup>9+</sup>

expand(lowerObj: ScopeType,upperObj: ScopeType): ScopeHelper

Obtains the union set of this **Scope** and the given lower and upper limits.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name  | Type                    | Mandatory| Description            |
| -------- | ------------------------ | ---- | ---------------- |
| lowerObj | [ScopeType](#scopetype8) | Yes  | Lower limit.|
| upperObj | [ScopeType](#scopetype8) | Yes  | Upper limit.|

**Return value**

| Type                        | Description                                |
| ---------------------------- | ------------------------------------ |
| [ScopeHelper](#scopehelper9) | Union set of this **Scope** and the given lower and upper limits.|

**Example**

  ```js
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let tempMidS = new Temperature(39);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.expand(tempMiDF, tempMidS);
  ```


### expand<sup>9+</sup>

expand(range: ScopeHelper): ScopeHelper

Obtains the union set of this **Scope** and the given **Scope**.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type                        | Mandatory| Description              |
| ------ | ---------------------------- | ---- | ------------------ |
| range  | [ScopeHelper](#scopehelper9) | Yes  | **Scope** specified.|

**Return value**

| Type                        | Description                              |
| ---------------------------- | ---------------------------------- |
| [ScopeHelper](#scopehelper9) | Union set of this **Scope** and the given **Scope**.|

**Example**

  ```js
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

Obtains the union set of this **Scope** and the given value.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type                    | Mandatory| Description            |
| ------ | ------------------------ | ---- | ---------------- |
| value  | [ScopeType](#scopetype8) | Yes  | Value specified.|

**Return value**

| Type                        | Description                            |
| ---------------------------- | -------------------------------- |
| [ScopeHelper](#scopehelper9) | Union set of this **Scope** and the given value.|

**Example**

  ```js
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.expand(tempMiDF);
  ```


### contains<sup>9+</sup>

contains(value: ScopeType): boolean

Checks whether a value is within this **Scope**.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type                    | Mandatory| Description            |
| ------ | ------------------------ | ---- | ---------------- |
| value  | [ScopeType](#scopetype8) | Yes  | Value specified.|

**Return value**

| Type   | Description                                               |
| ------- | --------------------------------------------------- |
| boolean | Returns **true** if the value is within this **Scope**; returns **false** otherwise.|

**Example**

  ```js
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.contains(tempMiDF);
  ```


### contains<sup>9+</sup>

contains(range: ScopeHelper): boolean

Checks whether a range is within this **Scope**.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type                        | Mandatory| Description              |
| ------ | ---------------------------- | ---- | ------------------ |
| range  | [ScopeHelper](#scopehelper9) | Yes  | **Scope** specified.|

**Return value**

| Type   | Description                                                 |
| ------- | ----------------------------------------------------- |
| boolean | Returns **true** if the range is within this **Scope**; returns **false** otherwise.|

**Example**

  ```js
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

Limits a value to this **Scope**.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type                    | Mandatory| Description          |
| ------ | ------------------------ | ---- | -------------- |
| value  | [ScopeType](#scopetype8) | Yes  | Value specified.|

**Return value**

| Type                    | Description                                                        |
| ------------------------ | ------------------------------------------------------------ |
| [ScopeType](#scopetype8) | Returns **lowerObj** if the specified value is less than the lower limit; returns **upperObj** if the specified value is greater than the upper limit; returns the specified value if it is within this **Scope**.|

**Example**

  ```js
let tempLower = new Temperature(30);
let tempUpper = new Temperature(40);
let tempMiDF = new Temperature(35);
let range = new util.ScopeHelper(tempLower, tempUpper);
let result = range.clamp(tempMiDF);
  ```

## Base64Helper<sup>9+</sup>

The Base64 encoding table contains 62 characters, which are the uppercase letters (A-Z), lowercase letters (a-z), digits (0-9), and the special characters plus sign (+) and slash (/). During encoding, the original data is divided into groups of three bytes, and each group contains a 6-bit number. Then, the corresponding characters in the Base64 encoding table are used to represent these numbers. If the last group contains only one or two bytes, the equal sign (=) is used for padding.

### constructor<sup>9+</sup>

constructor()

A constructor used to create a **Base64Helper** instance.

**System capability**: SystemCapability.Utils.Lang

**Example**

  ```js
let base64 = new  util.Base64Helper();
  ```

### encodeSync<sup>9+</sup>

encodeSync(src: Uint8Array): Uint8Array

Encodes the input content in to a Uint8Array object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type      | Mandatory| Description               |
| ------ | ---------- | ---- | ------------------- |
| src    | Uint8Array | Yes  | Uint8Array object to encode.|

**Return value**

| Type      | Description                         |
| ---------- | ----------------------------- |
| Uint8Array | Uint8Array object obtained.|

**Example**

  ```js
let that = new util.Base64Helper();
let array = new Uint8Array([115,49,51]);
let result = that.encodeSync(array);
  ```


### encodeToStringSync<sup>9+</sup>

encodeToStringSync(src: Uint8Array): string

Encodes the input content in to a Uint8Array object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type      | Mandatory| Description               |
| ------ | ---------- | ---- | ------------------- |
| src    | Uint8Array | Yes  | Uint8Array object to encode.|

**Return value**

| Type  | Description                |
| ------ | -------------------- |
| string | String obtained.|

**Example**

  ```js
let that = new util.Base64Helper();
let array = new Uint8Array([115,49,51]);
let result = that.encodeToStringSync(array);
  ```


### decodeSync<sup>9+</sup>

decodeSync(src: Uint8Array | string): Uint8Array

Decodes the input content into a string.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type                          | Mandatory| Description                         |
| ------ | ------------------------------ | ---- | ----------------------------- |
| src    | Uint8Array&nbsp;\|&nbsp;string | Yes  | Uint8Array object or string to decode.|

**Return value**

| Type      | Description                         |
| ---------- | ----------------------------- |
| Uint8Array | Uint8Array object obtained.|

**Example**

  ```js
let that = new util.Base64Helper();
let buff = 'czEz';
let result = that.decodeSync(buff);
  ```


### encode<sup>9+</sup>

encode(src: Uint8Array): Promise&lt;Uint8Array&gt;

Encodes the input content into a string. This API uses a promise to return the result.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type      | Mandatory| Description                   |
| ------ | ---------- | ---- | ----------------------- |
| src    | Uint8Array | Yes  | Uint8Array object to encode.|

**Return value**

| Type                     | Description                             |
| ------------------------- | --------------------------------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the Uint8Array object obtained.|

**Example**

  ```js
let that = new util.Base64Helper();
let array = new Uint8Array([115,49,51]);
let rarray = new Uint8Array([99,122,69,122]);
that.encode(array).then(val=>{    
    for (var i = 0; i < rarray.length; i++) {        
        console.log(val[i].toString())
    }
})
  ```


### encodeToString<sup>9+</sup>

encodeToString(src: Uint8Array): Promise&lt;string&gt;

Encodes the input content into a string. This API uses a promise to return the result.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type      | Mandatory| Description                   |
| ------ | ---------- | ---- | ----------------------- |
| src    | Uint8Array | Yes  | Uint8Array object to encode.|

**Return value**

| Type                 | Description                    |
| --------------------- | ------------------------ |
| Promise&lt;string&gt; | Promise used to return the string obtained.|

**Example**

  ```js
let that = new util.Base64Helper();
let array = new Uint8Array([115,49,51]);
that.encodeToString(array).then(val=>{    
    console.log(val)
})
  ```


### decode<sup>9+</sup>

decode(src: Uint8Array | string): Promise&lt;Uint8Array&gt;

Decodes the input content into a Uint8Array object. This API uses a promise to return the result.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type                          | Mandatory| Description                             |
| ------ | ------------------------------ | ---- | --------------------------------- |
| src    | Uint8Array&nbsp;\|&nbsp;string | Yes  | Uint8Array object or string to decode.|

**Return value**

| Type                     | Description                             |
| ------------------------- | --------------------------------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the Uint8Array object obtained.|

**Example**

  ```js
let that = new util.Base64Helper();
let array = new Uint8Array([99,122,69,122]);
let rarray = new Uint8Array([115,49,51]);
that.decode(array).then(val=>{    
    for (var i = 0; i < rarray.length; i++) {        
        console.log(val[i].toString())
    }
})
  ```

## types<sup>8+</sup>

Provides APIs to check different types of built-in objects, such as ArrayBuffer, Map, and Set, so as to avoid exceptions or crashes caused by type errors.

### constructor<sup>8+</sup>

constructor()

A constructor used to create a **Types** object.

**System capability**: SystemCapability.Utils.Lang

**Example**

  ```js
  let type = new util.types();
  ```


### isAnyArrayBuffer<sup>8+</sup>

isAnyArrayBuffer(value: Object): boolean

Checks whether the input value is of the ArrayBuffer type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the ArrayBuffer type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isAnyArrayBuffer(new ArrayBuffer(0));
  ```


### isArrayBufferView<sup>8+</sup>

isArrayBufferView(value: Object): boolean

Checks whether the input value is of the ArrayBufferView type.

**ArrayBufferView** is a helper type representing any of the following: Int8Array, Int16Array, Int32Array, Uint8Array, Uint8ClampedArray, Uint32Array, Float32Array, **Float64Array**, and DataView.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the ArrayBufferView type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isArrayBufferView(new Int8Array([]));
  ```


### isArgumentsObject<sup>8+</sup>

isArgumentsObject(value: Object): boolean

Checks whether the input value is of the arguments type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the arguments type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  function foo() {
      var result = that.isArgumentsObject(arguments);
  }
  let f = foo();
  ```


### isArrayBuffer<sup>8+</sup>

isArrayBuffer(value: Object): boolean

Checks whether the input value is of the ArrayBuffer type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the ArrayBuffer type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isArrayBuffer(new ArrayBuffer(0));
  ```


### isAsyncFunction<sup>8+</sup>

isAsyncFunction(value: Object): boolean

Checks whether the input value is an asynchronous function.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is an asynchronous function; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isAsyncFunction(async function foo() {});
  ```


### isBooleanObject<sup>8+</sup>

isBooleanObject(value: Object): boolean

Checks whether the input value is of the Boolean type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Boolean type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isBooleanObject(new Boolean(true));
  ```


### isBoxedPrimitive<sup>8+</sup>

isBoxedPrimitive(value: Object): boolean

Checks whether the input value is of the Boolean, Number, String, or Symbol type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Boolean, Number, String, or Symbol type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isBoxedPrimitive(new Boolean(false));
  ```


### isDataView<sup>8+</sup>

isDataView(value: Object): boolean

Checks whether the input value is of the DataView type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the DataView type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  const ab = new ArrayBuffer(20);
  let result = that.isDataView(new DataView(ab));
  ```


### isDate<sup>8+</sup>

isDate(value: Object): boolean

Checks whether the input value is of the Date type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Date type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isDate(new Date());
  ```


### isExternal<sup>8+</sup>

isExternal(value: Object): boolean

Checks whether the input value is of the native external type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the native external type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isExternal(true);
  ```


### isFloat32Array<sup>8+</sup>

isFloat32Array(value: Object): boolean

Checks whether the input value is of the Float32Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Float32Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isFloat32Array(new Float32Array());
  ```


### isFloat64Array<sup>8+</sup>

isFloat64Array(value: Object): boolean

Checks whether the input value is of the Float64Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Float64Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isFloat64Array(new Float64Array());
  ```


### isGeneratorFunction<sup>8+</sup>

isGeneratorFunction(value: Object): boolean

Checks whether the input value is a generator function.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is a generator function; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isGeneratorFunction(function* foo() {});
  ```


### isGeneratorObject<sup>8+</sup>

isGeneratorObject(value: Object): boolean

Checks whether the input value is a generator object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is a generator object; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  function* foo() {}
  const generator = foo();
  let result = that.isGeneratorObject(generator);
  ```


### isInt8Array<sup>8+</sup>

isInt8Array(value: Object): boolean

Checks whether the input value is of the Int8Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Int8Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isInt8Array(new Int8Array([]));
  ```


### isInt16Array<sup>8+</sup>

isInt16Array(value: Object): boolean

Checks whether the input value is of the Int16Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Int16Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isInt16Array(new Int16Array([]));
  ```


### isInt32Array<sup>8+</sup>

isInt32Array(value: Object): boolean

Checks whether the input value is of the Int32Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Int32Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isInt32Array(new Int32Array([]));
  ```


### isMap<sup>8+</sup>

isMap(value: Object): boolean

Checks whether the input value is of the Map type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Map type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isMap(new Map());
  ```


### isMapIterator<sup>8+</sup>

isMapIterator(value: Object): boolean

Checks whether the input value is of the MapIterator type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**


| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the MapIterator type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  const map = new Map();
  let result = that.isMapIterator(map.keys());
  ```


### isNativeError<sup>8+</sup>

isNativeError(value: Object): boolean

Checks whether the input value is of the Error type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Error type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isNativeError(new TypeError());
  ```


### isNumberObject<sup>8+</sup>

isNumberObject(value: Object): boolean

Checks whether the input value is a number object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is a number object; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isNumberObject(new Number(0));
  ```


### isPromise<sup>8+</sup>

isPromise(value: Object): boolean

Checks whether the input value is a promise.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is a promise; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isPromise(Promise.resolve(1));
  ```


### isProxy<sup>8+</sup>

isProxy(value: Object): boolean

Checks whether the input value is a proxy.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is a proxy; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  const target = {};
  const proxy = new Proxy(target, {});
  let result = that.isProxy(proxy);
  ```


### isRegExp<sup>8+</sup>

isRegExp(value: Object): boolean

Checks whether the input value is of the RegExp type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the RegExp type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isRegExp(new RegExp('abc'));
  ```


### isSet<sup>8+</sup>

isSet(value: Object): boolean

Checks whether the input value is of the Set type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Set type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isSet(new Set());
  ```


### isSetIterator<sup>8+</sup>

isSetIterator(value: Object): boolean

Checks whether the input value is of the SetIterator type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the SetIterator type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  const set = new Set();
  let result = that.isSetIterator(set.keys());
  ```


### isStringObject<sup>8+</sup>

isStringObject(value: Object): boolean

Checks whether the input value is a string object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is a string object; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isStringObject(new String('foo'));
  ```


### isSymbolObjec<sup>8+</sup>

isSymbolObject(value: Object): boolean

Checks whether the input value is a symbol object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is a symbol object; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  const symbols = Symbol('foo');
  let result = that.isSymbolObject(Object(symbols));
  ```


### isTypedArray<sup>8+</sup>

isTypedArray(value: Object): boolean

Checks whether the input value is of the TypedArray type.

**TypedArray** is a helper type representing any of the following: Int8Array, Int16Array, Int32Array, Uint8Array, Uint8ClampedArray, Uint16Array, Uint32Array, Float32Array, Float64Array, and DataView.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the TypedArray type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isTypedArray(new Float64Array([]));
  ```


### isUint8Array<sup>8+</sup>

isUint8Array(value: Object): boolean

Checks whether the input value is of the Uint8Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Uint8Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isUint8Array(new Uint8Array([]));
  ```


### isUint8ClampedArray<sup>8+</sup>

isUint8ClampedArray(value: Object): boolean

Checks whether the input value is of the Uint8ClampedArray type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Uint8ClampedArray type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isUint8ClampedArray(new Uint8ClampedArray([]));
  ```


### isUint16Array<sup>8+</sup>

isUint16Array(value: Object): boolean

Checks whether the input value is of the Uint16Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Uint16Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isUint16Array(new Uint16Array([]));
  ```


### isUint32Array<sup>8+</sup>

isUint32Array(value: Object): boolean

Checks whether the input value is of the Uint32Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the Uint32Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isUint32Array(new Uint32Array([]));
  ```


### isWeakMap<sup>8+</sup>

isWeakMap(value: Object): boolean

Checks whether the input value is of the WeakMap type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the WeakMap type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isWeakMap(new WeakMap());
  ```


### isWeakSet<sup>8+</sup>

isWeakSet(value: Object): boolean

Checks whether the input value is of the WeakSet type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the WeakSet type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isWeakSet(new WeakSet());
  ```


### isBigInt64Array<sup>8+</sup>

isBigInt64Array(value: Object): boolean

Checks whether the input value is of the BigInt64Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the BigInt64Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isBigInt64Array(new BigInt64Array([]));
  ```


### isBigUint64Array<sup>8+</sup>

isBigUint64Array(value: Object): boolean

Checks whether the input value is of the BigUint64Array type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the BigUint64Array type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isBigUint64Array(new BigUint64Array([]));
  ```


### isModuleNamespaceObject<sup>8+</sup>

isModuleNamespaceObject(value: Object): boolean

Checks whether the input value is a module namespace object.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is a module namespace object; returns **false** otherwise.|

**Example**

  ```js
  import url from '@ohos.url'
  let that = new util.types();
  let result = that.isModuleNamespaceObject(url);
  ```


### isSharedArrayBuffer<sup>8+</sup>

isSharedArrayBuffer(value: Object): boolean

Checks whether the input value is of the SharedArrayBuffer type.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | Object | Yes| Object to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the input value is of the SharedArrayBuffer type; returns **false** otherwise.|

**Example**

  ```js
  let that = new util.types();
  let result = that.isSharedArrayBuffer(new SharedArrayBuffer(0));
  ```

## LruBuffer<sup>(deprecated)</sup>

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache<sup>9+</sup>](#lrucache9) instead.

### Attributes

**System capability**: SystemCapability.Utils.Lang

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| length | number | Yes| No| Total number of values in this cache.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  pro.put(1,8);
  let result = pro.length;
  ```

### constructor<sup>(deprecated)</sup>

constructor(capacity?: number)

A constructor used to create a **LruBuffer** instance. The default capacity of the cache is 64.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.constructor<sup>9+</sup>](#constructor9-3) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| capacity | number | No| New capacity of the cache.|

**Example**

  ```js
  let lrubuffer= new util.LruBuffer();
  ```

### updateCapacity<sup>(deprecated)</sup>

updateCapacity(newCapacity: number): void

Changes the cache capacity. If the new capacity is less than or equal to **0**, an exception will be thrown.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.updateCapacity<sup>9+</sup>](#updatecapacity9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| newCapacity | number | Yes| New capacity of the cache.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.updateCapacity(100);
  ```

### toString<sup>(deprecated)</sup>

toString(): string

Obtains the string representation of this cache.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.toString<sup>9+</sup>](#tostring9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| string | String representation of this cache.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  pro.get(2);
  pro.remove(20);
  let result = pro.toString();
  ```

### getCapacity<sup>(deprecated)</sup>

getCapacity(): number

Obtains the capacity of this cache.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.getCapacity<sup>9+</sup>](#getcapacity9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| number | Capacity of the cache.|

**Example**
  ```js
  let pro = new util.LruBuffer();
  let result = pro.getCapacity();
  ```

### clear<sup>(deprecated)</sup>

clear(): void

Clears key-value pairs from this cache. The **afterRemoval()** method will be called to perform subsequent operations.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.clear<sup>9+</sup>](#clear9) instead.

**System capability**: SystemCapability.Utils.Lang

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.length;
  pro.clear();
  ```

### getCreateCount<sup>(deprecated)</sup>

getCreateCount(): number

Obtains the number of return values for **createDefault()**.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.getCreateCount<sup>9+</sup>](#getcreatecount9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| number | Number of return values for **createDefault()**.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(1,8);
  let result = pro.getCreateCount();
  ```

### getMissCount<sup>(deprecated)</sup>

getMissCount(): number

Obtains the number of times that the queried values are mismatched.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.getMissCount<sup>9+</sup>](#getmisscount9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| number | Number of times that the queried values are mismatched.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  pro.get(2);
  let result = pro.getMissCount();
  ```

### getRemovalCount<sup>(deprecated)</sup>

getRemovalCount(): number

Obtains the number of removals from this cache.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.getRemovalCount<sup>9+</sup>](#getremovalcount9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| number | Number of removals from the cache.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  pro.updateCapacity(2);
  pro.put(50,22);
  let result = pro.getRemovalCount();
  ```

### getMatchCount<sup>(deprecated)</sup>

getMatchCount(): number

Obtains the number of times that the queried values are matched.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.getMatchCount<sup>9+</sup>](#getmatchcount9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| number | Number of times that the queried values are matched.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  pro.get(2);
  let result = pro.getMatchCount();
  ```

### getPutCount<sup>(deprecated)</sup>

getPutCount(): number

Obtains the number of additions to this cache.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.getPutCount<sup>9+</sup>](#getputcount9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| number | Number of additions to the cache.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.getPutCount();
  ```

### isEmpty<sup>(deprecated)</sup>

isEmpty(): boolean

Checks whether this cache is empty.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.isEmpty<sup>9+</sup>](#isempty9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the cache does not contain any value.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.isEmpty();
  ```

### get<sup>(deprecated)</sup>

get(key: K): V | undefined

Obtains the value of the specified key.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.get<sup>9+</sup>](#get9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| key | K | Yes| Key based on which the value is queried.|

**Return value**

| Type| Description|
| -------- | -------- |
| V&nbsp;\|&nbsp;undefined | Returns the value of the key if a match is found in the cache; returns **undefined** otherwise.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  let result  = pro.get(2);
  ```

### put<sup>(deprecated)</sup>

put(key: K,value: V): V

Adds a key-value pair to this cache.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.put<sup>9+</sup>](#put9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| key | K | Yes| Key of the key-value pair to add.|
| value | V | Yes| Value of the key-value pair to add.|

**Return value**

| Type| Description|
| -------- | -------- |
| V | Returns the existing value if the key already exists; returns the value added otherwise; throws an error if **null** is passed in for **key** or **value**.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  let result = pro.put(2,10);
  ```

### values<sup>(deprecated)</sup>

values(): V[]

Obtains all values in this cache, listed from the most to the least recently accessed.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.values<sup>9+</sup>](#values9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| V&nbsp;[] | All values in the cache, listed from the most to the least recently accessed.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  pro.put(2,"anhu");
  pro.put("afaf","grfb");
  let result = pro.values();
  ```

### keys<sup>(deprecated)</sup>

keys(): K[]

Obtains all keys in this cache, listed from the most to the least recently accessed.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.keys<sup>9+</sup>](#keys9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| K&nbsp;[] | All keys in the cache, listed from the most to the least recently accessed.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.keys();
  ```

### remove<sup>(deprecated)</sup>

remove(key: K): V | undefined

Removes the specified key and its value from this cache.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.remove<sup>9+</sup>](#remove9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| key | K | Yes| Key to remove.|

**Return value**

| Type| Description|
| -------- | -------- |
| V&nbsp;\|&nbsp;undefined | Returns an **Optional** object containing the removed key-value pair if the key exists in the cache; returns an empty **Optional** object otherwise; throws an error if **null** is passed in for **key**.|

**Example**
  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.remove(20);
  ```

### afterRemoval<sup>(deprecated)</sup>

afterRemoval(isEvict: boolean,key: K,value: V,newValue: V): void

Performs subsequent operations after a value is removed.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.afterRemoval<sup>9+</sup>](#afterremoval9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| isEvict | boolean | Yes| Whether the capacity is insufficient. If the value is **true**, this API is called due to insufficient capacity.|
| key | K | Yes| Key removed.|
| value | V | Yes| Value removed.|
| newValue | V | Yes| New value for the key if the **put()** method is called and the key to be added already exists. In other cases, this parameter is left blank.|

**Example**

```js
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

Checks whether this cache contains the specified key.


> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.contains<sup>9+</sup>](#contains9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| key | K | Yes| Key to check.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the cache contains the specified key; returns **false** otherwise.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.contains(20);
  ```

### createDefault<sup>(deprecated)</sup>

createDefault(key: K): V

Creates a value if the value of the specified key is not available.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.createDefault<sup>9+</sup>](#createdefault9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| key | K | Yes| Key of which the value is missing.|

**Return value**

| Type| Description|
| -------- | -------- |
| V | Value of the key.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  let result = pro.createDefault(50);
  ```

### entries<sup>(deprecated)</sup>

entries(): IterableIterator&lt;[K,V]&gt;

Obtains a new iterator object that contains all key-value pairs in this object.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.entries<sup>9+</sup>](#entries9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| [K,&nbsp;V] | Iterable array.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  let result = pro.entries();
  ```

### [Symbol.iterator]<sup>(deprecated)</sup>

[Symbol.iterator]\(): IterableIterator&lt;[K, V]&gt;

Obtains a two-dimensional array in key-value pairs.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [LRUCache.Symbol.iterator<sup>9+</sup>](#symboliterator9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| [K,&nbsp;V] | Two-dimensional array in key-value pairs.|

**Example**

  ```js
  let pro = new util.LruBuffer();
  pro.put(2,10);
  let result = pro[Symbol.iterator]();
  ```

## Scope<sup>(deprecated)</sup>

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper<sup>9+</sup>](#scopehelper9) instead.

### constructor<sup>(deprecated)</sup>

constructor(lowerObj: ScopeType, upperObj: ScopeType)

A constructor used to create a **Scope** object with the specified upper and lower limits.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.constructor<sup>9+</sup>](#constructor9-4) instead.


**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| lowerObj | [ScopeType](#scopetype8) | Yes| Lower limit of the **Scope** object.|
| upperObj | [ScopeType](#scopetype8) | Yes| Upper limit of the **Scope** object.|

**Example**
  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  ```

### toString<sup>(deprecated)</sup>

toString(): string

Obtains a string representation that contains this **Scope**.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.toString<sup>9+</sup>](#tostring9-1) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| string | String representation containing the **Scope**.|

**Example**

  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.toString();
  ```

### intersect<sup>(deprecated)</sup>

intersect(range: Scope): Scope

Obtains the intersection of this **Scope** and the given **Scope**.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.intersect<sup>9+</sup>](#intersect9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| range | [Scope](#scopedeprecated) | Yes| **Scope** specified.|

**Return value**

| Type| Description|
| -------- | -------- |
| [Scope](#scopedeprecated) | Intersection of this **Scope** and the given **Scope**.|

**Example**

  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  let tempMiDF = new Temperature(35);
  let tempMidS = new Temperature(39);
  let rangeFir = new util.Scope(tempMiDF, tempMidS);
  range.intersect(rangeFir );
  ```

### intersect<sup>(deprecated)</sup>

intersect(lowerObj:ScopeType,upperObj:ScopeType):Scope

Obtains the intersection of this **Scope** and the given lower and upper limits.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.intersect<sup>9+</sup>](#intersect9-1) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| lowerObj | [ScopeType](#scopetype8) | Yes| Lower limit.|
| upperObj | [ScopeType](#scopetype8) | Yes| Upper limit.|

**Return value**

| Type| Description|
| -------- | -------- |
| [Scope](#scopedeprecated) | Intersection of this **Scope** and the given lower and upper limits.|

**Example**

  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let tempMidS = new Temperature(39);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.intersect(tempMiDF, tempMidS);
  ```

### getUpper<sup>(deprecated)</sup>

getUpper(): ScopeType

Obtains the upper limit of this **Scope**.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.getUpper<sup>9+</sup>](#getupper9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| [ScopeType](#scopetype8) | Upper limit of this **Scope**.|

**Example**

  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.getUpper();
  ```

### getLower<sup>(deprecated)</sup>

getLower(): ScopeType

Obtains the lower limit of this **Scope**.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.getLower<sup>9+</sup>](#getlower9) instead.

**System capability**: SystemCapability.Utils.Lang

**Return value**

| Type| Description|
| -------- | -------- |
| [ScopeType](#scopetype8) | Lower limit of this **Scope**.|

**Example**

  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.getLower();
  ```

### expand<sup>(deprecated)</sup>

expand(lowerObj: ScopeType,upperObj: ScopeType): Scope

Obtains the union set of this **Scope** and the given lower and upper limits.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.expand<sup>9+</sup>](#expand9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| lowerObj | [ScopeType](#scopetype8) | Yes| Lower limit.|
| upperObj | [ScopeType](#scopetype8) | Yes| Upper limit.|

**Return value**

| Type| Description|
| -------- | -------- |
| [Scope](#scopedeprecated) | Union set of this **Scope** and the given lower and upper limits.|

**Example**

  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let tempMidS = new Temperature(39);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.expand(tempMiDF, tempMidS);
  ```

### expand<sup>(deprecated)</sup>

expand(range: Scope): Scope

Obtains the union set of this **Scope** and the given **Scope**.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.expand<sup>9+</sup>](#expand9-1) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| range | [Scope](#scopedeprecated) | Yes| **Scope** specified.|

**Return value**

| Type| Description|
| -------- | -------- |
| [Scope](#scopedeprecated) | Union set of this **Scope** and the given **Scope**.|

**Example**

  ```js
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

Obtains the union set of this **Scope** and the given value.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.expand<sup>9+</sup>](#expand9-2) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | [ScopeType](#scopetype8) | Yes| Value specified.|

**Return value**

| Type| Description|
| -------- | -------- |
| [Scope](#scopedeprecated) | Union set of this **Scope** and the given value.|

**Example**

  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.expand(tempMiDF);
  ```

### contains<sup>(deprecated)</sup>

contains(value: ScopeType): boolean

Checks whether a value is within this **Scope**.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.contains<sup>9+</sup>](#contains9-1) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | [ScopeType](#scopetype8) | Yes| Value specified.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the value is within this **Scope**; returns **false** otherwise.|

**Example**

  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let range = new util.Scope(tempLower, tempUpper);
  range.contains(tempMiDF);
  ```

### contains<sup>(deprecated)</sup>

contains(range: Scope): boolean

Checks whether a range is within this **Scope**.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.contains<sup>9+</sup>](#contains9-2) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| range | [Scope](#scopedeprecated) | Yes| **Scope** specified.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the range is within this **Scope**; returns **false** otherwise.|

**Example**

  ```js
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

Limits a value to this **Scope**.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [ScopeHelper.clamp<sup>9+</sup>](#clamp9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | [ScopeType](#scopetype8) | Yes| Value specified.|

**Return value**

| Type| Description|
| -------- | -------- |
| [ScopeType](#scopetype8) | Returns **lowerObj** if the specified value is less than the lower limit; returns **upperObj** if the specified value is greater than the upper limit; returns the specified value if it is within this **Scope**.|

**Example**

  ```js
  let tempLower = new Temperature(30);
  let tempUpper = new Temperature(40);
  let tempMiDF = new Temperature(35);
  let range = new util.Scope(tempLower, tempUpper);
  let result = range.clamp(tempMiDF);
  ```


## Base64<sup>(deprecated)</sup>

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [Base64Helper<sup>9+</sup>](#base64helper9) instead.

### constructor<sup>(deprecated)</sup>

constructor()

A constructor used to create a **Base64** object.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [Base64Helper.constructor<sup>9+</sup>](#constructor9-5) instead.

**System capability**: SystemCapability.Utils.Lang

**Example**

  ```js
  let base64 = new  util.Base64();
  ```

### encodeSync<sup>(deprecated)</sup>

encodeSync(src: Uint8Array): Uint8Array

Encodes the input content into a Uint8Array object. This API returns the result synchronously.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [Base64Helper.encodeSync<sup>9+</sup>](#encodesync9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| src | Uint8Array | Yes| Uint8Array object to encode.|

**Return value**

| Type| Description|
| -------- | -------- |
| Uint8Array | Uint8Array object obtained.|

**Example**

  ```js
  let that = new util.Base64();
  let array = new Uint8Array([115,49,51]);
  let result = that.encodeSync(array);
  ```

### encodeToStringSync<sup>(deprecated)</sup>

encodeToStringSync(src: Uint8Array): string

Encodes the input content into a string. This API returns the result synchronously.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [Base64Helper.encodeToStringSync<sup>9+</sup>](#encodetostringsync9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| src | Uint8Array | Yes| Uint8Array object to encode.|

**Return value**

| Type| Description|
| -------- | -------- |
| string | String obtained.|

**Example**

  ```js
  let that = new util.Base64();
  let array = new Uint8Array([115,49,51]);
  let result = that.encodeToStringSync(array);
  ```

### decodeSync<sup>(deprecated)</sup>

decodeSync(src: Uint8Array | string): Uint8Array

Decodes the input content into a Uint8Array object.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [Base64Helper.decodeSync<sup>9+</sup>](#decodesync9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| src | Uint8Array&nbsp;\|&nbsp;string | Yes| Uint8Array object or string to decode.|

**Return value**

| Type| Description|
| -------- | -------- |
| Uint8Array | Uint8Array object obtained.|

**Example**

  ```js
  let that = new util.Base64();
  let buff = 'czEz';
  let result = that.decodeSync(buff);
  ```

### encode<sup>(deprecated)</sup>

encode(src: Uint8Array): Promise&lt;Uint8Array&gt;

Encodes the input content into a Uint8Array object. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [Base64Helper.encode<sup>9+</sup>](#encode9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| src | Uint8Array | Yes| Uint8Array object to encode.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the Uint8Array object obtained.|

**Example**

  ```js
  let that = new util.Base64();
  let array = new Uint8Array([115,49,51]);
  let rarray = new Uint8Array([99,122,69,122]);
  that.encode(array).then(val=>{    
      for (var i = 0; i < rarray.length; i++) {        
          console.log(val[i].toString())
      }
  })
  ```

### encodeToString<sup>(deprecated)</sup>

encodeToString(src: Uint8Array): Promise&lt;string&gt;

Encodes the input content into a string. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [Base64Helper.encodeToString<sup>9+</sup>](#encodetostring9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| src | Uint8Array | Yes| Uint8Array object to encode.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;string&gt; | Promise used to return the string obtained.|

**Example**

  ```js
  let that = new util.Base64();
  let array = new Uint8Array([115,49,51]);
  that.encodeToString(array).then(val=>{    
      console.log(val)
  })
  ```

### decode<sup>(deprecated)</sup>


decode(src: Uint8Array | string): Promise&lt;Uint8Array&gt;

Decodes the input content into a Uint8Array object. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [Base64Helper.decode<sup>9+</sup>](#decode9) instead.

**System capability**: SystemCapability.Utils.Lang

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| src | Uint8Array&nbsp;\|&nbsp;string | Yes| Uint8Array object or string to decode.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;Uint8Array&gt; | Promise used to return the Uint8Array object obtained.|

**Example**

  ```js
  let that = new util.Base64();
  let array = new Uint8Array([99,122,69,122]);
  let rarray = new Uint8Array([115,49,51]);
  that.decode(array).then(val=>{    
      for (var i = 0; i < rarray.length; i++) {        
          console.log(val[i].toString())
      }
  })
  ```
