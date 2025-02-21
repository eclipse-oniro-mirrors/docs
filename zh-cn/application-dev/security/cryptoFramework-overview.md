# 加解密算法库框架概述
加解密算法库框架是一个屏蔽了第三方密码学算法库实现差异的算法框架，提供加解密、签名验签、消息验证码、哈希、安全随机数等相关功能。开发者可以通过调用加解密算法库框架，忽略底层不同三方算法库的差异，实现迅捷开发。

> **说明：** 加解密算法库框架仅提供密钥的密码学操作，而不提供密钥管理功能。因此，使用算法库时，需要应用自己来保管密钥（适用于临时会话密钥等仅在内存中使用的场景，或者应用自己实现密钥安全存储的场景）。如果业务需要由系统提供密钥管理功能（密钥存储等），请使用[HUKS部件](huks-overview.md)。

## 框架实现原理
加解密算法库框架提供的组件分为三层：接口层，Framework层和插件层。接口层负责对外提供统一的JS接口，插件层实现针对具体三方算法库的功能，Framework层通过灵活加载插件层的插件适配并屏蔽三方算法库差异。

## 基本概念
**对称密钥**

对称密钥使用同一个密钥对数据进行加密解密操作。即对称加密算法中，数据发送方使用加密密钥对明文进行特殊加密算法处理后，使其变成复杂的加密密文发送出去。接收方收到密文后，若想解读原文，则需要使用同一个加密密钥以及相同算法的逆算法对密文进行解密，才能使其恢复成可读明文。

- **AES加密**

  AES的全称是Advanced Encryption Standard，是最常见的对称加密。AES为分组密码，分组密码也就是把明文分成一组一组的，每组长度相等，每次加密一组数据，直到加密完整个明文。在AES标准规范中，分组长度只能是128位，也就是说，每个分组为16个字节（每个字节8位）。密钥的长度可以使用128位、192位或256位。
- **3DES加密**
  
  3DES，也称为 3DESede 或 TripleDES，是三重数据加密算法，相当于是对每个数据块应用三次DES的对称加密算法，它使用3个64位的密钥对数据块进行三次加密。相比DES，3DES因密钥长度变长，安全性有所提高，但其处理速度不高。因此又出现了AES加密算法，AES较于3DES速度更快、安全性更高。

**非对称密钥**

非对称密钥使用公钥和私钥两个密钥来进行算法操作，公钥对外公开，私钥对外保密。对于加解密操作，一般使用公钥对明文进行加密形成密文，持有私钥的人即可对密文解密形成明文。对于签名验签操作，使用私钥对明文进行签名，公钥持有者可以通过公钥对签名数据做验签，验证数据是否被篡改。

- **RSA密钥**

  RSA密钥以极大整数做因数分解的数学难题作为密钥安全性的基石。生成密钥时，首先需要随机出两个大素数p和q，计算n = p * q并将n做为模，再选择一个大于1且小于(p - 1) * (q - 1)的整数e，确保e与(p - 1)*(q - 1)互素，最后计算d，使得e * d - 1为(p - 1)和(q - 1)的倍数，则可得到公钥(n, e)和私钥(n, d)。

  算法库框架除提供了默认的双素数RSA密钥生成外，还提供了多素数密钥生成方式，可以在密钥生成时通过指定primes参数（PRIMES_2, PRIMES_3, PRIMES_4, PRIMES_5）指定素数个数。多素数密钥的优点是可以减少解密、签名的计算量（中国剩余定理），但相对的劣势是密钥强度会越低，算法库依据OpenSSL的素数使用规则制定了相应规格，具体将在**约束与限制**章节中说明。
- **ECC密钥**
  
  ECC是一种基于椭圆曲线数学的公开密钥加密算法，其数学基础是利用椭圆曲线上的有理点构成Abel加法群上椭圆离散对数的计算困难性，算法库框架提供了多种椭圆曲线的ECC密钥生成能力。

**加解密**

