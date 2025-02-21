# Key Attestation Overview and Algorithm Specifications


HUKS provides attestation for the public keys of asymmetric key pairs.


HUKS issues a certificate for the public key of an asymmetric key pair stored in HUKS using the public key infrastructure (PKI) certificate chain technology. The certificate can prove the validity of the public key. The service can use the root CA certificate provided by the system to verify the key certificates issued by HUKS level by level to ensure that the public key and private key in the certificates are from a trusted hardware device and stored in HUKS. 

The key attestation process is as follows:


1. The service transfers the key alias and properties to HUKS.

2. HUKS issues an X.509 certificate chain, which consists of the root CA certificate, device CA certificate, device certificate, and key certificate in sequence, for the application.

3. The certificate chain is sent to a trusted server. The server parses the certificate chain and verifies the certificate chain validity and whether a single certificate is revoked.

Currently, the system provides two key attestation modes.
- Anonymous key attestation: This type of attestation will not disclose the caller identity information, and the caller does not require any permission. It is available to all applications. To protect user identity information, third-party applications can use anonymous attestation only.
- Non-anonymous key attestation: The identity information of the caller can be viewed, and the caller must have the ohos.permission.ATTEST_KEY permission. It is available only for system applications.


## Supported Algorithms

The following table lists the supported key attestation specifications.

The key management service specifications include mandatory specifications and optional specifications. Mandatory specifications are algorithm specifications that must be supported. Optional specifications can be used based on actual situation. Before using the optional specifications, refer to the documents provided by the vendor to ensure that the specifications are supported.

**You are advised to use mandatory specifications in your development for compatibility purposes.**

| Algorithm| Description| API Level| Mandatory| 
| -------- | -------- | -------- | -------- |
| RSA | The padding mode can be PSS or PKCS1_V1_5.| 8+ | Yes| 
| ECC | - | 8+ | Yes| 
| SM2 | - | 8+ | Yes| 
