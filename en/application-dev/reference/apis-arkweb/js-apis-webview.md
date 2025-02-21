

# @ohos.web.webview (Webview)

The **Webview** module provides APIs for web control. It can work with the [<Web\>](ts-basic-components-web.md) component, which is used to display web pages.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 9. Updates will be marked with a superscript to indicate their earliest API version.
>
> - You can preview how the APIs of this module work on a real device. The preview is not yet available in the DevEco Studio Previewer.

## Required Permissions

**ohos.permission.INTERNET**, required for accessing online web pages. For details about how to apply for a permission, see [Declaring Permissions](../../security/AccessToken/declare-permissions.md).

## Modules to Import

```ts
import web_webview from '@ohos.web.webview';
```

## once

once(type: string, callback: Callback\<void\>): void

Registers a one-time callback for web events of the specified type.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name | Type             | Mandatory| Description                 |
| ------- | ---------------- | ---- | -------------------- |
| type     | string          | Yes  | Web event type. The value can be **"webInited"**, indicating completion of web initialization.     |
| callback | Callback\<void\> | Yes  | Callback to register.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

web_webview.once("webInited", () => {
  console.log("configCookieSync")
  web_webview.WebCookieManager.configCookieSync("https://www.example.com", "a=b")
})

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

## WebMessagePort

Implements a **WebMessagePort** object to send and receive messages.

### postMessageEvent

postMessageEvent(message: WebMessage): void

