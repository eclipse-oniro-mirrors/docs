# @ohos.wifiManager (WLAN)
The **WLAN** module provides basic wireless local area network (WLAN) functions, peer-to-peer (P2P) functions, and WLAN message notification services. It allows applications to communicate with devices over WLAN.

> **NOTE**
>
> The initial APIs of this module are supported since API version 6. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```js
import wifiManager from '@ohos.wifiManager';
```

## wifiManager.enableWifi<sup>9+</sup>

enableWifi(): void

Enables WLAN.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|


## wifiManager.disableWifi<sup>9+</sup>

disableWifi(): void

Disables WLAN.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.isWifiActive<sup>9+</sup>

isWifiActive(): boolean

Checks whether WLAN is enabled.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| boolean | Returns **true** if WLAN is enabled; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.scan<sup>9+</sup>

scan(): void

Starts a scan for WLAN.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.STA

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.getScanResults<sup>9+</sup>

getScanResults(): Promise&lt;Array&lt;WifiScanInfo&gt;&gt;

Obtains the scan result. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_PEERS_MAC (or ohos.permission.LOCATION)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| Promise&lt;&nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo9)&gt;&nbsp;&gt; | Promise used to return the hotspots detected.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.getScanResults<sup>9+</sup>

getScanResults(callback: AsyncCallback&lt;Array&lt;WifiScanInfo&gt;&gt;): void

Obtains the scan result. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_PEERS_MAC (or ohos.permission.LOCATION)

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;&nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo9)&gt;&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the detected hotspots. Otherwise, **err** is a non-zero value and **data** is empty.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

**Example**
  ```js
  import wifiManager from '@ohos.wifiManager';
  
  wifiManager.getScanInfos((err, result) => {
      if (err) {
          console.error("get scan info error");
          return;
      }
  
      var len = Object.keys(result).length;
      console.log("wifi received scan info: " + len);
      for (var i = 0; i < len; ++i) {
          console.info("ssid: " + result[i].ssid);
          console.info("bssid: " + result[i].bssid);
          console.info("capabilities: " + result[i].capabilities);
          console.info("securityType: " + result[i].securityType);
          console.info("rssi: " + result[i].rssi);
          console.info("band: " + result[i].band);
          console.info("frequency: " + result[i].frequency);
          console.info("channelWidth: " + result[i].channelWidth);
          console.info("timestamp: " + result[i].timestamp);
      }
  });
  
  wifiManager.getScanInfos().then(result => {
      var len = Object.keys(result).length;
      console.log("wifi received scan info: " + len);
      for (var i = 0; i < len; ++i) {
          console.info("ssid: " + result[i].ssid);
          console.info("bssid: " + result[i].bssid);
          console.info("capabilities: " + result[i].capabilities);
          console.info("securityType: " + result[i].securityType);
          console.info("rssi: " + result[i].rssi);
          console.info("band: " + result[i].band);
          console.info("frequency: " + result[i].frequency);
          console.info("channelWidth: " + result[i].channelWidth);
          console.info("timestamp: " + result[i].timestamp);
      }
  });
  ```


## WifiScanInfo<sup>9+</sup>

Represents WLAN hotspot information.

**System capability**: SystemCapability.Communication.WiFi.STA


