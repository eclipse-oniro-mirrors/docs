# 构建弹窗


使用弹窗控制器显示自定义弹窗，设置其样式和内容。


弹窗接口集合定义在结构体里，命名为ArkUI_NativeDialogAPI_x （x表示版本），用于实现各种弹窗控制。
[OH_ArkUI_QueryModuleInterfaceByName](../reference/apis-arkui/_ark_u_i___native_module.md#oh_arkui_querymoduleinterfacebyname)用于获取指定类型的Native模块接口集合，可以通过其返回ArkUI_NativeDialogHandle类型的数据调用Native模块中的接口。


## 创建和销毁弹窗控制器

- 创建弹窗控制器
  [ArkUI_NativeDialogHandle](../reference/apis-arkui/_ark_u_i___native_module.md#arkui_nativedialoghandle)表示指向弹窗控制器的指针，可以通过调用[ArkUI_NativeDialogAPI_x](../reference/apis-arkui/_ark_u_i___native_dialog_a_p_i__1.md)的[create](../reference/apis-arkui/_ark_u_i___native_dialog_a_p_i__1.md#create)接口创建一个弹窗控制器。

  该方法返回ArkUI_NativeDialogHandle类型的数据。
  ```
  ArkUI_NativeDialogAPI_1 *dialogAPI = reinterpret_cast<ArkUI_NativeDialogAPI_1 *>(
      OH_ArkUI_QueryModuleInterfaceByName(ARKUI_NATIVE_DIALOG, "ArkUI_NativeDialogAPI_1"));
  auto dialogController = dialogAPI->create();
  ```

- 销毁弹窗控制器
  当不再需要弹窗操作时，需要主动调用dispose接口销毁弹窗控制器对象。
  ```
  ArkUI_NativeDialogAPI_1 *dialogAPI = reinterpret_cast<ArkUI_NativeDialogAPI_1 *>(
      OH_ArkUI_QueryModuleInterfaceByName(ARKUI_NATIVE_DIALOG, "ArkUI_NativeDialogAPI_1"));
  dialogAPI->dispose(dialogController);
  ```


## 设置弹窗样式

可以设置弹窗对齐方式、偏移量，弹窗背板圆角弧度、背景色、蒙层颜色以及区域等。

1. 创建弹窗内容节点。
   ```
   ArkUI_NodeHandle CreateDialogContent() {
       ArkUI_NativeNodeAPI_1 *nodeAPI = reinterpret_cast<ArkUI_NativeNodeAPI_1 *>(
           OH_ArkUI_QueryModuleInterfaceByName(ARKUI_NATIVE_NODE, "ArkUI_NativeNodeAPI_1"));
       ArkUI_NodeHandle text = nodeAPI->createNode(ARKUI_NODE_TEXT);
       ArkUI_NumberValue textWidthValue[] = {{.f32 = 300}};
       ArkUI_AttributeItem textWidthItem = {.value = textWidthValue,
                                            .size = sizeof(textWidthValue) / sizeof(ArkUI_NumberValue)};
       nodeAPI->setAttribute(text, NODE_WIDTH, &textWidthItem);
       ArkUI_NumberValue textHeightValue[] = {{.f32 = 300}};
       ArkUI_AttributeItem textHeightItem = {.value = textHeightValue,
                                             .size = sizeof(textWidthValue) / sizeof(ArkUI_NumberValue)};
       nodeAPI->setAttribute(text, NODE_HEIGHT, &textHeightItem);
       ArkUI_NodeHandle span = nodeAPI->createNode(ARKUI_NODE_SPAN);
       ArkUI_AttributeItem spanItem = {.string = "这是一个弹窗"};
       nodeAPI->setAttribute(span, NODE_SPAN_CONTENT, &spanItem);
       ArkUI_NodeHandle imageSpan = nodeAPI->createNode(ARKUI_NODE_IMAGE_SPAN);
       ArkUI_AttributeItem imageSpanItem = {.string = "/pages/common/sky.jpg"};
       nodeAPI->setAttribute(imageSpan, NODE_IMAGE_SPAN_SRC, &imageSpanItem);
       ArkUI_NumberValue imageSpanWidthValue[] = {{.f32 = 300}};
       ArkUI_AttributeItem imageSpanWidthItem = {.value = imageSpanWidthValue,
                                                 .size = sizeof(textWidthValue) / sizeof(ArkUI_NumberValue)};
       nodeAPI->setAttribute(imageSpan, NODE_WIDTH, &imageSpanWidthItem);
       ArkUI_NumberValue imageSpanHeightValue[] = {{.f32 = 200}};
       ArkUI_AttributeItem imageSpanHeightItem = {.value = imageSpanHeightValue,
                                                  .size = sizeof(textWidthValue) / sizeof(ArkUI_NumberValue)};
       nodeAPI->setAttribute(imageSpan, NODE_HEIGHT, &imageSpanHeightItem);
       nodeAPI->addChild(text, span);
       nodeAPI->addChild(text, imageSpan);
       return text;
   }
   ```

2. 通过controller控制弹窗样式。弹窗接口清单和描述可查看[native_dialog.h](../reference/apis-arkui/native__dialog_8h.md)。
   ```
   void ShowDialog() {
       ArkUI_NativeDialogAPI_1 *dialogAPI = reinterpret_cast<ArkUI_NativeDialogAPI_1 *>(
           OH_ArkUI_QueryModuleInterfaceByName(ARKUI_NATIVE_DIALOG, "ArkUI_NativeDialogAPI_1"));
       if (!dialogController) {
           dialogController = dialogAPI->create();
       }
       auto contentNode = CreateDialogContent();
       dialogAPI->setContent(dialogController, contentNode);
       dialogAPI->setContentAlignment(dialogController, static_cast<int32_t>(ARKUI_ALIGNMENT_BOTTOM), 0, 0);
       dialogAPI->setBackgroundColor(dialogController, 0xffffffff);
       dialogAPI->setCornerRadius(dialogController, 6, 6, 6, 6);
       dialogAPI->setModalMode(dialogController, false);
       dialogAPI->setAutoCancel(dialogController, true);
       dialogAPI->show(dialogController, false);
   }
   ```

3. 不需要弹窗时关闭弹窗。
   ```
   void CloseDialog() {
       ArkUI_NativeDialogAPI_1 *dialogAPI = reinterpret_cast<ArkUI_NativeDialogAPI_1 *>(
           OH_ArkUI_QueryModuleInterfaceByName(ARKUI_NATIVE_DIALOG, "ArkUI_NativeDialogAPI_1"));
       dialogAPI->close(dialogController);
   }
   ```


## 弹窗的交互

可创建交互页面，打开或关闭弹窗。

1. 创建可交互界面，点击Button后弹窗。其中获取与使用ArkUI_NodeContentHandle类型节点可参考[接入ArkTS页面](ndk-access-the-arkts-page.md)。
   ```
   constexpr int32_t BUTTON_CLICK_ID = 1;
   bool isShown = false;
   ArkUI_NativeDialogHandle dialogController;
   ArkUI_NodeHandle buttonNode;
   
   void MainViewMethod(ArkUI_NodeContentHandle handle) {
       ArkUI_NativeNodeAPI_1 *nodeAPI = reinterpret_cast<ArkUI_NativeNodeAPI_1 *>(
           OH_ArkUI_QueryModuleInterfaceByName(ARKUI_NATIVE_NODE, "ArkUI_NativeNodeAPI_1"));
       ArkUI_NodeHandle column = nodeAPI->createNode(ARKUI_NODE_COLUMN);
       ArkUI_NumberValue widthValue[] = {{.f32 = 300}};
       ArkUI_AttributeItem widthItem = {.value = widthValue, .size = sizeof(widthValue) / sizeof(ArkUI_NumberValue)};
       nodeAPI->setAttribute(column, NODE_WIDTH, &widthItem);
       ArkUI_NumberValue heightValue[] = {{.f32 = 300}};
       ArkUI_AttributeItem heightItem = {.value = heightValue, .size = sizeof(heightValue) / sizeof(ArkUI_NumberValue)};
       nodeAPI->setAttribute(column, NODE_HEIGHT, &heightItem);
       
       buttonNode = nodeAPI->createNode(ARKUI_NODE_BUTTON);
       ArkUI_NumberValue buttonWidthValue[] = {{.f32 = 200}};
       ArkUI_AttributeItem buttonWidthItem = {.value = buttonWidthValue,
                                              .size = sizeof(buttonWidthValue) / sizeof(ArkUI_NumberValue)};
       nodeAPI->setAttribute(buttonNode, NODE_WIDTH, &buttonWidthItem);
       ArkUI_NumberValue buttonHeightValue[] = {{.f32 = 50}};
       ArkUI_AttributeItem buttonHeightItem = {.value = buttonHeightValue,
                                               .size = sizeof(buttonHeightValue) / sizeof(ArkUI_NumberValue)};
       nodeAPI->setAttribute(buttonNode, NODE_HEIGHT, &buttonHeightItem);
       ArkUI_AttributeItem labelItem = {.string = "点击弹窗"};
       nodeAPI->setAttribute(buttonNode, NODE_BUTTON_LABEL, &labelItem);
       ArkUI_NumberValue buttonTypeValue[] = {{.i32 = static_cast<int32_t>(ARKUI_BUTTON_TYPE_NORMAL)}};
       ArkUI_AttributeItem buttonTypeItem = {.value = buttonTypeValue,
                                             .size = sizeof(buttonTypeValue) / sizeof(ArkUI_NumberValue)};
       nodeAPI->setAttribute(buttonNode, NODE_BUTTON_TYPE, &buttonTypeItem);
       nodeAPI->registerNodeEvent(buttonNode, NODE_ON_CLICK, BUTTON_CLICK_ID, nullptr);
       nodeAPI->addNodeEventReceiver(buttonNode, OnButtonClicked);
       nodeAPI->addChild(column, buttonNode);
       OH_ArkUI_NodeContent_AddNode(handle, column);
   }
   ```

2. 创建Button事件的回调函数，当Button点击时触发弹窗显示或关闭。
   ```
   void OnButtonClicked(ArkUI_NodeEvent *event) {
       if (!event || !buttonNode) {
           return;
       }
       auto eventId = OH_ArkUI_NodeEvent_GetTargetId(event);
       if (eventId == BUTTON_CLICK_ID) {
           ArkUI_NativeNodeAPI_1 *nodeAPI = reinterpret_cast<ArkUI_NativeNodeAPI_1 *>(
               OH_ArkUI_QueryModuleInterfaceByName(ARKUI_NATIVE_NODE, "ArkUI_NativeNodeAPI_1"));
           if (isShown) {
               isShown = false;
               ArkUI_AttributeItem labelItem = {.string = "显示弹窗"};
               nodeAPI->setAttribute(buttonNode, NODE_BUTTON_LABEL, &labelItem);
               CloseDialog();
           } else {
               isShown = true;
               ArkUI_AttributeItem labelItem = {.string = "关闭弹窗"};
               nodeAPI->setAttribute(buttonNode, NODE_BUTTON_LABEL, &labelItem);
               ShowDialog();
           }
       }
   }
   ```

   ![zh-cn_image_0000001902966196](figures/zh-cn_image_0000001902966196.gif)
