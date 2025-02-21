# 管理位置权限


Web组件提供位置权限管理能力。开发者可以通过[onGeolocationShow()](../reference/apis-arkweb/ts-basic-components-web.md#ongeolocationshow)接口对某个网站进行位置权限管理。Web组件根据接口响应结果，决定是否赋予前端页面权限。获取设备位置，需要开发者配置[ohos.permission.LOCATION](../security/AccessToken/request-user-authorization.md)，[ohos.permission.APPROXIMATELY_LOCATION](../security/AccessToken/request-user-authorization.md)权限，并同时在设备上打开应用的位置权限和控制中心的位置信息。


在下面的示例中，用户点击前端页面"获取位置"按钮，Web组件通过弹窗的形式通知应用侧位置权限请求消息。


- 前端页面代码。

  ```html
  <!DOCTYPE html>
  <html>
  <body>
  <p id="locationInfo">位置信息</p>
  <button onclick="getLocation()">获取位置</button>
  <script>
  var locationInfo=document.getElementById("locationInfo");
  function getLocation(){
    if (navigator.geolocation) {
      <!-- 前端页面访问设备地理位置 -->
      navigator.geolocation.getCurrentPosition(showPosition);
    }
  }
  function showPosition(position){
    locationInfo.innerHTML="Latitude: " + position.coords.latitude + "<br />Longitude: " + position.coords.longitude;
  }
  </script>
  </body>
  </html>
  ```


- 应用代码。

  ```ts
  // xxx.ets
  import web_webview from '@ohos.web.webview';
  import { abilityAccessCtrl, common } from '@kit.AbilityKit';
  import { BusinessError } from '@ohos.base';

  let context = getContext(this) as common.UIAbilityContext;
  let atManager = abilityAccessCtrl.createAtManager();

  // 向用户请求位置权限设置。
  atManager.requestPermissionsFromUser(context, ["ohos.permission.APPROXIMATELY_LOCATION"]).then((data) => {
    console.info('data:' + JSON.stringify(data));
    console.info('data permissions:' + data.permissions);
    console.info('data authResults:' + data.authResults);
  }).catch((error: BusinessError) => {
    console.error(`Failed to request permissions from user. Code is ${error.code}, message is ${error.message}`);
  })

  @Entry
  @Component
  struct WebComponent {
    controller: web_webview.WebviewController = new web_webview.WebviewController();
    build() {
      Column() {
        Web({ src:$rawfile('getLocation.html'), controller:this.controller })
          .geolocationAccess(true)
          .onGeolocationShow((event) => {  // 地理位置权限申请通知
            AlertDialog.show({
              title: '位置权限请求',
              message: '是否允许获取位置信息',
              primaryButton: {
                value: 'cancel',
                action: () => {
                  if (event) {
                    event.geolocation.invoke(event.origin, false, false);   // 不允许此站点地理位置权限请求
                  }
                }
              },
              secondaryButton: {
                value: 'ok',
                action: () => {
                  if (event) {
                    event.geolocation.invoke(event.origin, true, false);    // 允许此站点地理位置权限请求
                  }
                }
              },
              cancel: () => {
                if (event) {
                  event.geolocation.invoke(event.origin, false, false);   // 不允许此站点地理位置权限请求
                }
              }
            })
          })
      }
    }
  }
  ```
