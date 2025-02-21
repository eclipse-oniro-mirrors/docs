# native_huks_type.h


## Overview

Defines the enumerated variables, structures, and macros used in the HUKS APIs.

**Since:**
9

**Related Modules:**

[HuksTypeApi](_huks_type_api.md)


## Summary


### Structs

| Name | Description | 
| -------- | -------- |
| [OH_Huks_Result](_o_h___huks___result.md) | Defines the return data, including the result code and message.  | 
| [OH_Huks_Blob](_o_h___huks___blob.md) | Defines the structure for storing data.  | 
| [OH_Huks_Param](_o_h___huks___param.md) | Defines the parameter structure in a parameter set.  | 
| [OH_Huks_ParamSet](_o_h___huks___param_set.md) | Defines the structure of the parameter set.  | 
| [OH_Huks_CertChain](_o_h___huks___cert_chain.md) | Defines the structure of the certificate chain.  | 
| [OH_Huks_KeyInfo](_o_h___huks___key_info.md) | Defines the key information structure.  | 
| [OH_Huks_PubKeyInfo](_o_h___huks___pub_key_info.md) | Defines the structure of a public key.  | 
| [OH_Huks_KeyMaterialRsa](_o_h___huks___key_material_rsa.md) | Defines the structure of an RSA key.  | 
| [OH_Huks_KeyMaterialEcc](_o_h___huks___key_material_ecc.md) | Defines the structure of an ECC key.  | 
| [OH_Huks_KeyMaterialDsa](_o_h___huks___key_material_dsa.md) | Defines the structure of a DSA key.  | 
| [OH_Huks_KeyMaterialDh](_o_h___huks___key_material_dh.md) | Defines the structure of a DH key.  | 
| [OH_Huks_KeyMaterial25519](_o_h___huks___key_material25519.md) | Defines the structure of a 25519 key.  | 


### Macros

| Name | Value | 
| -------- | -------- |
| **OH_HUKS_AE_TAG_LEN**    | 16 | 
| **OH_HUKS_BITS_PER_BYTE**    |  8| 
| **OH_HUKS_MAX_KEY_SIZE**    | 2048 | 
| **OH_HUKS_AE_NONCE_LEN**    | 12 | 
| **OH_HUKS_MAX_KEY_ALIAS_LEN**    | 64 | 
| **OH_HUKS_MAX_PROCESS_NAME_LEN**    | 50| 
| **OH_HUKS_MAX_RANDOM_LEN**   | 1024  | 
| **OH_HUKS_SIGNATURE_MIN_SIZE**    | 64 | 
| **OH_HUKS_MAX_OUT_BLOB_SIZE**   |  (5 \* 1024 \* 1024) | 
| **OH_HUKS_WRAPPED_FORMAT_MAX_SIZE**    | (1024 \* 1024) | 
| **OH_HUKS_IMPORT_WRAPPED_KEY_TOTAL_BLOBS**    | 10 | 
| **TOKEN_CHALLENGE_LEN**    | 32 | 
| **SHA256_SIGN_LEN**    | 32 | 
| **TOKEN_SIZE**    | 32 | 
| **MAX_AUTH_TIMEOUT_SECOND**    | 60 | 
| **SECURE_SIGN_VERSION**    | 0x01000001 | 


### Enums