- **对称AES加解密**

  算法库目前提供了AES加解密常用的7种加密模式：ECB、CBC、OFB、CFB、CTR、GCM和CCM。AES为分组加密算法，分组长度大小为128位。实际应用中明文最后一组可能不足128位，不足数据可以使用各种padding模式做数据填充。下文中描述了各个padding的区别：
	- NoPadding：不带填充；
	- PKCS5：填充字符由一个字节序列组成，每个字节填充该填充字节序列的长度，规定是8字节填充；
	- PKCS7：填充字符和PKCS5填充方法一致，但是可以在1-255字节之间任意填充；

  > **说明：** ECB、CBC加密模式，明文长度不是128位整数倍，必须使用填充方法补足。<br/>由于需要填充至分组大小，所以实际算法库中的PKCS5和PKCS7都是以分组大小作为填充长度的，即AES加密填充至16字节。
- **对称3DES加解密**

  该算法的加解密过程分别是对明文/密文数据进行三次DES加密或解密，得到相应的密文或明文。

  算法库目前提供了3DES加解密常用的4种加密模式：ECB、CBC、OFB和CFB。DES为分组加密算法，分组长度大小为64位。实际应用中明文最后一组可能不足64位，不足数据可以使用各种padding模式做数据填充。下文中描述了各个padding的区别：
	- NoPadding：不带填充；
	- PKCS5：填充字符由一个字节序列组成，每个字节填充该填充字节序列的长度，规定是8字节填充；
	- PKCS7：填充字符和PKCS5填充方法一致，但是可以在1-255字节之间任意填充；

  > **说明：** ECB、CBC加密模式，明文长度不是64位整数倍，必须使用填充方法补足。<br/>由于需要填充至分组大小，所以实际算法库中的PKCS5和PKCS7都是以分组大小作为填充长度的，即3DES加密填充至8字节。

- **非对称RSA加解密**

  当持有RSA公钥(n, e)和私钥(n, d)后，RSA加密过程为：密文 = 明文 ^ e mod n, 解密过程为：明文 = 密文 ^ d mod n。算法库目前提供了RSA加解密常用的三种模式：PKCS1、PKCS1_OAEP和NoPadding。RSA为块加密算法，加密长度需要在固定长度进行，实际应用中会使用各种padding模式做数据填充。下文中描述了各个padding的区别：
	- NoPadding：不带填充，输入的数据必须与RSA钥模一样长，输出数据长度与RSA钥模一样长；
	- PKCS1：pkcs1padding V1.5是RSA加解密默认的填充方式，输入的数据必须<=RSA钥模-11，输出数据长度与RSA钥模一样长；
	- PKCS1_OAEP：RSA_PKCS1_OAEP_PADDING填充模式是PKCS#1推出的新填充方式，此模式需要设置两个摘要（md和mgf1_md），输入的数据必须小于RSA钥模 - md摘要长度 - mgf1_md摘要长度 - 2，输出数据长度与RSA钥模一样长；<br/>

  **补充说明：** RSA钥模 = (RSA的bits + 7) / 8

**签名验签**

- **RSA签名验签**

	当持有RSA公钥(n, e)和私钥(n, d)后，RSA签名生成过程为：签名 = 消息 ^ d mod n, 验签过程为：消息 = 签名 ^ d mod n。消息发送方发送数据时，同时发送消息和私钥签名后的签名信息，消息接收方接受到数据后，将签名信息用公钥解密并验证消息是否一致。因发送的消息长度大多大于RSA钥模，因此算法库框架提供了两种padding模式，通过摘要提取消息的散列值再做签名。算法库框架中提供了签名验签相关的两种模式：PKCS1和PSS。下问对两种模式做详细描述：
  - PKCS1: pkcs1padding V1.5是RSA加解密默认的填充方式，使用该模式时需要设置摘要（md）；
  - PSS: PSS模式是RSA 算法的基础上叠加上一种填充算法，使用该签名算法时需要使用摘要(md)和掩码函数（mgf1_md）;
- **ECDSA**

  椭圆曲线数字签名算法（ECDSA）是基于椭圆曲线密码（ECC）模拟数字签名算法（DSA）。相比普通的离散对数问题（DLP）和大数分解问题（IFP），椭圆曲线密码的单位比特强度要高于其他公钥体制。算法库框架提供了多种椭圆曲线及摘要算法组合的椭圆曲线数字签名算法（ECDSA）能力。

**密钥协商**

- **ECDH**

  ECDH的全称是椭圆曲线迪菲-赫尔曼秘钥交换，是用来在一个非安全通道中建立起安全的共有加密资料，交换双方可以在不共享任何秘密的情况下协商出一个密钥。算法库框架基于开源算法库提供了多种椭圆曲线的ECDH能力。

**摘要**

