# @ohos.advertising (Ads Service Framework)


The advertising module provides APIs for requesting and displaying ads.


> **NOTE**
>
> The initial APIs of this module are supported since API version 11. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import { advertising } from '@kit.AdsKit';
```
## AdLoader

Provides the APIs for loading ads.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

### constructor

constructor(context: common.Context);

Constructor.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| context | common.[Context](../apis-ability-kit/js-apis-inner-application-context.md) | Yes| Context of the ability or application.|

**Example**

For details about how to obtain the context, see [Context](../../application-models/application-context-stage.md#overview).

```ts
import { advertising } from '@kit.AdsKit';
import { common } from '@kit.AbilityKit';

function createConstructor(context: common.Context): void {
  const load: advertising.AdLoader = new advertising.AdLoader(context);
}
```


### loadAd

loadAd(adParam: AdRequestParams, adOptions: AdOptions, listener: AdLoadListener): void

Loads an ad.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

**Parameters**

| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| adParam | [AdRequestParams](#adrequestparams) | Yes| Ad request parameters.| 
| adOptions | [AdOptions](#adoptions) | Yes| Ad configuration.| 
| listener | [AdLoadListener](#adloadlistener) | Yes| Ad request callback.| 

**Error codes**

For details about the following error codes, see [Ads Service Framework Error Codes](errorcode-ads.md).

| ID| Error Message| 
| -------- | -------- |
| 401      | Invalid input parameter. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed. | 
| 801      | Device not supported.  |
| 21800001 | System internal error. | 
| 21800003 | Failed to load the ad request. | 


**Example**

For details about how to obtain the context, see [Context](../../application-models/application-context-stage.md#overview).

```ts
import { advertising } from '@kit.AdsKit';
import { common } from '@kit.AbilityKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

function requestAd(context: common.Context): void {
  const adRequestParam: advertising.AdRequestParams = {
    // Ad type.
    adType: 3,
    // Ad ID.
    adId: "testy63txaom86"
  };
  const adOptions: advertising.AdOptions = {
    // Optional custom parameter, which specifies whether the ad can be downloaded while mobile data is in use. The value 1 means that the ad can be downloaded while mobile data is in use, and 0 means the opposite.
    allowMobileTraffic: 0,
    // Set the maximum ad content rating. The following values are available: w: ages 3+, all audiences; PI: ages 7+, audiences under parental instruction; J: ages 12+, teenagers; A: ages 16+/18+, adults.
    adContentClassification: 'A',
    // Specify whether you want your ad content to be treated as COPPA-compliant. The following values are available: -1 (default value): uncertain; 0: no; 1: yes.
    tagForChildProtection: -1,
    // Specify whether you want the ad request to be processed in a way that meets the GDPR for users in the EEA under the age of consent. The following values are available: -1 (default value): uncertain; 0: no; 1: yes.
    tagForUnderAgeOfPromise: -1
  }
  // Listener for the ad loading status.
  const adLoaderListener: advertising.AdLoadListener = {
    // Called when the ad request fails.
    onAdLoadFailure: (errorCode: number, errorMsg: string) => {
      hilog.error(0x0000, 'testTag', '%{public}s',
        `request single ad errorCode is: ${errorCode}, errorMsg is: ${errorMsg}`);
    },
    // Called when the ad request is successful.
    onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
      hilog.info(0x0000, 'testTag', '%{public}s', 'succeed in requesting single ad!');
      // Save the requested ad content for display.
      const returnAds = ads;
    }
  };
  // Create an AdLoader object.
  const load: advertising.AdLoader = new advertising.AdLoader(context);
  // Load the ad.
  hilog.info(0x0000, 'testTag', '%{public}s', 'request single ad!');
  load.loadAd(adRequestParam, adOptions, adLoaderListener);
}
```


### loadAdWithMultiSlots

loadAdWithMultiSlots(adParams: AdRequestParams[], adOptions: AdOptions, listener: MultiSlotsAdLoadListener): void

Loads multiple ads.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

**Parameters**

| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| adParams | [AdRequestParams](#adrequestparams)[] | Yes| Ad request parameters.| 
| adOptions | [AdOptions](#adoptions) | Yes| Ad configuration.| 
| listener | [MultiSlotsAdLoadListener](#multislotsadloadlistener) | Yes| Ad request callback.| 

**Error codes**

For details about the following error codes, see [Ads Service Framework Error Codes](errorcode-ads.md).

| ID| Error Message| 
| -------- | -------- |
| 401      | Invalid input parameter. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed. | 
| 801      | Device not supported.  |
| 21800001 | System internal error. | 
| 21800003 | Failed to load the ad request. | 

**Example**

For details about how to obtain the context, see [Context](../../application-models/application-context-stage.md#overview).

```ts
import { advertising } from '@kit.AdsKit';
import { common } from '@kit.AbilityKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