| Name | Description | 
| -------- | -------- |
| [OH_Huks_KeyPurpose](_huks_type_api.md#oh_huks_keypurpose) {<br/>OH_HUKS_KEY_PURPOSE_ENCRYPT = 1, OH_HUKS_KEY_PURPOSE_DECRYPT = 2, OH_HUKS_KEY_PURPOSE_SIGN = 4, OH_HUKS_KEY_PURPOSE_VERIFY = 8,<br/>OH_HUKS_KEY_PURPOSE_DERIVE = 16, OH_HUKS_KEY_PURPOSE_WRAP = 32, OH_HUKS_KEY_PURPOSE_UNWRAP = 64, OH_HUKS_KEY_PURPOSE_MAC = 128,<br/>OH_HUKS_KEY_PURPOSE_AGREE = 256<br/>} | Enumerates the key purposes.  | 
| [OH_Huks_KeyDigest](_huks_type_api.md#oh_huks_keydigest) {<br/>OH_HUKS_DIGEST_NONE = 0, OH_HUKS_DIGEST_MD5 = 1, OH_HUKS_DIGEST_SM3 = 2, OH_HUKS_DIGEST_SHA1 = 10,<br/>OH_HUKS_DIGEST_SHA224 = 11, OH_HUKS_DIGEST_SHA256 = 12, OH_HUKS_DIGEST_SHA384 = 13, OH_HUKS_DIGEST_SHA512 = 14<br/>} | Enumerates the digest algorithms.  | 
| [OH_Huks_KeyPadding](_huks_type_api.md#oh_huks_keypadding) {<br/>OH_HUKS_PADDING_NONE = 0, OH_HUKS_PADDING_OAEP = 1, OH_HUKS_PADDING_PSS = 2, OH_HUKS_PADDING_PKCS1_V1_5 = 3,<br/>OH_HUKS_PADDING_PKCS5 = 4, OH_HUKS_PADDING_PKCS7 = 5<br/>} | Enumerates the padding algorithms.  | 
| [OH_Huks_CipherMode](_huks_type_api.md#oh_huks_ciphermode) {<br/>OH_HUKS_MODE_ECB = 1, OH_HUKS_MODE_CBC = 2, OH_HUKS_MODE_CTR = 3, OH_HUKS_MODE_OFB = 4,<br/>OH_HUKS_MODE_CCM = 31, OH_HUKS_MODE_GCM = 32<br/>} | Enumerates the cipher modes.  | 
| [OH_Huks_KeySize](_huks_type_api.md#oh_huks_keysize) {<br/>OH_HUKS_RSA_KEY_SIZE_512 = 512, OH_HUKS_RSA_KEY_SIZE_768 = 768, OH_HUKS_RSA_KEY_SIZE_1024 = 1024, OH_HUKS_RSA_KEY_SIZE_2048 = 2048,<br/>OH_HUKS_RSA_KEY_SIZE_3072 = 3072, OH_HUKS_RSA_KEY_SIZE_4096 = 4096, OH_HUKS_ECC_KEY_SIZE_224 = 224, OH_HUKS_ECC_KEY_SIZE_256 = 256,<br/>OH_HUKS_ECC_KEY_SIZE_384 = 384, OH_HUKS_ECC_KEY_SIZE_521 = 521, OH_HUKS_AES_KEY_SIZE_128 = 128, OH_HUKS_AES_KEY_SIZE_192 = 192,<br/>OH_HUKS_AES_KEY_SIZE_256 = 256, OH_HUKS_AES_KEY_SIZE_512 = 512, OH_HUKS_CURVE25519_KEY_SIZE_256 = 256, OH_HUKS_DH_KEY_SIZE_2048 = 2048,<br/>OH_HUKS_DH_KEY_SIZE_3072 = 3072, OH_HUKS_DH_KEY_SIZE_4096 = 4096, OH_HUKS_SM2_KEY_SIZE_256 = 256, OH_HUKS_SM4_KEY_SIZE_128 = 128<br/>} | Enumerates the key sizes.  | 
| [OH_Huks_KeyAlg](_huks_type_api.md#oh_huks_keyalg) {<br/>OH_HUKS_ALG_RSA = 1, OH_HUKS_ALG_ECC = 2, OH_HUKS_ALG_DSA = 3, OH_HUKS_ALG_AES = 20,<br/>OH_HUKS_ALG_HMAC = 50, OH_HUKS_ALG_HKDF = 51, OH_HUKS_ALG_PBKDF2 = 52, OH_HUKS_ALG_ECDH = 100,<br/>OH_HUKS_ALG_X25519 = 101, OH_HUKS_ALG_ED25519 = 102, OH_HUKS_ALG_DH = 103, OH_HUKS_ALG_SM2 = 150,<br/>OH_HUKS_ALG_SM3 = 151, OH_HUKS_ALG_SM4 = 152<br/>} | Enumerates the key algorithms.  | 
| [OH_Huks_AlgSuite](_huks_type_api.md#oh_huks_algsuite) { OH_HUKS_UNWRAP_SUITE_X25519_AES_256_GCM_NOPADDING = 1, OH_HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NOPADDING = 2 } | Enumerates the algorithm suites required for ciphertext imports.  | 
| [OH_Huks_KeyGenerateType](_huks_type_api.md#oh_huks_keygeneratetype) { OH_HUKS_KEY_GENERATE_TYPE_DEFAULT = 0, OH_HUKS_KEY_GENERATE_TYPE_DERIVE = 1, OH_HUKS_KEY_GENERATE_TYPE_AGREE = 2 } | Enumerates the key generation types.  | 
| [OH_Huks_KeyFlag](_huks_type_api.md#oh_huks_keyflag) { OH_HUKS_KEY_FLAG_IMPORT_KEY = 1, OH_HUKS_KEY_FLAG_GENERATE_KEY = 2, OH_HUKS_KEY_FLAG_AGREE_KEY = 3, OH_HUKS_KEY_FLAG_DERIVE_KEY = 4 } | Enumerates the key generation modes.  | 
| [OH_Huks_KeyStorageType](_huks_type_api.md#oh_huks_keystoragetype) { OH_HUKS_STORAGE_TEMP = 0, OH_HUKS_STORAGE_PERSISTENT = 1 } | Enumerates the key storage modes.  | 
| [OH_Huks_ImportKeyType](_huks_type_api.md#oh_huks_importkeytype) { OH_HUKS_KEY_TYPE_PUBLIC_KEY = 0, OH_HUKS_KEY_TYPE_PRIVATE_KEY = 1, OH_HUKS_KEY_TYPE_KEY_PAIR = 2 } | Enumerates the types of keys to import. By default, a public key is imported. This field is not required when a symmetric key is imported.  | 
| [OH_Huks_ErrCode](_huks_type_api.md#oh_huks_errcode) {<br/>OH_HUKS_SUCCESS = 0, OH_HUKS_ERR_CODE_PERMISSION_FAIL = 201, OH_HUKS_ERR_CODE_ILLEGAL_ARGUMENT = 401, OH_HUKS_ERR_CODE_NOT_SUPPORTED_API = 801,<br/>OH_HUKS_ERR_CODE_FEATURE_NOT_SUPPORTED = 12000001, OH_HUKS_ERR_CODE_MISSING_CRYPTO_ALG_ARGUMENT = 12000002, OH_HUKS_ERR_CODE_INVALID_CRYPTO_ALG_ARGUMENT = 12000003, OH_HUKS_ERR_CODE_FILE_OPERATION_FAIL = 12000004,<br/>OH_HUKS_ERR_CODE_COMMUNICATION_FAIL = 12000005, OH_HUKS_ERR_CODE_CRYPTO_FAIL = 12000006, OH_HUKS_ERR_CODE_KEY_AUTH_PERMANENTLY_INVALIDATED = 12000007, OH_HUKS_ERR_CODE_KEY_AUTH_VERIFY_FAILED = 12000008,<br/>OH_HUKS_ERR_CODE_KEY_AUTH_TIME_OUT = 12000009, OH_HUKS_ERR_CODE_SESSION_LIMIT = 12000010, OH_HUKS_ERR_CODE_ITEM_NOT_EXIST = 12000011, OH_HUKS_ERR_CODE_INTERNAL_ERROR = 12000012,<br/>OH_HUKS_ERR_CODE_CREDENTIAL_NOT_EXIST = 12000013<br/>} | Enumerates the error codes.  | 
| [OH_Huks_TagType](_huks_type_api.md#oh_huks_tagtype) {<br/>OH_HUKS_TAG_TYPE_INVALID = 0 &lt;&lt; 28, OH_HUKS_TAG_TYPE_INT = 1 &lt;&lt; 28, OH_HUKS_TAG_TYPE_UINT = 2 &lt;&lt; 28, OH_HUKS_TAG_TYPE_ULONG = 3 &lt;&lt; 28,<br/>OH_HUKS_TAG_TYPE_BOOL = 4 &lt;&lt; 28, OH_HUKS_TAG_TYPE_BYTES = 5 &lt;&lt; 28<br/>} | Enumerates the tag types.  | 
| [OH_Huks_UserAuthType](_huks_type_api.md#oh_huks_userauthtype) { OH_HUKS_USER_AUTH_TYPE_FINGERPRINT = 1 &lt;&lt; 0, OH_HUKS_USER_AUTH_TYPE_FACE = 1 &lt;&lt; 1, OH_HUKS_USER_AUTH_TYPE_PIN = 1 &lt;&lt; 2 } | Enumerates the user authentication types.  | 
| [OH_Huks_AuthAccessType](_huks_type_api.md#oh_huks_authaccesstype) { OH_HUKS_AUTH_ACCESS_INVALID_CLEAR_PASSWORD = 1 &lt;&lt; 0, OH_HUKS_AUTH_ACCESS_INVALID_NEW_BIO_ENROLL = 1 &lt;&lt; 1 } | Enumerates the access control types.  | 
| [OH_Huks_ChallengeType](_huks_type_api.md#oh_huks_challengetype) { OH_HUKS_CHALLENGE_TYPE_NORMAL = 0, OH_HUKS_CHALLENGE_TYPE_CUSTOM = 1, OH_HUKS_CHALLENGE_TYPE_NONE = 2 } | Enumerates the types of the challenges generated when a key is used.  | 
| [OH_Huks_ChallengePosition](_huks_type_api.md#oh_huks_challengeposition) { OH_HUKS_CHALLENGE_POS_0 = 0, OH_HUKS_CHALLENGE_POS_1, OH_HUKS_CHALLENGE_POS_2, OH_HUKS_CHALLENGE_POS_3 } | Enumerates the positions of the 8-byte valid value in a custom challenge generated.  | 
| [OH_Huks_SecureSignType](_huks_type_api.md#oh_huks_securesigntype) { OH_HUKS_SECURE_SIGN_WITH_AUTHINFO = 1 } | Enumerates the signature types of the keys generated or imported.  | 
| [OH_Huks_Tag](_huks_type_api.md#oh_huks_tag) {<br/> OH_HUKS_TAG_ALGORITHM = OH_HUKS_TAG_TYPE_UINT \| 1, OH_HUKS_TAG_PURPOSE = OH_HUKS_TAG_TYPE_UINT \| 2, OH_HUKS_TAG_KEY_SIZE = OH_HUKS_TAG_TYPE_UINT \| 3,<br/>OH_HUKS_TAG_DIGEST = OH_HUKS_TAG_TYPE_UINT \| 4, OH_HUKS_TAG_PADDING = OH_HUKS_TAG_TYPE_UINT \| 5, OH_HUKS_TAG_BLOCK_MODE = OH_HUKS_TAG_TYPE_UINT \| 6, OH_HUKS_TAG_KEY_TYPE = OH_HUKS_TAG_TYPE_UINT \| 7,<br/>OH_HUKS_TAG_ASSOCIATED_DATA = OH_HUKS_TAG_TYPE_BYTES \| 8, OH_HUKS_TAG_NONCE = OH_HUKS_TAG_TYPE_BYTES \| 9, OH_HUKS_TAG_IV = OH_HUKS_TAG_TYPE_BYTES \| 10, OH_HUKS_TAG_INFO = OH_HUKS_TAG_TYPE_BYTES \| 11,<br/>OH_HUKS_TAG_SALT = OH_HUKS_TAG_TYPE_BYTES \| 12, OH_HUKS_TAG_ITERATION = OH_HUKS_TAG_TYPE_UINT \| 14, OH_HUKS_TAG_KEY_GENERATE_TYPE = OH_HUKS_TAG_TYPE_UINT \| 15,<br/> OH_HUKS_TAG_AGREE_ALG = OH_HUKS_TAG_TYPE_UINT \| 19,<br/>OH_HUKS_TAG_AGREE_PUBLIC_KEY_IS_KEY_ALIAS = OH_HUKS_TAG_TYPE_BOOL \| 20, OH_HUKS_TAG_AGREE_PRIVATE_KEY_ALIAS = OH_HUKS_TAG_TYPE_BYTES \| 21, OH_HUKS_TAG_AGREE_PUBLIC_KEY = OH_HUKS_TAG_TYPE_BYTES \| 22, OH_HUKS_TAG_KEY_ALIAS = OH_HUKS_TAG_TYPE_BYTES \| 23,<br/>OH_HUKS_TAG_DERIVE_KEY_SIZE = OH_HUKS_TAG_TYPE_UINT \| 24, OH_HUKS_TAG_IMPORT_KEY_TYPE = OH_HUKS_TAG_TYPE_UINT \| 25, OH_HUKS_TAG_UNWRAP_ALGORITHM_SUITE = OH_HUKS_TAG_TYPE_UINT \| 26, OH_HUKS_TAG_ALL_USERS = OH_HUKS_TAG_TYPE_BOOL \| 301,<br/>OH_HUKS_TAG_USER_ID = OH_HUKS_TAG_TYPE_UINT \| 302, OH_HUKS_TAG_NO_AUTH_REQUIRED = OH_HUKS_TAG_TYPE_BOOL \| 303, OH_HUKS_TAG_USER_AUTH_TYPE = OH_HUKS_TAG_TYPE_UINT \| 304, OH_HUKS_TAG_AUTH_TIMEOUT = OH_HUKS_TAG_TYPE_UINT \| 305,<br/>OH_HUKS_TAG_AUTH_TOKEN = OH_HUKS_TAG_TYPE_BYTES \| 306, OH_HUKS_TAG_KEY_AUTH_ACCESS_TYPE = OH_HUKS_TAG_TYPE_UINT \| 307, OH_HUKS_TAG_KEY_SECURE_SIGN_TYPE = OH_HUKS_TAG_TYPE_UINT \| 308, OH_HUKS_TAG_CHALLENGE_TYPE = OH_HUKS_TAG_TYPE_UINT \| 309,<br/>OH_HUKS_TAG_CHALLENGE_POS = OH_HUKS_TAG_TYPE_UINT \| 310, OH_HUKS_TAG_ATTESTATION_CHALLENGE = OH_HUKS_TAG_TYPE_BYTES \| 501, OH_HUKS_TAG_ATTESTATION_APPLICATION_ID = OH_HUKS_TAG_TYPE_BYTES \| 502, <br/> OH_HUKS_TAG_ATTESTATION_ID_ALIAS = OH_HUKS_TAG_TYPE_BYTES \| 511,<br/>OH_HUKS_TAG_ATTESTATION_ID_SEC_LEVEL_INFO = OH_HUKS_TAG_TYPE_BYTES \| 514, OH_HUKS_TAG_ATTESTATION_ID_VERSION_INFO = OH_HUKS_TAG_TYPE_BYTES \| 515,<br/>OH_HUKS_TAG_IS_KEY_ALIAS = OH_HUKS_TAG_TYPE_BOOL \| 1001, OH_HUKS_TAG_KEY_STORAGE_FLAG = OH_HUKS_TAG_TYPE_UINT \| 1002, OH_HUKS_TAG_IS_ALLOWED_WRAP = OH_HUKS_TAG_TYPE_BOOL \| 1003, OH_HUKS_TAG_KEY_WRAP_TYPE = OH_HUKS_TAG_TYPE_UINT \| 1004,<br/>OH_HUKS_TAG_KEY_AUTH_ID = OH_HUKS_TAG_TYPE_BYTES \| 1005, OH_HUKS_TAG_KEY_ROLE = OH_HUKS_TAG_TYPE_UINT \| 1006, OH_HUKS_TAG_KEY_FLAG = OH_HUKS_TAG_TYPE_UINT \| 1007, OH_HUKS_TAG_IS_ASYNCHRONIZED = OH_HUKS_TAG_TYPE_UINT \| 1008,<br/> OH_HUKS_TAG_KEY_DOMAIN = OH_HUKS_TAG_TYPE_UINT \| 1011, OH_HUKS_TAG_SYMMETRIC_KEY_DATA = OH_HUKS_TAG_TYPE_BYTES \| 20001,<br/>OH_HUKS_TAG_ASYMMETRIC_PUBLIC_KEY_DATA = OH_HUKS_TAG_TYPE_BYTES \| 20002, OH_HUKS_TAG_ASYMMETRIC_PRIVATE_KEY_DATA = OH_HUKS_TAG_TYPE_BYTES \| 20003<br/>} | Enumerates the tag values used in parameter sets.  | 
