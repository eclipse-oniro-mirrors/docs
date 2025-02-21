# Managing Page Redirection and Browsing History Navigation


## History Navigation

When a user clicks a web page link on the frontend page, the **Web** component automatically opens and loads the target website by default. When the current page is assigned a new loading link, the address of the accessed web page is automatically recorded. You can call [forward()](../reference/apis/js-apis-webview.md#forward) or [backward()](../reference/apis/js-apis-webview.md#backward) to browse the previous or next history record.

  In the following example, when a user clicks the button, **backward()** is called to go back to the previous page.

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';

@Entry
@Component
struct WebComponent {
  webviewController: web_webview.WebviewController = new web_webview.WebviewController();
  build() {
    Column() {
      Button('loadData')
        .onClick(() => {
          if (this.webviewController.accessBackward()) {
            this.webviewController.backward();
            return true;
          }
        })
      Web({ src: 'https://www.example.com/cn/', controller: this.webviewController})
    }
  }
}
```


If a previous record exists, [accessBackward()](../reference/apis/js-apis-webview.md#accessbackward) will return **true**. Similarly, you can call [accessForward()](../reference/apis/js-apis-webview.md#accessforward) to check whether a next record exists. If you skip the check, [forward()](../reference/apis/js-apis-webview.md#forward) and [backward()](../reference/apis/js-apis-webview.md#backward) will not trigger any action if the user has navigated to the end of history records.


## Page Redirection

The **Web** component provides the [onUrlLoadIntercept()](../reference/arkui-ts/ts-basic-components-web.md#onurlloadintercept) API to redirect you from one page to another.

In the following example, the frontend page **route.html** is loaded on to the application home page **Index.ets**, and the user is redirected to the application page **ProfilePage.ets** when clicking the link on the **route.html** page.

- Code of the **index.ets** page:
  
  ```ts
  // index.ets
  import web_webview from '@ohos.web.webview';
  import router from '@ohos.router';
  @Entry
  @Component
  struct WebComponent {
    webviewController: web_webview.WebviewController = new web_webview.WebviewController();
  
    build() {
      Column() {
        Web({ src: $rawfile('route.html'), controller: this.webviewController })
          .onUrlLoadIntercept((event) => {
            let url: string = event.data as string;
            if (url.indexOf('native://') === 0) {
              // Redirect to another page.
              router.pushUrl({ url:url.substring(9) })
              return true;
            }
            return false;
          })
      }
    }
  }
  ```

- Code of the **route.html** page:
  
  ```html
  <!-- route.html -->
  <!DOCTYPE html>
  <html>
  <body>
    <div>
        <a href="native://pages/ProfilePage">My Profile</a>
     </div>
  </body>
  </html>
  ```

- Code of the **ProfilePage.ets** page:
  
  ```ts
  @Entry
  @Component
  struct ProfilePage {
    @State message: string = 'Hello World';
  
    build() {
      Column() {
        Text(this.message)
          .fontSize(20)
      }
    }
  }
  ```


## Cross-Application Redirection

The **Web** component supports redirection from one application to another.

In the following example, when a user clicks the link on the frontend page **call.html**, the user will be redirected to the dial screen of the phone app.

- Application code:
  
  ```ts
  // xxx.ets
  import web_webview from '@ohos.web.webview';
  import call from '@ohos.telephony.call';
  
  @Entry
  @Component
  struct WebComponent {
    webviewController: web_webview.WebviewController = new web_webview.WebviewController();
  
    build() {
      Column() {
        Web({ src: $rawfile('xxx.html'), controller: this.webviewController})
          .onUrlLoadIntercept((event) => {
            let url: string = event.data as string;
            // Check whether the link is redirecting to the dial screen of the phone app.
            if (url.indexOf('tel://') === 0) {
              // Redirect to the dial screen.
              call.makeCall(url.substring(6), (err) => {
                if (!err) {
                  console.info('make call succeeded.');
                } else {
                  console.info('make call fail, err is:' + JSON.stringify(err));
                }
              });
              return true;
            }
            return false;
          })
      }
    }
  }
  ```

- Code of the **call.html** page:
  
  ```html
  <!-- call.html -->
  <!DOCTYPE html>
  <html>
  <body>
    <div>
      <a href="tel://xxx xxxx xxx">Dial number</a>
    </div>
  </body>
  </html>
  ```