function requestMultiAd(context: common.Context): void {
  const adRequestParamArray: advertising.AdRequestParams[] = [{
    // Ad type.
    adType: 3,
    // Ad ID.
    adId: "testy63txaom86"
  } as advertising.AdRequestParams,
    {
      // Ad type.
      adType: 3,
      // Ad ID.
      adId: "testy63txaom86"
    } as advertising.AdRequestParams
  ];
  const adOptions: advertising.AdOptions = {
    // Optional custom parameter, which specifies whether the ad can be downloaded while mobile data is in use. The value 1 means that the ad can be downloaded while mobile data is in use, and 0 means the opposite.
    allowMobileTraffic: 0,
    // Set the maximum ad content rating. The following values are available: w: ages 3+, all audiences; PI: ages 7+, audiences under parental instruction; J: ages 12+, teenagers; A: ages 16+/18+, adults.
    adContentClassification: 'A',
    // Specify whether you want your ad content to be treated as COPPA-compliant. The following values are available: -1 (default value): uncertain; 0: no; 1: yes.
    tagForChildProtection: -1,
    // Specify whether you want the ad request to be processed in a way that meets the GDPR for users in the EEA under the age of consent. The following values are available: -1 (default value): uncertain; 0: no; 1: yes.
    tagForUnderAgeOfPromise: -1
  };
  // Listener for the ad loading status.
  const multiSlotsAdLoaderListener: advertising.MultiSlotsAdLoadListener = {
    // Called when the ad request fails.
    onAdLoadFailure: (errorCode: number, errorMsg: string) => {
      hilog.error(0x0000, 'testTag', '%{public}s',
        `request multi ads errorCode is: ${errorCode}, errorMsg is: ${errorMsg}`);
    },
    // Called when the ad request is successful.
    onAdLoadSuccess: (ads: Map<string, Array<advertising.Advertisement>>) => {
      hilog.info(0x0000, 'testTag', '%{public}s', 'succeed in requesting multi ads!');
      // Save the requested ad content for display.
      let returnAds: Array<advertising.Advertisement> = [];
      ads.forEach((adsArray) => returnAds.push(...adsArray));
    }
  };
  // Create an AdLoader object.
  const load: advertising.AdLoader = new advertising.AdLoader(context);
  // Load the ad.
  hilog.info(0x0000, 'testTag', '%{public}s', 'request multi ads!');
  load.loadAdWithMultiSlots(adRequestParamArray, adOptions, multiSlotsAdLoaderListener);
}
```


## showAd

showAd(ad: Advertisement, options: AdDisplayOptions, context?: common.UIAbilityContext): void

Shows a full-screen ad.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

**Parameters**


| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| ad | [Advertisement](#advertisement) | Yes| Ad object.| 
| options | [AdDisplayOptions](#addisplayoptions) | Yes| Ad display parameters.| 
| context | common.[UIAbilityContext](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) | No| Context of the UIAbility. If this parameter is not set, the value is obtained from @ohos.app.ability.common.| 


**Error codes**


For details about the following error codes, see [Ads Service Framework Error Codes](errorcode-ads.md).


| ID| Error Message| 
| -------- | -------- |
| 401 | Invalid input parameter. Possible causes: 1. Mandatory parameters are left unspecified.| 
| 21800001 | System internal error. | 
| 21800004 | Failed to display the ad. | 


**Example**

```ts
import { advertising } from '@kit.AdsKit';
import { hilog } from '@kit.PerformanceAnalysisKit'; 
import { common } from '@kit.AbilityKit';

