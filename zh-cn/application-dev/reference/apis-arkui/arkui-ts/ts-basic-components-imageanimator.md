# ImageAnimator

提供帧动画组件来实现逐帧播放图片的能力，可以配置需要播放的图片列表，每张图片可以配置时长。

>  **说明：**
>
> 该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。



## 子组件

无


## 接口

ImageAnimator()

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

## 属性

除支持[通用属性](ts-universal-attributes-size.md)外，还支持以下属性：

### images

images(value: Array&lt;ImageFrameInfo&gt;)

设置图片帧信息集合。不支持动态更新。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                   | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | Array&lt;[ImageFrameInfo](#imageframeinfo对象说明)&gt; | 是   | 设置图片帧信息集合。每一帧的帧信息(ImageFrameInfo)包含图片路径、图片大小、图片位置和图片播放时长信息，详见ImageFrameInfo属性说明。<br/>默认值：[] |

### state

state(value: AnimationStatus)

控制播放状态。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                    | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| value  | [AnimationStatus](ts-appendix-enums.md#animationstatus) | 是   | 默认为初始状态，用于控制播放状态。<br/>默认值：AnimationStatus.Initial |

### duration

duration(value: number)

设置播放时长。当Images中任意一帧图片设置了单独的duration后，该属性设置无效。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| value  | number | 是   | 播放时长。<br/>value为0时，不播放图片。<br/>value的改变只会在下一次循环开始时生效。<br/>单位：毫秒<br/>默认值：1000ms |

### reverse

reverse(value: boolean)

设置播放方向。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 播放方向。<br/>false表示从第1张图片播放到最后1张图片，true表示从最后1张图片播放到第1张图片。<br/>默认值：false |

### fixedSize

fixedSize(value: boolean)

设置图片大小是否固定为组件大小。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 设置图片大小是否固定为组件大小。&nbsp;true表示图片大小与组件大小一致，此时设置图片的width&nbsp;、height&nbsp;、top&nbsp;和left属性是无效的。false表示每一张图片的width&nbsp;、height&nbsp;、top和left属性都要单独设置。<br/>默认值：true |

### preDecode<sup>(deprecated)</sup>

preDecode(value: number)

设置预解码的图片数量。

从API version 9开始废弃。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| value  | number | 是   | 预解码的图片数量。例如该值设为2，则播放当前页时会提前加载后面两张图片至缓存以提升性能。<br/>默认值：0 |

### fillMode

fillMode(value: FillMode)

设置当前播放方向下，动画开始前和结束后的状态。动画结束后的状态由fillMode和reverse属性共同决定。例如，fillMode为Forwards表示停止时维持动画最后一个关键帧的状态，若reverse为false则维持正播的最后一帧，即最后一张图，若reverse为true则维持逆播的最后一帧，即第一张图。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                      | 必填 | 说明                                                         |
| ------ | ----------------------------------------- | ---- | ------------------------------------------------------------ |
| value  | [FillMode](ts-appendix-enums.md#fillmode) | 是   | 当前播放方向下，动画开始前和结束后的状态。<br/>默认值：FillMode.Forwards |

### iterations

iterations(value: number)

设置播放次数。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                                                   |
| ------ | ------ | ---- | ------------------------------------------------------ |
| value  | number | 是   | 默认播放一次，设置为-1时表示无限次播放。<br/>默认值：1 |

## ImageFrameInfo对象说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称   | 类型   | 必填 | 说明 |
| -------- | -------------- | -------- | -------- |
| src      | string \| [Resource](ts-types.md#resource)<sup>9+</sup> \| [PixelMap](../../apis-image-kit/js-apis-image.md#pixelmap7)<sup>12+</sup> | 是    | 图片路径，图片格式为jpg、jpeg、svg、png、bmp、webp、ico和heif，从API Version9开始支持[Resource](ts-types.md#resource)类型的路径，从API version 12开始支持[PixelMap](../../apis-image-kit/js-apis-image.md#pixelmap7)类型。 <br/>**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。|
| width    | number&nbsp;\|&nbsp;string | 否  | 图片宽度。<br/>默认值：0   <br/>**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用       |
| height   | number&nbsp;\|&nbsp;string | 否  | 图片高度。<br/>默认值：0     <br/>**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用        |
| top      | number&nbsp;\|&nbsp;string | 否  | 图片相对于组件左上角的纵向坐标。<br/>默认值：0  <br/>**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用  |
| left     | number&nbsp;\|&nbsp;string | 否  | 图片相对于组件左上角的横向坐标。<br/>默认值：0 <br/>**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用   |
| duration | number          | 否     | 每一帧图片的播放时长，单位毫秒。<br/>默认值：0         |

## 事件

除支持[通用事件](ts-universal-events-click.md)外，还支持以下事件：

### onStart

onStart(event:&nbsp;()&nbsp;=&gt;&nbsp;void)

状态回调，动画开始播放时触发。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onPause

onPause(event:&nbsp;()&nbsp;=&gt;&nbsp;void)

状态回调，动画暂停播放时触发。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onRepeat

onRepeat(event:&nbsp;()&nbsp;=&gt;&nbsp;void)

状态回调，动画重复播放时触发。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onCancel

onCancel(event:&nbsp;()&nbsp;=&gt;&nbsp;void)

状态回调，动画返回最初状态时触发。

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onFinish

onFinish(event:&nbsp;()&nbsp;=&gt;&nbsp;void)

状态回调，动画播放完成时或者停止播放时触发。 

**卡片能力：** 从API version 10开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full


## 示例

### 示例1（播放Resource动画）

通过ImageAnimator组件播放Resource动画。

```ts
// xxx.ets
@Entry
@Component
struct ImageAnimatorExample {
  @State state: AnimationStatus = AnimationStatus.Initial
  @State reverse: boolean = false
  @State iterations: number = 1

  build() {
    Column({ space: 10 }) {
      ImageAnimator()
        .images([
          {
            src: $r('app.media.img1')
          },
          {
            src: $r('app.media.img2')
          },
          {
            src: $r('app.media.img3')
          },
          {
            src: $r('app.media.img4')
          }
        ])
        .duration(2000)
        .state(this.state).reverse(this.reverse)
        .fillMode(FillMode.None).iterations(this.iterations).width(340).height(240)
        .margin({ top: 100 })
        .onStart(() => {
          console.info('Start')
        })
        .onPause(() => {
          console.info('Pause')
        })
        .onRepeat(() => {
          console.info('Repeat')
        })
        .onCancel(() => {
          console.info('Cancel')
        })
        .onFinish(() => {
          console.info('Finish')
          this.state = AnimationStatus.Stopped
        })
      Row() {
        Button('start').width(100).padding(5).onClick(() => {
          this.state = AnimationStatus.Running
        }).margin(5)
        Button('pause').width(100).padding(5).onClick(() => {
          this.state = AnimationStatus.Paused     // 显示当前帧图片
        }).margin(5)
        Button('stop').width(100).padding(5).onClick(() => {
          this.state = AnimationStatus.Stopped    // 显示动画的起始帧图片
        }).margin(5)
      }

      Row() {
        Button('reverse').width(100).padding(5).onClick(() => {
          this.reverse = !this.reverse
        }).margin(5)
        Button('once').width(100).padding(5).onClick(() => {
          this.iterations = 1
        }).margin(5)
        Button('infinite').width(100).padding(5).onClick(() => {
          this.iterations = -1 // 无限循环播放
        }).margin(5)
      }
    }.width('100%').height('100%')
  }
}
```

### 示例2（播放PixelMap动画）

通过ImageAnimator组件播放PixelMap动画。

```ts
// xxx.ets
import { image } from '@kit.ImageKit'

@Entry
@Component
struct ImageAnimatorExample {
  imagePixelMap: Array<PixelMap> = []
  @State state: AnimationStatus = AnimationStatus.Initial
  @State reverse: boolean = false
  @State iterations: number = 1
  @State images:Array<ImageFrameInfo> = []
  async aboutToAppear() {
    this.imagePixelMap.push(await this.getPixmapFromMedia($r('app.media.icon')))
    this.images.push({src:this.imagePixelMap[0]})
  }
  build() {
    Column({ space: 10 }) {
      ImageAnimator()
        .images(this.images)
        .duration(2000)
        .state(this.state).reverse(this.reverse)
        .fillMode(FillMode.None).iterations(this.iterations).width(340).height(240)
        .margin({ top: 100 })
        .onStart(() => {
          console.info('Start')
        })
        .onPause(() => {
          console.info('Pause')
        })
        .onRepeat(() => {
          console.info('Repeat')
        })
        .onCancel(() => {
          console.info('Cancel')
        })
        .onFinish(() => {
          console.info('Finish')
          this.state = AnimationStatus.Stopped
        })
      Row() {
        Button('start').width(100).padding(5).onClick(() => {
          this.state = AnimationStatus.Running
        }).margin(5)
        Button('pause').width(100).padding(5).onClick(() => {
          this.state = AnimationStatus.Paused     // 显示当前帧图片
        }).margin(5)
        Button('stop').width(100).padding(5).onClick(() => {
          this.state = AnimationStatus.Stopped    // 显示动画的起始帧图片
        }).margin(5)
      }
      Row() {
        Button('reverse').width(100).padding(5).onClick(() => {
          this.reverse = !this.reverse
        }).margin(5)
        Button('once').width(100).padding(5).onClick(() => {
          this.iterations = 1
        }).margin(5)
        Button('infinite').width(100).padding(5).onClick(() => {
          this.iterations = -1 // 无限循环播放
        }).margin(5)
      }
    }.width('100%').height('100%')
  }

  private async getPixmapFromMedia(resource: Resource) {
    let unit8Array = await getContext(this)?.resourceManager?.getMediaContent({
      bundleName: resource.bundleName,
      moduleName: resource.moduleName,
      id: resource.id
    })
    let imageSource = image.createImageSource(unit8Array.buffer.slice(0, unit8Array.buffer.byteLength))
    let createPixelMap: image.PixelMap = await imageSource.createPixelMap({
      desiredPixelFormat: image.PixelMapFormat.RGBA_8888
    })
    await imageSource.release()
    return createPixelMap
  }
}
```

![imageAnimator](figures/imageAnimator.gif)