消息摘要MD算法是一种能将任意长度的输入消息，通过哈希算法生成长度固定的摘要的算法。消息摘要算法通过其不可逆的特性能被用于敏感信息的加密。消息摘要算法也被称为哈希算法或单向散列算法。
在摘要算法相同时，生成的摘要值主要有下列特点：

- 当输入消息相同时，生成摘要序列相同； 
- 当输入消息的长度不一致时，生成摘要序列长度固定（摘要长度由算法决定）； 
- 当输入消息不一致时，生成摘要序列几乎不会相同（依然存在相同概率，由摘要长度决定相同概率）；

消息摘要算法主要分为三类：MD，SHA与MAC（详见HMAC章节）
MD算法包括MD2，MD4和MD5。
SHA算法主要包括SHA1，SHA224，SHA256，SHA384，SHA512。

**消息验证码**

HMAC（Hash-based Message Authentication Code）是一种基于密钥的消息认证码算法。HMAC通过指定摘要算法，以通信双方共享密钥与消息作为输入，生成消息认证码用于检验传递报文的完整性，HMAC生成的消息认证码为固定长度。HMAC在消息摘要算法的基础上增加了密钥的输入，确保了信息的正确性。

**随机数**

随机数在加解密过程中主要用于临时会话密钥的生成与非对称加密算法中密钥的生成。随机数由硬件生成的硬件随机数生成器或由软件生成的伪随机数生成器进行生成。在加解密的场景中，安全随机数生成器需要具备随机性，不可预测性，与不可重现性。密码学安全伪随机数生成器CSPRNG（Cryptography Secure Random Number Generators）生成的随机数满足密码学安全伪随机性

- **内部状态**代表随机数生成器内存中的数值，当内部状态相同时，随机数生成器会生成固定的随机数序列
- **种子**（seed）是一个用来对伪随机数的内部状态进行初始化的数据，随机数生成器通过种子来生成一系列的随机序列。


## 约束与限制

- 算法库框架不支持多线程并发操作。
- 算法库当前只支持OpenSSL。

### 密钥生成规格

**对称密钥生成规格**

- 支持的对称密钥生成参数：

  |对称密钥算法|密钥长度（bit）|字符串参数|
  |---|---|---|
  |3DES|192|3DES192|
  |AES|128|AES128|
  |AES|192|AES192|
  |AES|256|AES256|

  > **说明**：“字符串参数”是“对称密钥算法”和“密钥长度”拼接而成，用于在创建对称密钥生成器时，指定密钥规格。

**非对称密钥生成规格**
- **RSA密钥生成**

  支持的非对称密钥生成参数：

  |非对称密钥类型|素数个数|字符串参数|
  |---|---|---|
  |RSA512|2|RSA512\|PRIMES_2|
  |RSA768|2|RSA768\|PRIMES_2|
  |RSA1024|2|RSA1024\|PRIMES_2|
  |RSA1024|3|RSA1024\|PRIMES_3|
  |RSA2048|2|RSA2048\|PRIMES_2|
  |RSA2048|3|RSA2048\|PRIMES_3|
  |RSA3072|2|RSA3072\|PRIMES_2|
  |RSA3072|3|RSA3072\|PRIMES_3|
  |RSA4096|2|RSA4096\|PRIMES_2|
  |RSA4096|3|RSA4096\|PRIMES_3|
  |RSA4096|4|RSA4096\|PRIMES_4|
  |RSA8192|2|RSA8192\|PRIMES_2|
  |RSA8192|3|RSA8192\|PRIMES_3|
  |RSA8192|4|RSA8192\|PRIMES_4|
  |RSA8192|5|RSA8192\|PRIMES_5|

  > **说明**：生成RSA非对称密钥时，默认素数为2，PRIMES_2参数可省略。

- **ECC密钥生成**

  支持的非对称密钥生成参数：

  |非对称密钥算法|密钥长度|
  |---|---|
  |ECC|ECC224|
  |ECC|ECC256|
  |ECC|ECC384|
  |ECC|ECC521|

### 加解密规格

**对称加解密**