@Entry
@Component
export struct ShowAd {
  private context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext;
  // Requested ad content.
  private ad?: advertising.Advertisement;
  // Ad display parameters.
  private adDisplayOptions: advertising.AdDisplayOptions = {
    // Whether to mute the ad. By default, the ad is not muted.
    mute: false
  }

  build() {
    Column() {
        Button ('Show Ad')
          .onClick(() => {
            try {
              // Show the ad.
              advertising.showAd(this.ad, this.adDisplayOptions, this.context);
            } catch (err) {
              hilog.error(0x0000, 'testTag', '%{public}s', `show ad catch error: ${err.code} ${err.message}`);
            }
          });
    }
    .width('100%')
    .height('100%')
  }
}
```


## AdOptions

Defines the ad configuration.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads


| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| tagForChildProtection | number | No| Tag for child protection, which specifies whether you want the ad content to be treated as COPPA-compliant.<br>- **-1** (default value): uncertain. You do not want to specify whether the ad content needs to be treated as COPPA-compliant.<br>- **0**: No. You do not want the ad content to be treated as COPPA-compliant.<br>- 1: Yes. You want the ad content to be treated as COPPA-compliant. The default value is **-1**.| 
| adContentClassification | string | No| Maximum ad content rating.<br>- **W**: ages 3+, all audiences.<br>-** PI**: ages 7+, audiences under parental instruction.<br>- **J**: ages 12+, teenagers.<br>- **A**: ages 16+/18+, adults. The default value is "".| 
| nonPersonalizedAd | number | No| Whether to request only non-personalized ads.<br>- **0**: request for personalized and non-personalized ads.<br>- **1**: request for only non-personalized ads. If this parameter is left blank, the service logic prevails.| 
| [key: string] | number \| boolean \| string \| undefined | No| Custom parameters.<br> - **totalDuration**: The value is of the number type, in seconds. This parameter is mandatory for roll ads and is used to set the total duration of roll ads.<br> - **placementAdCountDownDesc**: The value is of the string type. This parameter is optional for roll ads and is used to set the countdown description of roll ads. This parameter must be encoded using the **encodeURI()** API. If this parameter is set, the countdown description is displayed. Otherwise, only the countdown is displayed.<br> - **allowMobileTraffic**: The value is of the number type. This parameter is optional. It specifies whether ads can be downloaded while mobile data is in use. The value **1** means that ads can be downloaded while mobile data is in use, and **0** means the opposite.<br> - **tagForUnderAgeOfPromise**: The value is of the number type. This parameter is optional. It specifies whether you want the ad request to be processed in a way that meets the GDPR for users in the EEA under the age of consent. The value **-1** means that you do not specify whether the ad request should be processed in a way that meets the GDPR for users in the EEA under the age of consent. The value **0** means that you do not want the ad request to be processed in a way that meets the GDPR for users in the EEA under the age of consent, and **1** means the opposite.|


## AdRequestParams

Defines the ad request parameters.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads


| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| adId | string | Yes| Ad ID| 
| adType | number | No| Type of the requested ad.<br>- **1**: splash ad.<br>- **3**: native ad.<br>- **7**: rewarded ad.<br>- **8**: banner ad.<br>- **12**: interstitial ad.<br>- **60**: roll ad.|
| adCount | number | No| Number of ads requested. If this parameter is left blank, the service logic prevails.| 
| adWidth | number | No| Ad width. The value must be greater than 0. If this parameter is left blank, the service logic prevails.| 
| adHeight | number | No| Ad height. The value must be greater than 0. If this parameter is left blank, the service logic prevails.| 
| adSearchKeyword | string | No| Ad keyword. If this parameter is left blank, "" is used by default.| 
| [key: string] | number \| boolean \| string \| undefined | No| Custom parameters.| 


## AdLoadListener

Enumerates the callbacks used for the request for loading an ad.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

### onAdLoadFailure

onAdLoadFailure(errorCode: number, errorMsg: string): void

Called when an ad request fails.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| errorCode | number | Yes| Result code indicating the ad request failure.| 
| errorMsg | string | Yes| Error message about the ad request failure.| 


### onAdLoadSuccess

onAdLoadSuccess(ads: Array&lt;advertising.Advertisement&gt;): void

Called when an ad request is successful.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| ads | Array&lt;advertising.[Advertisement](#advertisement)&gt; | Yes| Ad data.| 


**Example**

```ts
import { advertising } from '@kit.AdsKit';

