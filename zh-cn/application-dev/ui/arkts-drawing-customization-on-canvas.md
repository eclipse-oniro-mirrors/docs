# 使用画布绘制自定义图形（Canvas）


Canvas提供画布组件，用于自定义绘制图形，开发者使用CanvasRenderingContext2D对象和OffscreenCanvasRenderingContext2D对象在Canvas组件上进行绘制，绘制对象可以是基础形状、文本、图片等。


## 使用画布组件绘制自定义图形

可以由以下三种形式在画布绘制自定义图形：


- 使用[CanvasRenderingContext2D对象](../reference/arkui-ts/ts-canvasrenderingcontext2d.md)在Canvas画布上绘制。

  ```ts
  @Entry
  @Component
  struct CanvasExample1 {
    //用来配置CanvasRenderingContext2D对象的参数，包括是否开启抗锯齿，true表明开启抗锯齿。
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    //用来创建CanvasRenderingContext2D对象，通过在canvas中调用CanvasRenderingContext2D对象来绘制。
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        //在canvas中调用CanvasRenderingContext2D对象。
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#F5DC62')
          .onReady(() => {
            //可以在这里绘制内容。
            this.context.strokeRect(50, 50, 200, 150);
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  
  ```

  ![2023022793003(1)](figures/2023022793003(1).jpg)

- 离屏绘制是指将需要绘制的内容先绘制在缓存区，再将其转换成图片，一次性绘制到Canvas上，加快了绘制速度。过程为：
  1. 通过transferToImageBitmap方法将离屏画布最近渲染的图像创建为一个ImageBitmap对象。
  2. 通过CanvasRenderingContext2D对象的transferFromImageBitmap方法显示给定的ImageBitmap对象。

    具体使用参考[OffscreenCanvasRenderingContext2D对象](../reference/arkui-ts/ts-offscreencanvasrenderingcontext2d.md)。

  ```ts
  @Entry
  @Component
  struct CanvasExample2 {
  //用来配置CanvasRenderingContext2D对象和OffscreenCanvasRenderingContext2D对象的参数，包括是否开启抗锯齿。true表明开启抗锯齿
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  //用来创建OffscreenCanvasRenderingContext2D对象，width为离屏画布的宽度，height为离屏画布的高度。通过在canvas中调用OffscreenCanvasRenderingContext2D对象来绘制。
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
   
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#F5DC62')
          .onReady(() =>{
            //可以在这里绘制内容
            this.offContext.strokeRect(50, 50, 200, 150);
            //将离屏绘值渲染的图像在普通画布上显示
            let image = this.offContext.transferToImageBitmap();
            this.context.transferFromImageBitmap(image);
          })
      }
      .width('100%')
      .height('100%')
    }
  }

  ```

  ![2023022793003(1)](figures/2023022793003(1).jpg)

  >**说明：**
  >
  >在画布组件中，通过CanvasRenderingContext2D对象和OffscreenCanvasRenderingContext2D对象在Canvas组件上进行绘制时调用的接口相同，另接口参数如无特别说明，单位均为vp。

