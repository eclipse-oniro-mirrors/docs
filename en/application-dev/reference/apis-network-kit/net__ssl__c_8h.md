# net_ssl_c.h


## Overview

Defines C APIs for the SSL/TLS certificate chain verification module.

**Library**: libnet_ssl.so

**System capability**: SystemCapability.Communication.NetStack

**Since**: 11

**Related module**: [Netstack](netstack.md)


## Summary


### Callback

| Name| Description|
| -------- | -------- |
| [OH_NetStack_CertVerification](netstack.md#oh_netstack_certverification) (const struct [NetStack_CertBlob](_net_stack___cert_blob.md) \*cert, const struct [NetStack_CertBlob](_net_stack___cert_blob.md) \*caCert) | Verifies the certificate chain.|
| [OH_NetStack_GetPinSetForHostName](netstack.md#oh_netstack_getpinsetforhostname)(const char \*hostname, [NetStack_CertificatePinning](_net_stack___certificate_pinning.md) \*pin) | Obtains the certificate lock information.|
| [OH_NetStack_GetCertificatesForHostName](netstack.md#oh_netstack_getcertificatesforhostname)(const char \*hostname, [NetStack_Certificates](_net_stack___certificates.md) \*certs) | Obtains certificate information.|
| [OH_Netstack_DestroyCertificatesContent](netstack.md#oh_netstack_destroycertificatescontent)([NetStack_Certificates](_net_stack___certificates.md) \*certs) | Releases the certificate content.|
