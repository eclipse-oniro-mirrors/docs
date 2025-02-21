# Alert Dialog Box (AlertDialog)

You can set the text content and response callback for an alert dialog box.

>  **NOTE**
>
> The APIs of this module are supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.
>
> The functionality of this module depends on UI context. This means that the APIs of this module cannot be used where the UI context is unclear. For details, see [UIContext](../js-apis-arkui-UIContext.md#uicontext).
>
> Since API version 10, you can use the [showAlertDialog](../js-apis-arkui-UIContext.md#showalertdialog) API in [UIContext](../js-apis-arkui-UIContext.md#uicontext) to obtain the UI context.

## AlertDialog.show

static show(value: AlertDialogParamWithConfirm | AlertDialogParamWithButtons | AlertDialogParamWithOptions)

Shows an alert dialog box.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type | Mandatory| Description|
| ---- | --------------- | -------- | -------- |
| value | [AlertDialogParamWithConfirm](#alertdialogparamwithconfirm) \| [AlertDialogParamWithButtons](#alertdialogparamwithbuttons) \| [AlertDialogParamWithOptions](#alertdialogparamwithoptions10)<sup>10+</sup> | Yes| Defines and displays the **\<AlertDialog>** component.|

## AlertDialogParam

| Name                             | Type                                                        | Mandatory| Description                                                        |
| --------------------------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| title                             | [ResourceStr](ts-types.md#resourcestr)                       | No  | Title of the dialog box.                                                 |
| subtitle<sup>10+</sup>            | [ResourceStr](ts-types.md#resourcestr)                       | No  | Subtitle of the dialog box.                                                |
| message                           | [ResourceStr](ts-types.md#resourcestr)                       | Yes  | Content of the dialog box.                                                |
| autoCancel                        | boolean                                                      | No  | Whether to close the dialog box when the overlay is clicked. The value **true** means to close the dialog box when the overlay is clicked, and **false** means the opposite.<br>Default value: **true**|
| cancel                            | () =&gt; void                                      | No  | Callback invoked when the dialog box is closed after the overlay is clicked.                              |
| alignment                         | [DialogAlignment](#dialogalignment)                  | No  | Alignment mode of the dialog box in the vertical direction.<br>Default value: **DialogAlignment.Default**<br>**NOTE**<br>If **showInSubWindow** is set to **true** in **UIExtension**, the dialog box is aligned with the host window based on **UIExtension**.|
| offset                            | [Offset](ts-types.md#offset)                                 | No  | Offset of the dialog box relative to the alignment position.<br>Default value: **{ dx: 0 , dy: 0 }**|
| gridCount                         | number                                                       | No  | Number of grid columns occupied by the width of the dialog box.<br>Default value: **4**                   |
| maskRect<sup>10+</sup>            | [Rectangle](#rectangle8)                             | No  | Mask area of the dialog box. Events outside the mask area are transparently transmitted, and events within the mask area are not.<br>Default value: **{ x: 0, y: 0, width: '100%', height: '100%' }**<br>**NOTE**<br>**maskRect** does not take effect when **showInSubWindow** is set to **true**.|
| showInSubWindow<sup>11+</sup>     | boolean                                                      | No  | Whether to show the dialog box in a sub-window when the dialog box needs to be displayed outside the main window.<br>Default value: **false**<br>**NOTE**<br>A dialog box whose **showInSubWindow** attribute is **true** cannot trigger the display of another dialog box whose **showInSubWindow** attribute is also **true**.|
| isModal<sup>11+</sup>             | boolean                                                      | No  | Whether the dialog box is a modal. A modal dialog box has a mask applied, while a non-modal dialog box does not.<br>Default value: **true**|
| backgroundColor<sup>11+</sup>     | [ResourceColor](ts-types.md#resourcecolor)                   | No  | Background color of the dialog box.<br>Default value: **Color.Transparent**                |
| backgroundBlurStyle<sup>11+</sup> | [BlurStyle](ts-appendix-enums.md#blurstyle9)                 | No  | Background blur style of the dialog box.<br>Default value: **BlurStyle.COMPONENT_ULTRA_THICK**|

## AlertDialogParamWithConfirm

Inherits from [AlertDialogParam](#alertdialogparam).

| Name      | Type    | Mandatory    | Description        |
| ---------- | ---------------- | ---------- | ------------------------------- |
| confirm    | {<br>enabled<sup>10+</sup>?: boolean,<br>defaultFocus<sup>10+</sup>?: boolean,<br>style<sup>10+</sup>?: [DialogButtonStyle](#dialogbuttonstyle10),<br>value: [ResourceStr](ts-types.md#resourcestr),<br>fontColor?: [ResourceColor](ts-types.md#resourcecolor),<br>backgroundColor?:  [ResourceColor](ts-types.md#resourcecolor),<br>action: () =&gt; void<br>} | No  | Information about the confirm button. <br>**enabled**: whether to respond when the button is clicked. The value **true** means to respond when the button is clicked, and **false** means the opposite.<br>Default value: **true**<br>**defaultFocus**: whether the button is the default focus. The value **true** means that the button is the default focus, and **false** means the opposite.<br>Default value: **false**<br>**style**: button style.<br>Default value: **DialogButtonStyle.DEFAULT**<br>**value**: button text.<br>**fontColor**: font color of the button.<br>**backgroundColor**: background color of the button.<br>**action**: callback upon button clicking.|

Priorities of the **confirm** parameters: **fontColor** and **backgroundColor** > **style** > **defaultFocus**

| backgroundColor | fontColor | style                       | defaultFocus | Effect    |
| --------------- | --------- | --------------------------- | ------------ | -------- |
| Green           | Red     | -                           | -            | Red text on green background|
| Green           | -         | DialogButtonStyle.HIGHLIGHT | -            | White text on green background|
| Green           | -         | DialogButtonStyle.DEFAULT   | -            | Blue text on green background|
| Green           | -         | -                           | TRUE         | White text on green background|
| Green           | -         | -                           | FALSE/-      | Blue text on green background|
| -               | Red     | DialogButtonStyle.HIGHLIGHT | -            | Red text on blue background|
| -               | Red     | DialogButtonStyle.DEFAULT   | -            | Red text on white background|
| -               | Red     | -                           | TRUE         | Red text on blue background|
| -               | Red     | -                           | FALSE/-      | Red text on white background|
| -               | -         | DialogButtonStyle.HIGHLIGHT | -            | White text on blue background|
| -               | -         | DialogButtonStyle.DEFAULT   | -            | Blue text on white background|
| -               | -         | -                           | TRUE         | White text on blue background|
| -               | -         | -                           | FALSE/-      | Blue text on white background|

## AlertDialogParamWithButtons

Inherits from [AlertDialogParam](#alertdialogparam).

| Name            | Type               | Mandatory    | Description                    |
| --------------- | ---------------------- | ------------ | --------------------- |
| primaryButton   | {<br>enabled<sup>10+</sup>?: boolean,<br>defaultFocus<sup>10+</sup>?: boolean,<br>style<sup>10+</sup>?: [DialogButtonStyle](#dialogbuttonstyle10),<br>value: [ResourceStr](ts-types.md#resourcestr),<br>fontColor?: [ResourceColor](ts-types.md#resourcecolor),<br>backgroundColor?: [ResourceColor](ts-types.md#resourcecolor),<br>action: () =&gt; void;<br>} | No| Information about the confirm button. <br>**enabled**: whether to respond when the button is clicked.<br>Default value: **true**<br>**defaultFocus**: whether the button is the default focus.<br>Default value: **false**<br>**style**: button style.<br>Default value: **DialogButtonStyle.DEFAULT**<br>**value**: button text.<br>**fontColor**: font color of the button.<br>**backgroundColor**: background color of the button.<br>**action**: callback upon button clicking.|
| secondaryButton | {<br>enabled<sup>10+</sup>?: boolean,<br>defaultFocus<sup>10+</sup>?: boolean,<br>style<sup>10+</sup>?: [DialogButtonStyle](#dialogbuttonstyle10),<br>value: [ResourceStr](ts-types.md#resourcestr),<br>fontColor?: [ResourceColor](ts-types.md#resourcecolor),<br>backgroundColor?: [ResourceColor](ts-types.md#resourcecolor),<br>action: () =&gt; void;<br>} | No | Information about the confirm button.<br>**enabled**: whether to respond when the button is clicked.<br>Default value: **true**<br>**defaultFocus**: whether the button is the default focus.<br>Default value: **false**<br>**style**: button style.<br>Default value: **DialogButtonStyle.DEFAULT**<br>**value**: button text.<br>**fontColor**: font color of the button.<br>**backgroundColor**: background color of the button.<br>**action**: callback upon button clicking.|

## AlertDialogParamWithOptions<sup>10+</sup>

Inherits from [AlertDialogParam](#alertdialogparam).

| Name            | Type               | Mandatory    | Description                    |
| --------------- | ---------------------- | ------------ | --------------------- |
| buttons<sup>10+</sup>       | Array&lt;[AlertDialogButtonOptions](#alertdialogbuttonoptions10)&gt;                 | Yes | Buttons in the dialog box.|
|buttonDirection<sup>10+</sup>      | [DialogButtonDirection](#dialogbuttondirection10)| No | Direction in which buttons are laid out.<br>Default value: **DialogButtonDirection.AUTO**<br>When there are more than three buttons, the Auto mode (which automatically switches to the vertical layout when there are more than two buttons) is recommended. In non-Auto mode, buttons that extend beyond the display area are clipped.|

## AlertDialogButtonOptions<sup>10+</sup>
| Name            | Type               | Mandatory    | Description                    |
| ------------------| ---------------------- | ------------ | --------------------- |
| enabled           | boolean | No    | Whether to respond when the button is clicked.<br>Default value: **true**       |
| defaultFocus           | boolean | No    | Whether the button is the default focus.<br>Default value: **false**       |
| style           | [DialogButtonStyle](#dialogbuttonstyle10) | No    | Style of the button.<br>Default value: **DialogButtonStyle.DEFAULT**       |
| value           | [ResourceStr](ts-types.md#resourcestr) | Yes    | Text of the button. If the value is null, the button is not displayed.        |
| fontColor           | [ResourceColor](ts-types.md#resourcecolor) | No    | Font color of the button.       |
| backgroundColor           | [ResourceColor](ts-types.md#resourcecolor) | No    | Background color of the button.       |
| action           | 	() => void | Yes    | Callback upon button clicking.       |

## DialogButtonDirection<sup>10+</sup>
| Name                      | Description     |
| -------------------------- | --------- |
| AUTO                      | Buttons are laid out horizontally when there are two or fewer buttons and vertically otherwise.|
| HORIZONTAL                      | Buttons are laid out horizontally.|
| VERTICAL                      | Buttons are laid out vertically.|

## DialogAlignment

| Name                      | Description     |
| ------------------------ | ------- |
| Top                      | Vertical top alignment.|
| Center                   | Vertical center alignment.|
| Bottom                   | Vertical bottom alignment.|
| Default                  | Default alignment.  |
| TopStart<sup>8+</sup>    | Top left alignment.  |
| TopEnd<sup>8+</sup>      | Top right alignment.  |
| CenterStart<sup>8+</sup> | Center left alignment.  |
| CenterEnd<sup>8+</sup>   | Center right alignment.  |
| BottomStart<sup>8+</sup> | Bottom left alignment.  |
| BottomEnd<sup>8+</sup>   | Bottom right alignment.  |

## Rectangle<sup>8+</sup>

The **Rectangle** type is used to represent a mask area of a dialog box.

| Name    | Type                          | Mandatory| Description                               |
|--------|------------------------------|----|-----------------------------------|
| x      | [Length](ts-types.md#length) | No | X coordinate of the mask area of the dialog box relative to the upper left corner of the window.<br>Default value: **0vp**|
| y      | [Length](ts-types.md#length) | No | Y coordinate of the mask area of the dialog box relative to the upper left corner of the window.<br>Default value: **0vp**|
| width  | [Length](ts-types.md#length) | No | Width of the mask area of the dialog box.<br>Default value: **'100%'**       |
| height | [Length](ts-types.md#length) | No | Height of the mask area of the dialog box.<br>Default value: **'100%'**       |

>  **NOTE**
>
>  **x** and **y** can be set to a positive or negative percentage value. When **x** is set to **'100%'**, the mask area is moved rightward by the window width. When **x** is set to **'-100%'**, the mask area is moved leftward by the window width. When **y** is set to **'100%'**, the mask area is moved downward by the window height. When **y** is set to **'-100%'**, the mask area is moved upward by the window height.
>
>  **width** and **height** can be set in percentage and can only be set to positive values. If they are set to negative values, the default values are used instead.
>
>  The percentage is calculated based on the width and height of the window.

## DialogButtonStyle<sup>10+</sup>

| Name     | Description                             |
| --------- | --------------------------------- |
| DEFAULT   | Blue text on white background (black background under the dark theme).|
| HIGHLIGHT | White text on blue background.                       |

## Example

### Example 1

```ts
// xxx.ets
@Entry
@Component
struct AlertDialogExample {
  build() {
    Column({ space: 5 }) {
      Button('one button dialog')
        .onClick(() => {
          AlertDialog.show(
            {
              title: 'title',
              message: 'text',
              autoCancel: true,
              alignment: DialogAlignment.Bottom,
              offset: { dx: 0, dy: -20 },
              gridCount: 3,
              confirm: {
                value: 'button',
                action: () => {
                  console.info('Button-clicking callback')
                }
              },
              cancel: () => {
                console.info('Closed callbacks')
              }
            }
          )
        })
        .backgroundColor(0x317aff)
      Button('two button dialog')
        .onClick(() => {
          AlertDialog.show(
            {
              title: 'title',
              subtitle: 'subtitle',
              message: 'text',
              autoCancel: true,
              alignment: DialogAlignment.Bottom,
              gridCount: 4,
              offset: { dx: 0, dy: -20 },
              primaryButton: {
                value: 'cancel',
                action: () => {
                  console.info('Callback when the first button is clicked')
                }
              },
              secondaryButton: {
                enabled: true,
                defaultFocus: true,
                style: DialogButtonStyle.HIGHLIGHT,
                value: 'ok',
                action: () => {
                  console.info('Callback when the second button is clicked')
                }
              },
              cancel: () => {
                console.info('Closed callbacks')
              }
            }
          )
        }).backgroundColor(0x317aff)
        Button('three button dialog')
        .onClick(() => {
          AlertDialog.show(
            {
              title: 'title',
              subtitle: 'subtitle',
              message: 'text',
              autoCancel: true,
              alignment: DialogAlignment.Bottom,
              gridCount: 4,
              offset: { dx: 0, dy: -20 },
              buttonDirection: DialogButtonDirection.HORIZONTAL,
              buttons: [
                {
                  value: 'Button',
                  action: () => {
                    console.info('Callback when button1 is clicked')
                  }
                },
                {
                  value: 'Button',
                  action: () => {
                    console.info('Callback when button2 is clicked')
                  }
                },
                {
                  value: 'Button',
                  enabled: true,
                  defaultFocus: true,
                  style: DialogButtonStyle.HIGHLIGHT,
                  action: () => {
                    console.info('Callback when button3 is clicked')
                  }
                },
              ],
              cancel: () => {
                console.info('Closed callbacks')
              }
            }
          )
        }).backgroundColor(0x317aff)
    }.width('100%').margin({ top: 5 })
  }
}
```

![en-us_image_alert](figures/en-us_image_alert.gif)

### Example 2

```ts
// xxx.ets
@Entry
@Component
struct AlertDialogExample {
  build() {
    Column({ space: 5 }) {
        Button('one button dialog')
        .onClick(() => {
          AlertDialog.show(
            {
              title: 'title',
              subtitle: 'subtitle',
              message: 'text',
              autoCancel: true,
              alignment: DialogAlignment.Center,
              gridCount: 4,
              showInSubWindow: true,
              isModal: true,
              offset: { dx: 0, dy: -20 },
              buttonDirection: DialogButtonDirection.HORIZONTAL,
              buttons: [
                {
                  value: 'Button',
                  action: () => {
                    console.info('Callback when button1 is clicked')
                  }
                },
                {
                  value: 'Button',
                  action: () => {
                    console.info('Callback when button2 is clicked')
                  }
                },
                {
                  value: 'Button',
                  enabled: true,
                  defaultFocus: true,
                  style: DialogButtonStyle.HIGHLIGHT,
                  action: () => {
                    console.info('Callback when button3 is clicked')
                  }
                },
              ],
              cancel: () => {
                console.info('Closed callbacks')
              }
            }
          )
        }).backgroundColor(0x317aff)
    }.width('100%').margin({ top: 5 })
  }
}
```

![en-us_image_alert_showinsubwindow](figures/en-us_image_alert_showinsubwindow.jpg)