| **Name**| **Type**| **Readable**| **Writable**| **Description**|
| -------- | -------- | -------- | -------- | -------- |
| ssid | string | Yes| No| Service set identifier (SSID) of the hotspot, in UTF-8 format.|
| bssid | string | Yes| No| Basic service set identifier (BSSID) of the hotspot.|
| capabilities | string | Yes| No| Hotspot capabilities.|
| securityType | [WifiSecurityType](#wifisecuritytype9) | Yes| No| WLAN security type.|
| rssi | number | Yes| No| Received signal strength indicator (RSSI) of the hotspot, in dBm.|
| band | number | Yes| No| Frequency band of the WLAN access point (AP).|
| frequency | number | Yes| No| Frequency of the WLAN AP.|
| channelWidth | number | Yes| No| Channel width of the WLAN AP.|
| centerFrequency0 | number | Yes| No| Center frequency of the hotspot.|
| centerFrequency1 | number | Yes| No| Center frequency of the hotspot. If the hotspot uses two non-overlapping WLAN channels, two center frequencies, namely **centerFrequency0** and **centerFrequency1**, are returned.|
| infoElems | Array&lt;[WifiInfoElem](#wifiinfoelem9)&gt; | Yes| No| Information elements.|
| timestamp | number | Yes| No| Timestamp.|


## WifiSecurityType<sup>9+</sup>

Enumerates the WLAN security types.

**System capability**: SystemCapability.Communication.WiFi.Core


| **Name**| **Value**| **Description**|
| -------- | -------- | -------- |
| WIFI_SEC_TYPE_INVALID | 0 | Invalid security type.|
| WIFI_SEC_TYPE_OPEN | 1 | Open security type.|
| WIFI_SEC_TYPE_WEP | 2 | Wired Equivalent Privacy (WEP).|
| WIFI_SEC_TYPE_PSK | 3 | Pre-shared key (PSK).|
| WIFI_SEC_TYPE_SAE | 4 | Simultaneous Authentication of Equals (SAE).|
| WIFI_SEC_TYPE_EAP<sup>9+</sup> | 5 | Extensible Authentication protocol (EAP).|
| WIFI_SEC_TYPE_EAP_SUITE_B<sup>9+</sup> | 6 | Suite B 192-bit encryption.|
| WIFI_SEC_TYPE_OWE<sup>9+</sup> | 7 | Opportunistic Wireless Encryption (OWE).|
| WIFI_SEC_TYPE_WAPI_CERT<sup>9+</sup> | 8 | WLAN Authentication and Privacy Infrastructure (WAPI) in certificate-based mode (WAPI-CERT).|
| WIFI_SEC_TYPE_WAPI_PSK<sup>9+</sup> | 9 | WAPI-PSK.|


## WifiInfoElem<sup>9+</sup>

Represents a WLAN information element.

**System capability**: SystemCapability.Communication.WiFi.STA


| **Name**| **Type**| **Readable**| **Writable**| **Description**|
| -------- | -------- | -------- | -------- | -------- |
| eid | number | Yes| No| ID of the information element.|
| content | Uint8Array | Yes| No| Content of the information element.|


## WifiChannelWidth<sup>9+</sup>

Enumerates the WLAN channel widths.

**System capability**: SystemCapability.Communication.WiFi.STA


| **Name**| **Value**| **Description**|
| -------- | -------- | -------- |
| WIDTH_20MHZ | 0 | 20 MHz|
| WIDTH_40MHZ | 1 | 40 MHz|
| WIDTH_80MHZ | 2 | 80 MHz|
| WIDTH_160MHZ | 3 | 160 MHz|
| WIDTH_80MHZ_PLUS | 4 | 80 MHz<sup>+</sup>|
| WIDTH_INVALID | 5 | Invalid value|


## wifiManager.getScanResultsSync<sup>9+</sup>

getScanResultsSync(): &nbsp;Array&lt;WifiScanInfo&gt;

Obtains the scan result. This API returns the result synchronously.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_PEERS_MAC (or ohos.permission.LOCATION)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| &nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo9)&gt; | Scan result obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.addDeviceConfig<sup>9+</sup>

addDeviceConfig(config: WifiDeviceConfig): Promise&lt;number&gt;

Adds network configuration. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.SET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | Yes| WLAN configuration to add.|

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| Promise&lt;number&gt; | Promise used to return the ID of the added network configuration. If **-1** is returned, the network configuration fails to be added.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## WifiDeviceConfig<sup>9+</sup>

Represents the WLAN configuration.

**System capability**: SystemCapability.Communication.WiFi.STA


| **Name**| **Type**| **Readable**| **Writable**| **Description**|
| -------- | -------- | -------- | -------- | -------- |
| ssid | string | Yes| No| SSID of the hotspot, in UTF-8 format.|
| bssid | string | Yes| No| BSSID of the hotspot.|
| preSharedKey | string | Yes| No| PSK of the hotspot.|
| isHiddenSsid | boolean | Yes| No| Whether the network is hidden.|
| securityType | [WifiSecurityType](#wifisecuritytype9) | Yes| No| Security type.|
| creatorUid | number | Yes| No| ID of the creator.<br>**System API**: This is a system API.|
| disableReason | number | Yes| No| Reason for disabling WLAN.<br>**System API**: This is a system API.|
| netId | number | Yes| No| Network ID.<br>**System API**: This is a system API.|
| randomMacType | number | Yes| No| Random MAC type.<br>**System API**: This is a system API.|
| randomMacAddr | string | Yes| No| Random MAC address.<br>**System API**: This is a system API.|
| ipType | [IpType](#iptype9) | Yes| No| IP address type.<br>**System API**: This is a system API.|
| staticIp | [IpConfig](#ipconfig9) | Yes| No| Static IP address information.<br>**System API**: This is a system API.|
| eapConfig<sup>9+</sup> | [WifiEapConfig](#wifieapconfig9) | Yes| No| EAP configuration.<br>**System API**: This is a system API.|


## IpType<sup>9+</sup>

Enumerates the IP address types.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.WiFi.STA


| Name| Value| Description|
| -------- | -------- | -------- |
| STATIC | 0 | Static IP address.|
| DHCP | 1 | IP address allocated by DHCP.|
| UNKNOWN | 2 | Not specified.|


## IpConfig<sup>9+</sup>

Represents IP configuration information.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Type**| **Readable**| **Writable**| **Description**|
| -------- | -------- | -------- | -------- | -------- |
| ipAddress | number | Yes| No| IP address.|
| gateway | number | Yes| No| Gateway.|
| prefixLength | number | Yes| No| Subnet mask.|
| dnsServers | number[] | Yes| No| Domain name server (DNS) information.|
| domains | Array&lt;string&gt; | Yes| No| Domain information.|


## WifiEapConfig<sup>9+</sup>

Represents EAP configuration information.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Type**| **Readable**| **Writable**| **Description**|
| -------- | -------- | -------- | -------- | -------- |
| eapMethod | [EapMethod](#eapmethod9) | Yes| No| EAP authentication method.|
| phase2Method | [Phase2Method](#phase2method9) | Yes| No| Phase 2 authentication method.|
| identity | string | Yes| No| Identity Information.|
| anonymousIdentity | string | Yes| No| Anonymous identity.|
| password | string | Yes| No| Password.|
| caCertAliases | string | Yes| No| CA certificate alias.|
| caPath | string | Yes| No| CA certificate path.|
| clientCertAliases | string | Yes| No| Client certificate alias.|
| certEntry | Uint8Array | Yes| Yes| CA certificate content.|
| certPassword | string | Yes| Yes| CA certificate password.|
| altSubjectMatch | string | Yes| No| A string to match the alternate subject.|
| domainSuffixMatch | string | Yes| No| A string to match the domain suffix.|
| realm | string | Yes| No| Realm for the passpoint credential.|
| plmn | string | Yes| No| Public land mobile network (PLMN) of the passpoint credential provider.|
| eapSubId | number | Yes| No| Sub-ID of the SIM card.|


## EapMethod<sup>9+</sup>

Enumerates the EAP authentication methods.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Value| Description|
| -------- | -------- | -------- |
| EAP_NONE | 0 | Not specified.|
| EAP_PEAP | 1 | PEAP.|
| EAP_TLS | 2 | TLS.|
| EAP_TTLS | 3 | TTLS.|
| EAP_PWD | 4 | Password.|
| EAP_SIM | 5 | SIM.|
| EAP_AKA | 6 | AKA.|
| EAP_AKA_PRIME | 7 | AKA Prime.|
| EAP_UNAUTH_TLS | 8 | UNAUTH TLS.|


## Phase2Method<sup>9+</sup>

Enumerates the Phase 2 authentication methods.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Value| Description|
| -------- | -------- | -------- |
| PHASE2_NONE | 0 | Not specified.|
| PHASE2_PAP | 1 | PAP.|
| PHASE2_MSCHAP | 2 | MS-CHAP.|
| PHASE2_MSCHAPV2 | 3 | MS-CHAPv2.|
| PHASE2_GTC | 4 | GTC .|
| PHASE2_SIM | 5 | SIM.|
| PHASE2_AKA | 6 | AKA.|
| PHASE2_AKA_PRIME | 7 | AKA Prime.|


## wifiManager.addDeviceConfig<sup>9+</sup>

addDeviceConfig(config: WifiDeviceConfig, callback: AsyncCallback&lt;number&gt;): void

Adds network configuration. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.SET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | Yes| WLAN configuration to add.|
| callback | AsyncCallback&lt;number&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the network configuration ID. If **data** is **-1**, the operation has failed. If **err** is not **0**, an error has occurred.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.addCandidateConfig<sup>9+</sup>

addCandidateConfig(config: WifiDeviceConfig): Promise&lt;number&gt;

Adds the configuration of a candidate network. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | Yes| WLAN configuration to add.|

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| Promise&lt;number&gt; | Promise used to return the network configuration ID.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.addCandidateConfig<sup>9+</sup>

addCandidateConfig(config: WifiDeviceConfig, callback: AsyncCallback&lt;number&gt;): void

Adds the configuration of a candidate network. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | Yes| WLAN configuration to add.|
| callback | AsyncCallback&lt;number&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the network configuration ID. If **data** is **-1**, the operation has failed. If **err** is not **0**, an error has occurred.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.removeCandidateConfig<sup>9+</sup>

removeCandidateConfig(networkId: number): Promise&lt;void&gt;

Removes the configuration of a candidate network. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| networkId | number | Yes| ID of the network configuration to remove.|

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.removeCandidateConfig<sup>9+</sup>

removeCandidateConfig(networkId: number, callback: AsyncCallback&lt;void&gt;): void

Removes the configuration of a candidate network. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| networkId | number | Yes| ID of the network configuration to remove.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0**. If **err** is not **0**, an error has occurred.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.getCandidateConfigs<sup>9+</sup>

getCandidateConfigs(): &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig9)&gt;

Obtains candidate network configuration.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig9)&gt; | Candidate network configuration obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.connectToCandidateConfig<sup>9+</sup>

connectToCandidateConfig(networkId: number): void

Connects to a candidate network.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| networkId | number | Yes| ID of the candidate network configuration.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

## wifiManager.connectToNetwork<sup>9+</sup>

connectToNetwork(networkId: number): void

Connects to the specified network.

**System API**: This is a system API.

**Required permissions**: ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| networkId | number | Yes| Network configuration ID.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

## wifiManager.connectToDevice<sup>9+</sup>

connectToDevice(config: WifiDeviceConfig): void

Connects to the specified network.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO, ohos.permission.SET_WIFI_CONFIG, and ohos.permissio.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**:
  SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | Yes| Configuration of the WLAN to connect.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

## wifiManager.disconnect<sup>9+</sup>

disconnect(): void

Disconnects the network.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**:
  SystemCapability.Communication.WiFi.STA

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.getSignalLevel<sup>9+</sup>

getSignalLevel(rssi: number, band: number): number

Obtains the WLAN signal level.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| rssi | number | Yes| RSSI of the hotspot, in dBm.|
| band | number | Yes| Frequency band of the WLAN AP.|

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| number | Signal level obtained. The value range is [0, 4].|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.getLinkedInfo<sup>9+</sup>

getLinkedInfo(): Promise&lt;WifiLinkedInfo&gt;

Obtains WLAN connection information. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_LOCAL_MAC (if **macAddress** needs to be obtained; otherwise, **macAddress** is an empty string.)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;[WifiLinkedInfo](#wifilinkedinfo9)&gt; | Promise used to return the WLAN connection information obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

## wifiManager.getLinkedInfo<sup>9+</sup>

getLinkedInfo(callback: AsyncCallback&lt;WifiLinkedInfo&gt;): void

Obtains WLAN connection information. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_LOCAL_MAC (if **macAddress** needs to be obtained; otherwise, **macAddress** is an empty string.)

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;[WifiLinkedInfo](#wifilinkedinfo9)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the WLAN connection information obtained. If **err** is not **0**, an error has occurred.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

**Example**
  ```js
  import wifiManager from '@ohos.wifiManager';
  
  wifiManager.getLinkedInfo((err, data) => {
      if (err) {
          console.error("get linked info error");
          return;
      }
      console.info("get wifi linked info: " + JSON.stringify(data));
  });
  
  wifiManager.getLinkedInfo().then(data => {
      console.info("get wifi linked info: " + JSON.stringify(data));
  }).catch(error => {
      console.info("get linked info error");
  });
  ```


## WifiLinkedInfo<sup>9+</sup>

Represents the WLAN connection information.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| ssid | string | Yes| No| SSID of the hotspot, in UTF-8 format.|
| bssid | string | Yes| No| BSSID of the hotspot.|
| networkId | number | Yes| No| Network configuration ID.<br>**System API**: This is a system API.|
| rssi | number | Yes| No| RSSI of the hotspot, in dBm.|
| band | number | Yes| No| Band of the WLAN AP.|
| linkSpeed | number | Yes| No| Speed of the WLAN AP.|
| frequency | number | Yes| No| Frequency of the WLAN AP.|
| isHidden | boolean | Yes| No| Whether to hide the WLAN AP.|
| isRestricted | boolean | Yes| No| Whether to restrict data volume at the WLAN AP.|
| chload | number | Yes| No| Channel load. A larger value indicates a higher load.<br>**System API**: This is a system API.|
| snr | number | Yes| No| Signal-to-noise ratio (SNR).<br>**System API**: This is a system API.|
| macType<sup>9+</sup> | number | Yes| No| MAC address type.|
| macAddress | string | Yes| No| MAC address of the device.|
| ipAddress | number | Yes| No| IP address of the device that sets up the WLAN connection.|
| suppState | [SuppState](#suppstate9) | Yes| No| Supplicant state.<br>**System API**: This is a system API.|
| connState | [ConnState](#connstate9) | Yes| No| WLAN connection state.|


## ConnState<sup>9+</sup>

Enumerates the WLAN connection states.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Value| Description|
| -------- | -------- | -------- |
| SCANNING | 0 | The device is scanning for available APs.|
| CONNECTING | 1 | A WLAN connection is being established.|
| AUTHENTICATING | 2 | An authentication is being performed for a WLAN connection.|
| OBTAINING_IPADDR | 3 | The IP address of the WLAN connection is being acquired.|
| CONNECTED | 4 | A WLAN connection is established.|
| DISCONNECTING | 5 | The WLAN connection is being disconnected.|
| DISCONNECTED | 6 | The WLAN connection is disconnected.|
| UNKNOWN | 7 | Failed to set up the WLAN connection.|


## SuppState<sup>9+</sup>

Enumerates the supplicant states.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Value| Description|
| -------- | -------- | -------- |
| DISCONNECTED | 0 | The supplicant is disconnected from the AP.|
| INTERFACE_DISABLED | 1 | The network interface is disabled.|
| INACTIVE | 2 | The supplicant is inactive.|
| SCANNING | 3 | The supplicant is scanning for a WLAN connection.|
| AUTHENTICATING | 4 | The supplicant is being authenticated.|
| ASSOCIATING | 5 | The supplicant is being associated with an AP.|
| ASSOCIATED | 6 | The supplicant is associated with an AP.|
| FOUR_WAY_HANDSHAKE | 7 | A four-way handshake is being performed for the supplicant.|
| GROUP_HANDSHAKE | 8 | A group handshake is being performed for the supplicant.|
| COMPLETED | 9 | The authentication is complete.|
| UNINITIALIZED | 10 | The supplicant failed to set up the connection.|
| INVALID | 11 | Invalid value.|


## wifiManager.isConnected<sup>9+</sup>

isConnected(): boolean

Checks whether WLAN is connected.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| boolean | Returns **true** if the WLAN is connected; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.getSupportedFeatures<sup>9+</sup>

getSupportedFeatures(): number

Obtains the features supported by this device.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.Core

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| number | Feature value. |

**Feature IDs**

| Value| Description|
| -------- | -------- |
| 0x0001 | WLAN infrastructure mode|
| 0x0002 | 5 GHz feature|
| 0x0004 | Generic Advertisement Service (GAS)/Access Network Query Protocol (ANQP) feature|
| 0x0008 | Wi-Fi Direct|
| 0x0010 | SoftAP|
| 0x0040 | Wi-Fi Aware|
| 0x8000 | WLAN AP/STA concurrency|
| 0x8000000 | WPA3 Personal (WPA-3 SAE)|
| 0x10000000 | WPA3-Enterprise Suite B |
| 0x20000000 | Enhanced open feature|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2401000  | Operation failed.|

## wifiManager.isFeatureSupported<sup>9+</sup>

isFeatureSupported(featureId: number): boolean

Checks whether the device supports the specified WLAN feature.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.Core

**Parameters**


| **Name**| **Type**| Mandatory| **Description**|
| -------- | -------- | -------- | -------- |
| featureId | number | Yes| Feature ID.|

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| boolean | Returns **true** if the feature is supported; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2401000  | Operation failed.|

## wifiManager.getDeviceMacAddress<sup>9+</sup>

getDeviceMacAddress(): string[]

Obtains the device MAC address.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_LOCAL_MAC and ohos.permission.GET_WIFI_INFO (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| string[] | MAC address obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.getIpInfo<sup>9+</sup>

getIpInfo(): IpInfo

Obtains IP information.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| [IpInfo](#ipinfo9) | IP information obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## IpInfo<sup>9+</sup>

Represents IP information.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Type**| **Readable**| **Writable**| **Description**|
| -------- | -------- | -------- | -------- | -------- |
| ipAddress | number | Yes| No| IP address.|
| gateway | number | Yes| No| Gateway.|
| netmask | number | Yes| No| Subnet mask.|
| primaryDns | number | Yes| No| IP address of the preferred DNS server.|
| secondDns | number | Yes| No| IP address of the alternate DNS server.|
| serverIp | number | Yes| No| IP address of the DHCP server.|
| leaseDuration | number | Yes| No| Lease duration of the IP address.|


## wifiManager.getCountryCode<sup>9+</sup>

getCountryCode(): string

Obtains the country code.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.Core

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| string | Country code obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2401000  | Operation failed.|

## wifiManager.reassociate<sup>9+</sup>

reassociate(): void

Re-associates with the network.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

## wifiManager.reconnect<sup>9+</sup>

reconnect(): void

Reconnects to the network.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|
| 2501001  | Wifi is closed.|

## wifiManager.getDeviceConfigs<sup>9+</sup>

getDeviceConfigs(): &nbsp;Array&lt;WifiDeviceConfig&gt;

Obtains network configuration.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO, ohos.permission.LOCATION, and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig9)&gt; | Array of network configuration obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.updateNetwork<sup>9+</sup>

updateNetwork(config: WifiDeviceConfig): number

Updates network configuration.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.SET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| config | [WifiDeviceConfig](#wifideviceconfig9) | Yes| New WLAN configuration.|

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| number | ID of the updated network configuration. The value **-1** indicates that the operation has failed.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.disableNetwork<sup>9+</sup>

disableNetwork(netId: number): void

Disables network configuration.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| netId | number | Yes| ID of the network configuration to disable.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.removeAllNetwork<sup>9+</sup>

removeAllNetwork(): void

Removes the configuration of all networks.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.removeDevice<sup>9+</sup>

removeDevice(id: number): void

Removes the specified network configuration.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| id | number | Yes| ID of the network configuration to remove.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.enableHotspot<sup>9+</sup>

enableHotspot(): void

Enables this hotspot.

**System API**: This is a system API.

**Required permissions**: ohos.permission.MANAGE_WIFI_HOTSPOT (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.disableHotspot<sup>9+</sup>

disableHotspot(): void

Disables this hotspot.

**System API**: This is a system API.

**Required permissions**: ohos.permission.MANAGE_WIFI_HOTSPOT (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.isHotspotDualBandSupported<sup>9+</sup>

isHotspotDualBandSupported(): boolean

Checks whether the hotspot supports dual band.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.MANAGE_WIFI_HOTSPOT (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| boolean | Returns **true** if the hotspot supports dual band; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.isHotspotActive<sup>9+</sup>

isHotspotActive(): boolean

Checks whether this hotspot is active.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| boolean | Returns **true** if the hotspot is active; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.setHotspotConfig<sup>9+</sup>

setHotspotConfig(config: HotspotConfig): void

Sets hotspot configuration.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| config | [HotspotConfig](#hotspotconfig9) | Yes| Hotspot configuration to set.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2601000  | Operation failed.|

## HotspotConfig<sup>9+</sup>

Represents the hotspot configuration.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.WiFi.AP.Core

| **Name**| **Type**| **Readable**| **Writable**| **Description**|
| -------- | -------- | -------- | -------- | -------- |
| ssid | string | Yes| No| SSID of the hotspot, in UTF-8 format.|
| securityType | [WifiSecurityType](#wifisecuritytype9) | Yes| No| Security type.|
| band | number | Yes| No| Hotspot band. The value **1** stands for 2.4 GHz, the value **2** for 5 GHz, and the value **3** for dual band.|
| preSharedKey | string | Yes| No| PSK of the hotspot.|
| maxConn | number | Yes| No| Maximum number of connections allowed.|


## wifiManager.getHotspotConfig<sup>9+</sup>

getHotspotConfig(): HotspotConfig

Obtains hotspot configuration.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| [HotspotConfig](#hotspotconfig9) | Hotspot configuration obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.getStations<sup>9+</sup>

getStations(): &nbsp;Array&lt;[StationInfo](#stationinfo9)&gt;

Obtains information about the connected stations.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO, ohos.permission.LOCATION, and ohos.permission.MANAGE_WIFI_HOTSPOT (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| &nbsp;Array&lt;[StationInfo](#stationinfo9)&gt; | Connected stations obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2601000  | Operation failed.|

## StationInfo<sup>9+</sup>

Represents the station information.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.WiFi.AP.Core

| **Name**| **Type**| **Readable**| **Writable**| **Description**|
| -------- | -------- | -------- | -------- | -------- |
| name | string | Yes| No| Device name.|
| macAddress | string | Yes| No| MAC address.|
| ipAddress | string | Yes| No| IP address.|


## wifiManager.getP2pLinkedInfo<sup>9+</sup>

getP2pLinkedInfo(): Promise&lt;WifiP2pLinkedInfo&gt;

Obtains P2P link information. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo9)&gt; | Promise used to return the P2P link information obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## WifiP2pLinkedInfo<sup>9+</sup>

Represents the P2P link information.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| connectState | [P2pConnectState](#p2pconnectstate9) | Yes| No| P2P connection state.|
| isGroupOwner | boolean | Yes| No| Whether the device is the group owner.|
| groupOwnerAddr | string | Yes| No| MAC address of the group.


## P2pConnectState<sup>9+</sup>

Enumerates the P2P connection states.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Value| Description|
| -------- | -------- | -------- |
| DISCONNECTED | 0 | Disconnected.|
| CONNECTED | 1 | Connected.|


## wifiManager.getP2pLinkedInfo<sup>9+</sup>

getP2pLinkedInfo(callback: AsyncCallback&lt;WifiP2pLinkedInfo&gt;): void

Obtains P2P link information. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo9)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the P2P link information. If **err** is not **0**, an error has occurred.|


## wifiManager.getCurrentGroup<sup>9+</sup>

getCurrentGroup(): Promise&lt;WifiP2pGroupInfo&gt;

Obtains the current P2P group information. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo9)&gt; | Promise used to return the P2P group information obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.getCurrentGroup<sup>9+</sup>

getCurrentGroup(callback: AsyncCallback&lt;WifiP2pGroupInfo&gt;): void

Obtains the current P2P group information. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo9)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the group information obtained. If **err** is not **0**, an error has occurred.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.getP2pPeerDevices<sup>9+</sup>

getP2pPeerDevices(): Promise&lt;WifiP2pDevice[]&gt;

Obtains the peer device list in the P2P connection. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;[WifiP2pDevice[]](#wifip2pdevice9)&gt; | Promise used to return the peer device list.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.getP2pPeerDevices<sup>9+</sup>

getP2pPeerDevices(callback: AsyncCallback&lt;WifiP2pDevice[]&gt;): void

Obtains the peer device list in the P2P connection. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;[WifiP2pDevice[]](#wifip2pdevice9)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the peer device list obtained. If **err** is not **0**, an error has occurred.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## WifiP2pDevice<sup>9+</sup>

Represents the P2P device information.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| deviceName | string | Yes| No| Device name.|
| deviceAddress | string | Yes| No| MAC address of the device.|
| primaryDeviceType | string | Yes| No| Type of the primary device.|
| deviceStatus | [P2pDeviceStatus](#p2pdevicestatus9) | Yes| No| Device status.|
| groupCapabilities | number | Yes| No| Group capabilities.|


## P2pDeviceStatus<sup>9+</sup>

Enumerates the P2P device states.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Value| Description|
| -------- | -------- | -------- |
| CONNECTED | 0 | Connected.|
| INVITED | 1 | Invited.|
| FAILED | 2 | Failed.|
| AVAILABLE | 3 | Available.|
| UNAVAILABLE | 4 | Unavailable.|


## wifiManager.getP2pLocalDevice<sup>9+</sup>

getP2pLocalDevice(): Promise&lt;WifiP2pDevice&gt;

Obtains the local device information in the P2P connection. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;[WifiP2pDevice](#wifip2pdevice9)&gt; | Promise used to return the local device information obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.getP2pLocalDevice<sup>9+</sup>

getP2pLocalDevice(callback: AsyncCallback&lt;WifiP2pDevice&gt;): void

Obtains the local device information in the P2P connection. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;[WifiP2pDevice](#wifip2pdevice9)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the local device information obtained. If **err** is not **0**, an error has occurred.|


## wifiManager.createGroup<sup>9+</sup>

createGroup(config: WifiP2PConfig): void

Creates a P2P group.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| Mandatory| **Description**|
| -------- | -------- | -------- | -------- |
| config | [WifiP2PConfig](#wifip2pconfig9) | Yes| Group configuration.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## WifiP2PConfig<sup>9+</sup>

Represents P2P group configuration.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| deviceAddress | string | Yes| No| Device address.|
| netId | number | Yes| No| Network ID. The value **-1** indicates a temporary group, and **-2** indicates a persistent group.|
| passphrase | string | Yes| No| Passphrase of the group.|
| groupName | string | Yes| No| Name of the group.|
| goBand | [GroupOwnerBand](#groupownerband9) | Yes| No| Frequency band of the group.|


## GroupOwnerBand<sup>9+</sup>

Enumerates the P2P group frequency bands.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Value| Description|
| -------- | -------- | -------- |
| GO_BAND_AUTO | 0 | Auto.|
| GO_BAND_2GHZ | 1 | 2 GHz.|
| GO_BAND_5GHZ | 2 | 5 GHz.|


## wifiManager.removeGroup<sup>9+</sup>

removeGroup(): void

Removes this P2P group.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.p2pConnect<sup>9+</sup>

p2pConnect(config: WifiP2PConfig): void

Sets up a P2P connection.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**


| **Name**| **Type**| Mandatory| **Description**|
| -------- | -------- | -------- | -------- |
| config | [WifiP2PConfig](#wifip2pconfig9) | Yes| P2P group configuration.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

**Example**
  ```js
  import wifiManager from '@ohos.wifiManager';
  
  var recvP2pConnectionChangeFunc = result => {
      console.info("p2p connection change receive event: " + JSON.stringify(result));
      wifiManager.getP2pLinkedInfo((err, data) => {
          if (err) {
              console.error('failed to get getP2pLinkedInfo: ' + JSON.stringify(err));
              return;
          }
          console.info("get getP2pLinkedInfo: " + JSON.stringify(data));
      });
  }
  wifiManager.on("p2pConnectionChange", recvP2pConnectionChangeFunc);
  
  var recvP2pDeviceChangeFunc = result => {
      console.info("p2p device change receive event: " + JSON.stringify(result));
  }
  wifiManager.on("p2pDeviceChange", recvP2pDeviceChangeFunc);
  
  var recvP2pPeerDeviceChangeFunc = result => {
      console.info("p2p peer device change receive event: " + JSON.stringify(result));
      wifiManager.getP2pPeerDevices((err, data) => {
          if (err) {
              console.error('failed to get peer devices: ' + JSON.stringify(err));
              return;
          }
          console.info("get peer devices: " + JSON.stringify(data));
          var len = Object.keys(data).length;
          for (var i = 0; i < len; ++i) {
              if (data[i].deviceName === "my_test_device") {
                  console.info("p2p connect to test device: " + data[i].deviceAddress);
                  var config = {
                      "deviceAddress":data[i].deviceAddress,
                      "netId":-2,
                      "passphrase":"",
                      "groupName":"",
                      "goBand":0,
                  }
                  wifiManager.p2pConnect(config);
              }
          }
      });
  }
  wifiManager.on("p2pPeerDeviceChange", recvP2pPeerDeviceChangeFunc);
  
  var recvP2pPersistentGroupChangeFunc = () => {
      console.info("p2p persistent group change receive event");
  
      wifiManager.getCurrentGroup((err, data) => {
          if (err) {
              console.error('failed to get current group: ' + JSON.stringify(err));
              return;
          }
          console.info("get current group: " + JSON.stringify(data));
      });
  }
  wifiManager.on("p2pPersistentGroupChange", recvP2pPersistentGroupChangeFunc);
  
  setTimeout(function() {wifi.off("p2pConnectionChange", recvP2pConnectionChangeFunc);}, 125 * 1000);
  setTimeout(function() {wifi.off("p2pDeviceChange", recvP2pDeviceChangeFunc);}, 125 * 1000);
  setTimeout(function() {wifi.off("p2pPeerDeviceChange", recvP2pPeerDeviceChangeFunc);}, 125 * 1000);
  setTimeout(function() {wifi.off("p2pPersistentGroupChange", recvP2pPersistentGroupChangeFunc);}, 125 * 1000);
  console.info("start discover devices -> " + wifiManager.startDiscoverDevices());
  ```

## wifiManager.p2pCancelConnect<sup>9+</sup>

p2pCancelConnect(): void

Cancels this P2P connection.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.startDiscoverDevices<sup>9+</sup>

startDiscoverDevices(): void

Starts to discover devices.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.stopDiscoverDevices<sup>9+</sup>

stopDiscoverDevices(): void

Stops discovering devices.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.deletePersistentGroup<sup>9+</sup>

deletePersistentGroup(netId: number): void

Deletes a persistent group.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**


| **Name**| **Type**| Mandatory| **Description**|
| -------- | -------- | -------- | -------- |
| netId | number | Yes| ID of the group to delete.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.getP2pGroups<sup>9+</sup>

getP2pGroups(): Promise&lt;Array&lt;WifiP2pGroupInfo&gt;&gt;

Obtains information about all P2P groups. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;&nbsp;Array&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo9)&gt;&nbsp;&gt; | Promise used to return the group information obtained.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## WifiP2pGroupInfo<sup>9+</sup>

Represents the P2P group information.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| isP2pGo | boolean | Yes| No| Whether the device is the group owner.|
| ownerInfo | [WifiP2pDevice](#wifip2pdevice9) | Yes| No| Device information of the group.|
| passphrase | string | Yes| No| Passphrase of the group.|
| interface | string | Yes| No| Interface name.|
| groupName | string | Yes| No| Group name.|
| networkId | number | Yes| No| Network ID.|
| frequency | number | Yes| No| Frequency of the group.|
| clientDevices | [WifiP2pDevice[]](#wifip2pdevice9) | Yes| No| List of connected devices.|
| goIpAddress | string | Yes| No| IP address of the group.|


## wifiManager.getP2pGroups<sup>9+</sup>

getP2pGroups(callback: AsyncCallback&lt;Array&lt;WifiP2pGroupInfo&gt;&gt;): void

Obtains information about all P2P groups. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;&nbsp;Array&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo9)&gt;&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the group information obtained. If **err** is not **0**, an error has occurred.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.setDeviceName<sup>9+</sup>

setDeviceName(devName: string): void

Sets the device name.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| devName | string | Yes| Device name to set.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.on('wifiStateChange')<sup>9+</sup>

on(type: "wifiStateChange", callback: Callback&lt;number&gt;): void

Subscribes to WLAN state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **wifiStateChange**.|
| callback | Callback&lt;number&gt; | Yes| Callback invoked to return the WLAN state.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

**WLAN states** 

| **Value**| **Description**|
| -------- | -------- |
| 0 | Deactivated|
| 1 | Activated|
| 2 | Activating|
| 3 | Deactivating|


## wifiManager.off('wifiStateChange')<sup>9+</sup>

off(type: "wifiStateChange", callback?: Callback&lt;number&gt;): void

Unsubscribes from WLAN state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **wifiStateChange**.|
| callback | Callback&lt;number&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered. |

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

**Example**
  ```js
  import wifiManager from '@ohos.wifiManager';
  
  var recvPowerNotifyFunc = result => {
      console.info("Receive power state change event: " + result);
  }
  
  // Register an event.
  wifiManager.on("wifiStateChange", recvPowerNotifyFunc);
  
  // Unregister an event.
  wifiManager.off("wifiStateChange", recvPowerNotifyFunc);
  ```


## wifiManager.on('wifiConnectionChange')<sup>9+</sup>

on(type: "wifiConnectionChange", callback: Callback&lt;number&gt;): void

Subscribes to WLAN connection state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **wifiConnectionChange**.|
| callback | Callback&lt;number&gt; | Yes| Callback invoked to return the WLAN connection state.|

**WLAN connection states**

| **Value**| **Description**|
| -------- | -------- |
| 0 | Disconnected.|
| 1 | Connected.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.off('wifiConnectionChange')<sup>9+</sup>

off(type: "wifiConnectionChange", callback?: Callback&lt;number&gt;): void

Unsubscribes from WLAN connection state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **wifiConnectionChange**.|
| callback | Callback&lt;number&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered. |

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.on('wifiScanStateChange')<sup>9+</sup>

on(type: "wifiScanStateChange", callback: Callback&lt;number&gt;): void

Subscribes to WLAN scan state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **wifiScanStateChange**.|
| callback | Callback&lt;number&gt; | Yes| Callback invoked to return the WLAN scan state.|

**WLAN scan states**

| **Value**| **Description**|
| -------- | -------- |
| 0 | Scan failed.|
| 1 | Scan successful.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.off('wifiScanStateChange')<sup>9+</sup>

off(type: "wifiScanStateChange", callback?: Callback&lt;number&gt;): void

Unsubscribes from WLAN scan state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **wifiScanStateChange**.|
| callback | Callback&lt;number&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.on('wifiRssiChange')<sup>9+</sup>

on(type: "wifiRssiChange", callback: Callback&lt;number&gt;): void

Subscribes to RSSI changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **wifiRssiChange**.|
| callback | Callback&lt;number&gt; | Yes| Callback invoked to return the RSSI, in dBm.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.off('wifiRssiChange')<sup>9+</sup>

off(type: "wifiRssiChange", callback?: Callback&lt;number&gt;): void

Unsubscribes from RSSI changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **wifiRssiChange**.|
| callback | Callback&lt;number&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2501000  | Operation failed.|

## wifiManager.on('hotspotStateChange')<sup>9+</sup>

on(type: "hotspotStateChange", callback: Callback&lt;number&gt;): void

Subscribes to hotspot state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **hotspotStateChange**.|
| callback | Callback&lt;number&gt; | Yes| Callback invoked to return the hotspot state.|

**Hotspot states**

| **Value**| **Description**|
| -------- | -------- |
| 0 | Deactivated|
| 1 | Activated|
| 2 | Activating|
| 3 | Deactivating|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.off('hotspotStateChange')<sup>9+</sup>

off(type: "hotspotStateChange", callback?: Callback&lt;number&gt;): void

Unsubscribes from hotspot state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **hotspotStateChange**.|
| callback | Callback&lt;number&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2601000  | Operation failed.|

## wifiManager.on('p2pStateChange')<sup>9+</sup>

on(type: "p2pStateChange", callback: Callback&lt;number&gt;): void

Subscribes to P2P state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pStateChange**.|
| callback | Callback&lt;number&gt; | Yes| Callback invoked to return the P2P state change.|

**P2P states**

| **Value**| **Description**|
| -------- | -------- |
| 1 | Available|
| 2 | Opening|
| 3 | Opened|
| 4 | Closing|
| 5 | Closed|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pStateChange')<sup>9+</sup>

off(type: "p2pStateChange", callback?: Callback&lt;number&gt;): void

Unsubscribes from P2P state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pStateChange**.|
| callback | Callback&lt;number&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

  ## wifiManager.on('p2pConnectionChange')<sup>9+</sup>

on(type: "p2pConnectionChange", callback: Callback&lt;WifiP2pLinkedInfo&gt;): void

Subscribes to P2P connection state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pConnectionChange**.|
| callback | Callback&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo9)&gt; | Yes| Callback invoked to return the P2P connection state change.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pConnectionChange')<sup>9+</sup>

off(type: "p2pConnectionChange", callback?: Callback&lt;WifiP2pLinkedInfo&gt;): void

Unsubscribes from P2P connection state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pConnectionChange**.|
| callback | Callback&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo9)&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.on('p2pDeviceChange')<sup>9+</sup>

on(type: "p2pDeviceChange", callback: Callback&lt;WifiP2pDevice&gt;): void

Subscribes to P2P device state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pDeviceChange**.|
| callback | Callback&lt;[WifiP2pDevice](#wifip2pdevice9)&gt; | Yes| Callback invoked to return the device state change.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pDeviceChange')<sup>9+</sup>

off(type: "p2pDeviceChange", callback?: Callback&lt;WifiP2pDevice&gt;): void

Unsubscribes from P2P device state changes.

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pDeviceChange**.|
| callback | Callback&lt;[WifiP2pDevice](#wifip2pdevice9)&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.on('p2pPeerDeviceChange')<sup>9+</sup>

on(type: "p2pPeerDeviceChange", callback: Callback&lt;WifiP2pDevice[]&gt;): void

Subscribes to P2P peer device state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pPeerDeviceChange**.|
| callback | Callback&lt;[WifiP2pDevice[]](#wifip2pdevice9)&gt; | Yes| Callback invoked to return the P2P peer device state change. If the application has the **ohos.permission.GET_WIFI_PEERS_MAC** permission, **deviceAddress** in the return value is a real device address; otherwise, **deviceAddress** is a random device address.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pPeerDeviceChange')<sup>9+</sup>

off(type: "p2pPeerDeviceChange", callback?: Callback&lt;WifiP2pDevice[]&gt;): void

Unsubscribes from P2P peer device state changes.

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pPeerDeviceChange**.|
| callback | Callback&lt;[WifiP2pDevice[]](#wifip2pdevice9)&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.on('p2pPersistentGroupChange')<sup>9+</sup>

on(type: "p2pPersistentGroupChange", callback: Callback&lt;void&gt;): void

Subscribes to P2P persistent group state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pPersistentGroupChange**.|
| callback | Callback&lt;void&gt; | Yes| Callback invoked to return the P2P persistent group state change.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pPersistentGroupChange')<sup>9+</sup>

off(type: "p2pPersistentGroupChange", callback?: Callback&lt;void&gt;): void

Unsubscribes from P2P persistent group state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pPersistentGroupChange**.|
| callback | Callback&lt;void&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.on('p2pDiscoveryChange')<sup>9+</sup>

on(type: "p2pDiscoveryChange", callback: Callback&lt;number&gt;): void

Subscribes to P2P device discovery state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pDiscoveryChange**.|
| callback | Callback&lt;number&gt; | Yes| Callback invoked to return the P2P device discovery state change.|

**P2P discovered device states**

| **Value**| **Description**|
| -------- | -------- |
| 0 | Initial state.|
| 1 | Discovered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

## wifiManager.off('p2pDiscoveryChange')<sup>9+</sup>

off(type: "p2pDiscoveryChange", callback?: Callback&lt;number&gt;): void

Unsubscribes from P2P device discovery state changes.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type, which has a fixed value of **p2pDiscoveryChange**.|
| callback | Callback&lt;number&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks registered for the specified event will be unregistered.|

**Error codes**

For details about the error codes, see [Wi-Fi Error Codes](../errorcodes/errorcode-wifi.md).

| **Type**| **Description**|
| -------- | -------- |
| 2801000  | Operation failed.|

<!--no_check-->