Sends a message. For the complete sample code, see [postMessage](#postmessage).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name | Type  | Mandatory| Description          |
| ------- | ------ | ---- | :------------- |
| message | [WebMessage](#webmessage) | Yes  | Message to send.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100010 | Can not post message using this port. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  ports: web_webview.WebMessagePort[] = [];

  build() {
    Column() {
      Button('postMessageEvent')
        .onClick(() => {
          try {
            this.ports = this.controller.createWebMessagePorts();
            this.controller.postMessage('__init_port__', [this.ports[0]], '*');
            this.ports[1].postMessageEvent("post message from ets to html5");
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### onMessageEvent

onMessageEvent(callback: (result: WebMessage) => void): void

Registers a callback to receive messages from the HTML side. For the complete sample code, see [postMessage](#postmessage).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type    | Mandatory| Description                |
| -------- | -------- | ---- | :------------------- |
| result | [WebMessage](#webmessage) | Yes  | Message received.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                       |
| -------- | ----------------------------------------------- |
| 17100006 | Can not register message event using this port. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  ports: web_webview.WebMessagePort[] = [];

  build() {
    Column() {
      Button('onMessageEvent')
        .onClick(() => {
          try {
            this.ports = this.controller.createWebMessagePorts();
            this.ports[1].onMessageEvent((msg) => {
              if (typeof(msg) == "string") {
                console.log("received string message from html5, string is:" + msg);
              } else if (typeof(msg) == "object") {
                if (msg instanceof ArrayBuffer) {
                  console.log("received arraybuffer from html5, length is:" + msg.byteLength);
                } else {
                  console.log("not support");
                }
              } else {
                console.log("not support");
              }
            })
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### isExtentionType<sup>10+</sup>

**System capability**: SystemCapability.Web.Webview.Core

| Name        | Type  | Readable| Writable| Description                                             |
| ------------ | ------ | ---- | ---- | ------------------------------------------------|
| isExtentionType | boolean | Yes  | Yes| Whether to use the extended interface when creating a **WebMessagePort** instance.  |

### postMessageEventExt<sup>10+</sup>

postMessageEventExt(message: WebMessageExt): void

Sends a message. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name | Type  | Mandatory| Description          |
| ------- | ------ | ---- | :------------- |
| message | [WebMessageExt](#webmessageext10) | Yes  | Message to send.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100010 | Can not post message using this port. |

### onMessageEventExt<sup>10+</sup>

onMessageEventExt(callback: (result: WebMessageExt) => void): void

Registers a callback to receive messages from the HTML5 side.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type    | Mandatory| Description                |
| -------- | -------- | ---- | :------------------- |
| result | [WebMessageExt](#webmessageext10) | Yes  | Message received.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                       |
| -------- | ----------------------------------------------- |
| 17100006 | Can not register message event using this port. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

class TestObj {
  test(str: string): ArrayBuffer {
    let buf = new ArrayBuffer(str.length);
    let buff = new Uint8Array(buf);

    for (let i = 0; i < str.length; i++) {
      buff[i] = str.charCodeAt(i);
    }
    return buf;
  }
}

// Example of sending messages between an application and a web page: Use the init_web_messageport channel to receive messages from the web page on the application side through port 0 and receive messages from the application on the web page side through port 1.
@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  ports: web_webview.WebMessagePort[] = [];
  nativePort: web_webview.WebMessagePort | null = null;
  @State msg1: string = "";
  @State msg2: string = "";
  message: web_webview.WebMessageExt = new web_webview.WebMessageExt();
  @State testObjtest: TestObj = new TestObj();

  build() {
    Column() {
      Text(this.msg1).fontSize(16)
      Text(this.msg2).fontSize(16)
      Button('SendToH5 setString').margin({
        right: 800,
      })
        .onClick(() => {
          // Use the local port to send messages to HTML5.
          try {
            console.log("In ArkTS side send true start");
            if (this.nativePort) {
              this.message.setType(1);
              this.message.setString("helloFromEts");
              this.nativePort.postMessageEventExt(this.message);
            }
          }
          catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`In ArkTS side send message catch error, ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
        Button('SendToH5 setNumber').margin({
        top: 10,
        right: 800,
      })
        .onClick(() => {
          // Use the local port to send messages to HTML5.
          try {
            console.log("In ArkTS side send true start");
            if (this.nativePort) {
              this.message.setType(2);
              this.message.setNumber(12345);
              this.nativePort.postMessageEventExt(this.message);
            }
          }
          catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`In ArkTS side send message catch error, ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
        Button('SendToH5 setBoolean').margin({
        top: -90,
      })
        .onClick(() => {
          // Use the local port to send messages to HTML5.
          try {
            console.log("In ArkTS side send true start");
            if (this.nativePort) {
              this.message.setType(3);
              this.message.setBoolean(true);
              this.nativePort.postMessageEventExt(this.message);
            }
          }
          catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`In ArkTS side send message catch error, ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
        Button('SendToH5 setArrayBuffer').margin({
        top: 10,
      })
        .onClick(() => {
          // Use the local port to send messages to HTML5.
          try {
            console.log("In ArkTS side send true start");
            if (this.nativePort) {
              this.message.setType(4);
              this.message.setArrayBuffer(this.testObjtest.test("Name=test&Password=test"));
              this.nativePort.postMessageEventExt(this.message);
            }
          }
          catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`In ArkTS side send message catch error, ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
        Button('SendToH5 setArray').margin({
        top: -90,
        left: 800,
      })
        .onClick(() => {
          // Use the local port to send messages to HTML5.
          try {
            console.log("In ArkTS side send true start");
            if (this.nativePort) {
              this.message.setType(5);
              this.message.setArray([1,2,3]);
              this.nativePort.postMessageEventExt(this.message);
            }
          }
          catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`In ArkTS side send message catch error, ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
        Button('SendToH5 setError').margin({
        top: 10,
        left: 800,
      })
        .onClick(() => {
          // Use the local port to send messages to HTML5.
          try {
            console.log("In ArkTS side send true start");
            throw new ReferenceError("ReferenceError");
          }
          catch (error) {
            if (this.nativePort) {
              this.message.setType(6);
              this.message.setError(error);
              this.nativePort.postMessageEventExt(this.message);
            }
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`In ArkTS side send message catch error, ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })

      Web({ src: $rawfile('index.html'), controller: this.controller })
        .onPageEnd(() => {
          console.log("In ArkTS side message onPageEnd init mesaage channel");
          // 1. Create a message port.
          this.ports = this.controller.createWebMessagePorts(true);
          // 2. Send port 1 to HTML5.
          this.controller.postMessage("init_web_messageport", [this.ports[1]], "*");
          // 3. Save port 0 to the local host.
          this.nativePort = this.ports[0];
          // 4. Set the callback.
          this.nativePort.onMessageEventExt((result) => {
            console.log("In ArkTS side got message");
            try {
              let type = result.getType();
              console.log("In ArkTS side getType:" + type);
              switch (type) {
                case web_webview.WebMessageType.STRING: {
                  this.msg1 = "result type:" + typeof (result.getString());
                  this.msg2 = "result getString:" + ((result.getString()));
                  break;
                }
                case web_webview.WebMessageType.NUMBER: {
                  this.msg1 = "result type:" + typeof (result.getNumber());
                  this.msg2 = "result getNumber:" + ((result.getNumber()));
                  break;
                }
                case web_webview.WebMessageType.BOOLEAN: {
                  this.msg1 = "result type:" + typeof (result.getBoolean());
                  this.msg2 = "result getBoolean:" + ((result.getBoolean()));
                  break;
                }
                case web_webview.WebMessageType.ARRAY_BUFFER: {
                  this.msg1 = "result type:" + typeof (result.getArrayBuffer());
                  this.msg2 = "result getArrayBuffer byteLength:" + ((result.getArrayBuffer().byteLength));
                  break;
                }
                case web_webview.WebMessageType.ARRAY: {
                  this.msg1 = "result type:" + typeof (result.getArray());
                  this.msg2 = "result getArray:" + result.getArray();
                  break;
                }
                case web_webview.WebMessageType.ERROR: {
                  this.msg1 = "result type:" + typeof (result.getError());
                  this.msg2 = "result getError:" + result.getError();
                  break;
                }
                default: {
                  this.msg1 = "default break, type:" + type;
                  break;
                }
              }
            }
            catch (error) {
              let e: business_error.BusinessError = error as business_error.BusinessError;
              console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
            }
          });
        })
    }
  }
}
```

HTML file to be loaded:
```html
<!--index.html-->
<!DOCTYPE html>
<html lang="en-gb">
<head>
    <title>WebView MessagePort Demo</title>
</head>

<body>
<h1>Html5 Send and Receive Message</h1>
<h3 id="msg">Receive string:</h3>
<h3 id="msg2">Receive arraybuffer:</h3>
<div style="font-size: 10pt; text-align: center;">
    <input type="button" value="Send String" onclick="postStringToApp();" /><br/>
</div>
</body>
<script src="index.js"></script>
</html>
```

```js
//index.js
var h5Port;
window.addEventListener('message', function(event) {
    if (event.data == 'init_web_messageport') {
        if(event.ports[0] != null) {
            h5Port = event.ports[0]; // 1. Save the port number sent from the eTS side.
            h5Port.onmessage = function(event) {
                console.log("hwd In html got message");
                // 2. Receive the message sent from the eTS side.
                var result = event.data;
                console.log("In html got message, typeof: ", typeof(result));
                console.log("In html got message, result: ", (result));
                if (typeof(result) == "string") {
                    console.log("In html got message, String: ", result);
                    document.getElementById("msg").innerHTML  =  "String:" + result;
                } else if (typeof(result) == "number") {
                  console.log("In html side got message, number: ", result);
                    document.getElementById("msg").innerHTML = "Number:" + result;
                } else if (typeof(result) == "boolean") {
                    console.log("In html side got message, boolean: ", result);
                    document.getElementById("msg").innerHTML = "Boolean:" + result;
                } else if (typeof(result) == "object") {
                    if (result instanceof ArrayBuffer) {
                        document.getElementById("msg2").innerHTML  =  "ArrayBuffer:" + result.byteLength;
                        console.log("In html got message, byteLength: ", result.byteLength);
                    } else if (result instanceof Error) {
                        console.log("In html error message, err:" + (result));
                        console.log("In html error message, typeof err:" + typeof(result));
                        document.getElementById("msg2").innerHTML  =  "Error:" + result.name + ", msg:" + result.message;
                    } else if (result instanceof Array) {
                        console.log("In html got message, Array");
                        console.log("In html got message, Array length:" + result.length);
                        console.log("In html got message, Array[0]:" + (result[0]));
                        console.log("In html got message, typeof Array[0]:" + typeof(result[0]));
                        document.getElementById("msg2").innerHTML  =  "Array len:" + result.length + ", value:" + result;
                    } else {
                        console.log("In html got message, not any instance of support type");
                        document.getElementById("msg").innerHTML  = "not any instance of support type";
                    }
                } else {
                    console.log("In html got message, not support type");
                    document.getElementById("msg").innerHTML  = "not support type";
                }
            }
            h5Port.onmessageerror = (event) => {
                console.error(`hwd In html Error receiving message: ${event}`);
            };
        }
    }
})

// Use h5Port to send a message of the string type to the ets side.
function postStringToApp() {
    if (h5Port) {
        console.log("In html send string message");
        h5Port.postMessage("hello");
        console.log("In html send string message end");
    } else {
        console.error("In html h5port is null, please init first");
    }
}
```

### close

close(): void

Closes this message port. To use this API, a message port must first be created using [createWebMessagePorts](#createwebmessageports).

**System capability**: SystemCapability.Web.Webview.Core

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  msgPort: web_webview.WebMessagePort[] = [];

  build() {
    Column() {
      // Use createWebMessagePorts to create a message port.
      Button('createWebMessagePorts')
        .onClick(() => {
          try {
            this.msgPort = this.controller.createWebMessagePorts();
            console.log("createWebMessagePorts size:" + this.msgPort.length)
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('close')
        .onClick(() => {
          try {
            if (this.msgPort && this.msgPort.length == 2) {
              this.msgPort[1].close();
            } else {
              console.error("msgPort is null, Please initialize first");
            }
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

## WebviewController

Implements a **WebviewController** to control the behavior of the **\<Web>** component. A **WebviewController** can control only one **\<Web>** component, and the APIs (except static APIs) in the **WebviewController** can be invoked only after it has been bound to the target **\<Web>** component.

### constructor<sup>11+</sup>

constructor(webTag?: string)

Constructor used to create a **WebviewController** object.

> **NOTE**
>
> **webTag** represents a tag that you define and pass to the **\<Web>** component as a parameter of string type.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name    | Type  | Mandatory| Description                              |
| ---------- | ------ | ---- | -------------------------------- |
| webTag   | string | No  | Name of the **\<Web>** component. The default value is **Empty**.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

class WebObj {
  constructor() {
  }

  webTest(): string {
    console.log('Web test');
    return "Web test";
  }

  webString(): void {
    console.log('Web test toString');
  }
}

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController()
  @State webTestObj: WebObj = new WebObj();
  build() {
    Column() {
      Button('refresh')
        .onClick(() => {
          try {
            this.controller.refresh();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: '', controller: this.controller })
        .javaScriptAccess(true)
        .onControllerAttached(() => {
          this.controller.loadUrl($rawfile("index.html"));
          this.controller.registerJavaScriptProxy(this.webTestObj, "objTestName", ["webTest", "webString"]);
        })
    }
  }
}
```

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html>
    <meta charset="utf-8">
    <body>
      <button type="button" onclick="htmlTest()">Click Me!</button>
      <p id="demo"></p>
      <p id="webDemo"></p>
    </body>
    <script type="text/javascript">
    function htmlTest() {
      // This function call expects to return "Web test"
      let webStr = objTestName.webTest();
      document.getElementById("webDemo").innerHTML=webStr;
      console.log('objTestName.webTest result:'+ webStr)
    }
</script>
</html>
```

### initializeWebEngine

static initializeWebEngine(): void

Loads the dynamic link library (DLL) file of the web engine. This API can be called before the **\<Web>** component is initialized to improve the startup performance.

**System capability**: SystemCapability.Web.Webview.Core

**Example**

The following code snippet exemplifies calling this API after the EntryAbility is created.

```ts
// xxx.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import web_webview from '@ohos.web.webview';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import Want from '@ohos.app.ability.Want';

export default class EntryAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
    console.log("EntryAbility onCreate")
    web_webview.WebviewController.initializeWebEngine()
    console.log("EntryAbility onCreate done")
  }
}
```

### setHttpDns<sup>10+</sup>

static setHttpDns(secureDnsMode:SecureDnsMode, secureDnsConfig:string): void

Sets how the \<Web> component uses HTTPDNS for DNS resolution.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name             | Type   | Mandatory  |  Description|
| ------------------ | ------- | ---- | ------------- |
| secureDnsMode         |   [SecureDnsMode](#securednsmode10)   | Yes  | Mode in which HTTPDNS is used.|
| secureDnsConfig       | string | Yes| Information about the HTTPDNS server to use, which must use HTTPS. Only one HTTPDNS server can be configured.|

**Example**

```ts
// xxx.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import web_webview from '@ohos.web.webview';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import Want from '@ohos.app.ability.Want';
import business_error from '@ohos.base';

export default class EntryAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
    console.log("EntryAbility onCreate")
    try {
      web_webview.WebviewController.setHttpDns(web_webview.SecureDnsMode.AUTO, "https://example1.test")
    } catch (error) {
      let e: business_error.BusinessError = error as business_error.BusinessError;
      console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
    }

    AppStorage.setOrCreate("abilityWant", want);
    console.log("EntryAbility onCreate done")
  }
}
```

### setWebDebuggingAccess

static setWebDebuggingAccess(webDebuggingAccess: boolean): void

Sets whether to enable web debugging. For details, see [Debugging Frontend Pages by Using DevTools](../../web/web-debugging-with-devtools.md).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name             | Type   | Mandatory  |  Description|
| ------------------ | ------- | ---- | ------------- |
| webDebuggingAccess | boolean | Yes  | Whether to enable web debugging.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  aboutToAppear(): void {
    try {
      web_webview.WebviewController.setWebDebuggingAccess(true);
    } catch (error) {
      let e: business_error.BusinessError = error as business_error.BusinessError;
      console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
    }
  }

  build() {
    Column() {
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### loadUrl

loadUrl(url: string | Resource, headers?: Array\<WebHeader>): void

Loads a specified URL.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name | Type            | Mandatory| Description                 |
| ------- | ---------------- | ---- | :-------------------- |
| url     | string \| Resource | Yes  | URL to load.     |
| headers | Array\<[WebHeader](#webheader)> | No  | Additional HTTP request header of the URL.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100002 | Invalid url.                                                 |
| 17100003 | Invalid resource path or file type.                          |

**Example**

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
            // The URL to be loaded is of the string type.
            this.controller.loadUrl('www.example.com');
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

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
            // The headers parameter is passed.
            this.controller.loadUrl('www.example.com', [{ headerKey: "headerKey", headerValue: "headerValue" }]);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

There are three methods for loading local resource files:

1. Using $rawfile
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
            // Load a local resource file through $rawfile.
            this.controller.loadUrl($rawfile('index.html'));
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

2. Using the resources protocol
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
            // Load local resource files through the resource protocol.
            this.controller.loadUrl("resource://rawfile/index.html");
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

3. Using a sandbox path. For details, see the example of loading local resource files in the sandbox in [Web](ts-basic-components-web.md#web).

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <body>
    <p>Hello World</p>
  </body>
</html>
```

### loadData

loadData(data: string, mimeType: string, encoding: string, baseUrl?: string, historyUrl?: string): void

Loads specified data.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name    | Type  | Mandatory| Description                                                        |
| ---------- | ------ | ---- | ------------------------------------------------------------ |
| data       | string | Yes  | Character string obtained after being Base64 or URL encoded.                   |
| mimeType   | string | Yes  | Media type (MIME).                                          |
| encoding   | string | Yes  | Encoding type, which can be Base64 or URL.                      |
| baseUrl    | string | No  | URL (HTTP/HTTPS/data compliant), which is assigned by the **\<Web>** component to **window.origin**.|
| historyUrl | string | No  | URL used for historical records. If this parameter is not empty, historical records are managed based on this URL. This parameter is invalid when **baseUrl** is left empty.|

> **NOTE**
> 
> To load a local image, you can assign a space to either **baseUrl** or **historyUrl**. For details, see the sample code.
> In the scenario of loading a local image, **baseUrl** and **historyUrl** cannot be both empty. Otherwise, the image cannot be loaded.
> If the rich text in HTML contains special characters such as #, you are advised to assign a space to both **baseUrl** and **historyUrl**.

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

Example of loading local resource:
```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  updataContent: string = '<body><div><image src=resource://rawfile/xxx.png alt="image -- end" width="500" height="250"></image></div></body>'

  build() {
    Column() {
      Button('loadData')
        .onClick(() => {
          try {
            this.controller.loadData(this.updataContent, "text/html", "UTF-8", " ", " ");
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### accessForward

accessForward(): boolean

Checks whether going to the next page can be performed on the current page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type   | Description                             |
| ------- | --------------------------------- |
| boolean | Returns **true** if going to the next page can be performed on the current page; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('accessForward')
        .onClick(() => {
          try {
            let result = this.controller.accessForward();
            console.log('result:' + result);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### forward

forward(): void

Moves to the next page based on the history stack. This API is generally used together with **accessForward**.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('forward')
        .onClick(() => {
          try {
            this.controller.forward();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### accessBackward

accessBackward(): boolean

Checks whether going to the previous page can be performed on the current page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type   | Description                            |
| ------- | -------------------------------- |
| boolean | Returns **true** if moving to the previous page can be performed on the current page; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('accessBackward')
        .onClick(() => {
          try {
            let result = this.controller.accessBackward();
            console.log('result:' + result);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### backward

backward(): void

Moves to the previous page based on the history stack. This API is generally used together with **accessBackward**.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('backward')
        .onClick(() => {
          try {
            this.controller.backward();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### onActive

onActive(): void

Invoked to instruct the **\<Web>** component to enter the active foreground state.
<br>The application can interact with the user while in the active foreground state, and it remains in this state until the focus is moved away from it due to some event (for example, an incoming call is received or the device screen is turned off).

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('onActive')
        .onClick(() => {
          try {
            this.controller.onActive();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### onInactive

onInactive(): void

Invoked to instruct the **\<Web>** component to enter the inactive state. You can implement the behavior to perform after the application loses focus.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('onInactive')
        .onClick(() => {
          try {
            this.controller.onInactive();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### refresh
refresh(): void

Invoked to instruct the **\<Web>** component to refresh the web page.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('refresh')
        .onClick(() => {
          try {
            this.controller.refresh();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### accessStep

accessStep(step: number): boolean

Checks whether a specific number of steps forward or backward can be performed on the current page.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description                                  |
| ------ | -------- | ---- | ------------------------------------------ |
| step   | number   | Yes  | Number of the steps to take. A positive number means to move forward, and a negative number means to move backward.|

**Return value**

| Type   | Description              |
| ------- | ------------------ |
| boolean | Whether moving forward or backward is performed on the current page.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State steps: number = 2;

  build() {
    Column() {
      Button('accessStep')
        .onClick(() => {
          try {
            let result = this.controller.accessStep(this.steps);
            console.log('result:' + result);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### clearHistory

clearHistory(): void

Clears the browsing history.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('clearHistory')
        .onClick(() => {
          try {
            this.controller.clearHistory();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getHitTest

getHitTest(): WebHitTestType

Obtains the element type of the area being clicked.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type                                                        | Description                  |
| ------------------------------------------------------------ | ---------------------- |
| [WebHitTestType](#webhittesttype)| Element type of the area being clicked.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('getHitTest')
        .onClick(() => {
          try {
            let hitTestType = this.controller.getHitTest();
            console.log("hitTestType: " + hitTestType);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### registerJavaScriptProxy

registerJavaScriptProxy(object: object, name: string, methodList: Array\<string>): void

Registers a JavaScript object with the window. APIs of this object can then be invoked in the window. After this API is called, call [refresh](#refresh) for the registration to take effect.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name    | Type      | Mandatory| Description                                       |
| ---------- | -------------- | ---- | ------------------------------------------------------------ |
| object     | object         | Yes  | Application-side JavaScript object to be registered. Methods and attributes can be declared, but cannot be directly called on HTML5.<br>The parameter and return value can be any of the following types:<br>- String, number, or Boolean type<br>- Dictionary or Array type, with a maximum of 10 nested layers and 10,000 data records per layer.<br>Object, which must contain the **methodNameListForJsProxy:[fun1, fun2]** attribute, where **fun1** and **fun2** are methods that can be called.<br>The parameter can be a function or promise, but its callback cannot have return values.<br>The return value can be a promise, but its callback cannot have a return value.<br>For the example, see [Invoking Application Functions on the Frontend Page](../../web/web-in-page-app-function-invoking.md).|
| name       | string         | Yes  | Name of the object to be registered, which is the same as that invoked in the window. After registration, the window can use this name to access the JavaScript object at the application side.|
| methodList | Array\<string> | Yes  | Methods of the JavaScript object to be registered at the application side.                      |

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

class TestObj {
  constructor() {
  }

  test(testStr:string): string {
    console.log('Web Component str' + testStr);
    return testStr;
  }

  toString(): void {
    console.log('Web Component toString');
  }

  testNumber(testNum:number): number {
    console.log('Web Component number' + testNum);
    return testNum;
  }

  testBool(testBol:boolean): boolean {
    console.log('Web Component boolean' + testBol);
    return testBol;
  }
}

class WebObj {
  constructor() {
  }

  webTest(): string {
    console.log('Web test');
    return "Web test";
  }

  webString(): void {
    console.log('Web test toString');
  }
}

@Entry
@Component
struct Index {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State testObjtest: TestObj = new TestObj();
  @State webTestObj: WebObj = new WebObj();
  build() {
    Column() {
      Button('refresh')
        .onClick(() => {
          try {
            this.controller.refresh();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('Register JavaScript To Window')
        .onClick(() => {
          try {
            this.controller.registerJavaScriptProxy(this.testObjtest, "objName", ["test", "toString", "testNumber", "testBool"]);
            this.controller.registerJavaScriptProxy(this.webTestObj, "objTestName", ["webTest", "webString"]);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .javaScriptAccess(true)
    }
  }
}
```

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html>
    <meta charset="utf-8">
    <body>
      <button type="button" onclick="htmlTest()">Click Me!</button>
      <p id="demo"></p>
      <p id="webDemo"></p>
    </body>
    <script type="text/javascript">
    function htmlTest() {
      // This function call expects to return "ArkUI Web Component"
      let str=objName.test("webtest data");
      objName.testNumber(1);
      objName.testBool(true);
      document.getElementById("demo").innerHTML=str;
      console.log('objName.test result:'+ str)

      // This function call expects to return "Web test"
      let webStr = objTestName.webTest();
      document.getElementById("webDemo").innerHTML=webStr;
      console.log('objTestName.webTest result:'+ webStr)
    }
</script>
</html>
```
For more examples, see [Invoking Application Functions on the Frontend Page](../../web/web-in-page-app-function-invoking.md).

### runJavaScript

runJavaScript(script: string, callback : AsyncCallback\<string>): void

Executes a JavaScript script. This API uses an asynchronous callback to return the script execution result. **runJavaScript** can be invoked only after **loadUrl** is executed. For example, it can be invoked in **onPageEnd**.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                | Mandatory| Description                        |
| -------- | -------------------- | ---- | ---------------------------- |
| script   | string                   | Yes  | JavaScript script.                                            |
| callback | AsyncCallback\<string> | Yes  | Callback used to return the result. Returns **null** if the JavaScript script fails to be executed or no value is returned.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State webResult: string = ''

  build() {
    Column() {
      Text(this.webResult).fontSize(20)
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .javaScriptAccess(true)
        .onPageEnd(e => {
          try {
            this.controller.runJavaScript(
              'test()',
              (error, result) => {
                if (error) {
                  let e: business_error.BusinessError = error as business_error.BusinessError;
                  console.error(`run JavaScript error, ErrorCode: ${e.code},  Message: ${e.message}`);
                  return;
                }
                if (result) {
                  this.webResult = result
                  console.info(`The test() return value is: ${result}`)
                }
              });
            if (e) {
              console.info('url: ', e.url);
            }
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
    }
  }
}
```

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <meta charset="utf-8">
  <body>
      Hello world!
  </body>
  <script type="text/javascript">
  function test() {
      console.log('Ark WebComponent')
      return "This value is from index.html"
  }
  </script>
</html>
```

### runJavaScript

runJavaScript(script: string): Promise\<string>

Executes a JavaScript script. This API uses a promise to return the script execution result. **runJavaScript** can be invoked only after **loadUrl** is executed. For example, it can be invoked in **onPageEnd**.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description        |
| ------ | -------- | ---- | ---------------- |
| script | string   | Yes  | JavaScript script.|

**Return value**

| Type           | Description                                               |
| --------------- | --------------------------------------------------- |
| Promise\<string> | Promise used to return the result if the operation is successful and null otherwise.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .javaScriptAccess(true)
        .onPageEnd(e => {
          try {
            this.controller.runJavaScript('test()')
              .then((result) => {
                console.log('result: ' + result);
              })
              .catch((error: business_error.BusinessError) => {
                console.error("error: " + error);
              })
            if (e) {
              console.info('url: ', e.url);
            }
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
    }
  }
}
```

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <meta charset="utf-8">
  <body>
      Hello world!
  </body>
  <script type="text/javascript">
  function test() {
      console.log('Ark WebComponent')
      return "This value is from index.html"
  }
  </script>
</html>
```

### runJavaScriptExt<sup>10+</sup>

runJavaScriptExt(script: string, callback : AsyncCallback\<JsMessageExt>): void

Executes a JavaScript script. This API uses an asynchronous callback to return the script execution result. **runJavaScriptExt** can be invoked only after **loadUrl** is executed. For example, it can be invoked in **onPageEnd**.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                | Mandatory| Description                        |
| -------- | -------------------- | ---- | ---------------------------- |
| script   | string                   | Yes  | JavaScript script.                                            |
| callback | AsyncCallback\<[JsMessageExt](#jsmessageext10)\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State msg1: string = ''
  @State msg2: string = ''

  build() {
    Column() {
      Text(this.msg1).fontSize(20)
      Text(this.msg2).fontSize(20)
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .javaScriptAccess(true)
        .onPageEnd(e => {
          try {
            this.controller.runJavaScriptExt(
              'test()',
              (error, result) => {
                if (error) {
                  let e: business_error.BusinessError = error as business_error.BusinessError;
                  console.error(`run JavaScript error, ErrorCode: ${e.code},  Message: ${e.message}`)
                  return;
                }
                if (result) {
                  try {
                    let type = result.getType();
                    switch (type) {
                      case web_webview.JsMessageType.STRING: {
                        this.msg1 = "result type:" + typeof (result.getString());
                        this.msg2 = "result getString:" + ((result.getString()));
                        break;
                      }
                      case web_webview.JsMessageType.NUMBER: {
                        this.msg1 = "result type:" + typeof (result.getNumber());
                        this.msg2 = "result getNumber:" + ((result.getNumber()));
                        break;
                      }
                      case web_webview.JsMessageType.BOOLEAN: {
                        this.msg1 = "result type:" + typeof (result.getBoolean());
                        this.msg2 = "result getBoolean:" + ((result.getBoolean()));
                        break;
                      }
                      case web_webview.JsMessageType.ARRAY_BUFFER: {
                        this.msg1 = "result type:" + typeof (result.getArrayBuffer());
                        this.msg2 = "result getArrayBuffer byteLength:" + ((result.getArrayBuffer().byteLength));
                        break;
                      }
                      case web_webview.JsMessageType.ARRAY: {
                        this.msg1 = "result type:" + typeof (result.getArray());
                        this.msg2 = "result getArray:" + result.getArray();
                        break;
                      }
                      default: {
                        this.msg1 = "default break, type:" + type;
                        break;
                      }
                    }
                  }
                  catch (resError) {
                    let e: business_error.BusinessError = resError as business_error.BusinessError;
                    console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
                  }
                }
              });
            if (e) {
              console.info('url: ', e.url);
            }
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
    }
  }
}
```

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en-gb">
<body>
<h1>run JavaScript Ext demo</h1>
</body>
<script type="text/javascript">
function test() {
  return "hello, world";
}
</script>
</html>
```

### runJavaScriptExt<sup>10+</sup>

runJavaScriptExt(script: string): Promise\<JsMessageExt>

Executes a JavaScript script. This API uses a promise to return the script execution result. **runJavaScriptExt** can be invoked only after **loadUrl** is executed. For example, it can be invoked in **onPageEnd**.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description        |
| ------ | -------- | ---- | ---------------- |
| script | string   | Yes  | JavaScript script.|

**Return value**

| Type           | Description                                               |
| --------------- | --------------------------------------------------- |
| Promise\<[JsMessageExt](#jsmessageext10)> | Promise used to return the script execution result.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State webResult: string = '';
  @State msg1: string = ''
  @State msg2: string = ''

  build() {
    Column() {
      Text(this.webResult).fontSize(20)
      Text(this.msg1).fontSize(20)
      Text(this.msg2).fontSize(20)
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .javaScriptAccess(true)
        .onPageEnd(() => {
          this.controller.runJavaScriptExt('test()')
            .then((result) => {
              try {
                let type = result.getType();
                switch (type) {
                  case web_webview.JsMessageType.STRING: {
                    this.msg1 = "result type:" + typeof (result.getString());
                    this.msg2 = "result getString:" + ((result.getString()));
                    break;
                  }
                  case web_webview.JsMessageType.NUMBER: {
                    this.msg1 = "result type:" + typeof (result.getNumber());
                    this.msg2 = "result getNumber:" + ((result.getNumber()));
                    break;
                  }
                  case web_webview.JsMessageType.BOOLEAN: {
                    this.msg1 = "result type:" + typeof (result.getBoolean());
                    this.msg2 = "result getBoolean:" + ((result.getBoolean()));
                    break;
                  }
                  case web_webview.JsMessageType.ARRAY_BUFFER: {
                    this.msg1 = "result type:" + typeof (result.getArrayBuffer());
                    this.msg2 = "result getArrayBuffer byteLength:" + ((result.getArrayBuffer().byteLength));
                    break;
                  }
                  case web_webview.JsMessageType.ARRAY: {
                    this.msg1 = "result type:" + typeof (result.getArray());
                    this.msg2 = "result getArray:" + result.getArray();
                    break;
                  }
                  default: {
                    this.msg1 = "default break, type:" + type;
                    break;
                  }
                }
              }
              catch (resError) {
                let e: business_error.BusinessError = resError as business_error.BusinessError;
                console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
              }
            })
            .catch((error: business_error.BusinessError) => {
              console.error("error: " + error);
            })
        })
    }
  }
}
```

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en-gb">
<body>
<h1>run JavaScript Ext demo</h1>
</body>
<script type="text/javascript">
function test() {
  return "hello, world";
}
</script>
</html>
```

### deleteJavaScriptRegister

deleteJavaScriptRegister(name: string): void

Deletes a specific application JavaScript object that is registered with the window through **registerJavaScriptProxy**. After the deletion, the [refresh](#refresh) API must be called.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description |
| ------ | -------- | ---- | ---- |
| name   | string   | Yes  | Name of the registered JavaScript object, which can be used to invoke the corresponding object on the application side from the web side.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100008 | Cannot delete JavaScriptProxy.                               |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

class TestObj {
  constructor() {
  }

  test(): string {
    return "ArkUI Web Component";
  }

  toString(): void {
    console.log('Web Component toString');
  }
}

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State testObjtest: TestObj = new TestObj();
  @State name: string = 'objName';
  build() {
    Column() {
      Button('refresh')
        .onClick(() => {
          try {
            this.controller.refresh();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('Register JavaScript To Window')
        .onClick(() => {
          try {
            this.controller.registerJavaScriptProxy(this.testObjtest, this.name, ["test", "toString"]);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('deleteJavaScriptRegister')
        .onClick(() => {
          try {
            this.controller.deleteJavaScriptRegister(this.name);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .javaScriptAccess(true)
    }
  }
}
```

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html>
    <meta charset="utf-8">
    <body>
      <button type="button" onclick="htmlTest()">Click Me!</button>
      <p id="demo"></p>
    </body>
    <script type="text/javascript">
    function htmlTest() {
      let str=objName.test();
      document.getElementById("demo").innerHTML=str;
      console.log('objName.test result:'+ str)
    }
</script>
</html>
```

### zoom

zoom(factor: number): void

Zooms in or out of this web page. This API is effective only when [zoomAccess](ts-basic-components-web.md#zoomaccess) is **true**.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description|
| ------ | -------- | ---- | ------------------------------------------------------------ |
| factor | number   | Yes  | Relative zoom ratio. The value must be greater than 0. The value **1** indicates that the page is not zoomed. A value smaller than **1** indicates zoom-out, and a value greater than **1** indicates zoom-in.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100004 | Function not enable.                                         |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State factor: number = 1;

  build() {
    Column() {
      Button('zoom')
        .onClick(() => {
          try {
            this.controller.zoom(this.factor);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
        .zoomAccess(true)
    }
  }
}
```

### searchAllAsync

searchAllAsync(searchString: string): void

Searches the web page for content that matches the keyword specified by **'searchString'** and highlights the matches on the page. This API returns the result asynchronously through [onSearchResultReceive](ts-basic-components-web.md#onsearchresultreceive9).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name      | Type| Mandatory| Description      |
| ------------ | -------- | ---- | -------------- |
| searchString | string   | Yes  | Search keyword.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State searchString: string = "Hello World";

  build() {
    Column() {
      Button('searchString')
        .onClick(() => {
          try {
            this.controller.searchAllAsync(this.searchString);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .onSearchResultReceive(ret => {
          if (ret) {
            console.log("on search result receive:" + "[cur]" + ret.activeMatchOrdinal +
              "[total]" + ret.numberOfMatches + "[isDone]" + ret.isDoneCounting);
          }
        })
    }
  }
}
```

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <body>
    <p>Hello World Highlight Hello World</p>
  </body>
</html>
```

### clearMatches

clearMatches(): void

Clears the matches found through [searchAllAsync](#searchallasync).

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('clearMatches')
        .onClick(() => {
          try {
            this.controller.clearMatches();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
    }
  }
}
```

For details about the HTML file loaded, see the HMTL file loaded using [searchAllAsync](#searchallasync).

### searchNext

searchNext(forward: boolean): void

Searches for and highlights the next match.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name | Type| Mandatory| Description              |
| ------- | -------- | ---- | ---------------------- |
| forward | boolean  | Yes  | Whether to search forward.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('searchNext')
        .onClick(() => {
          try {
            this.controller.searchNext(true);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
    }
  }
}
```

For details about the HTML file loaded, see the HMTL file loaded using [searchAllAsync](#searchallasync).

### clearSslCache

clearSslCache(): void

Clears the user operation corresponding to the SSL certificate error event recorded by the **\<Web>** component.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('clearSslCache')
        .onClick(() => {
          try {
            this.controller.clearSslCache();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### clearClientAuthenticationCache

clearClientAuthenticationCache(): void

Clears the user operation corresponding to the client certificate request event recorded by the **\<Web>** component.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('clearClientAuthenticationCache')
        .onClick(() => {
          try {
            this.controller.clearClientAuthenticationCache();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### createWebMessagePorts

createWebMessagePorts(isExtentionType?: boolean): Array\<WebMessagePort>

Creates web message ports. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type                  | Mandatory| Description                            |
| ------ | ---------------------- | ---- | :------------------------------|
| isExtentionType<sup>10+</sup>   | boolean     | No | Whether to use the extended interface. The default value is **false**, indicating that the extended interface is not used. This parameter is supported since API version 10.|

**Return value**

| Type                  | Description             |
| ---------------------- | ----------------- |
| Array\<[WebMessagePort](#webmessageport)> | List of web message ports.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

  ```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  ports: web_webview.WebMessagePort[] = [];

  build() {
    Column() {
      Button('createWebMessagePorts')
        .onClick(() => {
          try {
            this.ports = this.controller.createWebMessagePorts();
            console.log("createWebMessagePorts size:" + this.ports.length)
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
  ```

### postMessage

postMessage(name: string, ports: Array\<WebMessagePort>, uri: string): void

Sends a web message to an HTML window.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type                  | Mandatory| Description                            |
| ------ | ---------------------- | ---- | :------------------------------- |
| name   | string                 | Yes  | Name of the message to send.           |
| ports  | Array\<WebMessagePort> | Yes  | Message ports for sending the message.           |
| uri    | string                 | Yes  | URI for receiving the message.               |

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  ports: web_webview.WebMessagePort[] = [];
  @State sendFromEts: string = 'Send this message from ets to HTML';
  @State receivedFromHtml: string = 'Display received message send from HTML';

  build() {
    Column() {
      // Display the received HTML content.
      Text(this.receivedFromHtml)
      // Send the content in the text box to an HTML window.
      TextInput({ placeholder: 'Send this message from ets to HTML' })
        .onChange((value: string) => {
          this.sendFromEts = value;
        })

      Button('postMessage')
        .onClick(() => {
          try {
            // 1. Create two message ports.
            this.ports = this.controller.createWebMessagePorts();
            // 2. Register a callback on a message port (for example, port 1) on the application side.
            this.ports[1].onMessageEvent((result: web_webview.WebMessage) => {
              let msg = 'Got msg from HTML:';
              if (typeof(result) == "string") {
                console.log("received string message from html5, string is:" + result);
                msg = msg + result;
              } else if (typeof(result) == "object") {
                if (result instanceof ArrayBuffer) {
                  console.log("received arraybuffer from html5, length is:" + result.byteLength);
                  msg = msg + "length is " + result.byteLength;
                } else {
                  console.log("not support");
                }
              } else {
                console.log("not support");
              }
              this.receivedFromHtml = msg;
            })
            // 3. Send another message port (for example, port 0) to the HTML side, which can then save the port for future use.
            this.controller.postMessage('__init_port__', [this.ports[0]], '*');
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })

      // 4. Use the port on the application side to send messages to the port that has been sent to the HTML side.
      Button('SendDataToHTML')
        .onClick(() => {
          try {
            if (this.ports && this.ports[1]) {
              this.ports[1].postMessageEvent(this.sendFromEts);
            } else {
              console.error(`ports is null, Please initialize first`);
            }
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
    }
  }
}
```

HTML file to be loaded:
```html
<!--index.html-->
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WebView Message Port Demo</title>
</head>

  <body>
    <h1>WebView Message Port Demo</h1>
    <div>
        <input type="button" value="SendToEts" onclick="PostMsgToEts(msgFromJS.value);"/><br/>
        <input id="msgFromJS" type="text" value="send this message from HTML to ets"/><br/>
    </div>
    <p class="output">display received message send from ets</p>
  </body>
  <script src="xxx.js"></script>
</html>
```

```js
//xxx.js
var h5Port;
var output = document.querySelector('.output');
window.addEventListener('message', function (event) {
    if (event.data == '__init_port__') {
        if (event.ports[0] != null) {
            h5Port = event.ports[0]; // 1. Save the port number sent from the eTS side.
            h5Port.onmessage = function (event) {
              // 2. Receive the message sent from the eTS side.
              var msg = 'Got message from ets:';
              var result = event.data;
              if (typeof(result) == "string") {
                console.log("received string message from html5, string is:" + result);
                msg = msg + result;
              } else if (typeof(result) == "object") {
                if (result instanceof ArrayBuffer) {
                  console.log("received arraybuffer from html5, length is:" + result.byteLength);
                  msg = msg + "length is " + result.byteLength;
                } else {
                  console.log("not support");
                }
              } else {
                console.log("not support");
              }
              output.innerHTML = msg;
            }
        }
    }
})

// 3. Use h5Port to send messages to the eTS side.
function PostMsgToEts(data) {
    if (h5Port) {
      h5Port.postMessage(data);
    } else {
      console.error("h5Port is null, Please initialize first");
    }
}
```

### requestFocus

requestFocus(): void

Requests focus for this web page.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('requestFocus')
        .onClick(() => {
          try {
            this.controller.requestFocus();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        });
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### zoomIn

zoomIn(): void

Zooms in on this web page by 20%.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100004 | Function not enable.                                         |

**Example**

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
      Button('zoomIn')
        .onClick(() => {
          try {
            this.controller.zoomIn();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### zoomOut

zoomOut(): void

Zooms out of this web page by 20%.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100004 | Function not enable.                                         |

**Example**

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
      Button('zoomOut')
        .onClick(() => {
          try {
            this.controller.zoomOut();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getHitTestValue

getHitTestValue(): HitTestValue

Obtains the element information of the area being clicked.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type        | Description                |
| ------------ | -------------------- |
| [HitTestValue](#hittestvalue) | Element information of the area being clicked.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('getHitTestValue')
        .onClick(() => {
          try {
            let hitValue = this.controller.getHitTestValue();
            console.log("hitType: " + hitValue.type);
            console.log("extra: " + hitValue.extra);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getWebId

getWebId(): number

Obtains the index value of this **\<Web>** component, which can be used for **\<Web>** component management.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                 |
| ------ | --------------------- |
| number | Index value of the current **\<Web>** component.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('getWebId')
        .onClick(() => {
          try {
            let id = this.controller.getWebId();
            console.log("id: " + id);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getUserAgent

getUserAgent(): string

Obtains the default user agent of this web page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description          |
| ------ | -------------- |
| string | Default user agent.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('getUserAgent')
        .onClick(() => {
          try {
            let userAgent = this.controller.getUserAgent();
            console.log("userAgent: " + userAgent);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

You can define a custom user agent based on the default user agent.
```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State ua: string = ""

  aboutToAppear():void {
    web_webview.once('webInited', () => {
      try {
        // Define a custom user agent on the application side.
        this.ua = this.controller.getUserAgent() + 'xxx';
      } catch(error) {
        let e:business_error.BusinessError = error as business_error.BusinessError;
        console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
      }
    })
  }

  build() {
    Column() {
      Web({ src: 'www.example.com', controller: this.controller })
        .userAgent(this.ua)
    }
  }
}
```

### getTitle

getTitle(): string

Obtains the title of the current web page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                |
| ------ | -------------------- |
| string | Title of the current web page.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('getTitle')
        .onClick(() => {
          try {
            let title = this.controller.getTitle();
            console.log("title: " + title);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getPageHeight

getPageHeight(): number

Obtains the height of this web page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                |
| ------ | -------------------- |
| number | Height of the current web page, in px.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('getPageHeight')
        .onClick(() => {
          try {
            let pageHeight = this.controller.getPageHeight();
            console.log("pageHeight : " + pageHeight);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### storeWebArchive

storeWebArchive(baseName: string, autoName: boolean, callback: AsyncCallback\<string>): void

Stores this web page. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type             | Mandatory| Description                                                        |
| -------- | --------------------- | ---- | ------------------------------------------------------------ |
| baseName | string                | Yes  | Save path of the web page. The value cannot be null.                                |
| autoName | boolean               | Yes  | Whether to automatically generate a file name. The value **false** means not to automatically generate a file name. The value **true** means to automatically generate a file name based on the URL of the current page and the **baseName** value.|
| callback | AsyncCallback\<string> | Yes  | Callback used to return the save path if the operation is successful and null otherwise.                  |

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100003 | Invalid resource path or file type.                          |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('storeWebArchive')
        .onClick(() => {
          try {
            this.controller.storeWebArchive("/data/storage/el2/base/", true, (error, filename) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`save web archive error, ErrorCode: ${e.code},  Message: ${e.message}`);
                return;
              }
              if (filename != null) {
                console.info(`save web archive success: ${filename}`)
              }
            });
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### storeWebArchive

storeWebArchive(baseName: string, autoName: boolean): Promise\<string>

Stores this web page. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type| Mandatory| Description                                                        |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| baseName | string   | Yes  | Save path of the web page. The value cannot be null.                                |
| autoName | boolean  | Yes  | Whether to automatically generate a file name. The value **false** means not to automatically generate a file name. The value **true** means to automatically generate a file name based on the URL of the current page and the **baseName** value.|

**Return value**

| Type           | Description                                                 |
| --------------- | ----------------------------------------------------- |
| Promise\<string> | Promise used to return the save path if the operation is successful and null otherwise.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100003 | Invalid resource path or file type.                          |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('storeWebArchive')
        .onClick(() => {
          try {
            this.controller.storeWebArchive("/data/storage/el2/base/", true)
              .then(filename => {
                if (filename != null) {
                  console.info(`save web archive success: ${filename}`)
                }
              })
              .catch((error:business_error.BusinessError) => {
                console.error(`ErrorCode: ${error.code},  Message: ${error.message}`);
              })
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getUrl

getUrl(): string

Obtains the URL of this page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description               |
| ------ | ------------------- |
| string | URL of the current page.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('getUrl')
        .onClick(() => {
          try {
            let url = this.controller.getUrl();
            console.log("url: " + url);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### stop

stop(): void

Stops page loading.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('stop')
        .onClick(() => {
          try {
            this.controller.stop();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        });
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### backOrForward

backOrForward(step: number): void

Performs a specific number of steps forward or backward on the current page based on the history stack. No redirection will be performed if the corresponding page does not exist in the history stack.

Because the previously loaded web pages are used for the operation, no page reloading is involved.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description              |
| ------ | -------- | ---- | ---------------------- |
| step   | number   | Yes  | Number of the steps to take.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State step: number = -2;

  build() {
    Column() {
      Button('backOrForward')
        .onClick(() => {
          try {
            this.controller.backOrForward(this.step);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### scrollTo

scrollTo(x:number, y:number): void

Scrolls the page to the specified absolute position.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description              |
| ------ | -------- | ---- | ---------------------- |
| x   | number   | Yes  | X coordinate of the absolute position. If the value is a negative number, the value 0 is used.|
| y   | number   | Yes  | Y coordinate of the absolute position. If the value is a negative number, the value 0 is used.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('scrollTo')
        .onClick(() => {
          try {
            this.controller.scrollTo(50, 50);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
    }
  }
}
```

HTML file to be loaded:
```html
<!--index.html-->
<!DOCTYPE html>
<html>
<head>
    <title>Demo</title>
    <style>
        body {
            width:3000px;
            height:3000px;
            padding-right:170px;
            padding-left:170px;
            border:5px solid blueviolet
        }
    </style>
</head>
<body>
Scroll Test
</body>
</html>
```

### scrollBy

scrollBy(deltaX:number, deltaY:number): void

Scrolls the page by the specified amount.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description              |
| ------ | -------- | ---- | ---------------------- |
| deltaX | number   | Yes  | Amount to scroll by along the x-axis. The positive direction is rightward.|
| deltaY | number   | Yes  | Amount to scroll by along the y-axis. The positive direction is downward.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('scrollBy')
        .onClick(() => {
          try {
            this.controller.scrollBy(50, 50);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
    }
  }
}
```

HTML file to be loaded:
```html
<!--index.html-->
<!DOCTYPE html>
<html>
<head>
    <title>Demo</title>
    <style>
        body {
            width:3000px;
            height:3000px;
            padding-right:170px;
            padding-left:170px;
            border:5px solid blueviolet
        }
    </style>
</head>
<body>
Scroll Test
</body>
</html>
```

### slideScroll

slideScroll(vx:number, vy:number): void

Simulates a slide-to-scroll action on the page at the specified velocity.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description              |
| ------ | -------- | ---- | ---------------------- |
| vx     | number   | Yes  | Horizontal velocity component of the slide-to-scroll action, where the positive direction is rightward.|
| vy     | number   | Yes  | Vertical velocity component of the slide-to-scroll action, where the positive direction is downward.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('slideScroll')
        .onClick(() => {
          try {
            this.controller.slideScroll(500, 500);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`); 
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
    }
  }
}
```

HTML file to be loaded:
```html
<!--index.html-->
<!DOCTYPE html>
<html>
<head>
    <title>Demo</title>
    <style>
        body {
            width:3000px;
            height:3000px;
            padding-right:170px;
            padding-left:170px;
            border:5px solid blueviolet
        }
    </style>
</head>
<body>
Scroll Test
</body>
</html>
```

### getOriginalUrl

getOriginalUrl(): string

Obtains the original URL of this page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                   |
| ------ | ----------------------- |
| string | Original URL of the current page.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('getOrgUrl')
        .onClick(() => {
          try {
            let url = this.controller.getOriginalUrl();
            console.log("original url: " + url);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getFavicon

getFavicon(): image.PixelMap

Obtains the favicon of this page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type                                  | Description                           |
| -------------------------------------- | ------------------------------- |
| [PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7) | **PixelMap** object of the favicon of the page.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import image from "@ohos.multimedia.image";
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State pixelmap: image.PixelMap | undefined = undefined;

  build() {
    Column() {
      Button('getFavicon')
        .onClick(() => {
          try {
            this.pixelmap = this.controller.getFavicon();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### setNetworkAvailable

setNetworkAvailable(enable: boolean): void

Sets the **window.navigator.onLine** attribute in JavaScript.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type   | Mandatory| Description                             |
| ------ | ------- | ---- | --------------------------------- |
| enable | boolean | Yes  | Whether to enable **window.navigator.onLine**.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('setNetworkAvailable')
        .onClick(() => {
          try {
            this.controller.setNetworkAvailable(true);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
    }
  }
}
```

HTML file to be loaded:
```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<body>
<h1>online attribute </h1>
<p id="demo"></p>
<button onclick="func()">click</button>
<script>
    let online = navigator.onLine;
    document.getElementById ("demo").innerHTML = "Browser online:" + online;

    function func(){
      var online = navigator.onLine;
      document.getElementById ("demo").innerHTML = "Browser online:" + online;
    }
</script>
</body>
</html>
```

### hasImage

hasImage(callback: AsyncCallback\<boolean>): void

Checks whether this page contains images. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                   | Mandatory| Description                      |
| -------- | ----------------------- | ---- | -------------------------- |
| callback | AsyncCallback\<boolean> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('hasImageCb')
        .onClick(() => {
          try {
            this.controller.hasImage((error, data) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`hasImage error, ErrorCode: ${e.code},  Message: ${e.message}`);
                return;
              }
              console.info("hasImage: " + data);
            });
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### hasImage

hasImage(): Promise\<boolean>

Checks whether this page contains images. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type             | Description                                   |
| ----------------- | --------------------------------------- |
| Promise\<boolean> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('hasImagePm')
        .onClick(() => {
          try {
            this.controller.hasImage().then((data) => {
              console.info('hasImage: ' + data);
            })
            .catch((error:business_error.BusinessError) => {
              console.error("error: " + error);
            })
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### removeCache

removeCache(clearRom: boolean): void

Clears the cache in the application. This API will clear the cache for all webviews in the same application.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type   | Mandatory| Description                                                    |
| -------- | ------- | ---- | -------------------------------------------------------- |
| clearRom | boolean | Yes  | Whether to clear the cache in the ROM and RAM at the same time. The value **true** means to clear the cache in the ROM and RAM at the same time, and **false** means to only clear the cache in the RAM.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('removeCache')
        .onClick(() => {
          try {
            this.controller.removeCache(false);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### pageUp

pageUp(top: boolean): void

Scrolls the page up by half the viewport or jumps to the top of the page.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type   | Mandatory| Description                                                        |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| top    | boolean | Yes  | Whether to jump to the top of the page. The value **true** means to jump to the top of the page; and **false** means to scroll the page up by half the viewport.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('pageUp')
        .onClick(() => {
          try {
            this.controller.pageUp(false);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### pageDown

pageDown(bottom: boolean): void

Scrolls the page down by half the viewport or jumps to the bottom of the page.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type   | Mandatory| Description                                                        |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| bottom | boolean | Yes  | Whether to jump to the bottom of the page. The value **true** means to jump to the bottom of the page; and **false** means to scroll the page down by half the viewport.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('pageDown')
        .onClick(() => {
          try {
            this.controller.pageDown(false);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getBackForwardEntries

getBackForwardEntries(): BackForwardList

Obtains the historical information list of the current webview.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type                               | Description                       |
| ----------------------------------- | --------------------------- |
| [BackForwardList](#backforwardlist) | Historical information list of the current webview.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

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
      Button('getBackForwardEntries')
        .onClick(() => {
          try {
            let list = this.controller.getBackForwardEntries()
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### serializeWebState

serializeWebState(): Uint8Array

Serializes the page status history of the current Webview.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type      | Description                                         |
| ---------- | --------------------------------------------- |
| Uint8Array | Serialized data of the page status history of the current WebView.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

1. To perform operations on files, you must first import the **fs** module. For details, see [File Management](../apis-core-file-kit/js-apis-file-fs.md).
```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import fs from '@ohos.file.fs';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('serializeWebState')
        .onClick(() => {
          try {
            let state = this.controller.serializeWebState();
            let path:string | undefined = AppStorage.get("cacheDir");
            if (path) {
              path += '/WebState';
              // Synchronously open a file.
              let file = fs.openSync(path, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
              fs.writeSync(file.fd, state.buffer);
              fs.closeSync(file.fd);
            }
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

2. Modify the **EntryAbility.ets** file.
Obtain the path of the application cache file.
```ts
// xxx.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import Want from '@ohos.app.ability.Want';

export default class EntryAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        // Data synchronization between the UIAbility component and the page can be implemented by binding cacheDir to the AppStorage object.
        AppStorage.setOrCreate("cacheDir", this.context.cacheDir);
    }
}
```

### restoreWebState

restoreWebState(state: Uint8Array): void

Restores the page status history from the serialized data of the current WebView.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type      | Mandatory| Description                        |
| ------ | ---------- | ---- | ---------------------------- |
| state  | Uint8Array | Yes  | Serialized data of the page status history.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

1. To perform operations on files, you must first import the **fs** module. For details, see [File Management](../apis-core-file-kit/js-apis-file-fs.md).
```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import fs from '@ohos.file.fs';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('RestoreWebState')
        .onClick(() => {
          try {
            let path:string | undefined = AppStorage.get("cacheDir");
            if (path) {
              path += '/WebState';
              // Synchronously open a file.
              let file = fs.openSync(path, fs.OpenMode.READ_WRITE);
              let stat = fs.statSync(path);
              let size = stat.size;
              let buf = new ArrayBuffer(size);
              fs.read(file.fd, buf, (err, readLen) => {
                if (err) {
                  console.info("mkdir failed with error message: " + err.message + ", error code: " + err.code);
                } else {
                  console.info("read file data succeed");
                  this.controller.restoreWebState(new Uint8Array(buf.slice(0, readLen)));
                  fs.closeSync(file);
                }
              });
            }
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

2. Modify the **EntryAbility.ets** file.
Obtain the path of the application cache file.
```ts
// xxx.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import Want from '@ohos.app.ability.Want';

export default class EntryAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        // Data synchronization between the UIAbility component and the page can be implemented by binding cacheDir to the AppStorage object.
        AppStorage.setOrCreate("cacheDir", this.context.cacheDir);
    }
}
```

### customizeSchemes

static customizeSchemes(schemes: Array\<WebCustomScheme\>): void

Grants the cross-origin request and fetch request permissions for the specified URL schemes (also known as protocols) to the web kernel. A cross-origin fetch request for any of the specified URL schemes can be intercepted by the **onInterceptRequest** API, so that you can further process the request. It is recommended that this API be called before any **\<Web>** component is initialized.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type   | Mandatory| Description                     |
| -------- | ------- | ---- | -------------------------------------- |
| schemes | Array\<[WebCustomScheme](#webcustomscheme)\> | Yes  | Array of up to 10 custom schemes.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  responseweb: WebResourceResponse = new WebResourceResponse()
  scheme1: web_webview.WebCustomScheme = {schemeName: "name1", isSupportCORS: true, isSupportFetch: true}
  scheme2: web_webview.WebCustomScheme = {schemeName: "name2", isSupportCORS: true, isSupportFetch: true}
  scheme3: web_webview.WebCustomScheme = {schemeName: "name3", isSupportCORS: true, isSupportFetch: true}

  aboutToAppear():void {
    try {
      web_webview.WebviewController.customizeSchemes([this.scheme1, this.scheme2, this.scheme3])
    } catch(error) {
      let e:business_error.BusinessError = error as business_error.BusinessError;
      console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
    }
  }

  build() {
    Column() {
      Web({ src: 'www.example.com', controller: this.controller })
        .onInterceptRequest((event) => {
          if (event) {
            console.log('url:' + event.request.getRequestUrl())
          }
          return this.responseweb
        })
    }
  }
}
```

### getCertificate<sup>10+</sup>

getCertificate(): Promise<Array<cert.X509Cert>>

Obtains the certificate information of this website. When the **\<Web>** component is used to load an HTTPS website, SSL certificate verification is performed. This API uses a promise to return the [X.509 certificate](../apis-device-certificate-kit/js-apis-cert.md#x509cert) of the current website.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type      | Description                                         |
| ---------- | --------------------------------------------- |
| Promise<Array<cert.X509Cert>> | Promise used to obtain the X.509 certificate array of the current HTTPS website.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';
import cert from '@ohos.security.cert';

function Uint8ArrayToString(dataArray:Uint8Array) {
  let dataString = ''
  for (let i = 0; i < dataArray.length; i++) {
    dataString += String.fromCharCode(dataArray[i])
  }
  return dataString
}

function ParseX509CertInfo(x509CertArray:Array<cert.X509Cert>) {
  let res: string = 'getCertificate success: len = ' + x509CertArray.length;
  for (let i = 0; i < x509CertArray.length; i++) {
    res += ', index = ' + i + ', issuer name = '
    + Uint8ArrayToString(x509CertArray[i].getIssuerName().data) + ', subject name = '
    + Uint8ArrayToString(x509CertArray[i].getSubjectName().data) + ', valid start = '
    + x509CertArray[i].getNotBeforeTime()
    + ', valid end = ' + x509CertArray[i].getNotAfterTime()
  }
  return res
}

@Entry
@Component
struct Index {
  // outputStr displays debug information on the UI.
  @State outputStr: string = ''
  webviewCtl: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Row() {
      Column() {
        List({space: 20, initialIndex: 0}) {
          ListItem() {
            Button() {
              Text('load bad ssl')
                .fontSize(10)
                .fontWeight(FontWeight.Bold)
            }
            .type(ButtonType.Capsule)
            .onClick(() => {
              // Load an expired certificate website and view the obtained certificate information.
              this.webviewCtl.loadUrl('https://expired.badssl.com')
            })
            .height(50)
          }

          ListItem() {
            Button() {
              Text('load example')
                .fontSize(10)
                .fontWeight(FontWeight.Bold)
            }
            .type(ButtonType.Capsule)
            .onClick(() => {
              // Load an HTTPS website and view the certificate information of the website.
              this.webviewCtl.loadUrl('https://www.example.com')
            })
            .height(50)
          }

          ListItem() {
            Button() {
              Text('getCertificate Promise')
                .fontSize(10)
                .fontWeight(FontWeight.Bold)
            }
            .type(ButtonType.Capsule)
            .onClick(() => {
              try {
                this.webviewCtl.getCertificate().then((x509CertArray:Array<cert.X509Cert>) => {
                  this.outputStr = ParseX509CertInfo(x509CertArray);
                })
              } catch (error) {
                let e:business_error.BusinessError = error as business_error.BusinessError;
                this.outputStr = 'getCertificate failed: ' + e.code + ", errMsg: " + e.message;
              }
            })
            .height(50)
          }

          ListItem() {
            Button() {
              Text('getCertificate AsyncCallback')
                .fontSize(10)
                .fontWeight(FontWeight.Bold)
            }
            .type(ButtonType.Capsule)
            .onClick(() => {
              try {
                this.webviewCtl.getCertificate((error:business_error.BusinessError, x509CertArray:Array<cert.X509Cert>) => {
                  if (error) {
                    this.outputStr = 'getCertificate failed: ' + error.code + ", errMsg: " + error.message;
                  } else {
                    this.outputStr = ParseX509CertInfo(x509CertArray);
                  }
                })
              } catch (error) {
                let e:business_error.BusinessError = error as business_error.BusinessError;
                this.outputStr = 'getCertificate failed: ' + e.code + ", errMsg: " + e.message;
              }
            })
            .height(50)
          }
        }
        .listDirection(Axis.Horizontal)
        .height('10%')

        Text(this.outputStr)
          .width('100%')
          .fontSize(10)

        Web({ src: 'https://www.example.com', controller: this.webviewCtl })
          .fileAccess(true)
          .javaScriptAccess(true)
          .domStorageAccess(true)
          .onlineImageAccess(true)
          .onPageEnd((e) => {
            if(e) {
              this.outputStr = 'onPageEnd : url = ' + e.url
            }
          })
          .onSslErrorEventReceive((e) => {
            // Ignore SSL certificate errors to test websites whose certificates have expired, for example, https://expired.badssl.com.
            e.handler.handleConfirm()
          })
          .width('100%')
          .height('70%')
      }
      .height('100%')
    }
  }
}
```

### getCertificate<sup>10+</sup>

getCertificate(callback: AsyncCallback<Array<cert.X509Cert>>): void

Obtains the certificate information of this website. When the **\<Web>** component is used to load an HTTPS website, SSL certificate verification is performed. This API uses an asynchronous callback to return the [X.509 certificate](../apis-device-certificate-kit/js-apis-cert.md#x509cert) of the current website.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                        | Mandatory| Description                                    |
| -------- | ---------------------------- | ---- | ---------------------------------------- |
| callback | AsyncCallback<Array<cert.X509Cert>> | Yes  | Callback used to obtain the X.509 certificate array of the current website.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';
import cert from '@ohos.security.cert';

function Uint8ArrayToString(dataArray:Uint8Array) {
  let dataString = ''
  for (let i = 0; i < dataArray.length; i++) {
    dataString += String.fromCharCode(dataArray[i])
  }
  return dataString
}

function ParseX509CertInfo(x509CertArray:Array<cert.X509Cert>) {
  let res: string = 'getCertificate success: len = ' + x509CertArray.length;
  for (let i = 0; i < x509CertArray.length; i++) {
    res += ', index = ' + i + ', issuer name = '
    + Uint8ArrayToString(x509CertArray[i].getIssuerName().data) + ', subject name = '
    + Uint8ArrayToString(x509CertArray[i].getSubjectName().data) + ', valid start = '
    + x509CertArray[i].getNotBeforeTime()
    + ', valid end = ' + x509CertArray[i].getNotAfterTime()
  }
  return res
}

@Entry
@Component
struct Index {
  // outputStr displays debug information on the UI.
  @State outputStr: string = ''
  webviewCtl: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Row() {
      Column() {
        List({space: 20, initialIndex: 0}) {
          ListItem() {
            Button() {
              Text('load bad ssl')
                .fontSize(10)
                .fontWeight(FontWeight.Bold)
            }
            .type(ButtonType.Capsule)
            .onClick(() => {
              // Load an expired certificate website and view the obtained certificate information.
              this.webviewCtl.loadUrl('https://expired.badssl.com')
            })
            .height(50)
          }

          ListItem() {
            Button() {
              Text('load example')
                .fontSize(10)
                .fontWeight(FontWeight.Bold)
            }
            .type(ButtonType.Capsule)
            .onClick(() => {
              // Load an HTTPS website and view the certificate information of the website.
              this.webviewCtl.loadUrl('https://www.example.com')
            })
            .height(50)
          }

          ListItem() {
            Button() {
              Text('getCertificate Promise')
                .fontSize(10)
                .fontWeight(FontWeight.Bold)
            }
            .type(ButtonType.Capsule)
            .onClick(() => {
              try {
                this.webviewCtl.getCertificate().then((x509CertArray:Array<cert.X509Cert>) => {
                  this.outputStr = ParseX509CertInfo(x509CertArray);
                })
              } catch (error) {
                let e:business_error.BusinessError = error as business_error.BusinessError;
                this.outputStr = 'getCertificate failed: ' + e.code + ", errMsg: " + e.message;
              }
            })
            .height(50)
          }

          ListItem() {
            Button() {
              Text('getCertificate AsyncCallback')
                .fontSize(10)
                .fontWeight(FontWeight.Bold)
            }
            .type(ButtonType.Capsule)
            .onClick(() => {
              try {
                this.webviewCtl.getCertificate((error:business_error.BusinessError, x509CertArray:Array<cert.X509Cert>) => {
                  if (error) {
                    this.outputStr = 'getCertificate failed: ' + error.code + ", errMsg: " + error.message;
                  } else {
                    this.outputStr = ParseX509CertInfo(x509CertArray);
                  }
                })
              } catch (error) {
                let e:business_error.BusinessError = error as business_error.BusinessError;
                this.outputStr = 'getCertificate failed: ' + e.code + ", errMsg: " + e.message;
              }
            })
            .height(50)
          }
        }
        .listDirection(Axis.Horizontal)
        .height('10%')

        Text(this.outputStr)
          .width('100%')
          .fontSize(10)

        Web({ src: 'https://www.example.com', controller: this.webviewCtl })
          .fileAccess(true)
          .javaScriptAccess(true)
          .domStorageAccess(true)
          .onlineImageAccess(true)
          .onPageEnd((e) => {
            if (e) {
              this.outputStr = 'onPageEnd : url = ' + e.url
            }
          })
          .onSslErrorEventReceive((e) => {
            // Ignore SSL certificate errors to test websites whose certificates have expired, for example, https://expired.badssl.com.
            e.handler.handleConfirm()
          })
          .width('100%')
          .height('70%')
      }
      .height('100%')
    }
  }
}
```

### setAudioMuted<sup>10+</sup>

setAudioMuted(mute: boolean): void

Mutes this web page.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type   | Mandatory| Description                     |
| -------- | ------- | ---- | -------------------------------------- |
| mute | boolean | Yes  | Whether to mute the web page. The value **true** means to mute the web page, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController()
  @State muted: boolean = false
  build() {
    Column() {
      Button("Toggle Mute")
        .onClick(event => {
          this.muted = !this.muted
          this.controller.setAudioMuted(this.muted)
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### prefetchPage<sup>10+</sup>

prefetchPage(url: string, additionalHeaders?: Array\<WebHeader>): void

Prefetches resources in the background for a page that is likely to be accessed in the near future, without executing the page JavaScript code or presenting the page. This can significantly reduce the load time for the prefetched page.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name            | Type                            | Mandatory | Description                     |
| ------------------| --------------------------------| ---- | ------------- |
| url               | string                          | Yes   | URL to be preloaded.|
| additionalHeaders | Array\<[WebHeader](#webheader)> | No   | Additional HTTP headers of the URL.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID | Error Message                                                     |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100002 | Invalid url.                                                 |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('prefetchPopularPage')
        .onClick(() => {
          try {
            // Replace 'https://www.example.com' with a real URL for the API to work.
            this.controller.prefetchPage('https://www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      // Replace ''www.example1.com' with a real URL for the API to work.
      Web({ src: 'www.example1.com', controller: this.controller })
    }
  }
}
```

### prepareForPageLoad<sup>10+</sup>

static prepareForPageLoad(url: string, preconnectable: boolean, numSockets: number): void

Preconnects to a URL. This API can be called before the URL is loaded, to resolve the DNS and establish a socket connection, without obtaining the resources.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name         | Type   |  Mandatory | Description                                           |
| ---------------| ------- | ---- | ------------- |
| url            | string  | Yes  | URL to be preconnected.|
| preconnectable | boolean | Yes  | Whether to perform preconnection, which involves DNS resolution and socket connection establishment. The value **true** means to perform preconnection, and **false** means the opposite.|
| numSockets     | number  | Yes  | Number of sockets to be preconnected. The value must be greater than 0. A maximum of six socket connections are allowed.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID | Error Message                                                     |
| -------- | ------------------------------------------------------------ |
| 17100002 | Invalid url.                                                 |
| 171000013| The number of preconnect sockets is invalid.                                                 |

**Example**

```ts
// xxx.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import web_webview from '@ohos.web.webview';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import Want from '@ohos.app.ability.Want';

export default class EntryAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        console.log("EntryAbility onCreate");
        web_webview.WebviewController.initializeWebEngine();
        // Replace 'https://www.example.com' with a real URL for the API to work.
        web_webview.WebviewController.prepareForPageLoad("https://www.example.com", true, 2);
        AppStorage.setOrCreate("abilityWant", want);
        console.log("EntryAbility onCreate done");
    }
}
```

### setCustomUserAgent<sup>10+</sup>

setCustomUserAgent(userAgent: string): void

Sets a custom user agent, which will overwrite the default user agent. You are advised to set the user agent in the **onControllerAttached** callback event instead of **onLoadIntercept**.

> **NOTE**
>
> The user agent set through **setCustomUserAgent** takes effect only after web redirection. As a result, while the user has been redirected, the page stack associated with the new agent has only one page, and **webviewController.accessBackward()** always returns **false**.
> In light of this, to the **setCustomUserAgent** API, append **this.controller.loadUrl(this.webUrl)**, where **webUrl** indicates the web page to be loaded. You can set **src** of the original **\<Web>** component to an empty string.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name         | Type   |  Mandatory | Description                                           |
| ---------------| ------- | ---- | ------------- |
| userAgent      | string  | Yes  | Information about the custom user agent. It is recommended that you obtain the current default user agent through [getUserAgent](#getuseragent) and then customize the obtained user agent.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID | Error Message                                                     |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State customUserAgent: string = 'test'

  build() {
    Column() {
      Button('setCustomUserAgent')
        .onClick(() => {
          try {
            let userAgent = this.controller.getUserAgent() + this.customUserAgent;
            this.controller.setCustomUserAgent(userAgent);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### setDownloadDelegate<sup>11+</sup>

setDownloadDelegate(delegate: WebDownloadDelegate): void

Sets a **WebDownloadDelegate** object to receive downloads and download progress triggered from a page.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name         | Type   |  Mandatory | Description                                           |
| ---------------| ------- | ---- | ------------- |
| delegate      | [WebDownloadDelegate](#webdownloaddelegate11)  | Yes  | Delegate used to receive the download progress.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID | Error Message                                                     |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### startDownload<sup>11+</sup>

startDownload(url: string): void

Downloads a file, such as an image, from the specified URL.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name         | Type   |  Mandatory | Description                                           |
| ---------------| ------- | ---- | ------------- |
| url      | string  | Yes  | Download URL.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID | Error Message                                                     |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100002 | Invalid url. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getCustomUserAgent<sup>10+</sup>

getCustomUserAgent(): string

Obtains a custom user agent.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| string | Information about the custom user agent.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID | Error Message                                                     |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State userAgent: string = ''

  build() {
    Column() {
      Button('getCustomUserAgent')
        .onClick(() => {
          try {
            this.userAgent = this.controller.getCustomUserAgent();
            console.log("userAgent: " + this.userAgent);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### setConnectionTimeout<sup>11+</sup>

static setConnectionTimeout(timeout: number): void

Sets the network connection timeout. You can use the **onErrorReceive** method in the **\<Web>** component to obtain the timeout error code.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name         | Type   |  Mandatory | Description                                           |
| ---------------| ------- | ---- | ------------- |
| timeout        | number  | Yes  | Socket connection timeout, in seconds.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('setConnectionTimeout')
        .onClick(() => {
          try {
            web_webview.WebviewController.setConnectionTimeout(5);
            console.log("setConnectionTimeout: 5s");
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
        .onErrorReceive((event) => {
          if (event) {
            console.log('getErrorInfo:' + event.error.getErrorInfo())
            console.log('getErrorCode:' + event.error.getErrorCode())
          }
        })
    }
  }
}
```

### enableSafeBrowsing<sup>11+</sup>

enableSafeBrowsing(enable: boolean): void

Enables the safe browsing feature. This feature is forcibly enabled and cannot be disabled for identified untrusted websites.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type   |  Mandatory | Description                      |
| --------| ------- | ---- | ---------------------------|
|  enable | boolean | Yes  | Whether to enable the safe browsing feature.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                 |
| -------- | ----------------------- |
|  401 | Invalid input parameter.    |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('enableSafeBrowsing')
        .onClick(() => {
          try {
            this.controller.enableSafeBrowsing(true);
            console.log("enableSafeBrowsing: true");
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### isSafeBrowsingEnabled<sup>11+</sup>

isSafeBrowsingEnabled(): boolean

Checks whether the safe browsing feature is enabled for this web page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type   | Description                                    |
| ------- | --------------------------------------- |
| boolean | Whether the safe browsing feature is enabled. The default value is **false**.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('isSafeBrowsingEnabled')
        .onClick(() => {
          let result = this.controller.isSafeBrowsingEnabled();
          console.log("result: " + result);
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### postUrl<sup>11+</sup>

postUrl(url: string, postData: ArrayBuffer): void

Loads the specified URL with **postData** using the POST method. If **url** is not a network URL, it will be loaded with [loadUrl](#loadurl) instead, and the **postData** parameter will be ignored.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name | Type            | Mandatory| Description                 |
| ------- | ---------------- | ---- | :-------------------- |
| url     | string | Yes  | URL to load.     |
| postData | ArrayBuffer | Yes  | Data to transfer using the POST method. The request must be encoded in "application/x-www-form-urlencoded" format.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |
| 17100002 | Invalid url.                                                 |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

class TestObj {
  constructor() {
  }

  test(str: string): ArrayBuffer {
    let buf = new ArrayBuffer(str.length);
    let buff = new Uint8Array(buf);

    for (let i = 0; i < str.length; i++) {
      buff[i] = str.charCodeAt(i);
    }
    return buf;
  }
}

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State testObjtest: TestObj = new TestObj();

  build() {
    Column() {
      Button('postUrl')
        .onClick(() => {
          try {
            // Convert data to the ArrayBuffer type.
            let postData = this.testObjtest.test("Name=test&Password=test");
            this.controller.postUrl('www.example.com', postData);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: '', controller: this.controller })
    }
  }
}
```

### createWebPrintDocumentAdapter<sup>11+</sup>

createWebPrintDocumentAdapter(jobName: string): print.PrintDocumentAdapter

Creates a **PrintDocumentAdapter** instance to provide content for printing.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name | Type   | Mandatory| Description                 |
| ------- | ------ | ---- | :-------------------- |
| jobName | string | Yes  | Name of the file to print.     |

**Return value**

| Type                | Description                     |
| -------------------- | ------------------------- |
| print.printDocumentAdapter | **PrintDocumentAdapter** instance created.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                                   |
| -------- | -------------------------------------------------------------------------- |
| 401 | Invalid input parameter.                                                        |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'
import print from '@ohos.print'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('createWebPrintDocumentAdapter')
        .onClick(() => {
          try {
            let webPrintDocadapter = this.controller.createWebPrintDocumentAdapter('example.pdf');
            print.print('example_jobid', webPrintDocadapter, null, getContext());
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```
### isIncognitoMode<sup>11+</sup>

isIncognitoMode(): boolean

Checks whether this Webview is in incognito mode.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type                | Description                     |
| -------------------- | ------------------------- |
| boolean              | Whether the Webview is in incognito mode.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                                   |
| -------- | -------------------------------------------------------------------------- |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('isIncognitoMode')
        .onClick(() => {
          try {
             let result = this.controller.isIncognitoMode();
             console.log('isIncognitoMode' + result);
            } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getSecurityLevel<sup>11+</sup>

getSecurityLevel(): SecurityLevel

Obtains the security level of this web page.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type                               | Description                       |
| ----------------------------------- | --------------------------- |
| [SecurityLevel](#securitylevel11) | Security level of the web page. The value can be **NONE**, **SECURE**, **WARNING**, or **DANGEROUS**.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example**

```ts
import webview from '@ohos.web.webview'


	
@Entry
@Component
struct WebComponent {
  controller: webview.WebviewController = new webview.WebviewController()
  build() {
    Column() {
      Web({ src: 'www.example.com', controller: this.controller })
        .onPageEnd((event) => {
          if (event) {
            let securityLevel = this.controller.getSecurityLevel()
            console.info('securityLevel: ', securityLevel)
          }
        })
    }
  }
}
```

## WebCookieManager

Implements a **WebCookieManager** instance to manage behavior of cookies in **\<Web>** components. All **\<Web>** components in an application share a **WebCookieManager** instance.

### getCookie<sup>(deprecated)</sup>

static getCookie(url: string): string

Obtains the cookie corresponding to the specified URL.

> **NOTE**
>
> This API is supported since API version 9 and deprecated since API version 11. You are advised to use [fetchCookieSync](#fetchcookiesync11) instead.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                     |
| ------ | ------ | ---- | :------------------------ |
| url    | string | Yes  | URL of the cookie to obtain. A complete URL is recommended.|

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| string | Cookie value corresponding to the specified URL.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100002 | Invalid url.                                           |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('getCookie')
        .onClick(() => {
          try {
            let value = web_webview.WebCookieManager.getCookie('https://www.example.com');
            console.log("value: " + value);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### fetchCookieSync<sup>11+</sup>

static fetchCookieSync(url: string, incognito?: boolean): string

Obtains the cookie corresponding to the specified URL.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                     |
| ------ | ------ | ---- | :------------------------ |
| url    | string | Yes  | URL of the cookie to obtain. A complete URL is recommended.|
| incognito    | boolean | No  | Whether to obtain the cookie in incognito mode. The value **true** means to obtain the cookie in incognito mode, and **false** means the opposite.|

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| string | Cookie value corresponding to the specified URL.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100002 | Invalid url.                                           |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('fetchCookieSync')
        .onClick(() => {
          try {
            let value = web_webview.WebCookieManager.fetchCookieSync('https://www.example.com');
            console.log("fetchCookieSync cookie = " + value);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### fetchCookie<sup>11+</sup>

static fetchCookie(url: string, callback: AsyncCallback\<string>): void

Obtains the cookie value of a specified URL. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                     |
| ------ | ------ | ---- | :------------------------ |
| url    | string | Yes  | URL of the cookie to obtain. A complete URL is recommended.|
| callback | AsyncCallback\<string> | Yes| Callback used to return the result.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 401 | Invalid input parameter.                                           |
| 17100002 | Invalid url.                                           |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('fetchCookie')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.fetchCookie('https://www.example.com', (error, cookie) => {
              if (error) {
                let e:business_error.BusinessError = error as business_error.BusinessError;
                console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
                return;
              }
              if (cookie) {
                console.log('fetchCookie cookie = ' + cookie);
              }
            })
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### fetchCookie<sup>11+</sup>

static fetchCookie(url: string): Promise\<string>

Obtains the cookie value of a specified URL. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                     |
| ------ | ------ | ---- | :------------------------ |
| url    | string | Yes  | URL of the cookie to obtain. A complete URL is recommended.|

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| Promise\<string> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 401 | Invalid input parameter.                                           |
| 17100002 | Invalid url.                                           |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('fetchCookie')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.fetchCookie('https://www.example.com')
              .then(cookie => {
                console.log("fetchCookie cookie = " + cookie);
              })
              .catch((error:business_error.BusinessError) => {
                console.error(`ErrorCode: ${error.code},  Message: ${error.message}`);
              })
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```


### setCookie<sup>(deprecated)</sup>

static setCookie(url: string, value: string): void

Sets a cookie for the specified URL.

> **NOTE**
>
> This API is supported since API version 9 and deprecated since API version 11. You are advised to use [configCookieSync<sup>11+</sup>](#configcookiesync11) instead.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                     |
| ------ | ------ | ---- | :------------------------ |
| url    | string | Yes  | URL of the cookie to set. A complete URL is recommended.|
| value  | string | Yes  | Cookie value to set.     |

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100002 | Invalid url.                                           |
| 17100005 | Invalid cookie value.                                  |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('setCookie')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.setCookie('https://www.example.com', 'a=b');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### configCookieSync<sup>11+</sup>

static configCookieSync(url: string, value: string, incognito?: boolean): void

Sets a cookie for the specified URL.

> **NOTE**
>
> You can set **url** in **configCookie** to a domain name so that cookies are attached to requests on the page.
> It is recommended that cookie syncing be completed before the webview is loaded.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                     |
| ------ | ------ | ---- | :------------------------ |
| url    | string | Yes  | URL of the cookie to set. A complete URL is recommended.|
| value  | string | Yes  | Cookie value to set.     |
| incognito    | boolean | No  | Whether to obtain the cookie in incognito mode. The value **true** means to obtain the cookie in incognito mode, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100002 | Invalid url.                                           |
| 17100005 | Invalid cookie value.                                  |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('configCookieSync')
        .onClick(() => {
          try {
            // Use commas (,) to separate cookie values. No comma is required when you set a single cookie value.
            web_webview.WebCookieManager.configCookieSync('https://www.example.com', 'a=b,c=d,e=f');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### configCookie<sup>11+</sup>

static configCookie(url: string, value: string, callback: AsyncCallback\<void>): void

Sets the value of a single cookie for a specified URL. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                     |
| ------ | ------ | ---- | :------------------------ |
| url    | string | Yes  | URL of the cookie to set. A complete URL is recommended.|
| value  | string | Yes  | Cookie value to set.     |
| callback | AsyncCallback\<void> | Yes| Callback used to return the result.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 401      | Invalid input parameter.                               |
| 17100002 | Invalid url.                                           |
| 17100005 | Invalid cookie value.                                  |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('configCookie')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.configCookie('https://www.example.com', "a=b", (error) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
              }
            })
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### configCookie<sup>11+</sup>

static configCookie(url: string, value: string): Promise\<void>

Sets the value of a single cookie for a specified URL. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                     |
| ------ | ------ | ---- | :------------------------ |
| url    | string | Yes  | URL of the cookie to set. A complete URL is recommended.|
| value  | string | Yes  | Cookie value to set.     |

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| Promise\<void> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                               |
| -------- | ------------------------------------------------------ |
| 401      | Invalid input parameter.                               |
| 17100002 | Invalid url.                                           |
| 17100005 | Invalid cookie value.                                  |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('configCookie')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.configCookie('https://www.example.com', 'a=b')
              .then(() => {
                console.log('configCookie success!');
              })
              .catch((error:business_error.BusinessError) => {
                console.log('error: ' + JSON.stringify(error));
              })
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### saveCookieAsync

static saveCookieAsync(callback: AsyncCallback\<void>): void

Saves the cookies in the memory to the drive. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                  | Mandatory| Description                                              |
| -------- | ---------------------- | ---- | :------------------------------------------------- |
| callback | AsyncCallback\<void> | Yes  | Callback used to return whether the cookies are successfully saved.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('saveCookieAsync')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.saveCookieAsync((error) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
              }
            })
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### saveCookieAsync

static saveCookieAsync(): Promise\<void>

Saves the cookies in the memory to the drive. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type            | Description                                     |
| ---------------- | ----------------------------------------- |
| Promise\<void> | Promise used to return the operation result.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('saveCookieAsync')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.saveCookieAsync()
              .then(() => {
                console.log("saveCookieAsyncCallback success!");
              })
              .catch((error:business_error.BusinessError) => {
                console.error("error: " + error);
              });
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### putAcceptCookieEnabled

static putAcceptCookieEnabled(accept: boolean): void

Sets whether the **WebCookieManager** instance has the permission to send and receive cookies.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type   | Mandatory| Description                                |
| ------ | ------- | ---- | :----------------------------------- |
| accept | boolean | Yes  | Whether the **WebCookieManager** instance has the permission to send and receive cookies.<br>Default value: **true**|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('putAcceptCookieEnabled')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.putAcceptCookieEnabled(false);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### isCookieAllowed

static isCookieAllowed(): boolean

Checks whether the **WebCookieManager** instance has the permission to send and receive cookies.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type   | Description                            |
| ------- | -------------------------------- |
| boolean | Whether the **WebCookieManager** instance has the permission to send and receive cookies. The default value is **true**.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('isCookieAllowed')
        .onClick(() => {
          let result = web_webview.WebCookieManager.isCookieAllowed();
          console.log("result: " + result);
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### putAcceptThirdPartyCookieEnabled

static putAcceptThirdPartyCookieEnabled(accept: boolean): void

Sets whether the **WebCookieManager** instance has the permission to send and receive third-party cookies.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type   | Mandatory| Description                                      |
| ------ | ------- | ---- | :----------------------------------------- |
| accept | boolean | Yes  | Whether the **WebCookieManager** instance has the permission to send and receive third-party cookies.<br>Default value: **false**|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('putAcceptThirdPartyCookieEnabled')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.putAcceptThirdPartyCookieEnabled(false);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### isThirdPartyCookieAllowed

static isThirdPartyCookieAllowed(): boolean

Checks whether the **WebCookieManager** instance has the permission to send and receive third-party cookies.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type   | Description                                  |
| ------- | -------------------------------------- |
| boolean | Whether the **WebCookieManager** instance has the permission to send and receive third-party cookies. The default value is **false**.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('isThirdPartyCookieAllowed')
        .onClick(() => {
          let result = web_webview.WebCookieManager.isThirdPartyCookieAllowed();
          console.log("result: " + result);
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### existCookie

static existCookie(incognito?: boolean): boolean

Checks whether cookies exist.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type   | Mandatory| Description                                      |
| ------ | ------- | ---- | :----------------------------------------- |
| incognito<sup>11+</sup>    | boolean | No  | Whether to check for cookies in incognito mode. The value **true** means to check for cookies in incognito mode, and **false** means the opposite.|

**Return value**

| Type   | Description                                  |
| ------- | -------------------------------------- |
| boolean | Whether cookies exist. The value **true** means that cookies exist, and **false** means the opposite.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('existCookie')
        .onClick(() => {
          let result = web_webview.WebCookieManager.existCookie();
          console.log("result: " + result);
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### deleteEntireCookie<sup>(deprecated)</sup>

static deleteEntireCookie(): void

Deletes all cookies.

> **NOTE**
>
> This API is supported since API version 9 and deprecated since API version 11. You are advised to use [clearAllCookiesSync](#clearallcookiessync11) instead.

**System capability**: SystemCapability.Web.Webview.Core

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('deleteEntireCookie')
        .onClick(() => {
          web_webview.WebCookieManager.deleteEntireCookie();
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### clearAllCookiesSync<sup>11+</sup>

static clearAllCookiesSync(incognito?: boolean): void

Deletes all cookies.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type   | Mandatory| Description                                      |
| ------ | ------- | ---- | :----------------------------------------- |
| incognito    | boolean | No  | Whether to delete all cookies in incognito mode. The value **true** means to delete all cookies in incognito mode, and **false** means the opposite.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('clearAllCookiesSync')
        .onClick(() => {
          web_webview.WebCookieManager.clearAllCookiesSync();
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### clearAllCookies<sup>11+</sup>

static clearAllCookies(callback: AsyncCallback\<void>): void

Clears all cookies. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                  | Mandatory| Description                                              |
| -------- | ---------------------- | ---- | :------------------------------------------------- |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('clearAllCookies')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.clearAllCookies((error) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
              }
            })
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### clearAllCookies<sup>11+</sup>

static clearAllCookies(): Promise\<void>

Clears all cookies. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type            | Description                                     |
| ---------------- | ----------------------------------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('clearAllCookies')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.clearAllCookies()
              .then(() => {
                console.log("clearAllCookies success!");
              })
              .catch((error:business_error.BusinessError) => {
                console.error("error: " + error);
              });
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### deleteSessionCookie<sup>(deprecated)</sup>

static deleteSessionCookie(): void

Deletes all session cookies.

> **NOTE**
>
> This API is supported since API version 9 and deprecated since API version 11. You are advised to use [clearSessionCookiesync](#clearsessioncookiesync11) instead.

**System capability**: SystemCapability.Web.Webview.Core

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('deleteSessionCookie')
        .onClick(() => {
          web_webview.WebCookieManager.deleteSessionCookie();
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### clearSessionCookieSync<sup>11+</sup>

static clearSessionCookieSync(): void

Deletes all session cookies.

**System capability**: SystemCapability.Web.Webview.Core

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('clearSessionCookieSync')
        .onClick(() => {
          web_webview.WebCookieManager.clearSessionCookieSync();
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### clearSessionCookie<sup>11+</sup>

static clearSessionCookie(callback: AsyncCallback\<void>): void

Clears all session cookies. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                  | Mandatory| Description                                              |
| -------- | ---------------------- | ---- | :------------------------------------------------- |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('clearSessionCookie')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.clearSessionCookie((error) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
              }
            })
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### clearSessionCookie<sup>11+</sup>

static clearSessionCookie(): Promise\<void>

Clears all session cookies. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type            | Description                                     |
| ---------------- | ----------------------------------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();

  build() {
    Column() {
      Button('clearSessionCookie')
        .onClick(() => {
          try {
            web_webview.WebCookieManager.clearSessionCookie()
              .then(() => {
                console.log("clearSessionCookie success!");
              })
              .catch((error:business_error.BusinessError) => {
                console.error("error: " + error);
              });
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

## WebStorage

Implements a **WebStorage** object to manage the Web SQL database and HTML5 Web Storage APIs. All **\<Web>** components in an application share a **WebStorage** object.

> **NOTE**
>
> You must load the **\<Web>** component before calling the APIs in **WebStorage**.

### deleteOrigin

static deleteOrigin(origin: string): void

Deletes all data in the specified origin.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                    |
| ------ | ------ | ---- | ------------------------ |
| origin | string | Yes  | Index of the origin, which is obtained through [getOrigins](#getorigins).|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100011 | Invalid origin.                             |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  origin: string = "resource://rawfile/";

  build() {
    Column() {
      Button('deleteOrigin')
        .onClick(() => {
          try {
            web_webview.WebStorage.deleteOrigin(this.origin);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }

        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .databaseAccess(true)
    }
  }
}
```

HTML file to be loaded:
 ```html
  <!-- index.html -->
  <!DOCTYPE html>
  <html>
  <head>
    <meta charset="UTF-8">
    <title>test</title>
    <script type="text/javascript">

      var db = openDatabase('mydb','1.0','Test DB',2 * 1024 * 1024);
      var msg;

      db.transaction(function(tx){
        tx.executeSql('INSERT INTO LOGS (id,log) VALUES(1,"test1")');
        tx.executeSql('INSERT INTO LOGS (id,log) VALUES(2,"test2")');
        msg = '<p>Data table created, with two data records inserted.</p>';

        document.querySelector('#status').innerHTML = msg;
      });

      db.transaction(function(tx){
        tx.executeSql('SELECT * FROM LOGS', [], function (tx, results) {
          var len = results.rows.length,i;
          msg = "<p>Number of records: " + len + "</p>";

          document.querySelector('#status').innerHTML += msg;

              for(i = 0; i < len; i++){
                msg = "<p><b>" + results.rows.item(i).log + "</b></p>";

          document.querySelector('#status').innerHTML += msg;
          }
        },null);
      });

      </script>
  </head>
  <body>
  <div id="status" name="status">Status</div>
  </body>
  </html>
  ```

### getOrigins

static getOrigins(callback: AsyncCallback\<Array\<WebStorageOrigin>>): void

Obtains information about all origins that are currently using the Web SQL Database. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                                  | Mandatory| Description                                                  |
| -------- | -------------------------------------- | ---- | ------------------------------------------------------ |
| callback | AsyncCallback\<Array\<[WebStorageOrigin](#webstorageorigin)>> | Yes  | Callback used to return the information about the origins. For details, see [WebStorageOrigin](#webstorageorigin).|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100012 | Invalid web storage origin.                             |

**Example**

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
      Button('getOrigins')
        .onClick(() => {
          try {
            web_webview.WebStorage.getOrigins((error, origins) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
                return;
              }
              for (let i = 0; i < origins.length; i++) {
                console.log('origin: ' + origins[i].origin);
                console.log('usage: ' + origins[i].usage);
                console.log('quota: ' + origins[i].quota);
              }
            })
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }

        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .databaseAccess(true)
    }
  }
}
```

For details about the HTML file loaded, see the HTML file loaded using the [deleteOrigin](#deleteorigin) API.

### getOrigins

static getOrigins(): Promise\<Array\<WebStorageOrigin>>

Obtains information about all origins that are currently using the Web SQL Database. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type                            | Description                                                        |
| -------------------------------- | ------------------------------------------------------------ |
| Promise\<Array\<[WebStorageOrigin](#webstorageorigin)>> | Promise used to return the information about the origins. For details, see [WebStorageOrigin](#webstorageorigin).|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100012 | Invalid web storage origin.                             |

**Example**

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
      Button('getOrigins')
        .onClick(() => {
          try {
            web_webview.WebStorage.getOrigins()
              .then(origins => {
                for (let i = 0; i < origins.length; i++) {
                  console.log('origin: ' + origins[i].origin);
                  console.log('usage: ' + origins[i].usage);
                  console.log('quota: ' + origins[i].quota);
                }
              })
              .catch((e : business_error.BusinessError) => {
                console.log('error: ' + JSON.stringify(e));
              })
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }

        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .databaseAccess(true)
    }
  }
}
```

For details about the HTML file loaded, see the HTML file loaded using the [deleteOrigin](#deleteorigin) API.

### getOriginQuota

static getOriginQuota(origin: string, callback: AsyncCallback\<number>): void

Obtains the storage quota of an origin in the Web SQL Database, in bytes. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                 | Mandatory| Description              |
| -------- | --------------------- | ---- | ------------------ |
| origin   | string                | Yes  | Index of the origin.|
| callback | AsyncCallback\<number> | Yes  | Storage quota of the origin.  |

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100011 | Invalid origin.                             |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  origin: string = "resource://rawfile/";

  build() {
    Column() {
      Button('getOriginQuota')
        .onClick(() => {
          try {
            web_webview.WebStorage.getOriginQuota(this.origin, (error, quota) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
                return;
              }
              console.log('quota: ' + quota);
            })
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }

        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .databaseAccess(true)
    }
  }
}
```

For details about the HTML file loaded, see the HTML file loaded using the [deleteOrigin](#deleteorigin) API.

### getOriginQuota

static getOriginQuota(origin: string): Promise\<number>

Obtains the storage quota of an origin in the Web SQL Database, in bytes. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| origin | string | Yes  | Index of the origin.|

**Return value**

| Type           | Description                                   |
| --------------- | --------------------------------------- |
| Promise\<number> | Promise used to return the storage quota of the origin.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100011 | Invalid origin.                             |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  origin: string = "resource://rawfile/";

  build() {
    Column() {
      Button('getOriginQuota')
        .onClick(() => {
          try {
            web_webview.WebStorage.getOriginQuota(this.origin)
              .then(quota => {
                console.log('quota: ' + quota);
              })
              .catch((e : business_error.BusinessError) => {
                console.log('error: ' + JSON.stringify(e));
              })
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }

        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .databaseAccess(true)
    }
  }
}
```

For details about the HTML file loaded, see the HTML file loaded using the [deleteOrigin](#deleteorigin) API.

### getOriginUsage

static getOriginUsage(origin: string, callback: AsyncCallback\<number>): void

Obtains the storage usage of an origin in the Web SQL Database, in bytes. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                 | Mandatory| Description              |
| -------- | --------------------- | ---- | ------------------ |
| origin   | string                | Yes  | Index of the origin.|
| callback | AsyncCallback\<number> | Yes  | Storage usage of the origin.  |

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100011 | Invalid origin.                             |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  origin: string = "resource://rawfile/";

  build() {
    Column() {
      Button('getOriginUsage')
        .onClick(() => {
          try {
            web_webview.WebStorage.getOriginUsage(this.origin, (error, usage) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
                return;
              }
              console.log('usage: ' + usage);
            })
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }

        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .databaseAccess(true)
    }
  }
}
```

For details about the HTML file loaded, see the HTML file loaded using the [deleteOrigin](#deleteorigin) API.

### getOriginUsage

static getOriginUsage(origin: string): Promise\<number>

Obtains the storage usage of an origin in the Web SQL Database, in bytes. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| origin | string | Yes  | Index of the origin.|

**Return value**

| Type           | Description                                 |
| --------------- | ------------------------------------- |
| Promise\<number> | Promise used to return the storage usage of the origin.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                             |
| -------- | ----------------------------------------------------- |
| 17100011 | Invalid origin.                            |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  origin: string = "resource://rawfile/";

  build() {
    Column() {
      Button('getOriginUsage')
        .onClick(() => {
          try {
            web_webview.WebStorage.getOriginUsage(this.origin)
              .then(usage => {
                console.log('usage: ' + usage);
              })
              .catch((e : business_error.BusinessError) => {
                console.log('error: ' + JSON.stringify(e));
              })
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }

        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .databaseAccess(true)
    }
  }
}
```

For details about the HTML file loaded, see the HTML file loaded using the [deleteOrigin](#deleteorigin) API.

### deleteAllData

static deleteAllData(incognito?: boolean): void

Deletes all data in the Web SQL Database.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| incognito<sup>11+</sup>    | boolean | No  | Whether to delete all data in the Web SQL Database in incognito mode. The value **true** means to delete all data in the Web SQL Database in incognito mode, and **false** means the opposite.|

**Example**

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
      Button('deleteAllData')
        .onClick(() => {
          try {
            web_webview.WebStorage.deleteAllData();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: $rawfile('index.html'), controller: this.controller })
        .databaseAccess(true)
    }
  }
}
```

For details about the HTML file loaded, see the HTML file loaded using the [deleteOrigin](#deleteorigin) API.

## WebDataBase

Implements a **WebDataBase** object.

> **NOTE**
>
> You must load the **\<Web>** component before calling the APIs in **WebDataBase**.

### getHttpAuthCredentials

static getHttpAuthCredentials(host: string, realm: string): Array\<string>

Retrieves HTTP authentication credentials for a given host and realm. This API returns the result synchronously.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                        |
| ------ | ------ | ---- | ---------------------------- |
| host   | string | Yes  | Host to which HTTP authentication credentials apply.|
| realm  | string | Yes  | Realm to which HTTP authentication credentials apply.  |

**Return value**

| Type | Description                                        |
| ----- | -------------------------------------------- |
| Array\<string> | Returns the array of the matching user names and passwords if the operation is successful; returns an empty array otherwise.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  host: string = "www.spincast.org";
  realm: string = "protected example";
  username_password: string[] = [];

  build() {
    Column() {
      Button('getHttpAuthCredentials')
        .onClick(() => {
          try {
            this.username_password = web_webview.WebDataBase.getHttpAuthCredentials(this.host, this.realm);
            console.log('num: ' + this.username_password.length);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### saveHttpAuthCredentials

static saveHttpAuthCredentials(host: string, realm: string, username: string, password: string): void

Saves HTTP authentication credentials for a given host and realm. This API returns the result synchronously.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type  | Mandatory| Description                        |
| -------- | ------ | ---- | ---------------------------- |
| host     | string | Yes  | Host to which HTTP authentication credentials apply.|
| realm    | string | Yes  | Realm to which HTTP authentication credentials apply.  |
| username | string | Yes  | User name.                    |
| password | string | Yes  | Password.                      |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  host: string = "www.spincast.org";
  realm: string = "protected example";

  build() {
    Column() {
      Button('saveHttpAuthCredentials')
        .onClick(() => {
          try {
            web_webview.WebDataBase.saveHttpAuthCredentials(this.host, this.realm, "Stromgol", "Laroche");
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### existHttpAuthCredentials

static existHttpAuthCredentials(): boolean

Checks whether any saved HTTP authentication credentials exist. This API returns the result synchronously.  

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type   | Description                                                        |
| ------- | ------------------------------------------------------------ |
| boolean | Whether any saved HTTP authentication credentials exist. Returns **true** if any saved HTTP authentication credentials exist; returns **false** otherwise.|

**Example**

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
      Button('existHttpAuthCredentials')
        .onClick(() => {
          try {
            let result = web_webview.WebDataBase.existHttpAuthCredentials();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### deleteHttpAuthCredentials

static deleteHttpAuthCredentials(): void

Deletes all HTTP authentication credentials saved in the cache. This API returns the result synchronously.

**System capability**: SystemCapability.Web.Webview.Core

**Example**

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
      Button('deleteHttpAuthCredentials')
        .onClick(() => {
          try {
            web_webview.WebDataBase.deleteHttpAuthCredentials();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

## GeolocationPermissions

Implements a **GeolocationPermissions** object.

> **NOTE**
>
> You must load the **\<Web>** component before calling the APIs in **GeolocationPermissions**.

### Required Permissions

**ohos.permission.LOCATION**, **ohos.permission.APPROXIMATELY_LOCATION**, and **ohos.permission.LOCATION_IN_BACKGROUND**, which are required for accessing the location information. For details about the permissions, see [@ohos.geolocation (Geolocation)](../apis-location-kit/js-apis-geolocation.md).

### allowGeolocation

static allowGeolocation(origin: string, incognito?: boolean): void

Allows the specified origin to use the geolocation information.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| origin | string | Yes  |Index of the origin.|
| incognito<sup>11+</sup>    | boolean | No  | Whether to allow the specified origin to use the geolocation information in incognito mode. The value **true** means to allow the specified origin to use the geolocation information in incognito mode, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100011 | Invalid origin.                             |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  origin: string = "file:///";

  build() {
    Column() {
      Button('allowGeolocation')
        .onClick(() => {
          try {
            web_webview.GeolocationPermissions.allowGeolocation(this.origin);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### deleteGeolocation

static deleteGeolocation(origin: string, incognito?: boolean): void

Clears the geolocation permission status of a specified origin.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description              |
| ------ | ------ | ---- | ------------------ |
| origin | string | Yes  | Index of the origin.|
| incognito<sup>11+</sup>    | boolean | No  | Whether to clear the geolocation permission status of a specified origin in incognito mode. The value **true** means to clear the geolocation permission status of a specified origin in incognito mode, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100011 | Invalid origin.                             |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  origin: string = "file:///";

  build() {
    Column() {
      Button('deleteGeolocation')
        .onClick(() => {
          try {
            web_webview.GeolocationPermissions.deleteGeolocation(this.origin);
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getAccessibleGeolocation

static getAccessibleGeolocation(origin: string, callback: AsyncCallback\<boolean>, incognito?: boolean): void

Obtains the geolocation permission status of the specified origin. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                  | Mandatory| Description                                                        |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| origin   | string                 | Yes  | Index of the origin.                                          |
| callback | AsyncCallback\<boolean> | Yes  | Callback used to return the geolocation permission status of the specified origin. If the operation is successful, the value **true** means that the geolocation permission is granted, and **false** means the opposite. If the operation fails, the geolocation permission status of the specified origin is not found.|
| incognito<sup>11+</sup>    | boolean | No  | Whether to obtain the geolocation permission status of the specified origin in incognito mode. The value **true** means to obtain the geolocation permission status of the specified origin in incognito mode, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100011 | Invalid origin.                             |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  origin: string = "file:///";

  build() {
    Column() {
      Button('getAccessibleGeolocation')
        .onClick(() => {
          try {
            web_webview.GeolocationPermissions.getAccessibleGeolocation(this.origin, (error, result) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`getAccessibleGeolocationAsync error, ErrorCode: ${e.code},  Message: ${e.message}`);
                return;
              }
              console.log('getAccessibleGeolocationAsync result: ' + result);
            });
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getAccessibleGeolocation

static getAccessibleGeolocation(origin: string, incognito?: boolean): Promise\<boolean>

Obtains the geolocation permission status of the specified origin. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type| Mandatory| Description            |
| ------ | -------- | ---- | -------------------- |
| origin | string   | Yes  | Index of the origin.|
| incognito<sup>11+</sup>    | boolean | No  | Whether to obtain the geolocation permission status of the specified origin in incognito mode. The value **true** means to obtain the geolocation permission status of the specified origin in incognito mode, and **false** means the opposite.|

**Return value**

| Type            | Description                                                        |
| ---------------- | ------------------------------------------------------------ |
| Promise\<boolean> | Promise used to return the geolocation permission status of the specified origin. If the operation is successful, the value **true** means that the geolocation permission is granted, and **false** means the opposite. If the operation fails, the geolocation permission status of the specified origin is not found.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                                              |
| -------- | ------------------------------------------------------ |
| 17100011 | Invalid origin.                             |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  origin: string = "file:///";

  build() {
    Column() {
      Button('getAccessibleGeolocation')
        .onClick(() => {
          try {
            web_webview.GeolocationPermissions.getAccessibleGeolocation(this.origin)
              .then(result => {
                console.log('getAccessibleGeolocationPromise result: ' + result);
              }).catch((error : business_error.BusinessError) => {
              console.error(`getAccessibleGeolocationPromise error, ErrorCode: ${error.code},  Message: ${error.message}`);
            });
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getStoredGeolocation

static getStoredGeolocation(callback: AsyncCallback\<Array\<string>>, incognito?: boolean): void

Obtains the geolocation permission status of all origins. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                        | Mandatory| Description                                    |
| -------- | ---------------------------- | ---- | ---------------------------------------- |
| callback | AsyncCallback\<Array\<string>> | Yes  | Callback used to return the geolocation permission status of all origins.|
| incognito<sup>11+</sup>    | boolean | No  | Whether to obtain the geolocation permission status of all origins in incognito mode. The value **true** means to obtain the geolocation permission status of all origins in incognito mode, and **false** means the opposite.|

**Example**

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
      Button('getStoredGeolocation')
        .onClick(() => {
          try {
            web_webview.GeolocationPermissions.getStoredGeolocation((error, origins) => {
              if (error) {
                let e: business_error.BusinessError = error as business_error.BusinessError;
                console.error(`getStoredGeolocationAsync error, ErrorCode: ${e.code},  Message: ${e.message}`);
                return;
              }
              let origins_str: string = origins.join();
              console.log('getStoredGeolocationAsync origins: ' + origins_str);
            });
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getStoredGeolocation

static getStoredGeolocation(incognito?: boolean): Promise\<Array\<string>>

Obtains the geolocation permission status of all origins. This API uses a promise to return the result.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                        | Mandatory| Description                                    |
| -------- | ---------------------------- | ---- | ---------------------------------------- |
| incognito<sup>11+</sup>    | boolean | No  | Whether to obtain the geolocation permission status of all origins in incognito mode. The value **true** means to obtain the geolocation permission status of all origins in incognito mode, and **false** means the opposite.|

**Return value**

| Type                  | Description                                                     |
| ---------------------- | --------------------------------------------------------- |
| Promise\<Array\<string>> | Promise used to return the geolocation permission status of all origins.|

**Example**

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
      Button('getStoredGeolocation')
        .onClick(() => {
          try {
            web_webview.GeolocationPermissions.getStoredGeolocation()
              .then(origins => {
                let origins_str: string = origins.join();
                console.log('getStoredGeolocationPromise origins: ' + origins_str);
              }).catch((error : business_error.BusinessError) => {
              console.error(`getStoredGeolocationPromise error, ErrorCode: ${error.code},  Message: ${error.message}`);
            });
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### deleteAllGeolocation

static deleteAllGeolocation(incognito?: boolean): void

Clears the geolocation permission status of all sources.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name  | Type                        | Mandatory| Description                                    |
| -------- | ---------------------------- | ---- | ---------------------------------------- |
| incognito<sup>11+</sup>    | boolean | No  | Whether to clear the geolocation permission status of all sources in incognito mode. The value **true** means to clear the geolocation permission status of all sources in incognito mode, and **false** means the opposite.|

**Example**

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
      Button('deleteAllGeolocation')
        .onClick(() => {
          try {
            web_webview.GeolocationPermissions.deleteAllGeolocation();
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```
## WebHeader

Describes the request/response header returned by the **\<Web>** component.

**System capability**: SystemCapability.Web.Webview.Core

| Name       | Type  | Readable| Writable|Description                |
| ----------- | ------ | -----|------|------------------- |
| headerKey   | string | Yes| Yes| Key of the request/response header.  |
| headerValue | string | Yes| Yes| Value of the request/response header.|

## WebHitTestType

The [getHitTest](#gethittest) API is used to indicate a cursor node.

**System capability**: SystemCapability.Web.Webview.Core

| Name         | Value| Description                                     |
| ------------- | -- |----------------------------------------- |
| EditText      | 0 |Editable area.                           |
| Email         | 1 |Email address.                           |
| HttpAnchor    | 2 |Hyperlink, where **src** is **http**.                    |
| HttpAnchorImg | 3 |Image with a hyperlink, where **src** is http + HTML::img.|
| Img           | 4 |HTML::img tag.                          |
| Map           | 5 |Geographical address.                               |
| Phone         | 6 |Phone number.                               |
| Unknown       | 7 |Unknown content.                               |

## SecurityLevel<sup>11+</sup>

Defines the security level of the web page.

**System capability**: SystemCapability.Web.Webview.Core

| Name         | Value| Description                                     |
| ------------- | -- |----------------------------------------- |
| NONE          | 0 |The web page is neither absolutely secure nor insecure, that is, neutral. A typical example is a web page whose URL scheme is not HTTP or HTTPS.|
| SECURE        | 1 |The web page is secure, using the HTTPS protocol and a trusted certificate.|
| WARNING       | 2 |The web page is possibly compromised. A typical example is a web page that uses the HTTP or HTTPS protocol but an outdated TLS version.|
| DANGEROUS     | 3 |The web page is insecure. This means that the page may have attempted to load HTTPS scripts to no avail, have failed authentication, or contain insecure active content in HTTPS, malware, phishing, or any other sources of major threats.|

##  HitTestValue

Provides the element information of the area being clicked. For details about the sample code, see [getHitTestValue](#gethittestvalue).

**System capability**: SystemCapability.Web.Webview.Core

| Name| Type| Readable| Writable| Description|
| ---- | ---- | ---- | ---- |---- |
| type | [WebHitTestType](#webhittesttype) | Yes| Yes| Element type of the area being clicked.|
| extra | string        | Yes| Yes|Extra information of the area being clicked. If the area being clicked is an image or a link, the extra information is the URL of the image or link.|

## WebMessage

Describes the data types supported for [WebMessagePort](#webmessageport).

**System capability**: SystemCapability.Web.Webview.Core

| Type      | Description                                    |
| -------- | -------------------------------------- |
| string   | String type.|
| ArrayBuffer   | Binary type.|

## JsMessageType<sup>10+</sup>

Describes the type of the returned result of script execution using [runJavaScirptExt](#runjavascriptext10).

**System capability**: SystemCapability.Web.Webview.Core

| Name        | Value| Description                             |
| ------------ | -- |--------------------------------- |
| NOT_SUPPORT  | 0 |Unsupported data type.|
| STRING       | 1 |String type.|
| NUMBER       | 2 |Number type.|
| BOOLEAN      | 3 |Boolean type.|
| ARRAY_BUFFER | 4 |Raw binary data buffer.|
| ARRAY        | 5 |Array type.|

## WebMessageType<sup>10+</sup>

Describes the data type supported by the [webMessagePort](#webmessageport) API.

**System capability**: SystemCapability.Web.Webview.Core

| Name        | Value| Description                           |
| ------------ | -- |------------------------------- |
| NOT_SUPPORT  | 0 |Unsupported data type.|
| STRING       | 1 |String type.|
| NUMBER       | 2 |Number type.|
| BOOLEAN      | 3 |Boolean type.|
| ARRAY_BUFFER | 4 |Raw binary data buffer.|
| ARRAY        | 5 |Array type.|
| ERROR        | 6 |Error object type.|

## JsMessageExt<sup>10+</sup>

Implements the **JsMessageExt** data object that is returned after script execution using the [runJavaScirptExt](#runjavascriptext10) API.

### getType<sup>10+</sup>

getType(): JsMessageType

Obtains the type of the data object. For the complete sample code, see [runJavaScriptExt](#runjavascriptext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description                                                     |
| --------------| --------------------------------------------------------- |
| [JsMessageType](#jsmessagetype10) | Type of the data object that is returned after script execution using the [runJavaScirptExt](#runjavascriptext10) API.|

### getString<sup>10+</sup>

getString(): string

Obtains string-type data of the data object. For the complete sample code, see [runJavaScriptExt](#runjavascriptext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| string | Data of the string type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the result. |

### getNumber<sup>10+</sup>

getNumber(): number

Obtains number-type data of the data object. For the complete sample code, see [runJavaScriptExt](#runjavascriptext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| number | Data of the number type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the result. |

### getBoolean<sup>10+</sup>

getBoolean(): boolean

Obtains Boolean-type data of the data object. For the complete sample code, see [runJavaScriptExt](#runjavascriptext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| boolean | Data of the Boolean type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the result. |

### getArrayBuffer<sup>10+</sup>

getArrayBuffer(): ArrayBuffer

Obtains raw binary data of the data object. For the complete sample code, see [runJavaScriptExt](#runjavascriptext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| ArrayBuffer | Raw binary data.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the result. |

### getArray<sup>10+</sup>

getArray(): Array\<string | number | boolean\>

Obtains array-type data of the data object. For the complete sample code, see [runJavaScriptExt](#runjavascriptext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| Array\<string \| number \| boolean\> | Data of the array type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the result. |

## WebMessageExt<sup>10+</sup>

Data object received and sent by the [webMessagePort](#webmessageport) interface.

### getType<sup>10+</sup>

getType(): WebMessageType

Obtains the type of the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description                                                     |
| --------------| --------------------------------------------------------- |
| [WebMessageType](#webmessagetype10) | Data type supported by the [webMessagePort](#webmessageport) API.|

### getString<sup>10+</sup>

getString(): string

Obtains string-type data of the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| string | Data of the string type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### getNumber<sup>10+</sup>

getNumber(): number

Obtains number-type data of the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| number | Data of the number type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### getBoolean<sup>10+</sup>

getBoolean(): boolean

Obtains Boolean-type data of the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| boolean | Data of the Boolean type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### getArrayBuffer<sup>10+</sup>

getArrayBuffer(): ArrayBuffer

Obtains raw binary data of the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| ArrayBuffer | Raw binary data.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### getArray<sup>10+</sup>

getArray(): Array\<string | number | boolean\>

Obtains array-type data of the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| Array\<string \| number \| boolean\> | Data of the array type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### getError<sup>10+</sup>

getError(): Error

Obtains the error-object-type data of the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type          | Description         |
| --------------| ------------- |
| Error | Data of the error object type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### setType<sup>10+</sup>

setType(type: WebMessageType): void

Sets the type for the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | ---------------------- |
| type  | [WebMessageType](#webmessagetype10) | Yes  | Data type supported by the [webMessagePort](#webmessageport) API.|

**Error codes**

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### setString<sup>10+</sup>

setString(message: string): void

Sets the string-type data of the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | -------------------- |
| message  | string | Yes  | String type.|

**Error codes**

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### setNumber<sup>10+</sup>

setNumber(message: number): void

Sets the number-type data of the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | -------------------- |
| message  | number | Yes  | Data of the number type.|

**Error codes**

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### setBoolean<sup>10+</sup>

setBoolean(message: boolean): void

Sets the Boolean-type data for the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | -------------------- |
| message  | boolean | Yes  | Data of the Boolean type.|

**Error codes**

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### setArrayBuffer<sup>10+</sup>

setArrayBuffer(message: ArrayBuffer): void

Sets the raw binary data for the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | -------------------- |
| message  | ArrayBuffer | Yes  | Raw binary data.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### setArray<sup>10+</sup>

setArray(message: Array\<string | number | boolean\>): void

Sets the array-type data for the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | -------------------- |
| message  | Array\<string \| number \| boolean\> | Yes  | Data of the array type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

### setError<sup>10+</sup>

setError(message: Error): void

Sets the error-object-type data for the data object. For the complete sample code, see [onMessageEventExt](#onmessageeventext10).

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | -------------------- |
| message  | Error | Yes  | Data of the error object type.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100014 | The type does not match with the value of the web message. |

## WebStorageOrigin

Provides usage information of the Web SQL Database.

**System capability**: SystemCapability.Web.Webview.Core

| Name  | Type  | Readable| Writable| Description|
| ------ | ------ | ---- | ---- | ---- |
| origin | string | Yes | Yes | Index of the origin.|
| usage  | number | Yes | Yes | Storage usage of the origin.    |
| quota  | number | Yes | Yes | Storage quota of the origin.  |

## BackForwardList

Provides the historical information list of the current webview.

**System capability**: SystemCapability.Web.Webview.Core

| Name        | Type  | Readable| Writable| Description                                                        |
| ------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| currentIndex | number | Yes  | Yes  | Index of the current page in the page history stack.                                |
| size         | number | Yes  | Yes  | Number of indexes in the history stack. The maximum value is 50. If this value is exceeded, the earliest index will be overwritten.|

### getItemAtIndex

getItemAtIndex(index: number): HistoryItem

Obtains the page record with the specified index in the history stack.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | ---------------------- |
| index  | number | Yes  | Index of the target page record in the history stack.|

**Return value**

| Type                       | Description        |
| --------------------------- | ------------ |
| [HistoryItem](#historyitem) | Historical page record.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview';
import image from "@ohos.multimedia.image";
import business_error from '@ohos.base';

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  @State icon: image.PixelMap | undefined = undefined;

  build() {
    Column() {
      Button('getBackForwardEntries')
        .onClick(() => {
          try {
            let list = this.controller.getBackForwardEntries();
            let historyItem = list.getItemAtIndex(list.currentIndex);
            console.log("HistoryItem: " + JSON.stringify(historyItem));
            this.icon = historyItem.icon;
          } catch (error) {
            let e: business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

## HistoryItem

Describes a historical page record.

**System capability**: SystemCapability.Web.Webview.Core

| Name         | Type                                  | Readable| Writable| Description                        |
| ------------- | -------------------------------------- | ---- | ---- | ---------------------------- |
| icon          | [PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7) | Yes  | No  | **PixelMap** object of the icon on the historical page.|
| historyUrl    | string                                 | Yes  | Yes  | URL of the historical page.       |
| historyRawUrl | string                                 | Yes  | Yes  | Original URL of the historical page.   |
| title         | string                                 | Yes  | Yes  | Title of the historical page.          |

## WebCustomScheme

Defines a custom URL scheme.

**System capability**: SystemCapability.Web.Webview.Core

| Name          | Type      | Readable| Writable| Description                        |
| -------------- | --------- | ---- | ---- | ---------------------------- |
| schemeName     | string    | Yes  | Yes  | Name of the custom URL scheme. The value can contain a maximum of 32 characters and include only lowercase letters, digits, periods (.), plus signs (+), and hyphens (-).       |
| isSupportCORS  | boolean   | Yes  | Yes  | Whether to support cross-origin resource sharing (CORS).   |
| isSupportFetch | boolean   | Yes  | Yes  | Whether to support fetch requests.          |

## SecureDnsMode<sup>10+</sup>

Describes the mode in which the **\<Web>** component uses HTTPDNS.

**System capability**: SystemCapability.Web.Webview.Core

| Name         | Value| Description                                     |
| ------------- | -- |----------------------------------------- |
| OFF                                  | 0 |HTTPDNS is not used. This value can be used to revoke the previously used HTTPDNS configuration.|
| AUTO                                 | 1 |HTTPDNS is used in automatic mode. If the specified HTTPDNS server is unavailable for resolution, the component falls back to the system DNS server.|
| SECURE_ONLY                          | 2 |The specified HTTPDNS server is forcibly used for DNS resolution.|

## WebDownloadState<sup>11+</sup>

Describes the state of a download task.

**System capability**: SystemCapability.Web.Webview.Core

| Name         | Value| Description                                     |
| ------------- | -- |----------------------------------------- |
| IN_PROGRESS                                  | 0 |The download task is in progress.|
| COMPLETED                                 | 1 |The download task is completed.|
| CANCELED                          | 2 |The download task has been canceled.|
| INTERRUPTED                          | 3 |The download task is interrupted.|
| PENDING                          | 4 |The download task is pending.|
| PAUSED                          | 5 |The download task is paused.|
| UNKNOWN                          | 6 |The state of the download task is unknown.|

## WebDownloadErrorCode<sup>11+</sup>

Describes the download task error code.

**System capability**: SystemCapability.Web.Webview.Core

| Name         | Value| Description                                     |
| ------------- | -- |----------------------------------------- |
| ERROR_UNKNOWN                                  | 0 |Unknown error.|
| FILE_FAILED | 1 |  Failed to operate the file.|
| FILE_ACCESS_DENIED | 2 | No permission to access the file.|
| FILE_NO_SPACE | 3 | The disk space is insufficient.|
| FILE_NAME_TOO_LONG | 5 | The file name is too long.|
| FILE_TOO_LARGE | 6 | The file is too large.|
| FILE_TRANSIENT_ERROR | 10 |  Some temporary issues occur, such as insufficient memory, files in use, and too many files open at the same time.|
| FILE_BLOCKED | 11 |  Access to the file is blocked due to certain local policies.|
| FILE_TOO_SHORT | 13 |  The file to resume downloading is not long enough. It may not exist.|
| FILE_HASH_MISMATCH | 14 |  Hash mismatch.|
| FILE_SAME_AS_SOURCE | 15 |  The file already exists.|
| NETWORK_FAILED | 20 |  Common network error.|
| NETWORK_TIMEOUT | 21 | Network connection timeout.|
| NETWORK_DISCONNECTED | 22 | Network disconnected.|
| NETWORK_SERVER_DOWN | 23 |  The server is shut down.|
| NETWORK_INVALID_REQUEST | 24 |  Invalid network request. The request may be redirected to an unsupported scheme or an invalid URL.|
| SERVER_FAILED | 30 | The server returns a general error.|
| SERVER_NO_RANGE | 31 |  The server does not support the range request.|
| SERVER_BAD_CONTENT | 33 |   The server does not have the requested data.|
| SERVER_UNAUTHORIZED | 34 |  The file cannot be downloaded from the server.|
| SERVER_CERT_PROBLEM | 35 |  The server certificate is incorrect.|
| SERVER_FORBIDDEN | 36 |  The access to the server is forbidden.|
| SERVER_UNREACHABLE | 37 |  The server cannot be accessed.|
| SERVER_CONTENT_LENGTH_MISMATCH | 38 |  The received data does not match the content length.|
| SERVER_CROSS_ORIGIN_REDIRECT | 39 | An unexpected cross-site redirection occurs.|
| USER_CANCELED | 40 | The user cancels the download.|
| USER_SHUTDOWN | 41 | The user closes the application.|
| CRASH | 50 | The application crashes.|

## WebDownloadItem<sup>11+</sup>

 Implements a **WebDownloadItem** object. You can use this object to perform operations on the corresponding download task.

> **NOTE**
>
> During the download, the download process is notified to the user through **WebDownloadDelegate**. The user can operate the download task through the **WebDownloadItem** parameter.

### getGuid<sup>11+</sup>

getGuid(): string

Obtains the unique ID of this download task.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| string | Unique ID of the download task.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getCurrentSpeed<sup>11+</sup>

getCurrentSpeed(): number

Obtains the download speed, in bytes per second.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| number | Download speed, in bytes per second.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update current speed: " + webDownloadItem.getCurrentSpeed());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getPercentComplete<sup>11+</sup>

getPercentComplete(): number

Obtains the download progress. The value **100** indicates that the download is complete.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| number | Download progress. The value **100** indicates that the download is complete.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getTotalBytes<sup>11+</sup>

getTotalBytes(): number

Obtains the total length of the file to be downloaded.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| number | Total length of the file to be downloaded.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update total bytes: " + webDownloadItem.getTotalBytes());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getState<sup>11+</sup>

getState(): WebDownloadState

Obtains the download state.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| [WebDownloadState](#webdownloadstate11) | Download state.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update download state: " + webDownloadItem.getState());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getLastErrorCode<sup>11+</sup>

getLastErrorCode(): WebDownloadErrorCode

Obtains the download error code.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| [WebDownloadErrorCode](#webdownloaderrorcode11) | Error code returned when the download error occurs.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              console.log("download error code: " + webDownloadItem.getLastErrorCode());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getMethod<sup>11+</sup>

getMethod(): string

Obtains the request mode of this download task.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| string | Request mode of the download task.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("Download will start. Method:" + webDownloadItem.getMethod());
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getMimeType<sup>11+</sup>

getMimeType(): string

Obtains the MIME type of this download task (for example, a sound file may be marked as audio/ogg, and an image file may be image/png).

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| string | MIME type (for example, audio/ogg for a sound file, and image/png for an image file).|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("Download will start. MIME type:" + webDownloadItem.getMimeType());
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getUrl<sup>11+</sup>

getUrl(): string

Obtains the download request URL.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| string | Download request URL.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download, url:" + webDownloadItem.getUrl());
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getSuggestedFileName<sup>11+</sup>

getSuggestedFileName(): string

Obtains the suggested file name for this download task.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| string | Suggested file name.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download, suggest name:" + webDownloadItem.getSuggestedFileName());
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getReceivedBytes<sup>11+</sup>

getReceivedBytes(): number

Obtains the number of received bytes.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| number | Number of received bytes.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              console.log("download update received bytes: " + webDownloadItem.getReceivedBytes());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### getFullPath<sup>11+</sup>

getFullPath(): string

Obtains the full path of the downloaded file on the disk.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| string | Full path of the downloaded file on the disk.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
              console.log("download finish full path: " + webDownloadItem.getFullPath());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### serialize<sup>11+</sup>

serialize(): Uint8Array

Serializes the failed download to a byte array.

**System capability**: SystemCapability.Web.Webview.Core

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| Uint8Array | Byte array into which the failed download is serialized.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### deserialize<sup>11+</sup>

static deserialize(serializedData: Uint8Array): WebDownloadItem

Deserializes the serialized byte array into a **WebDownloadItem** object.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name             | Type   | Mandatory  |  Description|
| ------------------ | ------- | ---- | ------------- |
| serializedData | Uint8Array | Yes  | Byte array into which the download is serialized.|

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| [WebDownloadItem](#webdownloaditem11) | **WebDownloadItem** object.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### start<sup>11+</sup>

start(downloadPath: string): void

Starts a download. This API must be used in the **onBeforeDownload** callback of **WebDownloadDelegate**. If it is not called in the callback, the download task remains in the PENDING state.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name| Type                  | Mandatory| Description                            |
| ------ | ---------------------- | ---- | ------------------------------|
| downloadPath   | string     | Yes | Path (including the file name) of the file to download.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### cancel<sup>11+</sup>

cancel(): void

Cancels a download task.

**System capability**: SystemCapability.Web.Webview.Core

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  download: web_webview.WebDownloadItem = new web_webview.WebDownloadItem();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              this.download = webDownloadItem;
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('cancel')
        .onClick(() => {
          try {
            this.download.cancel();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### pause<sup>11+</sup>

pause(): void

Pauses a download task.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID | Error Message                                                     |
| -------- | ------------------------------------------------------------ |
| 17100019 | The download has not been started yet. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  download: web_webview.WebDownloadItem = new web_webview.WebDownloadItem();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              this.download = webDownloadItem;
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('cancel')
        .onClick(() => {
          try {
            this.download.cancel();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
        Button('pause')
        .onClick(() => {
          try {
            this.download.pause();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### resume<sup>11+</sup>

resume(): void

Resumes a download task.

**System capability**: SystemCapability.Web.Webview.Core

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID | Error Message                                                     |
| -------- | ------------------------------------------------------------ |
| 17100016 | The download is not paused. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  download: web_webview.WebDownloadItem = new web_webview.WebDownloadItem();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              this.download = webDownloadItem;
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('cancel')
        .onClick(() => {
          try {
            this.download.cancel();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('pause')
        .onClick(() => {
          try {
            this.download.pause();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resume')
        .onClick(() => {
          try {
            this.download.resume();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

## WebDownloadDelegate<sup>11+</sup>

 Implements a **WebDownloadDelegate** class. You can use the callbacks of this class to notify users of the download state.

### onBeforeDownload<sup>11+</sup>

onBeforeDownload(callback: Callback\<WebDownloadItem>): void

Invoked to notify users before the download starts. **WebDownloadItem.start("xxx")** must be called in this API, with a download path provided. Otherwise, the download remains in the PENDING state.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Parameter  | Type   | Mandatory | Description           |
| ------- | ------ | ---- | :------------- |
| callback | Callback\<[WebDownloadItem](#webdownloaditem11)> | Yes   | Callback that triggers the download. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  download: web_webview.WebDownloadItem = new web_webview.WebDownloadItem();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              this.download = webDownloadItem;
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('cancel')
        .onClick(() => {
          try {
            this.download.cancel();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('pause')
        .onClick(() => {
          try {
            this.download.pause();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resume')
        .onClick(() => {
          try {
            this.download.resume();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### onDownloadUpdated<sup>11+</sup>

onDownloadUpdated(callback: Callback\<WebDownloadItem>): void

Invoked when the download progress is updated.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Parameter  | Type   | Mandatory | Description           |
| ------- | ------ | ---- | :------------- |
| callback | Callback\<[WebDownloadItem](#webdownloaditem11)> | Yes   | Callback in which the download progress is updated. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  download: web_webview.WebDownloadItem = new web_webview.WebDownloadItem();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              this.download = webDownloadItem;
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('cancel')
        .onClick(() => {
          try {
            this.download.cancel();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('pause')
        .onClick(() => {
          try {
            this.download.pause();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resume')
        .onClick(() => {
          try {
            this.download.resume();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### onDownloadFinish<sup>11+</sup>

onDownloadFinish(callback: Callback\<WebDownloadItem>): void

Invoked when the download is complete.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Parameter  | Type   | Mandatory | Description           |
| ------- | ------ | ---- | :------------- |
| callback | Callback\<[WebDownloadItem](#webdownloaditem11)> | Yes   | Callback in which the download is complete. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  download: web_webview.WebDownloadItem = new web_webview.WebDownloadItem();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              this.download = webDownloadItem;
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('cancel')
        .onClick(() => {
          try {
            this.download.cancel();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('pause')
        .onClick(() => {
          try {
            this.download.pause();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resume')
        .onClick(() => {
          try {
            this.download.resume();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### onDownloadFailed<sup>11+</sup>

onDownloadFailed(callback: Callback\<WebDownloadItem>): void

Invoked when the download fails.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Parameter  | Type   | Mandatory | Description           |
| ------- | ------ | ---- | :------------- |
| callback | Callback\<[WebDownloadItem](#webdownloaditem11)> | Yes   | Callback in which the download fails. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  download: web_webview.WebDownloadItem = new web_webview.WebDownloadItem();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              this.download = webDownloadItem;
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('cancel')
        .onClick(() => {
          try {
            this.download.cancel();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('pause')
        .onClick(() => {
          try {
            this.download.pause();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resume')
        .onClick(() => {
          try {
            this.download.resume();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

## WebDownloadManager<sup>11+</sup>

Implements a **WebDownloadManager** class. You can use the APIs of this class to resume failed download tasks.

### setDownloadDelegate<sup>11+</sup>

static setDownloadDelegate(delegate: WebDownloadDelegate): void

Sets the delegate used to receive download progress triggered from **WebDownloadManager**.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name         | Type   |  Mandatory | Description                                           |
| ---------------| ------- | ---- | ------------- |
| delegate      | [WebDownloadDelegate](#webdownloaddelegate11)  | Yes  | Delegate used to receive the download progress.|

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  download: web_webview.WebDownloadItem = new web_webview.WebDownloadItem();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              this.download = webDownloadItem;
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('cancel')
        .onClick(() => {
          try {
            this.download.cancel();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('pause')
        .onClick(() => {
          try {
            this.download.pause();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resume')
        .onClick(() => {
          try {
            this.download.resume();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```

### resumeDownload<sup>11+</sup>

static resumeDownload(webDownloadItem: WebDownloadItem): void

Resumes a download task.

**System capability**: SystemCapability.Web.Webview.Core

**Parameters**

| Name         | Type   |  Mandatory | Description                                           |
| ---------------| ------- | ---- | ------------- |
| webDownloadItem      | [WebDownloadItem](#webdownloaditem11)  | Yes  | Download task to resume.|

**Error codes**

For details about the error codes, see [Webview Error Codes](errorcode-webview.md).

| ID| Error Message                             |
| -------- | ------------------------------------- |
| 17100018 | No WebDownloadDelegate has been set yet. |

**Example**

```ts
// xxx.ets
import web_webview from '@ohos.web.webview'
import business_error from '@ohos.base'

@Entry
@Component
struct WebComponent {
  controller: web_webview.WebviewController = new web_webview.WebviewController();
  delegate: web_webview.WebDownloadDelegate = new web_webview.WebDownloadDelegate();
  download: web_webview.WebDownloadItem = new web_webview.WebDownloadItem();
  failedData: Uint8Array = new Uint8Array();

  build() {
    Column() {
      Button('setDownloadDelegate')
        .onClick(() => {
          try {
            this.delegate.onBeforeDownload((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("will start a download.");
              // Pass in a download path and start the download.
              webDownloadItem.start("xxxxxxxx");
            })
            this.delegate.onDownloadUpdated((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download update percent complete: " + webDownloadItem.getPercentComplete());
              this.download = webDownloadItem;
            })
            this.delegate.onDownloadFailed((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download failed guid: " + webDownloadItem.getGuid());
              // Serialize the failed download to a byte array.
              this.failedData = webDownloadItem.serialize();
            })
            this.delegate.onDownloadFinish((webDownloadItem: web_webview.WebDownloadItem) => {
              console.log("download finish guid: " + webDownloadItem.getGuid());
            })
            this.controller.setDownloadDelegate(this.delegate);
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('startDownload')
        .onClick(() => {
          try {
            this.controller.startDownload('www.example.com');
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resumeDownload')
        .onClick(() => {
          try {
            web_webview.WebDownloadManager.resumeDownload(web_webview.WebDownloadItem.deserialize(this.failedData));
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('cancel')
        .onClick(() => {
          try {
            this.download.cancel();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('pause')
        .onClick(() => {
          try {
            this.download.pause();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Button('resume')
        .onClick(() => {
          try {
            this.download.resume();
          } catch (error) {
            let e:business_error.BusinessError = error as business_error.BusinessError;
            console.error(`ErrorCode: ${e.code},  Message: ${e.message}`);
          }
        })
      Web({ src: 'www.example.com', controller: this.controller })
    }
  }
}
```
 