- 支持的对称加密算法：

  |对称加解密算法|分组模式| 字符串参数                                         |
  |---|---|---|
  |3DES|ECB|3DES192\|ECB\|[NoPadding\|PKCS5\|PKCS7]|
  |3DES|CBC|3DES192\|CBC\|[NoPadding\|PKCS5\|PKCS7]|
  |3DES|OFB|3DES192\|OFB\|[NoPadding\|PKCS5\|PKCS7]|
  |3DES|CFB|3DES192\|CFB\|[NoPadding\|PKCS5\|PKCS7]|
  |AES|ECB|AES[128\|192\|256]\|ECB\|[NoPadding\|PKCS5\|PKCS7]|
  |AES|CBC|AES[128\|192\|256]\|CBC\|[NoPadding\|PKCS5\|PKCS7]|
  |AES|CTR|AES[128\|192\|256]\|CTR\|[NoPadding\|PKCS5\|PKCS7]|
  |AES|OFB|AES[128\|192\|256]\|OFB\|[NoPadding\|PKCS5\|PKCS7]|
  |AES|CFB|AES[128\|192\|256]\|CFB\|[NoPadding\|PKCS5\|PKCS7]|
  |AES|GCM|AES[128\|192\|256]\|GCM\|[NoPadding\|PKCS5\|PKCS7]|
  |AES|CCM|AES[128\|192\|256]\|CCM\|[NoPadding\|PKCS5\|PKCS7]|

> **说明：** 
> 
> 1. []中只能任选一项。
> 2. “字符串参数”是“对称加解密算法（含密钥长度）”、“分组模式”、“填充模式”拼接而成，用于在创建对称加解密实例时，指定对称加解密算法规格。

**非对称RSA加解密**

RSA加解密时，涉及三种填充模式：NoPadding, PKCS1和PKCS1_OAEP。
- 使用NoPadding模式时可以指定的参数:

  |非对称密钥类型| 填充模式 | 字符串参数 |
  |---|---|---|
  |RSA512|NoPadding|RSA512\|NoPadding|
  |RSA768|NoPadding|RSA768\|NoPadding|
  |RSA1024|NoPadding|RSA1024\|NoPadding|
  |RSA2048|NoPadding|RSA2048\|NoPadding|
  |RSA3072|NoPadding|RSA3072\|NoPadding|
  |RSA4096|NoPadding|RSA4096\|NoPadding|
  |RSA8192|NoPadding|RSA8192\|NoPadding|

- 使用PKCS1模式时可以指定的参数: 

  |非对称密钥类型| 填充模式 | 字符串参数 |
  |---|---|---|
  |RSA512|PKCS1|RSA512\|PKCS1|
  |RSA768|PKCS1|RSA768\|PKCS1|
  |RSA1024|PKCS1|RSA1024\|PKCS1|
  |RSA2048|PKCS1|RSA2048\|PKCS1|
  |RSA3072|PKCS1|RSA3072\|PKCS1|
  |RSA4096|PKCS1|RSA4096\|PKCS1|
  |RSA8192|PKCS1|RSA8192\|PKCS1|

- 使用PKCS1_OAEP模式时可以指定的参数：
  > **说明：** 
  > 
  > 1.[]内的参数只能任选一项，非[]内的为固定值；
  > 2.使用时请从表格中选择非对称密钥类型、填充模式、摘要、掩码摘要四个数据，用|拼接成字符串。
  >   例如："RSA2048|PKCS1_OAEP|SHA256|MGF1_SHA256"

  | 非对称密钥类型 | 填充模式 | 摘要 | 掩码摘要 |
  |---|---|---|---|
  |RSA512|PKCS1_OAEP|MD5|  [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256]|
  |RSA512|PKCS1_OAEP|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256]|
  |RSA512|PKCS1_OAEP|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256]|
  |RSA512|PKCS1_OAEP|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224]
  |RSA768|PKCS1_OAEP|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA768|PKCS1_OAEP|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA768|PKCS1_OAEP|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA768|PKCS1_OAEP|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384]|
  |RSA768|PKCS1_OAEP|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256]|
  |RSA768|PKCS1_OAEP|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224]|
  |RSA1024|PKCS1_OAEP|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PKCS1_OAEP|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PKCS1_OAEP|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PKCS1_OAEP|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PKCS1_OAEP|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PKCS1_OAEP|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384]|
  |RSA2048|PKCS1_OAEP|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PKCS1_OAEP|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PKCS1_OAEP|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PKCS1_OAEP|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PKCS1_OAEP|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PKCS1_OAEP|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PKCS1_OAEP|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PKCS1_OAEP|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PKCS1_OAEP|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PKCS1_OAEP|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PKCS1_OAEP|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PKCS1_OAEP|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PKCS1_OAEP|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PKCS1_OAEP|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PKCS1_OAEP|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PKCS1_OAEP|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PKCS1_OAEP|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PKCS1_OAEP|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PKCS1_OAEP|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PKCS1_OAEP|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PKCS1_OAEP|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PKCS1_OAEP|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512  ]|
  |RSA8192|PKCS1_OAEP|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PKCS1_OAEP|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|


