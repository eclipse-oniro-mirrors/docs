# HuksTypeApi


## Overview

Defines the macros, enums, structs, and error codes used by OpenHarmony Universal KeyStore (HUKS) APIs.

\@syscap SystemCapability.Security.Huks

**Since**:
9


## Summary


### Files

| Name| Description|
| -------- | -------- |
| [native_huks_type.h](native__huks__type_8h.md) | Defines the enumerated variables, structs, and macros used in the HUKS APIs.<br>**File to include**: <huks/native_huks/native_huks_type.h><br>**Library**: libhuks_ndk.z.so|


### Structs

| Name| Description|
| -------- | -------- |
| [OH_Huks_Result](_o_h___huks___result.md) | Defines the returned status data, including the return code and message. |
| [OH_Huks_Blob](_o_h___huks___blob.md) | Defines the structure of the binary large object (BLOB) that stores data. |
| [OH_Huks_Param](_o_h___huks___param.md) | Defines the structure of the parameters in a parameter set. |
| [OH_Huks_ParamSet](_o_h___huks___param_set.md) | Defines the parameter set structure. |
| [OH_Huks_CertChain](_o_h___huks___cert_chain.md) | Defines the certificate chain structure. |
| [OH_Huks_KeyInfo](_o_h___huks___key_info.md) | Defines the key information structure. |
| [OH_Huks_PubKeyInfo](_o_h___huks___pub_key_info.md) | Defines the structure of a public key. |
| [OH_Huks_KeyMaterialRsa](_o_h___huks___key_material_rsa.md) | Defines the structure of an RSA key. |
| [OH_Huks_KeyMaterialEcc](_o_h___huks___key_material_ecc.md) | Defines the structure of an Elliptic Curve Cryptography (ECC) key. |
| [OH_Huks_KeyMaterialDsa](_o_h___huks___key_material_dsa.md) | Defines the structure of a DSA key. |
| [OH_Huks_KeyMaterialDh](_o_h___huks___key_material_dh.md) | Defines the structure of a Diffie-Hellman (DH) key. |
| [OH_Huks_KeyMaterial25519](_o_h___huks___key_material25519.md) | Defines the structure of a 25519 key. |


### Macros

| Name| Value|
| -------- | -------- |
| **OH_HUKS_AE_TAG_LEN**    | 16 |
| **OH_HUKS_BITS_PER_BYTE**  |  8|
| **OH_HUKS_MAX_KEY_SIZE**   | 2048 |
| **OH_HUKS_AE_NONCE_LEN**   | 12 |
| **OH_HUKS_MAX_KEY_ALIAS_LEN**  | 64 |
| **OH_HUKS_MAX_PROCESS_NAME_LEN**  | 50 |
| **OH_HUKS_MAX_RANDOM_LEN**   | 1024 |
| **OH_HUKS_SIGNATURE_MIN_SIZE** | 64 |
| **OH_HUKS_MAX_OUT_BLOB_SIZE**    | (5 \* 1024 \* 1024) |
| **OH_HUKS_WRAPPED_FORMAT_MAX_SIZE** |   (1024 \* 1024)  |
| **OH_HUKS_IMPORT_WRAPPED_KEY_TOTAL_BLOBS**   |  10 |
| **TOKEN_CHALLENGE_LEN**    |32  |
| **SHA256_SIGN_LEN**  | 32 |
| **TOKEN_SIZE**   |32  |
| **MAX_AUTH_TIMEOUT_SECOND**   | 60 |
| **SECURE_SIGN_VERSION**    | 0x01000001 |


### Enums

