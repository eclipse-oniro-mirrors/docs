# @ohos.advertising.AutoAdComponent (轮播广告展示组件)


本模块提供展示轮播广告的能力。


> **说明：**
> 
> 本模块首批接口从API Version 11开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import { AutoAdComponent } from '@ohos.advertising.AutoAdComponent';
```


## AutoAdComponent

AutoAdComponent(adParam: advertising.AdRequestParams, adOptions: advertising.AdOptions, displayOptions: advertising.AdDisplayOptions, interactionListener: advertising.AdInteractionListener): void

自动播放广告组件。

**系统能力：** SystemCapability.Advertising.Ads

**起始版本：** 11


**参数：**


| **参数名** | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| adParam | advertising.[AdRequestParams](js-apis-advertising.md#adrequestparams) | 是 | 广告请求参数。 | 
| adOptions | advertising.[AdOptions](js-apis-advertising.md#adoptions) | 是 | 广告配置。 | 
| displayOptions | advertising.[AdDisplayOptions](js-apis-advertising.md#addisplayoptions) | 是 | 广告展示参数。 | 
| interactionListener | advertising.[AdInteractionListener](js-apis-advertising.md#adinteractionlistener) | 是 | 广告状态变化回调。 | 


**示例：**
```ts
import advertising from '@ohos.advertising';
import { AutoAdComponent } from '@ohos.advertising.AutoAdComponent';
import hilog from '@ohos.hilog'; 

@Entry
@Component
export struct ShowCarouselAd {
  private adRequestParam: advertising.AdRequestParams = {
    // 广告类型
    adType: 8, 
    // 测试广告位ID
    adId: "test1", 
  };
  private adOptions: advertising.AdOptions = {
    // 设置广告内容分级上限
    adContentClassification: 'A',
  };
  // 广告展示参数
  private adDisplayOptions: advertising.AdDisplayOptions = {
    // 是否静音，默认不静音
    mute: false,
    // 广告轮播的时间间隔，单位ms，取值范围[30000, 120000]
    refreshTime: 30000
  }

  build() {
    Column() {
      // AutoAdComponent组件用于展示轮播非全屏广告
      AutoAdComponent({ adParam: this.adRequestParam, adOptions: this.adOptions, displayOptions: this.adDisplayOptions,
        interactionListener: {
          // 广告状态变化回调
          onStatusChanged: (status: string, ad: advertising.Advertisement, data: string) => {
            switch(status) {
              case 'onAdOpen':
                hilog.info(0x0000, 'testTag', '%{public}s', 'onAdOpen');
                break;
              case 'onAdClick':
                hilog.info(0x0000, 'testTag', '%{public}s', 'onAdClick');
                break;
              case 'onAdClose':
                hilog.info(0x0000, 'testTag', '%{public}s', 'onAdClose');
                break;
            }
          }}})
        .width('100%')
        .height('100%')
    }.width('100%').height('100%')
  }
}
```
