# @ohos.net.vpnExtension (Enhanced VPN Management)

The **vpnExtension** module implements virtual private network (VPN) management, such as starting and stopping a third-party VPN.
Third-party VPNs refer to VPN services provided by third parties. They usually provide more security and privacy functions and more comprehensive customization options.

> **NOTE**
> The initial APIs of this module are supported since API version 11. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import vpnExt from "@ohos.net.vpnExtension";
```

## vpnExt.startVpnExtensionAbility

startVpnExtensionAbility(want: Want): Promise\<void>

Enables the VPN extension ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core.

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name| Type                               | Mandatory| Description              |
| ------ | ----------------------------------- | ---- | ------------------ |
| want   | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | Yes  | Want information.|

**Return value**

| Type          | Description                   |
| -------------- | ----------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message                              |
| --------- | -------------------------------------- |
| 401       | Parameter error.                       |
| 16000001  | The specified ability does not exist.  |
| 16000002  | Incorrect ability type.                |
| 16000006  | Cross-user operations are not allowed. |
| 16000008  | The crowdtesting application expires.  |
| 16000011  | The context does not exist.            |
| 16000050  | Internal error.                        |
| 16200001  | The caller has been released.          |

**Example**
Stage model:

```ts
import common from '@ohos.app.ability.common';
import Want from '@ohos.app.ability.Want';
import vpnExt from '@ohos.net.vpnExtension';

let context = getContext(this) as common.VpnExtensionContext;
let want: Want = {
  deviceId: "",
  bundleName: "com.example.myvpndemo",
  abilityName: "MyVpnExtAbility",
};

@Entry
@Component
struct Index {
  @State message: string = 'Hello World'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold).onClick(() => {
          console.info("btn click") })
        Button('Start Extension').onClick(() => {
          vpnExt.startVpnExtensionAbility(want);
        }).width('70%').fontSize(45).margin(16)
        }.width('100%')
    }.height('100%')
  }
}
```

## vpnExt.stopVpnExtensionAbility

stopVpnExtensionAbility(want: Want): Promise\<void>

Stops the VPN extension ability.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core.

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name| Type                               | Mandatory| Description            |
| ------ | ----------------------------------- | ---- | ---------------- |
| want   | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | Yes  | Want information.|

**Return value**

| Type          | Description                   |
| -------------- | ----------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message                              |
| --------- | -------------------------------------- |
| 401       | Parameter error.                       |
| 16000001  | The specified ability does not exist.  |
| 16000002  | Incorrect ability type.                |
| 16000006  | Cross-user operations are not allowed. |
| 16000011  | The context does not exist.            |
| 16000050  | Internal error.                        |
| 16200001  | The caller has been released.          |

**Example**
Stage model:

```ts
import common from '@ohos.app.ability.common';
import Want from '@ohos.app.ability.Want';
import vpnExt from '@ohos.net.vpnExtension';

let context = getContext(this) as common.VpnExtensionContext;
let want: Want = {
  deviceId: "",
  bundleName: "com.example.myvpndemo",
  abilityName: "MyVpnExtAbility",
};

@Entry
@Component
struct Index {
  @State message: string = 'Hello World'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold).onClick(() => {
          console.info("btn click") })
        Button('Start Extension').onClick(() => {
          vpnExt.startVpnExtensionAbility(want);
        }).width('70%').fontSize(45).margin(16)
        Button('Stop Extension').onClick(() => {
          console.info("btn end")
          vpnExt.stopVpnExtensionAbility(want);
        }).width('70%').fontSize(45).margin(16)

        }.width('100%')
    }.height('100%')
  }
}
```


## vpnExt.createVpnConnection

createVpnConnection(context: VpnExtensionContext): VpnConnection

Creates a **VpnConnection** object.

**System capability**: SystemCapability.Communication.NetManager.Vpn

**Model restriction**: This API can be used only in the stage model.

**Parameters**

| Name | Type                                                        | Mandatory| Description          |
| ------- | ------------------------------------------------------------ | ---- | -------------- |
| context | [VpnExtensionContext](js-apis-inner-application-VpnExtensionContext.md) | Yes  | Specified context.|

**Return value**

| Type                           | Description                   |
| :------------------------------ | :---------------------- |
| [VpnConnection](#vpnconnection) | **VpnConnection** object.|

**Error codes**

| ID| Error Message        |
| --------- | ---------------- |
| 401       | Parameter error. |

**Example**
Stage model:

```ts
import vpnExt from '@ohos.net.vpnExtension';
import common from '@ohos.app.ability.common';
import Want from '@ohos.app.ability.Want';
import VpnExtensionAbility from '@ohos.app.ability.VpnExtensionAbility';