let adLoaderListener: advertising.AdLoadListener = {
  onAdLoadFailure: (errorCode: number, errorMsg: string) => {
  },
  onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
  }
}

```


## MultiSlotsAdLoadListener

Enumerates the callbacks used for the request for loading multiple ads.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

### onAdLoadFailure

onAdLoadFailure(errorCode: number, errorMsg: string): void

Called when a request for loading multiple ads fails.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| errorCode | number | Yes| Result code indicating the ad request failure.| 
| errorMsg | string | Yes| Error message about the ad request failure.| 


### onAdLoadSuccess

onAdLoadSuccess(adsMap: Map&lt;string, Array&lt;advertising.Advertisement&gt;&gt;): void

Called when a request for loading multiple ads is successful.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| adsMap |  Map&lt;string, Array&lt;advertising.[Advertisement](#advertisement)&gt;&gt;| Yes| Ad data.| 


**Example**

```ts
import { advertising } from '@kit.AdsKit';

let adLoaderListener: advertising.MultiSlotsAdLoadListener = {
  onAdLoadFailure: (errorCode: number, errorMsg: string) => {
  },
  onAdLoadSuccess: (adsMap: Map<string, Array<advertising.Advertisement>>) => {
  }
}
```


## Advertisement


Defines the requested ad content.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads


| Name| Type| Read-Only| Mandatory| Description|
| -------- | --------| -------- | -------- | -------- |
| adType | number | No|Yes| Ad type.| 
| uniqueId | string | No|Yes| Unique ID of the ad.| 
| rewarded | boolean | No|Yes| Whether users get rewarded for watching or clicking the ad.<br>- **true**: Users get rewarded.<br>- **false**: Users do not get rewarded.| 
| shown | boolean | No|Yes| Whether the ad is shown.<br>- **true**: The ad is shown.<br>- **false**: The ad is not shown.| 
| clicked | boolean | No|Yes| Whether the ad is clicked.<br>- **true**: The ad is clicked.<br>- **false**: The ad is not clicked.| 
| rewardVerifyConfig | Map&lt;string, string&gt; | No|Yes| Server verification parameter.<br>{<br>customData: "test",<br>userId: "12345"<br>} | 
| [key: string] | Object | No|Yes| Custom parameters.<br>- **isFullScreen**: The value is of the Boolean type. This parameter is used for splash ads to specify whether such an ad is in full-screen mode. The value **true** means that the ad is in full-screen mode, and **false** means that the ad is in half-screen mode.|


## AdDisplayOptions


Defines the ad display parameters.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads


| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| customData | string | No| Custom media data. It is used by the server to notify the media server that a user should be rewarded for interacting with the ad, so as to avoid spoofing. If this parameter is left blank, no notification is sent.| 
| userId | string | No| User ID. It is used by the server to notify the media server that a user should be rewarded for interacting with the ad, so as to avoid spoofing. If this parameter is left blank, no notification is sent.| 
| useMobileDataReminder | boolean | No| Whether to display a dialog box to notify users when they use mobile data to play videos or download applications.<br>- **true**: A dialog box is displayed.<br>- **false**: No dialog box is displayed. This parameter depends on the mobile data dialog box function. Currently, the complete function is not supported, and therefore the default value is not determined.| 
| mute | boolean | No| Whether to mute the ad video.<br>- **true**: The ad video is muted.<br>- **false**: The ad video is not muted. If this parameter is left blank, the default value **true** is used.| 
| audioFocusType | number | No| Type of the scenario where the audio focus is obtained during video playback.<br>- **0**: The focus is obtained when the video is played in mute or non-mute mode.<br>- **1**: The focus is not obtained when the video is played in mute mode.<br>- **2**: The focus is not obtained when the video is played in mute or non-mute mode. Currently, the function on which this API depends is not supported, and therefore the default value is not determined.| 
| [key: string] | number \| boolean \| string \| undefined | No| Custom parameters.<br>- **refreshTime**: The value is of the number type, in ms. The value is in the range [30000, 120000]. This parameter is optional for the AutoAdComponent module and specifies the interval at which the ads rotate. If this parameter is set, ads are rotated at the interval specified by this parameter. Otherwise, ads are not rotated and only the first ad in the ad response is displayed.|


## AdInteractionListener


Defines the ad status change callback.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

### onStatusChanged

onStatusChanged(status: string, ad: advertising.[Advertisement](#advertisement), data: string)

Called when the ad display status changes.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| status | string | Yes| **status**: ad display status, which can be<br>**onAdOpen**, **onAdClose**, **onAdClick**, **onVideoPlayBegin**, **onVideoPlayEnd**, **onAdLoad**, **onAdFail**, **onMediaProgress**, **onMediaStart**, **onMediaPause**, **onMediaStop**, **onMediaComplete**, **onMediaError**, **onLandscape**, **onPortrait**, **onAdReward**, **onMediaCountDown**, or **onBackClicked**.| 
| ad | advertising.[Advertisement](#advertisement) | Yes| Content of the ad.| 
| data | string | Yes| Extended information.| 

**Example**

```ts
import { advertising } from '@kit.AdsKit';