- 在Canvas上加载Lottie动画时，需要先按照如下方式下载Lottie。

  ```ts
  import lottie from '@ohos/lottie'
  ```

  具体接口请参考[Lottie](https://gitee.com/openharmony-tpc/lottieETS)。


## 初始化画布组件

onReady(event: () =&gt; void)是Canvas组件初始化完成时的事件回调，调用该事件后，可获取Canvas组件的确定宽高，进一步使用CanvasRenderingContext2D对象和OffscreenCanvasRenderingContext2D对象调用相关API进行图形绘制。

```ts
Canvas(this.context)
  .width('100%')
  .height('100%')
  .backgroundColor('#F5DC62')
  .onReady(() => {
    this.context.fillStyle = '#0097D4';
    this.context.fillRect(50, 50, 100, 100);
  })

```

![2023022793350(1)](figures/2023022793350(1).jpg)


## 画布组件绘制方式

在Canvas组件生命周期接口onReady()调用之后，开发者可以直接使用canvas组件进行绘制。或者可以脱离Canvas组件和onready生命周期，单独定义Path2d对象构造理想的路径，并在onready调用之后使用Canvas组件进行绘制。

- 通过CanvasRenderingContext2D对象和OffscreenCanvasRenderingContext2D对象直接调用相关API进行绘制。

  ```ts
  Canvas(this.context)
    .width('100%')
    .height('100%')
    .backgroundColor('#F5DC62')
    .onReady(() =>{
      this.context.beginPath();
      this.context.moveTo(50, 50);
      this.context.lineTo(280, 160);
      this.context.stroke();
     })
  ```

  ![2023022793719(1)](figures/2023022793719(1).jpg)

- 先单独定义path2d对象构造理想的路径，再通过调用CanvasRenderingContext2D对象和OffscreenCanvasRenderingContext2D对象的stroke接口或者fill接口进行绘制，具体使用可以参考[Path2D对象](../reference/arkui-ts/ts-components-canvas-path2d.md)。

  ```ts
  Canvas(this.context)
    .width('100%')
    .height('100%')
    .backgroundColor('#F5DC62')
    .onReady(() =>{
       let region = new Path2D();
       region.arc(100, 75, 50, 0, 6.28);
       this.context.stroke(region);
    })
  ```

  ![2023022794031(1)](figures/2023022794031(1).jpg)


## 画布组件常用方法

OffscreenCanvasRenderingContext2D对象和CanvasRenderingContext2D对象提供了大量的属性和方法，可以用来绘制文本、图形，处理像素等，是Canvas组件的核心。常用接口有[fill](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#fill)(对封闭路径进行填充）、[clip](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#clip)(设置当前路径为剪切路径)、[stroke](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#stroke)（进行边框绘制操作）等等，同时提供了[fillStyle](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#fillstyle)（指定绘制的填充色）、[globalAlpha](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#globalalpha)（设置透明度）与[strokeStyle](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#strokestyle)（设置描边的颜色）等属性修改绘制内容的样式。将通过以下几个方面简单介绍画布组件常见使用方法：

- 基础形状绘制。
  可以通过[arc](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#arc)（绘制弧线路径）、 [ellipse](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#ellipse)（绘制一个椭圆）、[rect](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#rect)（创建矩形路径）等接口绘制基础形状。

  ```ts
  Canvas(this.context)
    .width('100%')
    .height('100%')
    .backgroundColor('#F5DC62')
    .onReady(() =>{
       //绘制矩形
       this.context.beginPath();
       this.context.rect(100, 50, 100, 100);
       this.context.stroke();
       //绘制圆形
       this.context.beginPath();
       this.context.arc(150, 250, 50, 0, 6.28);
       this.context.stroke();
       //绘制椭圆
       this.context.beginPath();
       this.context.ellipse(150, 450, 50, 100, Math.PI * 0.25, Math.PI * 0, Math.PI * 2);
       this.context.stroke();
    })

  ```

  ![2023022794521(1)](figures/2023022794521(1).jpg)

- 文本绘制。

  可以通过[fillText](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#filltext)（绘制填充类文本）、[strokeText](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#stroketext)（绘制描边类文本）等接口进行文本绘制。

  ```ts
  Canvas(this.context)
    .width('100%')
    .height('100%')
    .backgroundColor('#F5DC62')
    .onReady(() =>{
       //绘制填充类文本
       this.context.font = '50px sans-serif';
       this.context.fillText("Hello World!", 50, 100);
       //绘制描边类文本
       this.context.font = '55px sans-serif';
       this.context.strokeText("Hello World!", 50, 150);
    })
  ```

  ![2023022795105(1)](figures/2023022795105(1).jpg)

- 绘制图片和图像像素信息处理。

  可以通过[drawImage](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#drawimage)（图像绘制）、[putImageData](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#putimagedata)（使用[ImageData](../reference/arkui-ts/ts-components-canvas-imagedata.md)数据填充新的矩形区域）等接口绘制图片，通过[createImageData](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#createimagedata)（创建新的ImageData 对象）、[getPixelMap](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#getpixelmap)（以当前canvas指定区域内的像素创建[PixelMap](../reference/apis/js-apis-image.md#pixelmap7)对象）、[getImageData](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#getimagedata)（以当前canvas指定区域内的像素创建ImageData对象）等接口进行图像像素信息处理。

  ```ts
  @Entry
  @Component
  struct GetImageData {
   private settings: RenderingContextSettings = new RenderingContextSettings(true)
   private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
   private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
   private img:ImageBitmap = new ImageBitmap("/common/images/1234.png")

    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#F5DC62')
          .onReady(() =>{
            // 使用drawImage接口将图片画在（0，0）为起点，宽高130的区域
            this.offContext.drawImage(this.img,0,0,130,130);
            // 使用getImageData接口，获得canvas组件区域中，（50，50）为起点，宽高130范围内的绘制内容
            let imagedata = this.offContext.getImageData(50,50,130,130);
            // 使用putImageData接口将得到的ImageData画在起点为（150， 150）的区域中
            this.offContext.putImageData(imagedata,150,150);
            // 将离屏绘制的内容画到canvas组件上
            let image = this.offContext.transferToImageBitmap();
            this.context.transferFromImageBitmap(image);
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![drawimage](figures/drawimage.PNG)

- 其他方法。

  Canvas中还提供其他类型的方法。渐变（[CanvasGradient对象](../reference/arkui-ts/ts-components-canvas-canvasgradient.md)）相关的方法：[createLinearGradient](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#createlineargradient)（创建一个线性渐变色）、[createRadialGradient](../reference/arkui-ts/ts-canvasrenderingcontext2d.md#createradialgradient)（创建一个径向渐变色）等。

  ```ts
  Canvas(this.context)
    .width('100%')
    .height('100%')
    .backgroundColor('#F5DC62')
    .onReady(() =>{
       //创建一个径向渐变色的CanvasGradient对象
       let grad = this.context.createRadialGradient(200,200,50, 200,200,200)
       //为CanvasGradient对象设置渐变断点值，包括偏移和颜色
       grad.addColorStop(0.0, '#E87361');
       grad.addColorStop(0.5, '#FFFFF0');
       grad.addColorStop(1.0, '#BDDB69');
       //用CanvasGradient对象填充矩形
       this.context.fillStyle = grad;
       this.context.fillRect(0, 0, 400, 400);
    })
  ```

  ![2023022700701(1)](figures/2023022700701(1).jpg)


## 场景示例

- 规则基础形状绘制。

  ```ts
  @Entry
  @Component
  struct ClearRect {
   private settings: RenderingContextSettings = new RenderingContextSettings(true);
   private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings);

    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#F5DC62')
          .onReady(() =>{
            // 设定填充样式，填充颜色设为蓝色
            this.context.fillStyle = '#0097D4';
            // 以(50, 50)为左上顶点，画一个宽高200的矩形
            this.context.fillRect(50,50,200,200);
            // 以(70, 70)为左上顶点，清除宽150高100的区域
            this.context.clearRect(70,70,150,100);
        })
      }
      .width('100%')
      .height('100%')
    }
  }

  ```

  ![2023022701120(1)](figures/2023022701120(1).jpg)

- 不规则图形绘制。

  ```ts
  @Entry
  @Component
  struct Path2d {
    private settings: RenderingContextSettings = new RenderingContextSettings(true);
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings);
    
    build() {
      Row() {
        Column() {
          Canvas(this.context)
            .width('100%')
            .height('100%')
            .backgroundColor('#F5DC62')
            .onReady(() =>{
              // 使用Path2D的接口构造一个五边形
              let path = new Path2D();
              path.moveTo(150, 50);
              path.lineTo(50, 150);
              path.lineTo(100, 250);
              path.lineTo(200, 250);
              path.lineTo(250, 150);
              path.closePath();
              // 设定填充色为蓝色
              this.context.fillStyle = '#0097D4';
              // 使用填充的方式，将Path2D描述的五边形绘制在canvas组件内部
              this.context.fill(path);
            })
        }
        .width('100%')
      }
      .height('100%')
    }
  }
  ```

  ![2023032422159](figures/2023032422159.jpg)

  ​

## 相关实例

使用画布绘制自定义图形，有以下相关实例可供参考：

- [Lottie动画](https://gitee.com/openharmony/applications_app_samples/tree/master/code/Solutions/Game/Lottie)