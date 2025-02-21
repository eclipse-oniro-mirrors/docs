# 管理位置权限


Web组件提供位置权限管理能力。开发者可以通过[onGeolocationShow()](../reference/arkui-ts/ts-basic-components-web.md#ongeolocationshow)接口对某个网站进行位置权限管理。Web组件根据接口响应结果，决定是否赋予前端页面权限。获取设备位置，需要开发者配置[ohos.permission.LOCATION](../security/accesstoken-guidelines.md)权限，并同时在设备上打开应用的位置权限和控制中心的位置信息。


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
  import common from '@ohos.app.ability.common';
  import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
  import geoLocationManager from '@ohos.geoLocationManager';

  let context = getContext(this) as common.UIAbilityContext;
  let atManager = abilityAccessCtrl.createAtManager();

  try{
    atManager.requestPermissionsFromUser(context, ["ohos.permission.APPROXIMATELY_LOCATION"], (err, data) => {
      let requestInfo: geoLocationManager.LocationRequest = {
        'priority': 0x203,
        'scenario': 0x300,
        'maxAccuracy': 0
      };
      let locationChange = (location: geoLocationManager.Location):void => {
        if(location){
          console.log('locationChanger: location=' + JSON.stringify(location));
        }
      };
      try{
        geoLocationManager.on('locationChange', requestInfo, locationChange);
        geoLocationManager.off('locationChange', locationChange);
      } catch (err) {
        console.error("errCode:" + err.code + ", errMessage:" + err.message);
      }
    })
  } catch (err) {
    console.error("err:", err);
  }

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
                  if(event){
                  event.geolocation.invoke(event.origin, false, false);   // 不允许此站点地理位置权限请求
                  }
                }
              },
              secondaryButton: {
                value: 'ok',
                action: () => {
                  if(event){
                  event.geolocation.invoke(event.origin, true, false);    // 允许此站点地理位置权限请求
                  }                
                }
              },
              cancel: () => {
                if(event){
                event.geolocation.invoke(event.origin, false, false);   // 不允许此站点地理位置权限请求
                }
              }
            })
          })
      }
    }
  }
  ```
