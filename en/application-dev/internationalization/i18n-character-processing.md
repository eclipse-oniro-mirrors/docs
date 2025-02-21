# Character Processing

## Use Cases

Character rules vary greatly in different languages, and it is usually difficult to extract expected information from the corresponding text. Character processing makes it possible to process text with similar logic under different language rules.

## How to Develop


### Character Type Identification Using Character Attributes

Character attributes are used to determine the character type, for example, digit, letter, or space, and check whether a character is of the right-to-left (RTL) language or whether a character is an ideographic character (for example, Chinese, Japanese, or Korean).

These functions are implemented by APIs of the **Unicode** class. For example, you can use [isDigit](../reference/apis-localization-kit/js-apis-i18n.md#isdigit9) to check whether a character is a digit. The development procedure is as follows:

1. Import the **i18n** module.

   ```ts
   import { i18n } from '@kit.LocalizationKit';
   ```

2. Obtain the character attribute.

   ```ts
   let isDigit: boolean = i18n.Unicode.isDigit(char: string);
   ```

3. Obtain the character type. The following code snippet uses the common type as an example. For details, see the **getType** API reference.

   ```ts
   let type = i18n.Unicode.getType(char: string);
   ```

**Development Example**
```ts
// Import the i18n module.
import { i18n } from '@kit.LocalizationKit';

// Check whether the input character is a digit.
let isDigit = i18n.Unicode.isDigit('1'); // isDigit: true

// Check whether a character is of the RTL language.
let isRTL = i18n.Unicode.isRTL('a'); // isRTL: false

// Check whether a character is an ideographic character.
let isIdeograph = i18n.Unicode.isIdeograph('Hua'); // isIdeograph: true

// Obtain the character type.
let type = i18n.Unicode.getType('a'); // type: U_LOWERCASE_LETTER
```


### Transliteration

Transliteration means to use content with similar pronunciation in the local language to replace the original content. This function is implemented through the [transform](../reference/apis-localization-kit/js-apis-i18n.md#transform9) API of the **Transliterator** class. The development procedure is as follows:

> **NOTE**
> This module supports the transliteration from Chinese characters to pinyin. However, it does not guaranteed that polyphonic characters are effectively processed based on the context.

1. Import the **i18n** module.
   ```ts
   import { i18n } from '@kit.LocalizationKit';
   ```

2. Create a **Transliterator** object to obtain the transliteration list.
   ```ts
   let transliterator: i18n.Transliterator = i18n.Transliterator.getInstance(id: string);  // Pass in a valid ID to create a Transliterator object.
   let ids: string[] = i18n.Transliterator.getAvailableIDs();  // Obtain the list of IDs supported by the Transliterator object.
   ```

3. Transliterate text.
   ```ts
   let res: string = transliterator.transform(text: string);  // Transliterate the text content.
   ```


**Development Example**
```ts
// Import the i18n module.
import { i18n } from '@kit.LocalizationKit';

// Transliterate the text into the Latn format.
let transliterator = i18n.Transliterator.getInstance('Any-Latn');
let wordArray = ["中国", "德国", "美国", "法国"]
for (let i = 0; i < wordArray.length; i++) {
    let res = transliterator.transform(wordArray[i]); // res: zhōng guó, dé guó, měi guó, fǎ guó
}

// Chinese transliteration and tone removal
let transliter = i18n.Transliterator.getInstance('Any-Latn;Latin-Ascii');
let result = transliter.transform ('中国'); // result: zhong guo

// Chinese surname pronunciation
let nameTransliter = i18n.Transliterator.getInstance('Han-Latin/Names');
let result = nameTransliter.transform ('单老师'); // result: shàn lǎo shī
let result2 = nameTransliter.transform ('长孙无忌'); // result2: zhǎng sūn wú jì


// Obtain the list of IDs supported by the Transliterator object.
let ids = i18n.Transliterator.getAvailableIDs(); // ids: ['ASCII-Latin', 'Accents-Any', ...]
```


### Character Normalization

Character normalization means to the standardize characters according to the specified paradigm. This function is implemented through the [normalize](../reference/apis-localization-kit/js-apis-i18n.md#normalize10) API of the **Normalizer** class. The development procedure is as follows:

1. Import the **i18n** module.
   ```ts
   import { i18n } from '@kit.LocalizationKit';
   ```

2. Create a **Normalizer** object. Pass in the text normalization paradigm to create a **Normalizer** object. The text normalization paradigm can be NFC, NFD, NFKC, or NFKD. For details, see [Unicode Normalization Forms](https://www.unicode.org/reports/tr15/#Norm_Forms).
   ```ts
   let normalizer: i18n.Normalizer = i18n.Normalizer.getInstance(mode: NormalizerMode);
   ```

3. Normalize the text.
   ```ts
   let normalizedText: string = normalizer.normalize(text: string); // Normalize the text.
   ```

**Development Example**
```ts
// Import the i18n module.
import { i18n } from '@kit.LocalizationKit';

// Normalize characters in the NFC form.
let normalizer = i18n.Normalizer.getInstance(i18n.NormalizerMode.NFC);
let normalizedText = normalizer.normalize('\u1E9B\u0323'); // normalizedText: \u1E9B\u0323
```


### Line Wrapping

Line wrapping means to obtain the text break position based on the specified text boundary and wrap the line. It is implemented by using the APIs of the [BreakIterator](../reference/apis-localization-kit/js-apis-i18n.md#breakiterator8) class. The development procedure is as follows:

1. Import the **i18n** module.
   ```ts
   import { i18n } from '@kit.LocalizationKit';
   ```

2. Create a **BreakIterator** object.
   Pass a valid locale to create a **BreakIterator** object. This object wraps lines based on the rules specified by the locale.

   ```ts
   let iterator: i18n.BreakIterator = i18n.getLineInstance(locale: string);
   ```

3. Set the text to be processed.
   ```ts
   iterator.setLineBreakText(text: string); // Set the text to be processed.
   let breakText: string = iterator.getLineBreakText(); // View the text being processed by the BreakIterator object.
   ```

4. Obtain the break positions of the text.
   ```ts
   let currentPos: number = iterator.current(); // Obtain the position of BreakIterator in the text.
   let firstPos: number = iterator.first(); // Set the position of BreakIterator as the first break point and return the position of the break point. The first break point is always at the beginning of the text, that is firstPos = 0.
   let nextPos: number = iterator.next(number); // Move BreakIterator by the specified number of break points. If the number is a positive number, the iterator is moved backward. If the number is a negative number, the iterator is moved forward. The default value is 1. nextPos indicates the position after moving. If BreakIterator is moved out of the text length range, -1 is returned.
   let isBoundary: boolean = iterator.isBoundary(number); // Check whether the position indicated by the specified number is a break point.
   ```


**Development Example**
```ts
// Import the i18n module.
import { i18n } from '@kit.LocalizationKit';

// Create a BreakIterator object.
let iterator = i18n.getLineInstance('en-GB');

// Set the text to be processed.
iterator.setLineBreakText('Apple is my favorite fruit.');

// Move BreakIterator to the beginning of the text.
let firstPos = iterator.first(); // firstPos: 0

// Move BreakIterator by several break points.
let nextPos = iterator.next(2); // nextPos: 9

// Check whether a position is a break point.
let isBoundary = iterator.isBoundary(9); // isBoundary: true

// Obtain the text processed by BreakIterator.
let breakText = iterator.getLineBreakText(); // breakText: Apple is my favorite fruit.
```
<!--RP1--><!--RP1End-->

<!--no_check-->