| Name| Description|
| -------- | -------- |
| [OH_Huks_KeyPurpose](#oh_huks_keypurpose) {<br>OH_HUKS_KEY_PURPOSE_ENCRYPT = 1, <br>OH_HUKS_KEY_PURPOSE_DECRYPT = 2, <br>OH_HUKS_KEY_PURPOSE_SIGN = 4, <br>OH_HUKS_KEY_PURPOSE_VERIFY = 8, <br>OH_HUKS_KEY_PURPOSE_DERIVE = 16, <br>OH_HUKS_KEY_PURPOSE_WRAP = 32, <br>OH_HUKS_KEY_PURPOSE_UNWRAP = 64, <br>OH_HUKS_KEY_PURPOSE_MAC = 128,<br>OH_HUKS_KEY_PURPOSE_AGREE = 256<br>} | Enumerates the key purposes. |
| [OH_Huks_KeyDigest](#oh_huks_keydigest) {<br>OH_HUKS_DIGEST_NONE = 0, <br>OH_HUKS_DIGEST_MD5 = 1, <br>OH_HUKS_DIGEST_SM3 = 2, <br>OH_HUKS_DIGEST_SHA1 = 10, <br>OH_HUKS_DIGEST_SHA224 = 11, <br>OH_HUKS_DIGEST_SHA256 = 12, <br>OH_HUKS_DIGEST_SHA384 = 13, <br>OH_HUKS_DIGEST_SHA512 = 14<br>} | Enumerates the digest algorithms. |
| [OH_Huks_KeyPadding](#oh_huks_keypadding) {<br>OH_HUKS_PADDING_NONE = 0, <br>OH_HUKS_PADDING_OAEP = 1, <br>OH_HUKS_PADDING_PSS = 2, <br>OH_HUKS_PADDING_PKCS1_V1_5 = 3,<br>OH_HUKS_PADDING_PKCS5 = 4, <br>OH_HUKS_PADDING_PKCS7 = 5<br>} | Enumerates the padding algorithms. |
| [OH_Huks_CipherMode](#oh_huks_ciphermode) {<br>OH_HUKS_MODE_ECB = 1, <br>OH_HUKS_MODE_CBC = 2, <br>OH_HUKS_MODE_CTR = 3, <br>OH_HUKS_MODE_OFB = 4,<br>OH_HUKS_MODE_CCM = 31, <br>OH_HUKS_MODE_GCM = 32<br>} | Enumerates the cipher modes. |
| [OH_Huks_KeySize](#oh_huks_keysize) {<br>OH_HUKS_RSA_KEY_SIZE_512 = 512, <br>OH_HUKS_RSA_KEY_SIZE_768 = 768, <br>OH_HUKS_RSA_KEY_SIZE_1024 = 1024, <br>OH_HUKS_RSA_KEY_SIZE_2048 = 2048,<br>OH_HUKS_RSA_KEY_SIZE_3072 = 3072, <br>OH_HUKS_RSA_KEY_SIZE_4096 = 4096, <br>OH_HUKS_ECC_KEY_SIZE_224 = 224, <br>OH_HUKS_ECC_KEY_SIZE_256 = 256,<br>OH_HUKS_ECC_KEY_SIZE_384 = 384, <br>OH_HUKS_ECC_KEY_SIZE_521 = 521, <br>OH_HUKS_AES_KEY_SIZE_128 = 128, <br>OH_HUKS_AES_KEY_SIZE_192 = 192,<br>OH_HUKS_AES_KEY_SIZE_256 = 256, <br>OH_HUKS_AES_KEY_SIZE_512 = 512, <br>OH_HUKS_CURVE25519_KEY_SIZE_256 = 256, <br>OH_HUKS_DH_KEY_SIZE_2048 = 2048,<br>OH_HUKS_DH_KEY_SIZE_3072 = 3072, <br>OH_HUKS_DH_KEY_SIZE_4096 = 4096, <br>OH_HUKS_SM2_KEY_SIZE_256 = 256, <br>OH_HUKS_SM4_KEY_SIZE_128 = 128<br>} | Enumerates key sizes of different algorithms. |
| [OH_Huks_KeyAlg](#oh_huks_keyalg) {<br>OH_HUKS_ALG_RSA = 1, <br>OH_HUKS_ALG_ECC = 2, <br>OH_HUKS_ALG_DSA = 3, <br>OH_HUKS_ALG_AES = 20,<br>OH_HUKS_ALG_HMAC = 50,<br>OH_HUKS_ALG_HKDF = 51, <br>OH_HUKS_ALG_PBKDF2 = 52, <br>OH_HUKS_ALG_ECDH = 100,<br>OH_HUKS_ALG_X25519 = 101, <br>OH_HUKS_ALG_ED25519 = 102, <br>OH_HUKS_ALG_DH = 103, <br>OH_HUKS_ALG_SM2 = 150,<br>OH_HUKS_ALG_SM3 = 151, <br>OH_HUKS_ALG_SM4 = 152<br>} | Enumerates the algorithms for keys. |
| [OH_Huks_AlgSuite](#oh_huks_algsuite) { <br>OH_HUKS_UNWRAP_SUITE_X25519_AES_256_GCM_NOPADDING = 1, <br>OH_HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NOPADDING = 2  <br>} | Enumerates the algorithm suites for the import of a wrapped key. |
| [OH_Huks_KeyGenerateType](#oh_huks_keygeneratetype) { <br>OH_HUKS_KEY_GENERATE_TYPE_DEFAULT = 0, <br>OH_HUKS_KEY_GENERATE_TYPE_DERIVE = 1, <br>OH_HUKS_KEY_GENERATE_TYPE_AGREE = 2 <br>} | Enumerates the types of the key generated. |
| [OH_Huks_KeyFlag](#oh_huks_keyflag) { <br>OH_HUKS_KEY_FLAG_IMPORT_KEY = 1, <br>OH_HUKS_KEY_FLAG_GENERATE_KEY = 2, <br>OH_HUKS_KEY_FLAG_AGREE_KEY = 3, <br>OH_HUKS_KEY_FLAG_DERIVE_KEY = 4 <br>} | Enumerates the key generation types. |
| [OH_Huks_KeyStorageType](#oh_huks_keystoragetype) { <br>OH_HUKS_STORAGE_TEMP = 0, <br>OH_HUKS_STORAGE_PERSISTENT = 1, <br>OH_HUKS_STORAGE_ONLY_USED_IN_HUKS = 2, <br>OH_HUKS_STORAGE_KEY_EXPORT_ALLOWED = 3 <br>} | Enumerates the key storage types. |
| [OH_Huks_ImportKeyType](#oh_huks_importkeytype) { <br>OH_HUKS_KEY_TYPE_PUBLIC_KEY = 0, <br>OH_HUKS_KEY_TYPE_PRIVATE_KEY = 1, <br>OH_HUKS_KEY_TYPE_KEY_PAIR = 2 <br>} | Enumerates the types of the key to import. By default, a public key is imported. This field is not required when a symmetric key is imported. |
| [OH_Huks_RsaPssSaltLenType](#oh_huks_rsapsssaltlentype) { <br> OH_HUKS_RSA_PSS_SALT_LEN_DIGEST = 0, OH_HUKS_RSA_PSS_SALT_LEN_MAX = 1 <br>} | Enumerates the salt length types when the PSS padding mode is used in RSA signing or signature verification.|
| [OH_Huks_ErrCode](#oh_huks_errcode) {<br>OH_HUKS_SUCCESS = 0, <br>OH_HUKS_ERR_CODE_PERMISSION_FAIL = 201, <br>OH_HUKS_ERR_CODE_ILLEGAL_ARGUMENT = 401, <br>OH_HUKS_ERR_CODE_NOT_SUPPORTED_API = 801,<br>OH_HUKS_ERR_CODE_FEATURE_NOT_SUPPORTED = 12000001, <br>OH_HUKS_ERR_CODE_MISSING_CRYPTO_ALG_ARGUMENT = 12000002, <br>OH_HUKS_ERR_CODE_INVALID_CRYPTO_ALG_ARGUMENT = 12000003, <br>OH_HUKS_ERR_CODE_FILE_OPERATION_FAIL = 12000004,<br>OH_HUKS_ERR_CODE_COMMUNICATION_FAIL = 12000005, <br>OH_HUKS_ERR_CODE_CRYPTO_FAIL = 12000006, <br>OH_HUKS_ERR_CODE_KEY_AUTH_PERMANENTLY_INVALIDATED = 12000007, <br>OH_HUKS_ERR_CODE_KEY_AUTH_VERIFY_FAILED = 12000008,<br>OH_HUKS_ERR_CODE_KEY_AUTH_TIME_OUT = 12000009, <br>OH_HUKS_ERR_CODE_SESSION_LIMIT = 12000010, <br>OH_HUKS_ERR_CODE_ITEM_NOT_EXIST = 12000011, <br>OH_HUKS_ERR_CODE_INTERNAL_ERROR = 12000012,<br>OH_HUKS_ERR_CODE_CREDENTIAL_NOT_EXIST = 12000013<br>} | Enumerates the error codes. |
| [OH_Huks_TagType](#oh_huks_tagtype) {<br>OH_HUKS_TAG_TYPE_INVALID = 0  &lt;&lt; 28, <br>OH_HUKS_TAG_TYPE_INT = 1 &lt;&lt; 28, <br>OH_HUKS_TAG_TYPE_UINT = 2 &lt;&lt; 28, <br>OH_HUKS_TAG_TYPE_ULONG = 3 &lt;&lt; 28,<br>OH_HUKS_TAG_TYPE_BOOL = 4 &lt;&lt; 28, <br>OH_HUKS_TAG_TYPE_BYTES = 5 &lt;&lt; 28<br>} | Enumerates the mask values of the parameter type in the parameter set. |
| [OH_Huks_UserAuthType](#oh_huks_userauthtype) { <br>OH_HUKS_USER_AUTH_TYPE_FINGERPRINT = 1 &lt;&lt; 0, <br>OH_HUKS_USER_AUTH_TYPE_FACE = 1 &lt;&lt; 1, <br>OH_HUKS_USER_AUTH_TYPE_PIN = 1 &lt;&lt; 2 <br>} | Enumerates the user authentication types in key access control. |
| [OH_Huks_AuthAccessType](#oh_huks_authaccesstype) { <br>OH_HUKS_AUTH_ACCESS_INVALID_CLEAR_PASSWORD = 1 &lt;&lt; 0, <br>OH_HUKS_AUTH_ACCESS_INVALID_NEW_BIO_ENROLL = 1 &lt;&lt; 1 <br>} | Enumerates the rules for invalidating a key. |
| [OH_Huks_ChallengeType](#oh_huks_challengetype) { <br>OH_HUKS_CHALLENGE_TYPE_NORMAL = 0, <br>OH_HUKS_CHALLENGE_TYPE_CUSTOM = 1, <br>OH_HUKS_CHALLENGE_TYPE_NONE = 2 <br>} | Enumerates the types of the challenge generated when a key is used. |
| [OH_Huks_ChallengePosition](#oh_huks_challengeposition) { <br>OH_HUKS_CHALLENGE_POS_0 = 0, <br>OH_HUKS_CHALLENGE_POS_1, <br>OH_HUKS_CHALLENGE_POS_2, <br>OH_HUKS_CHALLENGE_POS_3 <br>} | Enumerates the positions of the 8-byte valid value in a custom challenge generated. |
| [OH_Huks_SecureSignType](#oh_huks_securesigntype) { OH_HUKS_SECURE_SIGN_WITH_AUTHINFO = 1 } | Enumerates the signature types of the key generated or imported. |
| [OH_Huks_Tag](#oh_huks_tag) {<br> OH_HUKS_TAG_ALGORITHM = OH_HUKS_TAG_TYPE_UINT \| 1, OH_HUKS_TAG_PURPOSE = OH_HUKS_TAG_TYPE_UINT \| 2, OH_HUKS_TAG_KEY_SIZE = OH_HUKS_TAG_TYPE_UINT \| 3,<br>OH_HUKS_TAG_DIGEST = OH_HUKS_TAG_TYPE_UINT \| 4, OH_HUKS_TAG_PADDING = OH_HUKS_TAG_TYPE_UINT \| 5, OH_HUKS_TAG_BLOCK_MODE = OH_HUKS_TAG_TYPE_UINT \| 6, OH_HUKS_TAG_KEY_TYPE = OH_HUKS_TAG_TYPE_UINT \| 7,<br>OH_HUKS_TAG_ASSOCIATED_DATA = OH_HUKS_TAG_TYPE_BYTES \| 8, OH_HUKS_TAG_NONCE = OH_HUKS_TAG_TYPE_BYTES \| 9, OH_HUKS_TAG_IV = OH_HUKS_TAG_TYPE_BYTES \| 10, OH_HUKS_TAG_INFO = OH_HUKS_TAG_TYPE_BYTES \| 11,<br>OH_HUKS_TAG_SALT = OH_HUKS_TAG_TYPE_BYTES \| 12, OH_HUKS_TAG_ITERATION = OH_HUKS_TAG_TYPE_UINT \| 14, OH_HUKS_TAG_KEY_GENERATE_TYPE = OH_HUKS_TAG_TYPE_UINT \| 15, OH_HUKS_TAG_AGREE_ALG = OH_HUKS_TAG_TYPE_UINT \| 19,<br>OH_HUKS_TAG_AGREE_PUBLIC_KEY_IS_KEY_ALIAS = OH_HUKS_TAG_TYPE_BOOL \| 20, OH_HUKS_TAG_AGREE_PRIVATE_KEY_ALIAS = OH_HUKS_TAG_TYPE_BYTES \| 21, OH_HUKS_TAG_AGREE_PUBLIC_KEY = OH_HUKS_TAG_TYPE_BYTES \| 22, OH_HUKS_TAG_KEY_ALIAS = OH_HUKS_TAG_TYPE_BYTES \| 23,<br>OH_HUKS_TAG_DERIVE_KEY_SIZE = OH_HUKS_TAG_TYPE_UINT \| 24, OH_HUKS_TAG_IMPORT_KEY_TYPE = OH_HUKS_TAG_TYPE_UINT \| 25, OH_HUKS_TAG_UNWRAP_ALGORITHM_SUITE = OH_HUKS_TAG_TYPE_UINT \| 26, OH_HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG = OH_HUKS_TAG_TYPE_UINT \| 29, OH_HUKS_TAG_RSA_PSS_SALT_LEN_TYPE = OH_HUKS_TAG_TYPE_UINT \| 30, OH_HUKS_TAG_ALL_USERS = OH_HUKS_TAG_TYPE_BOOL \| 301,<br>OH_HUKS_TAG_USER_ID = OH_HUKS_TAG_TYPE_UINT \| 302, OH_HUKS_TAG_NO_AUTH_REQUIRED = OH_HUKS_TAG_TYPE_BOOL \| 303, OH_HUKS_TAG_USER_AUTH_TYPE = OH_HUKS_TAG_TYPE_UINT \| 304, OH_HUKS_TAG_AUTH_TIMEOUT = OH_HUKS_TAG_TYPE_UINT \| 305,<br>OH_HUKS_TAG_AUTH_TOKEN = OH_HUKS_TAG_TYPE_BYTES \| 306, OH_HUKS_TAG_KEY_AUTH_ACCESS_TYPE = OH_HUKS_TAG_TYPE_UINT \| 307, OH_HUKS_TAG_KEY_SECURE_SIGN_TYPE = OH_HUKS_TAG_TYPE_UINT \| 308, OH_HUKS_TAG_CHALLENGE_TYPE = OH_HUKS_TAG_TYPE_UINT \| 309,<br>OH_HUKS_TAG_CHALLENGE_POS = OH_HUKS_TAG_TYPE_UINT \| 310, OH_HUKS_TAG_KEY_AUTH_PURPOSE = OH_HUKS_TAG_TYPE_UINT \| 311, OH_HUKS_TAG_ATTESTATION_CHALLENGE = OH_HUKS_TAG_TYPE_BYTES \| 501, OH_HUKS_TAG_ATTESTATION_APPLICATION_ID = OH_HUKS_TAG_TYPE_BYTES \| 502, OH_HUKS_TAG_ATTESTATION_ID_ALIAS = OH_HUKS_TAG_TYPE_BYTES \| 511,<br>OH_HUKS_TAG_ATTESTATION_ID_SEC_LEVEL_INFO = OH_HUKS_TAG_TYPE_BYTES \| 514, OH_HUKS_TAG_ATTESTATION_ID_VERSION_INFO = OH_HUKS_TAG_TYPE_BYTES \| 515,<br>OH_HUKS_TAG_IS_KEY_ALIAS = OH_HUKS_TAG_TYPE_BOOL \| 1001, OH_HUKS_TAG_KEY_STORAGE_FLAG = OH_HUKS_TAG_TYPE_UINT \| 1002, OH_HUKS_TAG_IS_ALLOWED_WRAP = OH_HUKS_TAG_TYPE_BOOL \| 1003, OH_HUKS_TAG_KEY_WRAP_TYPE = OH_HUKS_TAG_TYPE_UINT \| 1004,<br>OH_HUKS_TAG_KEY_AUTH_ID = OH_HUKS_TAG_TYPE_BYTES \| 1005, OH_HUKS_TAG_KEY_ROLE = OH_HUKS_TAG_TYPE_UINT \| 1006, OH_HUKS_TAG_KEY_FLAG = OH_HUKS_TAG_TYPE_UINT \| 1007, OH_HUKS_TAG_IS_ASYNCHRONIZED = OH_HUKS_TAG_TYPE_UINT \| 1008,<br> OH_HUKS_TAG_KEY_DOMAIN = OH_HUKS_TAG_TYPE_UINT \| 1011, OH_HUKS_TAG_SYMMETRIC_KEY_DATA = OH_HUKS_TAG_TYPE_BYTES \| 20001,<br>OH_HUKS_TAG_ASYMMETRIC_PUBLIC_KEY_DATA = OH_HUKS_TAG_TYPE_BYTES \| 20002, OH_HUKS_TAG_ASYMMETRIC_PRIVATE_KEY_DATA = OH_HUKS_TAG_TYPE_BYTES \| 20003<br>} | Enumerates the tag values used in the parameter set. |


## Enum Description


### OH_Huks_AlgSuite


```
enum OH_Huks_AlgSuite
```
**Description**

Enumerates the algorithm suites for the import of a wrapped key.

| Value| Description|
| -------- | -------- |
| OH_HUKS_UNWRAP_SUITE_X25519_AES_256_GCM_NOPADDING  | Key material format (Length-Value format), use X25519 for key agreement, and use AES-256-GCM for encryption and decryption: \| x25519_plain_pubkey_length (4 Byte) \| x25519_plain_pubkey \| agreekey_aad_length (4 Byte) \| agreekey_aad \| agreekey_nonce_length (4 Byte) \| agreekey_nonce \| agreekey_aead_tag_len(4 Byte) \| agreekey_aead_tag \| kek_enc_data_length (4 Byte) \| kek_enc_data \| kek_aad_length (4 Byte) \| kek_aad \| kek_nonce_length (4 Byte) \| kek_nonce \| kek_aead_tag_len (4 Byte) \| kek_aead_tag \| key_material_size_len (4 Byte) \| key_material_size \| key_mat_enc_length (4 Byte) \| key_mat_enc_data |
| OH_HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NOPADDING  | Key material format (Length-Value format), use ECDH-p256 for key agreement, and use AES-256-GCM for encryption and decryption: \| ECC_plain_pubkey_length (4 Byte) \| ECC_plain_pubkey \| agreekey_aad_length (4 Byte) \| agreekey_aad \| agreekey_nonce_length (4 Byte) \| agreekey_nonce \| agreekey_aead_tag_len(4 Byte) \| agreekey_aead_tag \| kek_enc_data_length (4 Byte) \| kek_enc_data \| kek_aad_length (4 Byte) \| kek_aad \| kek_nonce_length (4 Byte) \| kek_nonce \| kek_aead_tag_len (4 Byte) \| kek_aead_tag \| key_material_size_len (4 Byte) \| key_material_size \| key_mat_enc_length (4 Byte) \| key_mat_enc_data |


### OH_Huks_AuthAccessType


```
enum OH_Huks_AuthAccessType
```
**Description**

Enumerates the rules for invalidating a key.

| Name | Description|
| -------- | -------- |
| OH_HUKS_AUTH_ACCESS_INVALID_CLEAR_PASSWORD  | The key becomes invalid after the password is cleared.|
| OH_HUKS_AUTH_ACCESS_INVALID_NEW_BIO_ENROLL  | The key becomes invalid after a new biometric feature is enrolled.|


### OH_Huks_ChallengePosition


```
enum OH_Huks_ChallengePosition
```
**Description**

Enumerates the positions of the 8-byte valid value in a custom challenge generated.

| Name | Description|
| -------- | -------- |
| OH_HUKS_CHALLENGE_POS_0  | Bytes 0 to 7.|
| OH_HUKS_CHALLENGE_POS_1  | Bytes 8 to 15.|
| OH_HUKS_CHALLENGE_POS_2  | Bytes 16 to 23.|
| OH_HUKS_CHALLENGE_POS_3  | Bytes 24 to 31.|


### OH_Huks_ChallengeType


```
enum OH_Huks_ChallengeType
```
**Description**

Enumerates the types of the challenge generated when a key is used.

**See**

[OH_Huks_ChallengePosition](#oh_huks_challengeposition)

| Name | Description|
| -------- | -------- |
| OH_HUKS_CHALLENGE_TYPE_NORMAL  | Normal challenge, which is of 32 bytes by default.|
| OH_HUKS_CHALLENGE_TYPE_CUSTOM  | Custom challenge, which supports only one authentication for multiple keys. The valid value of a custom challenge is of 8 bytes.|
| OH_HUKS_CHALLENGE_TYPE_NONE  | Challenge is not required.|


### OH_Huks_CipherMode


```
enum OH_Huks_CipherMode
```
**Description**

Enumerates the cipher modes.

| Name | Description|
| -------- | -------- |
| OH_HUKS_MODE_ECB  | Electronic Code Block (ECB) mode.|
| OH_HUKS_MODE_CBC  | Cipher Block Chaining (CBC) mode.|
| OH_HUKS_MODE_CTR  | Counter (CTR) mode.|
| OH_HUKS_MODE_OFB  | Output Feedback (OFB) mode.|
| OH_HUKS_MODE_CCM  | Counter with CBC-MAC (CCM) mode.|
| OH_HUKS_MODE_GCM  | Galois/Counter (GCM) mode.|


### OH_Huks_RsaPssSaltLenType

```
enum OH_Huks_RsaPssSaltLenType
```
**Description**

Enumerates the types of the salt length when the PSS padding mode is used in RSA signing or signature verification.

**Since**:
10

| Name | Description|
| -------- | -------- |
| OH_HUKS_RSA_PSS_SALT_LEN_DIGEST | The salt length is set to the digest length.|
| OH_HUKS_RSA_PSS_SALT_LEN_MAX | The salt length is set to the maximum length.|


### OH_Huks_ErrCode


```
enum OH_Huks_ErrCode
```
**Description**

Enumerates the error codes.

| Name | Description|
| -------- | -------- |
| OH_HUKS_SUCCESS  | Success.|
| OH_HUKS_ERR_CODE_PERMISSION_FAIL  | Permission verification failed.|
| OH_HUKS_ERR_CODE_ILLEGAL_ARGUMENT  | Invalid parameter (universal).|
| OH_HUKS_ERR_CODE_NOT_SUPPORTED_API  | The API is not supported.|
| OH_HUKS_ERR_CODE_FEATURE_NOT_SUPPORTED  | The feature is not supported.|
| OH_HUKS_ERR_CODE_MISSING_CRYPTO_ALG_ARGUMENT  | Key algorithm parameters are missing.|
| OH_HUKS_ERR_CODE_INVALID_CRYPTO_ALG_ARGUMENT  | Invalid key algorithm parameter.|
| OH_HUKS_ERR_CODE_FILE_OPERATION_FAIL  | File operation failed.|
| OH_HUKS_ERR_CODE_COMMUNICATION_FAIL  | The process communication failed.|
| OH_HUKS_ERR_CODE_CRYPTO_FAIL  | Failed to operate the crypto algorithm library.|
| OH_HUKS_ERR_CODE_KEY_AUTH_PERMANENTLY_INVALIDATED  | Failed to access the key because the key has expired.|
| OH_HUKS_ERR_CODE_KEY_AUTH_VERIFY_FAILED  | Failed to access the key because the authentication has failed.|
| OH_HUKS_ERR_CODE_KEY_AUTH_TIME_OUT  | Key access timed out.|
| OH_HUKS_ERR_CODE_SESSION_LIMIT  | The number of key operation sessions has reached the limit.|
| OH_HUKS_ERR_CODE_ITEM_NOT_EXIST  | The entity does not exist.|
| OH_HUKS_ERR_CODE_INTERNAL_ERROR  | Internal error.|
| OH_HUKS_ERR_CODE_CREDENTIAL_NOT_EXIST  | The authentication credential does not exist.|


### OH_Huks_ImportKeyType


```
enum OH_Huks_ImportKeyType
```
**Description**

Enumerates the types of the key to import. By default, a public key is imported. This field is not required when a symmetric key is imported.

| Name | Description|
| -------- | -------- |
| OH_HUKS_KEY_TYPE_PUBLIC_KEY  | Public key.|
| OH_HUKS_KEY_TYPE_PRIVATE_KEY  | Private key.|
| OH_HUKS_KEY_TYPE_KEY_PAIR  | Public and private key pair.|


### OH_Huks_KeyAlg


```
enum OH_Huks_KeyAlg
```
**Description**

Enumerates the algorithms for keys.

| Name | Description|
| -------- | -------- |
| OH_HUKS_ALG_RSA  | RSA.|
| OH_HUKS_ALG_ECC  | ECC.|
| OH_HUKS_ALG_DSA  | DSA.|
| OH_HUKS_ALG_AES  | Advanced Encryption Standard (AES).|
| OH_HUKS_ALG_HMAC  | HMAC algorithm.|
| OH_HUKS_ALG_HKDF  | HKDF.|
| OH_HUKS_ALG_PBKDF2  | PBKDF2.|
| OH_HUKS_ALG_ECDH  | ECDH.|
| OH_HUKS_ALG_X25519  | X25519.|
| OH_HUKS_ALG_ED25519  | Ed25519.|
| OH_HUKS_ALG_DH  | DH.|
| OH_HUKS_ALG_SM2  | ShangMi2 (SM2).|
| OH_HUKS_ALG_SM3  | SM3.|
| OH_HUKS_ALG_SM4  | ShangMi4 (SM4).|


### OH_Huks_KeyDigest


```
enum OH_Huks_KeyDigest
```
**Description**

Enumerates the digest algorithms.

| Name | Description|
| -------- | -------- |
| OH_HUKS_DIGEST_NONE  | No digest algorithm.|
| OH_HUKS_DIGEST_MD5  | MD5.|
| OH_HUKS_DIGEST_SM3  | SM3.|
| OH_HUKS_DIGEST_SHA1  | SHA-1.|
| OH_HUKS_DIGEST_SHA224  | SHA-224.|
| OH_HUKS_DIGEST_SHA256  | SHA-256.|
| OH_HUKS_DIGEST_SHA384  | SHA-384.|
| OH_HUKS_DIGEST_SHA512  | SHA-512.|


### OH_Huks_KeyFlag


```
enum OH_Huks_KeyFlag
```
**Description**

Enumerates the key generation types.

| Name | Description|
| -------- | -------- |
| OH_HUKS_KEY_FLAG_IMPORT_KEY  | Import a public key using an API.|
| OH_HUKS_KEY_FLAG_GENERATE_KEY  | Generate a key by using an API.|
| OH_HUKS_KEY_FLAG_AGREE_KEY  | Generate a key by using a key agreement API.|
| OH_HUKS_KEY_FLAG_DERIVE_KEY  | Derive a key by using an API.|


### OH_Huks_KeyGenerateType


```
enum OH_Huks_KeyGenerateType
```
**Description**

Enumerates the types of the key generated.

| Name | Description|
| -------- | -------- |
| OH_HUKS_KEY_GENERATE_TYPE_DEFAULT  | Key generated by default.|
| OH_HUKS_KEY_GENERATE_TYPE_DERIVE  | Derived key.|
| OH_HUKS_KEY_GENERATE_TYPE_AGREE  | Key generated by key agreement.|


### OH_Huks_KeyPadding


```
enum OH_Huks_KeyPadding
```
**Description**

Enumerates the padding algorithms.

| Name | Description|
| -------- | -------- |
| OH_HUKS_PADDING_NONE  | No padding algorithm.|
| OH_HUKS_PADDING_OAEP  | Optimal Asymmetric Encryption Padding (OAEP).|
| OH_HUKS_PADDING_PSS  | Probabilistic Signature Scheme (PSS).|
| OH_HUKS_PADDING_PKCS1_V1_5  | Public Key Cryptography Standards (PKCS) #1 v1.5.|
| OH_HUKS_PADDING_PKCS5  | PKCS #5.|
| OH_HUKS_PADDING_PKCS7  | PKCS #7.|


### OH_Huks_KeyPurpose


```
enum OH_Huks_KeyPurpose
```
**Description**

Enumerates the key purposes.

| Name | Description|
| -------- | -------- |
| OH_HUKS_KEY_PURPOSE_ENCRYPT  | Used to encrypt the plaintext.|
| OH_HUKS_KEY_PURPOSE_DECRYPT  | Used to decrypt the cipher text.|
| OH_HUKS_KEY_PURPOSE_SIGN  | Used for signing.|
| OH_HUKS_KEY_PURPOSE_VERIFY  | Used to verify the signature.|
| OH_HUKS_KEY_PURPOSE_DERIVE  | Used to derive a key.|
| OH_HUKS_KEY_PURPOSE_WRAP  | Used for an encrypted export.|
| OH_HUKS_KEY_PURPOSE_UNWRAP  | Used for an encrypted import.|
| OH_HUKS_KEY_PURPOSE_MAC  | Used to generate a message authentication code (MAC).|
| OH_HUKS_KEY_PURPOSE_AGREE  | Used for key agreement.|


### OH_Huks_KeySize


```
enum OH_Huks_KeySize
```
**Description**

Enumerates key sizes of different algorithms.

| Name | Description|
| -------- | -------- |
| OH_HUKS_RSA_KEY_SIZE_512  | Rivest-Shamir-Adleman (RSA) key of 512 bits.|
| OH_HUKS_RSA_KEY_SIZE_768  | RSA key of 768 bits.|
| OH_HUKS_RSA_KEY_SIZE_1024  | RSA key of 1024 bits.|
| OH_HUKS_RSA_KEY_SIZE_2048  | RSA key of 2048 bits.|
| OH_HUKS_RSA_KEY_SIZE_3072  | RSA key of 3072 bits.|
| OH_HUKS_RSA_KEY_SIZE_4096  | RSA key of 4096 bits.|
| OH_HUKS_ECC_KEY_SIZE_224  | ECC key of 224 bits.|
| OH_HUKS_ECC_KEY_SIZE_256  | ECC key of 256 bits.|
| OH_HUKS_ECC_KEY_SIZE_384  | ECC key of 384 bits.|
| OH_HUKS_ECC_KEY_SIZE_521  | ECC key of 521 bits.|
| OH_HUKS_AES_KEY_SIZE_128  | AES key of 128 bits.|
| OH_HUKS_AES_KEY_SIZE_192  | AES key of 192 bits.|
| OH_HUKS_AES_KEY_SIZE_256  | AES key of 256 bits.|
| OH_HUKS_AES_KEY_SIZE_512  | AES key of 512 bits.|
| OH_HUKS_CURVE25519_KEY_SIZE_256  | Curve25519 key of 256 bits.|
| OH_HUKS_DH_KEY_SIZE_2048  | DH key of 2048 bits.|
| OH_HUKS_DH_KEY_SIZE_3072  | DH key of 3072 bits.|
| OH_HUKS_DH_KEY_SIZE_4096  | DH key of 4096 bits.|
| OH_HUKS_SM2_KEY_SIZE_256  | SM2 key of 256 bits.|
| OH_HUKS_SM4_KEY_SIZE_128  | SM4 key of 128 bits.|


### OH_Huks_KeyStorageType


```
enum OH_Huks_KeyStorageType
```
**Description**

Enumerates the key storage types.

| Name | Description|
| -------- | -------- |
| OH_HUKS_STORAGE_TEMP  | The key is managed locally.|
| OH_HUKS_STORAGE_PERSISTENT  | The key is managed by the HUKS service.|
| OH_HUKS_STORAGE_ONLY_USED_IN_HUKS  | The key is stored only in the HUKS.|
| OH_HUKS_STORAGE_KEY_EXPORT_ALLOWED  | The key is exported from the HUKS and is not stored.|


### OH_Huks_SecureSignType


```
enum OH_Huks_SecureSignType
```
**Description**

Enumerates the signature types of the key generated or imported.

| Name | Description|
| -------- | -------- |
| OH_HUKS_SECURE_SIGN_WITH_AUTHINFO  | The signature carries authentication information. This field is specified when a key is generated or imported. When the key is used for signing, the data will be added with the authentication information and then be signed.|


### OH_Huks_Tag


```
enum OH_Huks_Tag
```
**Description**

Enumerates the tag values used in the parameter set.

| Name | Description|
| :------- | -------- |
| Tags for key parameters: 1 to 200 | |
| OH_HUKS_TAG_ALGORITHM  | Algorithm type. |
| OH_HUKS_TAG_PURPOSE  | Key purpose.|
| OH_HUKS_TAG_KEY_SIZE  | Key length.|
| OH_HUKS_TAG_DIGEST  | Digest algorithm.|
| OH_HUKS_TAG_PADDING  | Padding algorithm.|
| OH_HUKS_TAG_BLOCK_MODE  | Cipher mode.|
| OH_HUKS_TAG_KEY_TYPE  | Key type.|
| OH_HUKS_TAG_ASSOCIATED_DATA  | Associated authentication data.|
| OH_HUKS_TAG_NONCE  | Field for key encryption and decryption.|
| OH_HUKS_TAG_IV  | Initialized vector (IV).|
| OH_HUKS_TAG_INFO  | Information generated during key derivation.|
| OH_HUKS_TAG_SALT  | Salt value used for key derivation.|
| OH_HUKS_TAG_ITERATION  | Number of iterations for key derivation.|
| OH_HUKS_TAG_KEY_GENERATE_TYPE  | Type of the generated key. For details, see [OH_Huks_KeyGenerateType](#oh_huks_keygeneratetype).|
| OH_HUKS_TAG_AGREE_ALG  | Algorithm used in key agreement.|
| OH_HUKS_TAG_AGREE_PUBLIC_KEY_IS_KEY_ALIAS  | Alias of the public key used for key agreement.|
| OH_HUKS_TAG_AGREE_PRIVATE_KEY_ALIAS  | Alias of the private key used for key agreement.|
| OH_HUKS_TAG_AGREE_PUBLIC_KEY  | Public key used for key agreement.|
| OH_HUKS_TAG_KEY_ALIAS  | Key alias.|
| OH_HUKS_TAG_DERIVE_KEY_SIZE  | Size of the derived key.|
| OH_HUKS_TAG_IMPORT_KEY_TYPE  | Type of the key to import. For details, see {@link OH_Huks_ImportKeyType}.|
| OH_HUKS_TAG_UNWRAP_ALGORITHM_SUITE  | Algorithm suite required for encrypted imports.|
|  OH_HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG  | Storage type of the derived/agreed key.|
| OH_HUKS_TAG_RSA_PSS_SALT_LEN_TYPE | Salt length type when the PSS padding mode is used for the RSA algorithm.|
| Tags for key access control and authentication: 300 to 500 | |
| OH_HUKS_TAG_ALL_USERS  | All users in multi-user scenarios. |
| OH_HUKS_TAG_USER_ID  | Multi-user ID.|
| OH_HUKS_TAG_NO_AUTH_REQUIRED  | Whether key access control is required.|
| OH_HUKS_TAG_USER_AUTH_TYPE  | User authentication type in key access control.|
| OH_HUKS_TAG_AUTH_TIMEOUT  | Timeout duration for key access.|
| OH_HUKS_TAG_AUTH_TOKEN  | Authentication token for the key.|
| OH_HUKS_TAG_KEY_AUTH_ACCESS_TYPE  | Access control type. For details, see {@link OH_Huks_AuthAccessType}. This parameter must be set together with the user authentication type.|
| OH_HUKS_TAG_KEY_SECURE_SIGN_TYPE  | Signature type of the key generated or imported.|
| OH_HUKS_TAG_CHALLENGE_TYPE  | Type of the challenge generated for a key. For details, see {@link OH_Huks_ChallengeType}.|
| OH_HUKS_TAG_CHALLENGE_POS  | Position of the 8-byte valid value in a custom challenge. For details, see {@link OH_Huks_ChallengePosition}.|
| H_HUKS_TAG_KEY_AUTH_PURPOSE | Type of the key authentication purpose.|
| Tags for key attestation: 501 to 600 | |
| OH_HUKS_TAG_ATTESTATION_CHALLENGE  | Challenge value used for key attestation. |
| OH_HUKS_TAG_ATTESTATION_APPLICATION_ID  | ID of the application, to which the key belongs, in key attestation.|
| OH_HUKS_TAG_ATTESTATION_ID_ALIAS  | Key alias.|
| OH_HUKS_TAG_ATTESTATION_ID_SEC_LEVEL_INFO  | Security level used in key attestation.|
| OH_HUKS_TAG_ATTESTATION_ID_VERSION_INFO  | Version information used in key attestation.|
| 601 to 1000 are reserved. Extended tags: 1001 to 9999 | |
| OH_HUKS_TAG_IS_KEY_ALIAS  | Whether the key alias is used. |
| OH_HUKS_TAG_KEY_STORAGE_FLAG  | Key storage mode. For details, see [OH_Huks_KeyStorageType](#oh_huks_keystoragetype).|
| OH_HUKS_TAG_IS_ALLOWED_WRAP  | Whether to allow the key to be wrapped.|
| OH_HUKS_TAG_KEY_WRAP_TYPE  |  Key wrap type.|
| OH_HUKS_TAG_KEY_AUTH_ID  | Authentication ID.|
| OH_HUKS_TAG_KEY_ROLE  | Role of the key.|
| OH_HUKS_TAG_KEY_FLAG  | Key flag. For details, see [OH_Huks_KeyFlag](#oh_huks_keyflag).|
| OH_HUKS_TAG_IS_ASYNCHRONIZED  | Whether the invocation is asynchronous.|
| OH_HUKS_TAG_KEY_DOMAIN  | Key domain.|
| 11000 to 12000 are reserved. Reserved values for other tags: 20001 - N | |
| OH_HUKS_TAG_SYMMETRIC_KEY_DATA  | Symmetric key data. |
| OH_HUKS_TAG_ASYMMETRIC_PUBLIC_KEY_DATA  | Public key data of the asymmetric key pair.|
| OH_HUKS_TAG_ASYMMETRIC_PRIVATE_KEY_DATA  | Private key data of the asymmetric key pair.|


### OH_Huks_TagType


```
enum OH_Huks_TagType
```
**Description**

Enumerates the mask values of the parameter type in the parameter set.

**See**

[OH_Huks_Param](_o_h___huks___param.md)

| Name | Description|
| -------- | -------- |
| OH_HUKS_TAG_TYPE_INVALID  | Invalid tag type.|
| OH_HUKS_TAG_TYPE_INT  | int32_t.|
| OH_HUKS_TAG_TYPE_UINT  | uin32_t.|
| OH_HUKS_TAG_TYPE_ULONG  | uin64_t.|
| OH_HUKS_TAG_TYPE_BOOL  | Boolean.|
| OH_HUKS_TAG_TYPE_BYTES  | OH_Huks_Blob.|


### OH_Huks_UserAuthType


```
enum OH_Huks_UserAuthType
```
**Description**

Enumerates the user authentication types in key access control.

| Name | Description|
| -------- | -------- |
| OH_HUKS_USER_AUTH_TYPE_FINGERPRINT  | Fingerprint authentication.|
| OH_HUKS_USER_AUTH_TYPE_FACE  | Facial authentication.|
| OH_HUKS_USER_AUTH_TYPE_PIN  | PIN authentication.|
