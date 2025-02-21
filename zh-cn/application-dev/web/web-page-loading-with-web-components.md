# 使用Web组件加载页面


页面加载是Web组件的基本功能。根据页面加载数据来源可以分为三种常用场景，包括加载网络页面、加载本地页面、加载HTML格式的富文本数据。


页面加载过程中，若涉及网络资源获取，需要配置[ohos.permission.INTERNET](../security/AccessToken/declare-permissions.md)网络访问权限。


## 加载网络页面

开发者可以在Web组件创建时，指定默认加载的网络页面 。在默认页面加载完成后，如果开发者需要变更此Web组件显示的网络页面，可以通过调用[loadUrl()](../reference/apis-arkweb/js-apis-webview.md#loadurl)接口加载指定的网页。[Web组件](../reference/apis-arkweb/ts-basic-components-web.md#web)的第一个参数变量src不能通过状态变量（例如：@State）动态更改地址，如需更改，请通过[loadUrl()](../reference/apis-arkweb/js-apis-webview.md#loadurl)重新加载。


在下面的示例中，在Web组件加载完“www\.example.com”页面后，开发者可通过loadUrl接口将此Web组件显示页面变更为“www\.example1.com”。



```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('loadUrl')
        .onClick(() => {
          try {
            // 点击按钮时，通过loadUrl，跳转到www.example1.com
            this.controller.loadUrl('www.example1.com');
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      // 组件创建时，加载www.example.com
      Web({ src: 'www.example.com', controller: this.controller})
    }
  }
}
```


## 加载本地页面

将本地页面文件放在应用的rawfile目录下，开发者可以在Web组件创建的时候指定默认加载的本地页面 ，并且加载完成后可通过调用[loadUrl()](../reference/apis-arkweb/js-apis-webview.md#loadurl)接口变更当前Web组件的页面。


在下面的示例中展示加载本地页面文件的方法：


- 将资源文件放置在应用的resources/rawfile目录下。

    **图1** 资源文件路径  

    ![resource-path](figures/resource-path.png)


- 应用侧代码。

  ```ts
  // xxx.ets
  import web_webview from '@ohos.web.webview';
  import business_error from '@ohos.base';

  @Entry
  @Component
  struct WebComponent {
    controller: web_webview.WebviewController = new web_webview.WebviewController();

    build() {
      Column() {
        Button('loadUrl')
          .onClick(() => {
            try {
              // 点击按钮时，通过loadUrl，跳转到local1.html
              this.controller.loadUrl($rawfile("local1.html"));
            } catch (error) {
              let e: business_error.BusinessError = error as business_error.BusinessError;
              console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
            }
          })
        // 组件创建时，通过$rawfile加载本地文件local.html
        Web({ src: $rawfile("local.html"), controller: this.controller })
      }
    }
  }
  ```


- local.html页面代码。

  ```html
  <!-- local.html -->
  <!DOCTYPE html>
  <html>
    <body>
      <p>Hello World</p>
    </body>
  </html>
  ```

- local1.html页面代码。

  ```html
  <!-- local1.html -->
  <!DOCTYPE html>
  <html>
    <body>
      <p>This is local1 page</p>
    </body>
  </html>
  ```


## 加载HTML格式的文本数据

Web组件可以通过[loadData()](../reference/apis-arkweb/js-apis-webview.md#loaddata)接口实现加载HTML格式的文本数据。当开发者不需要加载整个页面，只需要显示一些页面片段时，可通过此功能来快速加载页面。



```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('loadData')
        .onClick(() => {
          try {
            // 点击按钮时，通过loadData，加载HTML格式的文本数据
            this.controller.loadData(
              "<html><body bgcolor=\"white\">Source:<pre>source</pre></body></html>",
              "text/html",
              "UTF-8"
            );
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      // 组件创建时，加载www.example.com
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

## 动态创建web组件
支持命令式创建Web组件，这种方式创建的组件不会立即挂载到组件树，即不会对用户呈现（组件状态为Hidden和InActive），开发者可以在后续使用中按需动态挂载。后台启动的Web实例不建议超过200个。  

```ts
// 载体Ability
// EntryAbility.ets
import { createNWeb } from "../pages/common"
onWindowStageCreate(windowStage: window.WindowStage): void {
  windowStage.loadContent('pages/Index', (err, data) => {
    // 创建Web动态组件（需传入UIContext），loadContent之后的任意时机均可创建
    createNWeb("https://www.example.com", windowStage.getMainWindowSync().getUIContext());
    if (err.code) {
      return;
    }
  });
}
```
```ts
// 创建NodeController
// common.ets
import { UIContext } from '@ohos.arkui.UIContext';
import web_webview from '@ohos.web.webview'
import { NodeController, BuilderNode, Size, FrameNode }  from '@ohos.arkui.node';
// @Builder中为动态组件的具体组件内容
// Data为入参封装类
class Data{
  url: string = "https://www.example.com";
  controller: WebviewController = new web_webview.WebviewController();
}

@Builder
function WebBuilder(data:Data) {
  Column() {
    Web({ src: data.url, controller: data.controller })
      .width("100%")
      .height("100%")
  }
}

let wrap = wrapBuilder<Data[]>(WebBuilder);

// 用于控制和反馈对应的NodeContainer上的节点的行为，需要与NodeContainer一起使用
export class myNodeController extends NodeController {
  private rootnode: BuilderNode<Data[]> | null = null;
  // 必须要重写的方法，用于构建节点数、返回节点挂载在对应NodeContainer中
  // 在对应NodeContainer创建的时候调用、或者通过rebuild方法调用刷新
  makeNode(uiContext: UIContext): FrameNode | null {
    console.log(" uicontext is undefined : "+ (uiContext === undefined));
    if (this.rootnode != null) {
      // 返回FrameNode节点
      return this.rootnode.getFrameNode();
    }
    // 返回null控制动态组件脱离绑定节点
    return null;
  }
  // 当布局大小发生变化时进行回调
  aboutToResize(size: Size) {
    console.log("aboutToResize width : " + size.width  +  " height : " + size.height )
  }

  // 当controller对应的NodeContainer在Appear的时候进行回调
  aboutToAppear() {
    console.log("aboutToAppear")
  }

  // 当controller对应的NodeContainer在Disappear的时候进行回调
  aboutToDisappear() {
    console.log("aboutToDisappear")
  }

  // 此函数为自定义函数，可作为初始化函数使用
  // 通过UIContext初始化BuilderNode，再通过BuilderNode中的build接口初始化@Builder中的内容
  initWeb(url:string, uiContext:UIContext, control:WebviewController) {
    if(this.rootnode != null)
    {
      return;
    }
    // 创建节点，需要uiContext
    this.rootnode = new BuilderNode(uiContext)
    // 创建动态Web组件
    this.rootnode.build(wrap, { url:url, controller:control })
  }
}
 // 创建Map保存所需要的NodeController
let NodeMap:Map<string, myNodeController | undefined> = new Map();
// 创建Map保存所需要的WebViewController
let controllerMap:Map<string, WebviewController | undefined> = new Map();

// 初始化需要UIContext 需在Ability获取
export const createNWeb = (url: string, uiContext: UIContext) => {
  // 创建NodeController 
  let baseNode = new myNodeController();
  let controller = new web_webview.WebviewController() ;
  // 初始化自定义web组件
  baseNode.initWeb(url, uiContext, controller);
  controllerMap.set(url, controller)
  NodeMap.set(url, baseNode);
}
// 自定义获取NodeController接口
export const getNWeb = (url : string) : myNodeController | undefined => {
  return NodeMap.get(url);
}
```
```ts
// 使用NodeController的Page页
// Index.ets
import { getNWeb } from "./common"
@Entry
@Component
struct Index {
  build() {
    Row() {
      Column() {
        // NodeContainer用于与NodeController节点绑定，rebuild会触发makeNode
        // Page页通过NodeContainer接口绑定NodeController，实现动态组件页面显示
        NodeContainer(getNWeb("https://www.example.com"))
          .height("90%")
          .width("100%")
      }
      .width('100%')
    }
    .height('100%')
  }
}

```
## 相关实例

针对Web组件开发，有以下相关实例可供参考：

- [浏览器（ArkTS）（Full SDK）(API9)](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/Web/Browser)