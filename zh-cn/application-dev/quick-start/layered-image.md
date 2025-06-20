# 配置应用图标

应用图标分为分层图标和单层图标，分层图标包括前景图和背景图两层，本页面提供应用图标的配置指导。图标规范详见<!--RP1-->[图标交付](https://docs.openharmony.cn/pages/v5.0/zh-cn/design/ux-design/visual-app-icons.md#%E5%9B%BE%E6%A0%87%E4%BA%A4%E4%BB%98)<!--RP1End-->，图标配置规则详见[图标配置](../application-models/application-component-configuration-stage.md#图标和标签配置)。

## 配置分层图标

应用图标如果采用分层图标（包括前景图和背景图两层），可以参考本章节进行配置。

1. 将前景资源和背景资源文件放在“AppScope\resources\base\media”文件下。
   本例中采用的前景资源和背景资源的文件名分别为“foreground.png”和“background.png”。
2. 在“AppScope\resources\base\media”文件夹下创建layered_image.json文件，并在该文件中配置分层图标的前景资源与背景资源信息。
    ```json
    {
      "layered-image":
      {
        "background" : "$media:background",
        "foreground" : "$media:foreground"
      }
    }
    ```
3. 在[app.json5配置文件](app-configuration-file.md)中引用分层图标资源文件。示例如下：
     ```json
        {
          "app": {
            "icon": "$media:layered_image",
            // ...
          }
        }
    ```
4. 如果在module.json5配置文件的[abilities标签](module-configuration-file.md#abilities标签)中配置了icon和label，且该对应的ability中skills标签下面的entities中包含"entity.system.home"、actions中包含"ohos.want.action.home"或者"action.system.home"，在module.json5文件中，需要将abilities标签下的icon配置值修改为分层图标的资源配置路径。配置要求参考[图标生成机制](../application-models/application-component-configuration-stage.md#生成机制)。

     ```json
        {
          "module": {
            "abilities": [
              "name": "EntryAbility",
              // ...
              "icon": "$media:layered_image", // 修改icon的配置为分层图标的资源配置路径
              "skills": [
                {
                  "entities": [
                    "entity.system.home"
                  ],
                  "actions": [
                    "ohos.want.action.home"
                  ]
                }
              ],
              // ...
            ]
            // ...
          }
        }
    ```

## 配置单层图标

应用如果配置单层图标，请参考[配置示例](../application-models/application-component-configuration-stage.md#配置示例)。