let context: vpnExt.VpnExtensionContext;
export default class MyVpnExtAbility extends VpnExtensionAbility {
  onCreate(want: Want) {
    let VpnConnection : vpnExt.VpnConnection = vpnExt.createVpnConnection(context);
    console.info("vpn createVpnConnection: " + JSON.stringify(VpnConnection));
  }
}
```

## VpnConnection

Defines a **VpnConnection** object. Before calling **VpnConnection** APIs, you need to create a VPN connection object by calling **vpnExt.createVpnConnection**.

### create

create(config: VpnConfig): Promise\<number\>

Creates a VPN based on the specified configuration. This API uses a promise to return the result.

**System capability**: SystemCapability.Communication.NetManager.Vpn

**Parameters**

| Name| Type                   | Mandatory| Description                     |
| ------ | ----------------------- | ---- | ------------------------- |
| config | [VpnConfig](#vpnconfig) | Yes  | VPN configuration.|

**Return value**

| Type             | Description                                                          |
| ----------------- | -------------------------------------------------------------- |
| Promise\<number\> | Promise used to return the result, which is the file descriptor of the vNIC.|

**Error codes**

| ID| Error Message                                        |
| --------- | ------------------------------------------------ |
| 401       | Parameter error.                                 |
| 2200001   | Invalid parameter value.                         |
| 2200002   | Operation failed. Cannot connect to service.     |
| 2200003   | System internal error.                           |
| 2203001   | VPN creation denied, please check the user type. |
| 2203002   | VPN exist already, please execute destroy first. |

**Example**

```js
import vpnExt from '@ohos.net.vpnExtension';
import Want from '@ohos.app.ability.Want';
import common from '@ohos.app.ability.common';
import VpnExtensionAbility from '@ohos.app.ability.VpnExtensionAbility';
import hilog from '@ohos.hilog';

let context: vpnExt.VpnExtensionContext;
export default class MyVpnExtAbility extends VpnExtensionAbility {
  private tunIp: string = '10.0.0.5';
  private blockedAppName: string = 'com.example.myvpndemo';
  onCreate(want: Want) {
    let VpnConnection : vpnExt.VpnConnection = vpnExt.createVpnConnection(context);
    console.info("vpn createVpnConnection: " + JSON.stringify(VpnConnection));
    this.SetupVpn();
  }
  SetupVpn() {
        class Address {
            address: string;
            family: number;

            constructor(address: string, family: number) {
                this.address = address;
                this.family = family;
            }
        }

        class AddressWithPrefix {
            address: Address;
            prefixLength: number;

            constructor(address: Address, prefixLength: number) {
                this.address = address;
                this.prefixLength = prefixLength;
            }
        }

        class Config {
            addresses: AddressWithPrefix[];
            mtu: number;
            dnsAddresses: string[];
            trustedApplications: string[];
            blockedApplications: string[];

            constructor(
                tunIp: string,
                blockedAppName: string
            ) {
                this.addresses = [
                    new AddressWithPrefix(new Address(tunIp, 1), 24)
                ];
                this.mtu = 1400;
                this.dnsAddresses = ["114.114.114.114"];
                this.trustedApplications = [];
                this.blockedApplications = [blockedAppName];
            }
        }

        let config = new Config(this.tunIp, this.blockedAppName);

        try {
            let VpnConnection : vpnExt.VpnConnection = vpnExt.createVpnConnection(context);
            VpnConnection.create(config).then((data) => {
                hilog.error(0x0000, 'developTag', 'tunfd: %{public}s', JSON.stringify(data) ?? '');
            })
        } catch (error) {
            hilog.error(0x0000, 'developTag', 'vpn setUp fail: %{public}s', JSON.stringify(error) ?? '');
        }
    }
}
```

### protect

protect(socketFd: number): Promise\<void\>

Protects sockets against a VPN connection. The data sent through sockets is directly transmitted over the physical network and therefore the traffic does not traverse through the VPN. This API uses a promise to return the result.

**System capability**: SystemCapability.Communication.NetManager.Vpn

**Parameters**

| Name  | Type  | Mandatory| Description                                                                                       |
| -------- | ------ | ---- | ------------------------------------------------------------------------------------------- |
| socketFd | number | Yes  | Socket file descriptor. It can be obtained through [getSocketFd](js-apis-socket.md#getsocketfd10-1).|

**Return value**

| Type           | Description                                                 |
| --------------- | ----------------------------------------------------- |
| Promise\<void\> | Promise used to return the result. If the operation is successful, the operation result is returned. If the operation fails, an error message is returned.|

**Error codes**

| ID| Error Message                                    |
| --------- | -------------------------------------------- |
| 401       | Parameter error.                             |
| 2200001   | Invalid parameter value.                     |
| 2200002   | Operation failed. Cannot connect to service. |
| 2200003   | System internal error.                       |
| 2203004   | Invalid socket file descriptor.              |

**Example**

```js
import vpnExt from '@ohos.net.vpnExtension';
import Want from '@ohos.app.ability.Want';
import VpnExtensionAbility from '@ohos.app.ability.VpnExtensionAbility';
import hilog from '@ohos.hilog';

