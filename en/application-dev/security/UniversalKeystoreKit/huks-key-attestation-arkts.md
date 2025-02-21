# Non-anonymous Key Attestation (for System Applications Only) (ArkTS)

Non-anonymous key attestation is available only for system applications, and the caller must have the ohos.permission.ATTEST_KEY permission.

## How to Develop

1. Set the key alias (**keyAlias**), which cannot exceed 64 bytes.

2. Initializes a parameter set.

   The **properties** field in [HuksOptions](../../reference/apis-universal-keystore-kit/js-apis-huks.md#huksoptions) must contain [HUKS_TAG_ATTESTATION_ID_SEC_LEVEL_INFO](../../reference/apis-universal-keystore-kit/js-apis-huks.md#hukstag) and [HUKS_TAG_ATTESTATION_CHALLENGE](../../reference/apis-universal-keystore-kit/js-apis-huks.md#hukstag). Optional parameters include [HUKS_TAG_ATTESTATION_ID_VERSION_INFO](../../reference/apis-universal-keystore-kit/js-apis-huks.md#hukstag) and [HUKS_TAG_ATTESTATION_ID_ALIAS](../../reference/apis-universal-keystore-kit/js-apis-huks.md#hukstag).

3. Generate an asymmetric key. For details, see [Key Generation](huks-key-generation-overview.md).

4. Use [huks.attestKeyItem](../../reference/apis-universal-keystore-kit/js-apis-huks.md#huksattestkeyitem9) with the key alias and parameter set to perform key attestation.

```ts
/*
 * Perform non-anonymous key attestation. This example uses promise-based APIs.
 */
import huks from '@ohos.security.huks';
import { BusinessError } from '@ohos.base';
/* 1. Set the key alias. */
let keyAliasString = "key attest";
let aliasString = keyAliasString;
let aliasUint8 = StringToUint8Array(keyAliasString);
let securityLevel = StringToUint8Array('sec_level');
let challenge = StringToUint8Array('challenge_data');
let versionInfo = StringToUint8Array('version_info');
let attestCertChain: Array<string>;
class throwObject {
  isThrow: boolean = false;
}
class genKeyPropertyType {
  tag: huks.HuksTag = huks.HuksTag.HUKS_TAG_ALGORITHM;
  value: huks.HuksKeyAlg | huks.HuksKeyStorageType | huks.HuksKeySize | huks.HuksKeyPurpose | huks.HuksKeyDigest
    | huks.HuksKeyPadding | huks.HuksKeyGenerateType | huks.HuksCipherMode = huks.HuksKeyAlg.HUKS_ALG_RSA
}
/* Encapsulate the key parameter set. */
let genKeyProperties: genKeyPropertyType[] = [
  {
    tag: huks.HuksTag.HUKS_TAG_ALGORITHM,
    value: huks.HuksKeyAlg.HUKS_ALG_RSA
  },
  {
    tag: huks.HuksTag.HUKS_TAG_KEY_SIZE,
    value: huks.HuksKeySize.HUKS_RSA_KEY_SIZE_2048
  },
  {
    tag: huks.HuksTag.HUKS_TAG_PURPOSE,
    value: huks.HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
  },
  {
    tag: huks.HuksTag.HUKS_TAG_DIGEST,
    value: huks.HuksKeyDigest.HUKS_DIGEST_SHA256
  },
  {
    tag: huks.HuksTag.HUKS_TAG_PADDING,
    value: huks.HuksKeyPadding.HUKS_PADDING_PSS
  },
  {
    tag: huks.HuksTag.HUKS_TAG_KEY_GENERATE_TYPE,
    value: huks.HuksKeyGenerateType.HUKS_KEY_GENERATE_TYPE_DEFAULT
  },
  {
    tag: huks.HuksTag.HUKS_TAG_BLOCK_MODE,
    value: huks.HuksCipherMode.HUKS_MODE_ECB
  }
]
let genOptions: huks.HuksOptions = {
  properties: genKeyProperties
};
class attestKeypropertyType {
  tag: huks.HuksTag = huks.HuksTag.HUKS_TAG_ATTESTATION_ID_SEC_LEVEL_INFO;
  value: Uint8Array = securityLevel;
}
/* 2. Encapsulate the parameter set for key attestation. */
let attestKeyproperties: attestKeypropertyType[] = [
  {
    tag: huks.HuksTag.HUKS_TAG_ATTESTATION_ID_SEC_LEVEL_INFO,
    value: securityLevel
  },
  {
    tag: huks.HuksTag.HUKS_TAG_ATTESTATION_CHALLENGE,
    value: challenge
  },
  {
    tag: huks.HuksTag.HUKS_TAG_ATTESTATION_ID_VERSION_INFO,
    value: versionInfo
  },
  {
    tag: huks.HuksTag.HUKS_TAG_ATTESTATION_ID_ALIAS,
    value: aliasUint8
  }
]
let huksOptions: huks.HuksOptions = {
  properties: attestKeyproperties
};
function StringToUint8Array(str: string) {
  let arr: number[] = [];
  for (let i = 0, j = str.length; i < j; ++i) {
    arr.push(str.charCodeAt(i));
  }
  return new Uint8Array(arr);
}
function generateKeyItem(keyAlias: string, huksOptions: huks.HuksOptions, throwObject: throwObject) {
  return new Promise<void>((resolve, reject) => {
    try {
      huks.generateKeyItem(keyAlias, huksOptions, (error, data) => {
        if (error) {
          reject(error);
        } else {
          resolve(data);
        }
      });
    } catch (error) {
      throwObject.isThrow = true;
      throw(error as Error);
    }
  });
}
/* 3. Generate a key. */
async function publicGenKeyFunc(keyAlias: string, huksOptions: huks.HuksOptions) {
  console.info(`enter promise generateKeyItem`);
  let throwObject: throwObject = {isThrow: false};
  try {
    await generateKeyItem(keyAlias, huksOptions, throwObject)
      .then((data) => {
        console.info(`promise: generateKeyItem success, data = ${JSON.stringify(data)}`);
      })
      .catch((error: BusinessError) => {
        if (throwObject.isThrow) {
          throw(error as Error);
        } else {
          console.error(`promise: generateKeyItem failed` + error);
        }
      });
  } catch (error) {
    console.error(`promise: generateKeyItem input arg invalid` + error);
  }
}
/* 4. Attest the key. */
function attestKeyItem(keyAlias: string, huksOptions: huks.HuksOptions, throwObject: throwObject) {
  return new Promise<huks.HuksReturnResult>((resolve, reject) => {
    try {
      huks.attestKeyItem(keyAlias, huksOptions, (error, data) => {
        if (error) {
          reject(error);
        } else {
          resolve(data);
        }
      });
    } catch (error) {
      throwObject.isThrow = true;
      throw(error as Error);
    }
  });
}
async function publicAttestKey(keyAlias: string, huksOptions: huks.HuksOptions) {
  console.info(`enter promise attestKeyItem`);
  let throwObject: throwObject = {isThrow: false};
  try {
    await attestKeyItem(keyAlias, huksOptions, throwObject)
      .then ((data) => {
        console.info(`promise: attestKeyItem success, data = ${JSON.stringify(data)}`);
        if (data !== null && data.certChains !== null) {
          attestCertChain = data.certChains as string[];
        }
      })
      .catch((error: BusinessError) => {
        if (throwObject.isThrow) {
          throw(error as Error);
        } else {
          console.error(`promise: attestKeyItem failed` + error);
        }
      });
  } catch (error) {
    console.error(`promise: attestKeyItem input arg invalid` + error);
  }
}
async function AttestKeyTest() {
  await publicGenKeyFunc(aliasString, genOptions);
  await publicAttestKey(aliasString, huksOptions);
  console.info('attest certChain data: ' + attestCertChain)
}
```
