# Key Derivation Overview and Algorithm Specifications


To stretch keys into longer keys or to obtain keys in the required format, you can use the HUKS APIs to derive one or more secrete keys from a key (base key) by using a pseudorandom function.


## Supported Algorithms

The following table lists the supported key derivation specifications.

The key management service specifications include mandatory specifications and optional specifications. Mandatory specifications are algorithm specifications that must be supported. Optional specifications can be used based on actual situation. Before using the optional specifications, refer to the documents provided by the vendor to ensure that the specifications are supported.

**You are advised to use mandatory specifications in your development for compatibility purposes.**

A derived key is the key session result obtained using the Init-Update-Finish mechanism. It can be managed by HUKS (the key is always in a TEE) or independently managed by the service based on service requirements.

| Algorithm/MD| Algorithm/Length of the Base Key| Available Algorithm/Length of the Derived Key| API Level| Mandatory| 
| -------- | -------- | -------- | -------- | -------- |
| HKDF/SHA256 | AES/192-256 | AES/128/192/256<br>HMAC/8-1024<br>SM4/128 | 8+ | Yes| 
| HKDF/SHA384 | AES/256 | AES/128/192/256<br>HMAC/8-1024<br>SM4/128 | 8+ | Yes| 
| HKDF/SHA512 | AES/256 | AES/128/192/256<br>HMAC/8-1024<br>SM4/128 | 8+ | Yes| 
| PBKDF2/SHA256 | AES/192-256 | AES/128/192/256<br>HMAC/8-1024<br>SM4/128 | 8+ | Yes| 
| PBKDF2/SHA384 | AES/256 | AES/128/192/256<br>HMAC/8-1024<br>SM4/128 | 8+ | Yes| 
| PBKDF2/SHA512 | AES/256 | AES/128/192/256<br>HMAC/8-1024<br>SM4/128 | 8+ | Yes| 
