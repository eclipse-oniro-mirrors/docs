# ArkWeb_ControllerAPI


## 概述

Controller相关的Native API结构体。 在调用API前建议通过ARKWEB_MEMBER_MISSING校验该函数结构体是否有对应函数指针，避免SDK与设备ROM不匹配导致crash问题。

**起始版本：** 12

**相关模块：**[Web](_web.md)


## 汇总


### 成员变量

| 名称 | 描述 | 
| -------- | -------- |
| size_t [size](#size) | 结构体的大小。  | 
| void(\* [runJavaScript](#runjavascript) )(const char \*webTag, const [ArkWeb_JavaScriptObject](_ark_web___java_script_object.md) \*javascriptObject) | 注入JavaScript脚本。  | 
| void(\* [registerJavaScriptProxy](#registerjavascriptproxy) )(const char \*webTag, const [ArkWeb_ProxyObject](_ark_web___proxy_object.md) \*proxyObject) | 注入JavaScript对象到window对象中，并在window对象中调用该对象的同步方法。  | 
| void(\* [deleteJavaScriptRegister](#deletejavascriptregister) )(const char \*webTag, const char \*objName) | 删除通过registerJavaScriptProxy注册到window上的指定name的应用侧JavaScript对象。  | 
| void(\* [refresh](#refresh) )(const char \*webTag) | 刷新当前网页。  | 
| void(\* [registerAsyncJavaScriptProxy](#registerasyncjavascriptproxy) )(const char \*webTag, const [ArkWeb_ProxyObject](_ark_web___proxy_object.md) \*proxyObject) | 注入JavaScript对象到window对象中，并在window对象中调用该对象的异步方法。  | 
| [ArkWeb_WebMessagePortPtr](_web.md#arkweb_webmessageportptr) \*(\* [createWebMessagePorts](#createwebmessageports) )(const char \*webTag, size_t \*[size](#size)) | 创建Post Message端口。  | 
| void(\* [destroyWebMessagePorts](#destroywebmessageports) )([ArkWeb_WebMessagePortPtr](_web.md#arkweb_webmessageportptr) \*\*ports, size_t [size](#size)) | 销毁端口。  | 
| [ArkWeb_ErrorCode](_web.md#arkweb_errorcode)(\* [postWebMessage](#postwebmessage) )(const char \*webTag, const char \*name, [ArkWeb_WebMessagePortPtr](_web.md#arkweb_webmessageportptr) \*webMessagePorts, size_t [size](#size), const char \*url) | 将端口发送到HTML主页面.  | 


## 结构体成员变量说明


### createWebMessagePorts

```
ArkWeb_WebMessagePortPtr*(* ArkWeb_ControllerAPI::createWebMessagePorts) (const char *webTag, size_t *size)
```
**描述：**

创建Post Message端口。

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| webTag | Web组件名字。  | 
| size | 出参，端口数量。  | 

**返回：**

Post Message端口结构体指针。


### deleteJavaScriptRegister

```
void(* ArkWeb_ControllerAPI::deleteJavaScriptRegister) (const char *webTag, const char *objName)
```
**描述：**

删除通过registerJavaScriptProxy注册到window上的指定name的应用侧JavaScript对象。


### destroyWebMessagePorts

```
void(* ArkWeb_ControllerAPI::destroyWebMessagePorts) (ArkWeb_WebMessagePortPtr *ports, size_t *size)
```
**描述：**

销毁端口。

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| ports | Message端口结构体指针数组。  | 
| size | 端口数量。 | 


### postWebMessage

```
ArkWeb_ErrorCode(* ArkWeb_ControllerAPI::postWebMessage) (const char *webTag, const char *name, ArkWeb_WebMessagePortPtr *webMessagePorts, size_t size, const char *url)
```
**描述：**

将端口发送到HTML主页面.

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| webTag | Web组件名字。  | 
| name | 发送给HTML的消息名称。  | 
| webMessagePorts | Post Message端口结构体指针。  | 
| size | 端口数量。  | 
| url | 接收到消息的页面url。  | 

**返回：**

返回值错误码。 [ARKWEB_SUCCESS](_web.md) 执行成功。 [ARKWEB_INVALID_PARAM](_web.md) 参数无效。 [ARKWEB_INIT_ERROR](_web.md) 初始化失败，没有找到与webTag绑定的Web组件。


### refresh

```
void(* ArkWeb_ControllerAPI::refresh) (const char *webTag)
```
**描述：**

刷新当前网页。


### registerAsyncJavaScriptProxy

```
void(* ArkWeb_ControllerAPI::registerAsyncJavaScriptProxy) (const char *webTag, const ArkWeb_ProxyObject *proxyObject)
```
**描述：**

注入JavaScript对象到window对象中，并在window对象中调用该对象的异步方法。


### registerJavaScriptProxy

```
void(* ArkWeb_ControllerAPI::registerJavaScriptProxy) (const char *webTag, const ArkWeb_ProxyObject *proxyObject)
```
**描述：**

注入JavaScript对象到window对象中，并在window对象中调用该对象的同步方法。


### runJavaScript

```
void(* ArkWeb_ControllerAPI::runJavaScript) (const char *webTag, const ArkWeb_JavaScriptObject *javascriptObject)
```
**描述：**

注入JavaScript脚本。


### size

```
size_t ArkWeb_ControllerAPI::size
```
**描述：**

结构体的大小。
