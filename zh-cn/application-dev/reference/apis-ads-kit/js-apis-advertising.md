# @ohos.advertising (广告服务框架)


本模块提供广告操作能力，包括请求广告、展示广告。


> **说明：**
> 本模块首批接口从API version 11开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import advertising from '@ohos.advertising';
```
## AdLoader

提供加载广告的功能

**系统能力：** SystemCapability.Advertising.Ads

### constructor

constructor(context: common.Context);

构造函数。

**系统能力：** SystemCapability.Advertising.Ads

**参数：**

| **参数名** | **类型** | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| context | common.[Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是 | ability或application的上下文环境。 |

**示例：**

其中context的获取方式参见[各类Context的获取方式](../../application-models/application-context-stage.md#概述)。

```ts
import advertising from '@ohos.advertising';
import common from '@ohos.app.ability.common';

function createConstructor(context: common.Context): void {
  const load: advertising.AdLoader = new advertising.AdLoader(context);
}
```


### loadAd

loadAd(adParam: AdRequestParams, adOptions: AdOptions, listener: AdLoadListener): void

请求单广告位广告。

**系统能力：** SystemCapability.Advertising.Ads

**参数：**

| **参数名** | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| adParam | [AdRequestParams](#adrequestparams) | 是 | 广告请求参数。 | 
| adOptions | [AdOptions](#adoptions) | 是 | 广告配置。 | 
| listener | [AdLoadListener](#adloadlistener) | 是 | 请求广告回调监听。 | 

**错误码：**

以下错误码的详细介绍请参见[广告服务框架错误码参考](errorcode-ads.md)。

| 错误码ID | 错误信息 | 
| -------- | -------- |
| 21800001 | System internal error. | 
| 21800003 | Failed to load the ad request. | 

**示例：**

其中context的获取方式参见[各类Context的获取方式](../../application-models/application-context-stage.md#概述)。

```ts
import advertising from '@ohos.advertising';
import common from '@ohos.app.ability.common';
import hilog from '@ohos.hilog'; 

function requestAd(context: common.Context): void {
  const adRequestParam: advertising.AdRequestParams = {
    // 广告类型
    adType: 3,
    // 测试广告位ID
    adId: "testy63txaom8", 
  };
  const adOptions: advertising.AdOptions = {
    // 设置广告内容分级上限
    adContentClassification: 'A',
    // 可选自定义参数，设置是否允许使用流量下载广告素材 0：不允许，1：允许
    allowMobileTraffic: 0,
  };
  // 广告请求回调监听
  const adLoaderListener: advertising.AdLoadListener = {
    // 广告请求失败回调
    onAdLoadFailure: (errorCode: number, errorMsg: string) => {
      hilog.error(0x0000, 'testTag', '%{public}s', `request single ad errorCode is: ${errorCode}, errorMsg is: ${errorMsg}`);
    },
    // 广告请求成功回调
    onAdLoadSuccess: (ads: Array<advertising.Advertisement>) => {
      hilog.info(0x0000, 'testTag', '%{public}s', 'request single ad success!');
      // 保存请求到的广告内容用于展示
      const returnAds = ads;
    }
  };
  // 创建AdLoader广告对象
  const load: advertising.AdLoader = new advertising.AdLoader(context);
  // 调用广告请求接口
  hilog.info(0x0000, 'testTag', '%{public}s', 'request single ad!');
  load.loadAd(adRequestParam, adOptions, adLoaderListener);
}
```


### loadAdWithMultiSlots

loadAdWithMultiSlots(adParams: AdRequestParams[], adOptions: AdOptions, listener: MultiSlotsAdLoadListener): void

请求多广告位广告。

**系统能力：** SystemCapability.Advertising.Ads

**参数：**

| **参数名** | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| adParams | [AdRequestParams](#adrequestparams)[] | 是 | 广告请求参数。 | 
| adOptions | [AdOptions](#adoptions) | 是 | 广告配置。 | 
| listener | [MultiSlotsAdLoadListener](#multislotsadloadlistener) | 是 | 请求广告回调监听。 | 

**错误码：**

以下错误码的详细介绍请参见[广告服务框架错误码参考](errorcode-ads.md)。

| 错误码ID | 错误信息 | 
| -------- | -------- |
| 21800001 | System internal error. | 
| 21800003 | Failed to load the ad request. | 

**示例：**

其中context的获取方式参见[各类Context的获取方式](../../application-models/application-context-stage.md#概述)。

```ts
import advertising from '@ohos.advertising';
import common from '@ohos.app.ability.common';
import hilog from '@ohos.hilog'; 

