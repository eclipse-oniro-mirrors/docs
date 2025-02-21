# 在新窗口中打开页面


Web组件提供了在新窗口打开页面的能力，开发者可以通过[multiWindowAccess()](../reference/arkui-ts/ts-basic-components-web.md#multiwindowaccess9)接口来设置是否允许网页在新窗口打开。当有新窗口打开时，应用侧会在[onWindowNew()](../reference/arkui-ts/ts-basic-components-web.md#onwindownew9)接口中收到Web组件新窗口事件，开发者需要在此接口事件中，新建窗口来处理Web组件窗口请求。


> **说明：**
>
> 如果开发者在[onWindowNew()](../reference/arkui-ts/ts-basic-components-web.md#onwindownew9)接口通知中不需要打开新窗口，需要将[ControllerHandler.setWebController()](../reference/arkui-ts/ts-basic-components-web.md##setwebcontroller9)接口返回值设置成null。


如下面的本地示例，当用户点击“新窗口中打开网页”按钮时，应用侧会在[onWindowNew()](../reference/arkui-ts/ts-basic-components-web.md#onwindownew9)接口中收到Web组件新窗口事件。


- 应用侧代码。

  ```ts
  // xxx.ets
  import web_webview from '@ohos.web.webview'

  //在同一page页有两个web组件。在WebComponent新开窗口时，会跳转到NewWebViewComp。
  @CustomDialog
  struct NewWebViewComp {
  controller?: CustomDialogController
  webviewController1: web_webview.WebviewController = new web_webview.WebviewController()
  build() {
      Column() {
        Web({ src: "", controller: this.webviewController1 })
          .javaScriptAccess(true)
          .multiWindowAccess(false)
          .onWindowExit(()=> {
            console.info("NewWebViewComp onWindowExit")
            if (this.controller) {
              this.controller.close()
            }
          })
        }
    }
  }

  @Entry
  @Component
  struct WebComponent {
      controller: web_webview.WebviewController = new web_webview.WebviewController()
      dialogController: CustomDialogController | null = null
      build() {
        Column() {
          Web({ src:$rawfile("window.html"), controller: this.controller })
            .javaScriptAccess(true)
           //需要使能multiWindowAccess
            .multiWindowAccess(true)
            .onWindowNew((event) => {
            if (this.dialogController) {
              this.dialogController.close()
            }
            let popController:web_webview.WebviewController = new web_webview.WebviewController()
            this.dialogController = new CustomDialogController({
              builder: NewWebViewComp({webviewController1: popController})
            })
            this.dialogController.open()
            //将新窗口对应WebviewController返回给Web内核。
            //如果不需要打开新窗口请调用event.handler.setWebController接口设置成null。
            //若不调用event.handler.setWebController接口，会造成render进程阻塞。
            event.handler.setWebController(popController)
          })
      }
    }
  }
  ```


- window.html页面代码。

  ```html
   <!DOCTYPE html>
  <html>
  <head>
      <meta charset="utf-8">
      <title>WindowEvent</title>
  </head>
  <body>
  <input type="button" value="新窗口中打开网页" onclick="OpenNewWindow()">
  <script type="text/javascript">
      function OpenNewWindow()
      {
          let openedWindow = window.open("about:blank", "", "location=no,status=no,scrollvars=no");

          openedWindow.document.write("<p>这是我的窗口</p>");
          openedWindow.focus();

      }
  </script>
  </body>
  </html>
  ```
## 相关实例

针对创建新窗口，有以下相关实例可供参考：

- [浏览器（ArkTS）（Full SDK）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/OpenHarmony-3.2-Release/code/BasicFeature/Web/Browser)