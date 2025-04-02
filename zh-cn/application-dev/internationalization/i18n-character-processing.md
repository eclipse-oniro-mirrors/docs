# 字符处理

## 使用场景

不同语言中字符规则差异较大，通常很难从对应文本中提取需要的信息。通过字符处理，可以在不同语言规则下，以相似的逻辑处理文本。

## 开发步骤


### 字符属性

字符属性用于判断字符类别，如判断字符是否为数字、字母、空格，是否为从右到左语言的字符，是否为表意文字(主要是中文日文韩文)等。

该功能通过Unicode类的[isDigit](../reference/apis-localization-kit/js-apis-i18n.md#isdigit9)等接口实现，具体开发步骤如下。

1. 导入模块。

   ```ts
   import { i18n } from '@kit.LocalizationKit';
   ```

2. 判断字符属性。

   ```ts
   let isDigit: boolean = i18n.Unicode.isDigit(char: string);
   ```

3. 以一般类别值为例，判断字符类类型，具体请参考getType接口文档。

   ```ts
   let unicodeType: string = i18n.Unicode.getType(char: string);
   ```

**开发实例**
```ts
// 导入模块
import { i18n } from '@kit.LocalizationKit';

// 判断字符是否是数字
let isDigit: boolean = i18n.Unicode.isDigit('1'); // isDigit = true

// 判断字符是否是从右到左语言的字符
let isRTL: boolean = i18n.Unicode.isRTL('a'); // isRTL = false

// 判断字符是否是表意文字
let isIdeograph: boolean = i18n.Unicode.isIdeograph('华'); // isIdeograph = true

// 获取字符的一般类别值
let unicodeType: string = i18n.Unicode.getType('a'); // unicodeType = 'U_LOWERCASE_LETTER'
```


### 音译

音译是指以当地语言发音相近的内容替换原本的内容。通过Transliterator类的[transform](../reference/apis-localization-kit/js-apis-i18n.md#transform9)接口实现，具体开发步骤如下。

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块支持中文汉字转为拼音，但对于多音字无法根据上下文语义有效处理。

1. 导入模块。
   ```ts
   import { i18n } from '@kit.LocalizationKit';
   ```

2. 创建Transliterator对象，获取音译列表。
   ```ts
   let ids: string[] = i18n.Transliterator.getAvailableIDs(); // 获取音译支持的ID列表
   let transliterator: i18n.Transliterator = i18n.Transliterator.getInstance(id: string); // 传入音译支持的ID，创建Transliterator对象
   ```

3. 音译文本。
   ```ts
   let translatedText: string = transliterator.transform(text: string); // 对text内容进行音译
   ```


**开发实例**
```ts
// 导入模块
import { i18n } from '@kit.LocalizationKit';

// 音译成Latn格式
let transliterator: i18n.Transliterator = i18n.Transliterator.getInstance('Any-Latn');
let text: string = '中国';
let translatedText: string = transliterator.transform(text); // translatedText = 'zhōng guó'

// 汉语音译去声调
let toneLessTransliterator: i18n.Transliterator = i18n.Transliterator.getInstance('Any-Latn;Latin-Ascii');
translatedText = toneLessTransliterator.transform('中国'); // translatedText = 'zhong guo'

// 汉语姓氏读音
let nameTransliterator: i18n.Transliterator = i18n.Transliterator.getInstance('Han-Latin/Names');
translatedText = nameTransliterator.transform('单老师'); // translatedText = 'shàn lǎo shī'
translatedText = nameTransliterator.transform('长孙无忌'); // translatedText = 'zhǎng sūn wú jì'

// 获取音译支持的ID列表
let ids: string[] = i18n.Transliterator.getAvailableIDs(); // ids = ['ASCII-Latin', 'Accents-Any', ...]
```


### 字符标准化

字符标准化是指按指定的范式标准化字符。通过Normalizer类的[normalize](../reference/apis-localization-kit/js-apis-i18n.md#normalize10)接口实现，具体开发步骤如下。

1. 导入模块。
   ```ts
   import { i18n } from '@kit.LocalizationKit';
   ```

2. 创建标准化对象。传入文本标准化的范式，创建标准化对象，文本标准化的范式包括NFC、NFD、NFKC和NFKD，范式的详细介绍请参考[国际标准](https://www.unicode.org/reports/tr15/#Norm_Forms)。
   ```ts
   let normalizer: i18n.Normalizer = i18n.Normalizer.getInstance(mode: NormalizerMode);
   ```

3. 文本标准化。
   ```ts
   let normalizedText: string = normalizer.normalize(text: string); // 对text文本进行标准化
   ```

**开发实例**
```ts
// 导入模块
import { i18n } from '@kit.LocalizationKit';

// 以NFC范式标准化字符
let normalizer: i18n.Normalizer = i18n.Normalizer.getInstance(i18n.NormalizerMode.NFC);
let normalizedText: string = normalizer.normalize('\u1E9B\u0323'); // normalizedText = 'ẛ̣'
```


### 断词换行

断词换行是指根据设定的区域参数获取文本中的分割点，通过[BreakIterator](../reference/apis-localization-kit/js-apis-i18n.md#breakiterator8)类的接口实现，具体开发步骤如下。

1. 导入模块。
   ```ts
   import { i18n } from '@kit.LocalizationKit';
   ```

2. 创建用于断句的对象。
   传入合法的locale参数，生成BreakIterator类型的对象，该对象将按照locale所指定的区域的规则进行断句。

   ```ts
   let iterator: i18n.BreakIterator = i18n.getLineInstance(locale: string);
   ```

3. 设置要处理的文本。
   ```ts
   iterator.setLineBreakText(text: string); // 设置要处理的文本
   let breakText: string = iterator.getLineBreakText(); // 查看iterator正在处理的文本
   ```

4. 获取可断句的位置。
   ```ts
   let currentPos: number = iterator.current(); // 获取iterator在当前所处理文本中的位置
   let firstPos: number = iterator.first(); // 设置为第一个可断句的分割点，返回该分割点的位置。第一个分割点总是在文本的起始位置，firstPos = 0
   let nextPos: number = iterator.next(index?: number); // 将iterator移动index数量个分割点，index为正数代表向后移动，index为负数代表向前移动，默认值为1。nextPos为移动后在文本中的位置，如果超出文本的长度范围，返回-1
   let isBoundary: boolean = iterator.isBoundary(offset: number); // 判断offset位置是否是分割点
   ```


**开发实例**
```ts
// 导入模块
import { i18n } from '@kit.LocalizationKit';

// 断句对象
let iterator: i18n.BreakIterator  = i18n.getLineInstance('en-GB');

// 断句文本
iterator.setLineBreakText('Apple is my favorite fruit.');

// 将BreakIterator对象移动到文本起始位置
let firstPos: number = iterator.first(); // firstPos = 0

// 将BreakIterator对象移动几个分割点
let nextPos: number = iterator.next(2); // nextPos = 9

// 判断某个位置是否是分割点
let isBoundary: boolean = iterator.isBoundary(9); // isBoundary = true

// 获取BreakIterator对象处理的文本
let breakText: string = iterator.getLineBreakText(); // breakText = 'Apple is my favorite fruit.'
```
<!--RP1--><!--RP1End-->