let adInteractionListener: advertising.AdInteractionListener = {
  onStatusChanged: (status: string, ad: advertising.Advertisement, data: string) => {

  }
}
```

## getAdRequestBody<sup>12+</sup>  
getAdRequestBody(adParams: AdRequestParams[], adOptions: AdOptions): Promise&lt;string&gt;

Obtains the body of an ad request. This API uses a promise to return the result.

**System capability**: SystemCapability.Advertising.Ads

**Parameters**
| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| adParams | [AdRequestParams[]](#adrequestparams) | Yes| Ad request parameters.| 
| adOptions | [AdOptions](#adoptions) | Yes| Ad configuration.| 

**Return value**

| Type| Description| 
| -------- | -------- |
| Promise&lt;string&gt; | Promise used to return the ad data of the string type.| 

**Error codes**

For details about the following error codes, see [Ads Service Framework Error Codes](errorcode-ads.md).

| ID| Error Message                        |
| -------- | -------------------------------- |
| 401      | Invalid input parameter. Possible causes: 1.Mandatory parameters are left unspecified |
| 801      | Device not supported.            |
| 21800001 | System internal error.           |

**Example** 

```ts
import { hilog } from '@kit.PerformanceAnalysisKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { advertising } from '@kit.AdsKit';
import { Prompt } from '@kit.ArkUI';

function getAdRequestBody(): void {
  let adReqParamsListForRequest: Array<advertising.AdRequestParams> = [];
  const adReqParams: Record<string, Object> = {
    'adId': 'testu7m3hc4gvm',
    'adType': 3,
    'adCount': 2,
    'adWidth': 100,
    'adHeight': 100
  };

  adReqParamsListForRequest.push(adReqParams as advertising.AdRequestParams);
  const adOption: Record<string, Object> = {
    // Set the maximum ad content rating. The following values are available: w: ages 3+, all audiences; PI: ages 7+, audiences under parental instruction; J: ages 12+, teenagers; A: ages 16+/18+, adults.
    'adContentClassification': 'A',
    // Set whether to request only non-personalized ads. 0: to request personalized ads and non-personalized ads; 1: to request only non-personalized ads. If this parameter is left blank, the service logic prevails.
    'nonPersonalizedAd': 0,
    // Specify whether you want your ad content to be treated as COPPA-compliant. The following values are available: -1 (default value): uncertain; 0: no; 1: yes.
    'tagForChildProtection': 1,
    // Specify whether you want the ad request to be processed in a way that meets the GDPR for users in the EEA under the age of consent. The following values are available: -1 (default value): uncertain; 0: no; 1: yes.
    'tagForUnderAgeOfPromise': -1
  };
  advertising.getAdRequestBody(adReqParamsListForRequest, adOption as advertising.AdOptions).then((data) => {
    hilog.info(0x0000, 'testTag', '%{public}s', `succeeded in getting AdRequestBody by promise: ${data}`);
    Prompt.showToast({
      message: data,
      duration: 1000
    });
  }).catch((error: BusinessError) => {
    hilog.error(0x0000, 'testTag', '%{public}s',
      `getAdRequestBody failed, code: ${error.code}, message: ${error.message}`);
    Prompt.showToast({
      message: error.code.toString() + ',' + error.message,
      duration: 1000
    });
  })
}
```

## parseAdResponse<sup>12+</sup>

parseAdResponse(adResponse: string, listener: MultiSlotsAdLoadListener, context: common.UIAbilityContext): void

Parses the body of an ad response.

**System capability**: SystemCapability.Advertising.Ads

**Parameters**

| Name| Type                                                    | Mandatory| Description                   |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------- |
| adResponse | string                                                       | Yes  | Ad request parameters.         |
| listener   | [MultiSlotsAdLoadListener](#multislotsadloadlistener)        | Yes  | Ad request callback.     |
| context    | common.[UIAbilityContext](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) | Yes  | UIAbility context.|

**Error codes**

For details about the following error codes, see [Ads Service Framework Error Codes](errorcode-ads.md).

| ID| Error Message                        |
| -------- | -------------------------------- |
| 401      | Invalid input parameter. Possible causes: 1.Mandatory parameters are left unspecified |
| 801      | Device not supported.            |
| 21800001 | System internal error.           |
| 21800005 | Failed to parse the ad response. |

**Example**

For details about how to obtain the context, see [Obtaining the Context of UIAbility](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).

```ts
import { common } from '@kit.AbilityKit';
import { advertising } from '@kit.AdsKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