### 签名验签规格

**RSA签名验签**

RSA签名验签时，涉及两种填充模式：PKCS1和PSS。
-  使用PKCS1模式时可以指定的参数: 

  | 非对称密钥类型 | 填充模式 | 摘要 | 字符串参数 |
  |---|---|---|---|
  |RSA512|PKCS1|[MD5\|SHA1\|SHA224\|SHA256\|SHA384]|RSA512\|PKCS1\|  [MD5\|SHA1\|SHA224\|SHA256\|SHA384]|
  |RSA768|PKCS1|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|RSA768\|PKCS1\|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|
  |RSA1024|PKCS1|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|RSA1024\|PKCS1\|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|
  |RSA2048|PKCS1|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|RSA2048\|PKCS1\|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|
  |RSA3072|PKCS1|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|RSA3072\|PKCS1\|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|
  |RSA4096|PKCS1|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|RSA4096\|PKCS1\|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|
  |RSA8192|PKCS1|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|RSA8192\|PKCS1\|[MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512]|

- 使用PSS模式时可以指定的参数：
  > **说明：** 
  > 
  > 1.[]内的参数只能任选一项，非[]内的为固定值；
  > 2.使用时请从表格中选择非对称密钥类型、填充模式、摘要、掩码摘要四个数据，用|拼接成字符串。
  >  例如："RSA2048|PSS|SHA256|MGF1_SHA256"

  | 非对称密钥类型 | 填充模式 | 摘要 | 掩码摘要 |
  |---|---|---|---|
  |RSA512|PSS|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256]|
  |RSA512|PSS|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256]|
  |RSA512|PSS|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256]|
  |RSA512|PSS|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224]|RSA512\|PSS\|SHA256\|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224]|
  |RSA768|PSS|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA768|PSS|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA768|PSS|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA768|PSS|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384]|
  |RSA768|PSS|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256]|
  |RSA768|PSS|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224]|
  |RSA1024|PSS|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PSS|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PSS|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PSS|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PSS|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA1024|PSS|SHA512| [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384]|
  |RSA2048|PSS|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PSS|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PSS|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PSS|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PSS|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA2048|PSS|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PSS|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PSS|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PSS|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PSS|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PSS|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA3072|PSS|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PSS|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PSS|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PSS|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PSS|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PSS|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA4096|PSS|SHA512|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PSS|MD5|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PSS|SHA1|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PSS|SHA224|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PSS|SHA256|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PSS|SHA384|[MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|
  |RSA8192|PSS|SHA512| [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512]|

**ECDSA签名验签**

- 支持的ECDSA参数：

  |非对称密钥算法|支持种类|
  |---|---|
  |ECC|ECC224|
  |ECC|ECC256|
  |ECC|ECC384|
  |ECC|ECC521|

  |摘要算法|支持种类|
  |---|---|
  |HASH|SHA1|
  |HASH|SHA224|
  |HASH|SHA256|
  |HASH|SHA384|
  |HASH|SHA512|

### 密钥协商规格

**ECDH**

- 支持的ECDH参数：

  |非对称密钥算法|支持种类|
  |---|---|
  |ECC|ECC224|
  |ECC|ECC256|
  |ECC|ECC384|
  |ECC|ECC521|

### MD消息摘要算法规格
- 加解密算法库框架当前支持的MD算法参数：

  |摘要算法|支持种类|
  |---|---|
  |HASH|SHA1|
  |HASH|SHA224|
  |HASH|SHA256|
  |HASH|SHA384|
  |HASH|SHA512|
  |HASH|MD5|

### HMAC消息认证码算法规格
- 加解密算法库框架当前支持的HMAC算法参数：

  |摘要算法|支持种类|
  |---|---|
  |HASH|SHA1|
  |HASH|SHA224|
  |HASH|SHA256|
  |HASH|SHA384|
  |HASH|SHA512|