let g_tunnelFd = -1;
let context: vpnExt.VpnExtensionContext;
export default class MyVpnExtAbility extends VpnExtensionAbility {
  private vpnServerIp: string = '192.168.31.13';
  onCreate(want: Want) {
    let VpnConnection : vpnExt.VpnConnection = vpnExt.createVpnConnection(context);
    console.info("vpn createVpnConnection: " + JSON.stringify(VpnConnection));
    this.CreateTunnel();
    this.Protect();
  }
  CreateTunnel() {
      g_tunnelFd = 8888;
  }
  Protect() {
        hilog.info(0x0000, 'developTag', '%{public}s', 'vpn Protect');
        let VpnConnection : vpnExt.VpnConnection = vpnExt.createVpnConnection(context);
        VpnConnection.protect(g_tunnelFd).then(() => {
            hilog.info(0x0000, 'developTag', '%{public}s', 'vpn Protect Success');
        }).catch((err : Error) => {
            hilog.error(0x0000, 'developTag', 'vpn Protect Failed %{public}s', JSON.stringify(err) ?? '');
        })
  }
}
```

### destroy

destroy(): Promise\<void\>

Destroys a VPN. This API uses a promise to return the result.

**System capability**: SystemCapability.Communication.NetManager.Vpn

**Return value**

| Type           | Description                                                 |
| --------------- | ----------------------------------------------------- |
| Promise\<void\> | Promise used to return the result. If the operation is successful, the operation result is returned. If the operation fails, an error message is returned.|

**Error codes**

| ID| Error Message                                    |
| --------- | -------------------------------------------- |
| 401       | Parameter error.                             |
| 2200002   | Operation failed. Cannot connect to service. |
| 2200003   | System internal error.                       |

**Example**

```js
import vpnExt from '@ohos.net.vpnExtension';
import common from '@ohos.app.ability.common';
import Want from '@ohos.app.ability.Want';
import VpnExtensionAbility from '@ohos.app.ability.VpnExtensionAbility';
import { BusinessError } from '@kit.BasicServicesKit';

let context: vpnExt.VpnExtensionContext;
export default class MyVpnExtAbility extends VpnExtensionAbility {
  onCreate(want: Want) {
    let VpnConnection : vpnExt.VpnConnection = vpnExt.createVpnConnection(context);
    console.info("vpn createVpnConnection: " + JSON.stringify(VpnConnection));
    VpnConnection.destroy().then(() => {
      console.info("destroy success.");
    }).catch((error : BusinessError) => {
      console.error("destroy fail" + JSON.stringify(error));
    });
  }
}
```

## VpnConfig

Defines the VPN configuration.

**System capability**: SystemCapability.Communication.NetManager.Vpn

| Name               | Type                                                          | Mandatory| Description                               |
| ------------------- | -------------------------------------------------------------- | ---- | ----------------------------------- |
| addresses           | Array\<[LinkAddress](js-apis-net-connection.md#linkaddress)\> | Yes  | IP address of the vNIC.           |
| routes              | Array\<[RouteInfo](js-apis-net-connection.md#routeinfo)\>     | No  | Route information of the vNIC.           |
| dnsAddresses        | Array\<string\>                                                | No  | IP address of the DNS server.               |
| searchDomains       | Array\<string\>                                                | No  | List of DNS search domains.                 |
| mtu                 | number                                                         | No  | Maximum transmission unit (MTU), in bytes.    |
| isIPv4Accepted      | boolean                                                        | No  | Whether IPv4 is supported. The default value is **true**.     |
| isIPv6Accepted      | boolean                                                        | No  | Whether IPv6 is supported. The default value is **false**.    |
| isInternal          | boolean                                                        | No  | Whether the built-in VPN is supported. The default value is **false**.  |
| isBlocking          | boolean                                                        | No  | Whether the blocking mode is used. The default value is **false**.      |
| trustedApplications | Array\<string\>                                                | No  | List of trusted applications, which are represented by bundle names of the string type. |
| blockedApplications | Array\<string\>                                                | No  | List of blocked applications, which are represented by bundle names of the string type. |
