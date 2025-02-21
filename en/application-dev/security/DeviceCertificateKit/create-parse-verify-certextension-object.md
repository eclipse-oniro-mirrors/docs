# Certificate Extension Development


This topic walks you through on how to create a certificate extension (**CertExtension**) instance, obtain the certificate extension information based on an object identifier (OID), and check whether the certificate is a CA certificate.


## How to Develop

1. Import the [certFramework](../../reference/apis-device-certificate-kit/js-apis-cert.md) module.
   ```ts
   import certFramework from '@ohos.security.cert';
   ```

2. Use [cryptoCert.createCertExtension](../../reference/apis-device-certificate-kit/js-apis-cert.md#cryptocertcreatecertextension10) to create a **CertExtension** instance.

3. Use [CertExtension.getEntry](../../reference/apis-device-certificate-kit/js-apis-cert.md#getentry10) to obtain the certificate extension of the specified OID.
     

4. Use [CertExtension.checkCA](../../reference/apis-device-certificate-kit/js-apis-cert.md#checkca10) to check whether the certificate is a CA certificate.

```ts
import certFramework from '@ohos.security.cert';
import { BusinessError } from '@ohos.base';
import util from '@ohos.util';

// Certificate extension data. The following is only an example.
let extData = new Uint8Array([
  0x30, 0x40, 0x30, 0x0F, 0x06, 0x03, 0x55, 0x1D,
  0x13, 0x01, 0x01, 0xFF, 0x04, 0x05, 0x30, 0x03,
  0x01, 0x01, 0xFF, 0x30, 0x0E, 0x06, 0x03, 0x55,
  0x1D, 0x0F, 0x01, 0x01, 0xFF, 0x04, 0x04, 0x03,
  0x02, 0x01, 0xC6, 0x30, 0x1D, 0x06, 0x03, 0x55,
  0x1D, 0x0E, 0x04, 0x16, 0x04, 0x14, 0xE0, 0x8C,
  0x9B, 0xDB, 0x25, 0x49, 0xB3, 0xF1, 0x7C, 0x86,
  0xD6, 0xB2, 0x42, 0x87, 0x0B, 0xD0, 0x6B, 0xA0,
  0xD9, 0xE4
]);

// Certificate extension example.
function certExtensionSample(): void {
  let textEncoder = new util.TextEncoder();
  let encodingBlob: certFramework.EncodingBlob = {
    data: extData,
    // Certificate extension format. Currently, only the DER format is supported.
    encodingFormat: certFramework.EncodingFormat.FORMAT_DER
  };

  // Create a CertExtension instance.
  certFramework.createCertExtension(encodingBlob, (err, certExtension) => {
    if (err != null) {
      // The CertExtension instance fails to be created.
      console.error(`createCertExtension failed, errCode:${err.code}, errMsg:${err.message} `);
      return;
    }
    // The CertExtension instance is created.
    console.log('createCertExtension success');

    try {
      // Obtain the certificate extension information based on an OID.
      let oidData = '2.5.29.14';
      let oid: certFramework.DataBlob = {
        data: textEncoder.encodeInto(oidData),
      }
      let entry = certExtension.getEntry(certFramework.ExtensionEntryType.EXTENSION_ENTRY_TYPE_ENTRY, oid);

      // Check whether the certificate is a CA certificate.
      let pathLen = certExtension.checkCA();
      console.log('test cert extension success');
    } catch (err) {
      let e: BusinessError = err as BusinessError;
      console.error(`operation failed, message:${e.message} ,code:${e.code} `);
    }
  });
}
```