function parseAdResponse(adResponse: string, context: common.UIAbilityContext): void {
  // Listen for the ad parsing callback.
  const multiSlotsAdLoaderListener: advertising.MultiSlotsAdLoadListener = {
    // Called when ad parsing fails.
    onAdLoadFailure: (errorCode: number, errorMsg: string) => {
      hilog.error(0x0000, 'testTag', '%{public}s',
        `request multi ads errorCode is: ${errorCode}, errorMsg is: ${errorMsg}`);
    },
    // Called when ad parsing is successful.
    onAdLoadSuccess: (ads: Map<string, Array<advertising.Advertisement>>) => {
      hilog.info(0x0000, 'testTag', '%{public}s', 'succeeded in requesting multi ads!');
      // Save the parsed ad content as an array for display.
      let returnAds: Array<advertising.Advertisement> = [];
      ads.forEach((adsArray) => returnAds.push(...adsArray));
    }
  };
  // Call the API to parse the response body.
  hilog.info(0x0000, 'testTag', '%{public}s', 'parse ad response!');
  advertising.parseAdResponse(adResponse, multiSlotsAdLoaderListener, context);
}
```

## registerWebAdInterface<sup>12+</sup>

registerWebAdInterface(controller: web_webview.WebviewController, context: common.UIAbilityContext): void

Injects an ad JavaScript object to the **Web** component.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Advertising.Ads

**Parameters**


| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| controller | web_webview.[WebviewController](../apis-arkweb/js-apis-webview.md#webviewcontroller) | Yes| Controller of the **Web** component.| 
| context | common.[UIAbilityContext](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) | Yes| UIAbility context.| 


**Error codes**


For details about the following error codes, see [Ads Service Framework Error Codes](errorcode-ads.md).


| ID| Error Message| 
| -------- | -------- |
| 401 | Invalid input parameter. Possible causes: 1.Mandatory parameters are left unspecified | 
| 21800001 | System internal error. | 


**Example**

```ts
import { webview } from '@kit.ArkWeb';
import { common } from '@kit.AbilityKit';
import { advertising } from '@kit.AdsKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

@Entry
@Component
struct Index {
  private webController: webview.WebviewController = new webview.WebviewController();
  private context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext;

  build() {
    Column() {
      Button('Inject Ad Object to Web')
        .onClick(() => {
          try {
            advertising.registerWebAdInterface(this.webController, this.context);
          } catch (err) {
            hilog.error(0x0000, 'testTag', '%{public}s', 
              `register web ad interface error: ${err.code}, ${err.message}`);
          }
        })

      Web({
        src: 'www.example.com',
        controller: this.webController,
      })
        .width("100%")
        .height("100%")
    }
  }
}
```