function requestMultiAd(context: common.Context): void {
  const adRequestParamArray: advertising.AdRequestParams[] = [{
      // 广告类型
      adType: 3,
      // 测试广告位ID
      adId: "testy63txaom8",
    } as advertising.AdRequestParams,
    {
      // 广告类型
      adType: 3,
      // 测试广告位ID
      adId: "testy63txaom8", 
    } as advertising.AdRequestParams
  ];
  const adOptions: advertising.AdOptions = {
    //设置广告内容分级上限
    adContentClassification: 'A',
    // 可选自定义参数，设置是否允许使用流量下载广告素材 0：不允许，1：允许
    allowMobileTraffic: 0,
  };
  // 广告请求回调监听
  const multiSlotsAdLoaderListener: advertising.MultiSlotsAdLoadListener = {
    // 广告请求失败回调
    onAdLoadFailure: (errorCode: number, errorMsg: string) => {
      hilog.error(0x0000, 'testTag', '%{public}s', `request multi ads errorCode is: ${errorCode}, errorMsg is: ${errorMsg}`);
    },
    // 广告请求成功回调
    onAdLoadSuccess: (ads: Map<string, Array<advertising.Advertisement>>) => {
      hilog.info(0x0000, 'testTag', '%{public}s', 'request multi ads success!');
      // 保存请求到的广告内容为数组用于展示
      let returnAds: Array<advertising.Advertisement> = [];
      ads.forEach((adsArray) => returnAds.push(...adsArray));
    }
  };
  // 创建AdLoader广告对象
  const load: advertising.AdLoader = new advertising.AdLoader(context);
  // 调用广告请求接口
  hilog.info(0x0000, 'testTag', '%{public}s', 'request multi ads!');
  load.loadAdWithMultiSlots(adRequestParamArray, adOptions, multiSlotsAdLoaderListener);
}
```


## showAd

showAd(ad: Advertisement, options: AdDisplayOptions, context?: common.UIAbilityContext): void

展示全屏广告。

**系统能力：** SystemCapability.Advertising.Ads

**参数：**


| **参数名** | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| ad | [Advertisement](#advertisement) | 是 | 广告对象。 | 
| options | [AdDisplayOptions](#addisplayoptions) | 是 | 广告展示参数。 | 
| context | common.[UIAbilityContext](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) | 否 | UIAbility的上下文环境，不设置从api: @ohos.app.ability.common中获取。 | 


**错误码：**


以下错误码的详细介绍请参见[广告服务框架错误码参考](errorcode-ads.md)。


| 错误码ID | 错误信息 | 
| -------- | -------- |
| 21800001 | System internal error. | 
| 21800004 | Failed to display the ad. | 


**示例：**

```ts
import advertising from '@ohos.advertising';
import hilog from '@ohos.hilog'; 
import common from '@ohos.app.ability.common';

@Entry
@Component
export struct ShowAd {
  private context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext;
  // 请求到的广告内容
  private ad?: advertising.Advertisement;
  // 广告展示参数
  private adDisplayOptions: advertising.AdDisplayOptions = {
    // 是否静音，默认不静音
    mute: false,
  }

