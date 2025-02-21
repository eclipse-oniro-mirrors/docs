# Certificate and CRL Collection Development

This topic walks you through on how to filter certificates or CRLs based on a [CertCRLCollection](../../reference/apis/js-apis-cert.md#certcrlcollection11) instance.

## How to Develop

1. Import the [certFramework](../../reference/apis-device-certificate-kit/js-apis-cert.md) module.

   ```ts
   import certFramework from '@ohos.security.cert';
   ```

2. Use [cryptoCert.createX509Cert](../../reference/apis-device-certificate-kit/js-apis-cert.md#cryptocertcreatex509cert) to create an X.509 certificate instance.

3. Use [cryptoCert.createX509CRL](../../reference/apis-device-certificate-kit/js-apis-cert.md#cryptocertcreatex509crl11) to create an X.509 CRL instance.

4. Use [cryptoCert.createCertCRLCollection](../../reference/apis-device-certificate-kit/js-apis-cert.md#cryptocertcreatecertcrlcollection11) to create a [CertCRLCollection](../../reference/apis-device-certificate-kit/js-apis-cert.md#certcrlcollection11) instance.

5. Use [CertCRLCollection.selectCerts](../../reference/apis-device-certificate-kit/js-apis-cert.md#selectcerts11) to search for all certificates that match [X509CertMatchParameters](../../reference/apis-device-certificate-kit/js-apis-cert.md#x509certmatchparameters11).

6. Use [CertCRLCollection.selectCRLs](../../reference/apis-device-certificate-kit/js-apis-cert.md#selectcrls11) to search for all CRLs that match [X509CRLMatchParameters](../../reference/apis-device-certificate-kit/js-apis-cert.md#x509crlmatchparameters11).

```ts
import certFramework from '@ohos.security.cert';
import { BusinessError } from '@ohos.base';
import util from '@ohos.util';

async function createX509CRL(): Promise<certFramework.X509CRL> {
  let crlData = '-----BEGIN X509 CRL-----\n' +
    'MIHzMF4CAQMwDQYJKoZIhvcNAQEEBQAwFTETMBEGA1UEAxMKQ1JMIGlzc3VlchcN\n' +
    'MTcwODA3MTExOTU1WhcNMzIxMjE0MDA1MzIwWjAVMBMCAgPoFw0zMjEyMTQwMDUz\n' +
    'MjBaMA0GCSqGSIb3DQEBBAUAA4GBACEPHhlaCTWA42ykeaOyR0SGQIHIOUR3gcDH\n' +
    'J1LaNwiL+gDxI9rMQmlhsUGJmPIPdRs9uYyI+f854lsWYisD2PUEpn3DbEvzwYeQ\n' +
    '5SqQoPDoM+YfZZa23hoTLsu52toXobP74sf/9K501p/+8hm4ROMLBoRT86GQKY6g\n' +
    'eavsH0Q3\n' +
    '-----END X509 CRL-----\n';

  // Binary data of the CRL, which must be set based on the service.
  let textEncoder = new util.TextEncoder();
  let encodingBlob: certFramework.EncodingBlob = {
    data: textEncoder.encodeInto(crlData),
    // Set the encoding format, which can be FORMAT_PEM or FORMAT_DER.
    encodingFormat: certFramework.EncodingFormat.FORMAT_PEM
  };
  let x509CRL: certFramework.X509CRL = {} as certFramework.X509CRL;
  try {
    x509CRL = await certFramework.createX509CRL(encodingBlob);
  } catch (err) {
    let e: BusinessError = err as BusinessError;
    console.error(`createX509CRL failed, errCode: ${e.code}, errMsg: ${e.message}`);
  }
  return x509CRL;
}

async function createX509Cert(): Promise<certFramework.X509Cert> {
  let certData = '-----BEGIN CERTIFICATE-----\n' +
    'MIIBHTCBwwICA+gwCgYIKoZIzj0EAwIwGjEYMBYGA1UEAwwPRXhhbXBsZSBSb290\n' +
    'IENBMB4XDTIzMDkwNTAyNDgyMloXDTI2MDUzMTAyNDgyMlowGjEYMBYGA1UEAwwP\n' +
    'RXhhbXBsZSBSb290IENBMFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEHjG74yMI\n' +
    'ueO7z3T+dyuEIrhxTg2fqgeNB3SGfsIXlsiUfLTatUsU0i/sePnrKglj2H8Abbx9\n' +
    'PK0tsW/VgqwDIDAKBggqhkjOPQQDAgNJADBGAiEApVZno/Z7WyDc/muRN1y57uaY\n' +
    'Mjrgnvp/AMdE8qmFiDwCIQCrIYdHVO1awaPgcdALZY+uLQi6mEs/oMJLUcmaag3E\n' +
    'Qw==\n' +
    '-----END CERTIFICATE-----\n';

  let textEncoder = new util.TextEncoder();
  let encodingBlob: certFramework.EncodingBlob = {
    data: textEncoder.encodeInto(certData),
    // Set the encoding format, which can be FORMAT_PEM or FORMAT_DER.
    encodingFormat: certFramework.EncodingFormat.FORMAT_PEM
  };

  let x509Cert: certFramework.X509Cert = {} as certFramework.X509Cert;
  try {
    x509Cert = await certFramework.createX509Cert(encodingBlob);
  } catch (err) {
    let e: BusinessError = err as BusinessError;
    console.error(`createX509Cert failed, errCode: ${e.code}, errMsg: ${e.message}`);
  }
  return x509Cert;
}

async function sample() {
  const x509Cert = await createX509Cert();
  const x509CRL = await createX509CRL();
  let collection: certFramework.CertCRLCollection = {} as certFramework.CertCRLCollection;
  try {
    collection = certFramework.createCertCRLCollection([x509Cert], [x509CRL]);
    console.log('createCertCRLCollection success');
  } catch (err) {
    console.error('createCertCRLCollection failed');
  }

  const certParam: certFramework.X509CertMatchParameters = {
    validDate: '231128000000Z'
  }
  try {
    let certs: certFramework.X509Cert[] = await collection.selectCerts(certParam);
  } catch (err) {
    console.error('selectCerts failed');
  }

  const crlParam: certFramework.X509CRLMatchParameters = {
    x509Cert: x509Cert
  }
  try {
    let crls: certFramework.X509CRL[] = await collection.selectCRLs(crlParam);
    console.error('selectCRLs success');
  } catch (err) {
    console.error('selectCRLs failed');
  }
}
```


