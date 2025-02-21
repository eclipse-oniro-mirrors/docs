# Checking a Key (ArkTS)


Check whether a key exists.


## How to Develop

1. Set the key alias (**keyAlias**), which cannot exceed 64 bytes.

2. Initialize the key property set to specify the properties of the key to check, for example, check all keys or a single key. To check a single key, leave **properties** empty.

3. Use [isKeyItemExist](../../reference/apis-universal-keystore-kit/js-apis-huks.md#huksiskeyitemexist9) to check whether the key exists.

```ts
import huks from '@ohos.security.huks';
/* 1. Set the key alias. */
let keyAlias = 'test_key';
let isKeyExist: Boolean;
/* 2. Construct an empty object. */
let huksOptions:huks.HuksOptions = {
  properties: []
}
try {
  /* 3. Check whether the key exists. */
  huks.isKeyItemExist(keyAlias, huksOptions, (error, data) => {
    if (error) {
      console.error(`callback: isKeyItemExist failed` + error);
    } else {
      if (data !== null && data.valueOf() !== null) {
        isKeyExist = data.valueOf();
        console.info(`callback: isKeyItemExist success, isKeyExist = ${isKeyExist}`);
      }
    }
  });
} catch (error) {
  console.error(`callback: isKeyItemExist input arg invalid` + error);
}
```