  build() {
    Column() {
        Button('展示广告')
          .onClick(() => {
            try {
              // 调用全屏广告展示接口
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

广告配置参数。

**系统能力：** SystemCapability.Advertising.Ads


| 名称 | 类型 | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| tagForChildProtection | number | 否 | 设置儿童保护标签。<br/>- -1：您不希望表明您的广告内容是否需要符合COPPA的规定。<br/>- 0：表明您的广告内容不需要符合COPPA的规定。<br/>- 1：表明您的广告内容需要符合COPPA的规定（该广告请求无法获取到任何广告）。 | 
| adContentClassification | string | 否 | 设置广告内容分级上限。<br/>- W：适合幼儿及以上年龄段观众的内容。<br/>- PI：适合少儿及以上年龄段观众的内容。<br/>- J：适合青少年及以上年龄段观众的内容。<br/>- A：仅适合成人观众的内容。 | 
| nonPersonalizedAd | number | 否 | 设置是否只请求非个性化广告。<br/>- 0：请求个性化广告与非个性化广告。<br/>- 1：只请求非个性化广告。 | 
| [key: string] | number \| boolean \| string \| undefined | 否 | 自定义参数。<br/> - totalDuration：类型number，单位：s。贴片广告必填自定义参数，用于设置贴片广告展示时长。<br/> - placementAdCountDownDesc：类型string。贴片广告可选自定义参数，用于设置贴片广告倒计时文案，该参数需要使用encodeURI()方法编码。填写了该参数，则展示倒计时文案，否则只展示倒计时。<br/> - allowMobileTraffic：类型number。可选自定义参数，设置是否允许使用流量下载广告素材。0：不允许，1：允许 |


## AdRequestParams

广告请求参数。

**系统能力：** SystemCapability.Advertising.Ads


| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| adId | string | 是 | 广告位ID。 | 
| adType | number | 否 | 请求的广告类型。<br/>- 1：开屏广告。<br/>- 3：原生广告。<br/>- 7：激励广告。<br/>- 8：banner广告。<br/>- 12：插屏广告。<br/>- 60：贴片广告。 |
| adCount | number | 否 | 请求的广告数量。 | 
| adWidth | number | 否 | 广告位宽度。 | 
| adHeight | number | 否 | 广告位高度。 | 
| adSearchKeyword | string | 否 | 广告关键字。 | 
| [key: string] | number \| boolean \| string \| undefined | 否 | 自定义参数。 | 


## AdLoadListener

单广告位广告请求回调。

**系统能力：** SystemCapability.Advertising.Ads

### onAdLoadFailure

onAdLoadFailure(errorCode: number, errorMsg: string): void

广告请求失败回调。

**系统能力：** SystemCapability.Advertising.Ads

| **参数名** | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| errorCode | number | 是 | 广告请求失败的错误码。 | 
| errorMsg | string | 是 | 广告请求失败的错误信息。 | 


### onAdLoadSuccess

onAdLoadSuccess(ads: Array&lt;advertising.[Advertisement](#advertisement)&gt;): void

广告请求成功后回调。

**系统能力：** SystemCapability.Advertising.Ads

| **参数名** | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| ads | Array&lt;advertising.[Advertisement](#advertisement)&gt; | 是 | 广告数据。 | 


**示例：**

```ts
import advertising from '@ohos.advertising';

let adLoaderListener: advertising.AdLoadListener = {
  onAdLoadFailure: (errorCode: number, errorMsg: string) => {

  },
  onAdLoadSuccess: (ads: Array<advertising.Advertisement>): void {

  }
}

```


## MultiSlotsAdLoadListener

多广告位广告请求回调。

**系统能力：** SystemCapability.Advertising.Ads

### onAdLoadFailure

onAdLoadFailure(errorCode: number, errorMsg: string): void

多广告位广告请求失败回调。

**系统能力：** SystemCapability.Advertising.Ads

| **参数名** | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| errorCode | number | 是 | 广告请求失败的错误码。 | 
| errorMsg | string | 是 | 广告请求失败的错误信息。 | 


### onAdLoadSuccess

onAdLoadSuccess(adsMap: Map&lt;string, Array&lt;advertising.[Advertisement](#advertisement)&gt;&gt;): void

多广告位广告请求成功后回调。

**系统能力：** SystemCapability.Advertising.Ads

| **参数名** | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| adsMap |  Map&lt;string, Array&lt;advertising.[Advertisement](#advertisement)&gt;&gt;| 是 | 广告数据。 | 


**示例：**

```ts
import advertising from '@ohos.advertising';

let adLoaderListener: advertising.MultiSlotsAdLoadListener = {
  onAdLoadFailure: (errorCode: number, errorMsg: string) => {

  },
  onAdLoadSuccess: (ads: Map<string, Array<advertising.Advertisement>>): void {

  }
}
```


## Advertisement


请求的广告内容。


**系统能力：** SystemCapability.Advertising.Ads


| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| adType | number | 是 | 广告类型。 | 
| uniqueId | string | 是 | 广告唯一标识。 | 
| rewarded | boolean | 是 | 广告是否获得奖励。<br/>- true：获得奖励。<br/>- false：没有获得奖励。 | 
| shown | boolean | 是 | 广告是否展示。<br/>- true：展示。<br/>- false：未展示。 | 
| clicked | boolean | 是 | 广告是否被点击。<br/>- true：被点击。<br/>- false：未被点击。 | 
| rewardVerifyConfig | Map&lt;string, string&gt; | 是 | 服务器验证参数。<br/>{<br/>customData: "test",<br/>userId: "12345"<br/>} | 
| [key: string] | Object | 是 | 自定义参数。<br/>- isFullScreen：类型boolean。开屏广告自定义参数，用于标识返回的广告是否为全屏，true为全屏广告，false为半屏广告。 |


## AdDisplayOptions


广告展示参数。


**系统能力：** SystemCapability.Advertising.Ads


| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| customData | string | 否 | 媒体自定义数据。用于服务端通知媒体服务器某位用户因为与激励视频广告互动而应予以奖励，从而规避欺骗的行为。 | 
| userId | string | 否 | 媒体自定义用户id。用于服务端通知媒体服务器某位用户因为与激励视频广告互动而应予以奖励，从而规避欺骗的行为。 | 
| useMobileDataReminder | boolean | 否 | 使用移动数据播放视频或下载应用时是否弹框通知用户。<br/>- true：弹框通知。<br/>- false：不弹框通知。 | 
| mute | boolean | 否 | 广告视频播放是否静音。<br/>- true：静音播放。<br/>- false：非静音播放。 | 
| audioFocusType | number | 否 | 视频播放过程中获得音频焦点的场景类型。<br/>- 0：视频播放静音、非静音时都获取焦点。<br/>- 1：视频静音播放时不获取焦点。<br/>- 2：视频播放静音、非静音时都不获取焦点。 | 
| [key: string] | number \| boolean \| string \| undefined | 否 | 自定义参数。<br/>- refreshTime：类型number，单位：ms，取值范围[30000, 120000]。AutoAdComponent组件可选自定义参数，用于控制广告的轮播时间间隔。填写了该参数，则广告按照参数配置的时间间隔轮播，否则广告不会轮播，只会展示广告响应中的第一个广告内容。 |


## AdInteractionListener


广告状态变化回调。


**系统能力：** SystemCapability.Advertising.Ads

### onStatusChanged

onStatusChanged(status: number, ad: advertising.[Advertisement](#advertisement), data: string)

广告状态回调。

**系统能力：** SystemCapability.Advertising.Ads

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| status | string | 是 | status：广告展示状态，取值<br/>onAdOpen（打开广告回调）、onAdClose（关闭广告回调）、onAdClick（点击广告回调）、onVideoPlayBegin（广告视频开始播放回调）、onVideoPlayEnd（广告视频播放结束回调）、onAdLoad（广告加载成功回调）、onAdFail（广告加载失败回调）、onMediaProgress（广告播放进度回调）、onMediaStart（广告开始播放回调）、onMediaPause（广告暂停播放回调）、onMediaStop（广告停止播放回调）、onMediaComplete（广告播放完成回调）、onMediaError（广告播放失败回调）、onLandscape（竖屏状态下点击全屏按钮回调）、onPortrait（全屏状态下点击返回按钮回调）、onAdReward (广告获得奖励回调) 、onMediaCountDown (广告倒计时回调) 、onBackClicked (返回点击广告回调)。 | 
| ad | advertising.[Advertisement](#advertisement) | 是 | 发生状态变化的广告内容。 | 
| data | string | 是 | 扩展信息。 | 

**示例：**

```ts
import advertising from '@ohos.advertising';

let adInteractionListener: advertising.AdInteractionListener = {
  onStatusChanged: (status: string, ad: advertising.Advertisement, data: string) => {

  }
}
```
