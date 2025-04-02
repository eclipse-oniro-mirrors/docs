# Text Component Common APIs

>**NOTE**
>
>This topic covers the common APIs of text components.
>The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## CaretStyle<sup>10+</sup>

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type                                  | Mandatory| Description|
| ------ | ------------------------------------------ | ---- | -------- |
| width  | [Length](ts-types.md#length)               | No  | Caret size. It cannot be set in percentage.|
| color  | [ResourceColor](ts-types.md#resourcecolor) | No  | Caret color.|

## LayoutManager<sup>12+</sup>

Implements a **LayoutManager** object.

> **NOTE**
>
> After the text content is changed, you must wait for the layout to be completed before you can obtain the most up-to-date layout information.

### Objects to Import
The following uses the **Text** component as an example.
```
controller: TextController = new TextController()
let layoutManager: LayoutManager = this.controller.getLayoutManager();
```

### getLineCount

getLineCount(): number

Obtains the total number of lines in the component.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type    | Description       |
| ------ | --------- |
| number | Total number of lines in the component.|

### getGlyphPositionAtCoordinate

getGlyphPositionAtCoordinate(x: number, y: number): PositionWithAffinity

Obtains the position of a glyph close to a given coordinate.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name   | Type  | Mandatory  | Description                |
| ------ | ------ | ---- | -------------------- |
| x | number | Yes   | X coordinate relative to the component.<br>Unit: px|
| y | number | Yes   | Y coordinate relative to the component.<br>Unit: px|

**Return value**

| Type                                         | Description       |
| --------------------------------------------- | ----------- |
| [PositionWithAffinity](#positionwithaffinity12) | Position of the glyph.|

### getLineMetrics

getLineMetrics(lineNumber: number): LineMetrics

Obtains the metrics information of a specified line.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name   | Type  | Mandatory  | Description                |
| ------ | ------ | ---- | -------------------- |
| lineNumber | number | Yes   | Line number, starting at 0.|

**Return value**

| Type                                      | Description      |
| ---------------------------------------- | -------- |
| [LineMetrics](#linemetrics12) | Button("Line Metrics")|

### getRectsForRange<sup>14+</sup>

getRectsForRange(range: TextRange, widthStyle: RectWidthStyle, heightStyle: RectHeightStyle): Array\<TextBox>

Obtains the drawing area information for characters or placeholders within a specified text range, based on the specified width and height of a rectangle.

**Atomic service API**: This API can be used in atomic services since API version 14.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name     | Type                                | Mandatory| Description                    |
| ----------- | ----------------------------------- | ---- | ------------------------ |
| range       | [TextRange](#textrange12)| Yes  | Text range for which to obtain the area information. |
| widthStyle  | [RectWidthStyle](#rectwidthstyle14)   | Yes  | Width of the rectangle.|
| heightStyle | [RectHeightStyle](#rectheightstyle14) | Yes  | Height of the rectangle.|

**Return value**

| Type                        | Description       |
| --------------------------- | ----------- |
| Array\<[TextBox](#textbox14)> | Array holding the rectangles obtained.|

## PositionWithAffinity<sup>12+</sup>

Describes the position and affinity of a glyph.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name     | Type                  | Read Only| Optional| Description                     |
| --------- | --------------------- | ---- | ---- | ------------------------ |
| position  | number                | Yes  | No  | Index of the glyph relative to the paragraph. The value is an integer. |
| affinity  | [Affinity](#affinity12) | Yes  | Yes  | Affinity of the position.            |

## TextMenuItemId<sup>12+</sup>

Provides the menu ID.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### Attributes

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name          | Type             | Read Only  | Optional | Description    |
| ------------ |---------------------| ---- | ---- | ------ |
| CUT  | [TextMenuItemId](#textmenuitemid12) |  Yes |  Yes| Default cut operation.<br>**Atomic service API**: This API can be used in atomic services since API version 12.|
| COPY  | [TextMenuItemId](#textmenuitemid12) |  Yes |  Yes | Default copy operation.<br>**Atomic service API**: This API can be used in atomic services since API version 12.|
| PASTE | [TextMenuItemId](#textmenuitemid12)   | Yes   | Yes   | Default paste operation.<br>**Atomic service API**: This API can be used in atomic services since API version 12.|
| SELECT_ALL   | [TextMenuItemId](#textmenuitemid12)   | Yes   | Yes   | Default select-all operation.<br>**Atomic service API**: This API can be used in atomic services since API version 12.|
| COLLABORATION_SERVICE   | [TextMenuItemId](#textmenuitemid12)   | Yes   | Yes   | Collaboration service.<br>**Atomic service API**: This API can be used in atomic services since API version 12.|
| CAMERA_INPUT   | [TextMenuItemId](#textmenuitemid12)   | Yes   | Yes  | Camera input.<br>**Atomic service API**: This API can be used in atomic services since API version 12.|
| AI_WRITER<sup>13+</sup>   | [TextMenuItemId](#textmenuitemid12)   | Yes   | Yes   | Text enhancement features, such as polishing, summary extraction, and formatting, for selected text. This menu item requires foundation model capabilities to function.<br>**Atomic service API**: This API can be used in atomic services since API version 13.|
| TRANSLATE<sup>15+</sup>   | [TextMenuItemId](#textmenuitemid12)   | Yes   | Yes   | Translation service.<br>**Atomic service API**: This API can be used in atomic services since API version 16.|

### of

static of(id: ResourceStr): TextMenuItemId

Creates a **TextMenuItemId** object based on **id**.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name | Type                             | Mandatory| Description                                                        |
| ------- | --------------------------------- | ---- | ------------------------------------------------------------ |
| id | [ResourceStr](ts-types.md#resourcestr) | Yes  | Menu ID.|

**Return value**

| Type             |       Description      |
| ------- | --------------------------------- |
| [TextMenuItemId](#textmenuitemid12) | **TextMenuItemId** object.|

### equals

equals(id: TextMenuItemId): boolean

Checks whether this **TextMenuItemId** object is the same as another **TextMenuItemId** object.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name | Type                             | Mandatory| Description                                                        |
| ------- | --------------------------------- | ---- | ------------------------------------------------------------ |
| id | [TextMenuItemId](#textmenuitemid12) | Yes  | ID of the **TextMenuItemId** object to compare.|

**Return value**

| Type             |       Description      |
| ------- | --------------------------------- |
| boolean | Whether the two **TextMenuItemId** objects are the same.|

## TextMenuItem<sup>12+</sup>

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name | Type                             | Mandatory| Description  |
| ------- | --------------------------------- | ---- | --------------------------------- |
| content | [ResourceStr](ts-types.md#resourcestr) | Yes  | Menu name.|
| icon | [ResourceStr](ts-types.md#resourcestr) | No  | Menu icon.<br>Online images are not supported.|
| id | [TextMenuItemId](#textmenuitemid12) | Yes  | Menu ID.|
| labelInfo<sup>15+</sup> | [ResourceStr](ts-types.md#resourcestr) | No  | Shortcut key hint.<br>This field is only supported on 2-in-1 devices.<br>**Atomic service API**: This API can be used in atomic services since API version 15.|

## EditMenuOptions

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### onCreateMenu<sup>12+</sup>

onCreateMenu(menuItems: Array\<TextMenuItem>): Array\<TextMenuItem>

Creates a menu with the specified menu items.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name | Type                             | Mandatory| Description  |
| ------- | --------------------------------- | ---- | --------------------------------- |
| menuItems | Array\<[TextMenuItem](#textmenuitem12)> | Yes  | Menu items.<br>**NOTE**<br>Changes to the name of the default menu item do not take effect.|

**Return value**

| Type             |       Description      |
| ------- | --------------------------------- |
| Array\<[TextMenuItem](#textmenuitem12)> | Menu items set.<br>**NOTE**<br>The icon of the default menu item is not returned.|

### onMenuItemClick<sup>12+</sup>

onMenuItemClick(menuItem: TextMenuItem, range: TextRange): boolean

Called when the specified menu item is clicked.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name | Type                             | Mandatory| Description  |
| ------- | --------------------------------- | ---- | --------------------------------- |
| menuItem | [TextMenuItem](#textmenuitem12) | Yes  | Menu item.|
| range | [TextRange](#textrange12) | Yes  | Selected text.|

**Return value**

| Type             |       Description      |
| ------- | --------------------------------- |
| boolean | Execution logic of the menu item.<br>Returns **true** if the default system logic is intercepted and only the custom logic is executed.<br>Returns **false** if the custom logic is executed before the default system logic.|

## TextRange<sup>12+</sup>

Defines the text range.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type| Mandatory| Description|
| -- | -- | -- | -- |
| start | number | No| Start index.|
| end | number | No| End index.|

## EditableTextOnChangeCallback<sup>12+</sup>

type EditableTextOnChangeCallback = (value: string, previewText?: PreviewText, options?: TextChangeOptions) => void

Represents the callback triggered when the content in the text box changes.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type| Mandatory| Description|
| -- | -- | -- | -- |
| value | string | Yes| Text displayed in the text box.|
| previewText | [PreviewText](#previewtext12) | No| Information about the preview text, including its start position and text content.|
| options<sup>15+</sup> | [TextChangeOptions](#textchangeoptions15) | No| Information about the text change, including the selection range before and after the change, the text content before the change, and the preview text information.|

## TextDataDetectorType<sup>11+</sup>

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name | Value  | Description                              |
| ----- | ----- | --------------------------------- |
| PHONE_NUMBER  | 0 | Phone number.|
| URL | 1 | URL.|
| EMAIL | 2 | Email address.|
| ADDRESS | 3 | Address.|
| DATE_TIME<sup>12+</sup> | 4 | Time.|

## TextDeleteDirection<sup>12+</sup>

Defines the direction for deleting text.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name   | Value  | Description                       |
| ------- | ---- | ---------------------------------- |
| BACKWARD | 0    | Backward delete.|
| FORWARD    | 1    | Forward delete.|

## MenuType<sup>13+</sup>

Enumerates the menu types.

**Atomic service API**: This API can be used in atomic services since API version 13.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Value| Description|
| ------- | ---- | ------------------- |
| SELECTION_MENU | 0 | Text selection menu.|
| PREVIEW_MENU | 1 | Preview menu.|

## KeyboardAppearance<sup>15+</sup>

Enumerates the appearance modes of the keyboard.

**Atomic service API**: This API can be used in atomic services since API version 16.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Value| Description|
| ------- | ---- | ------------------- |
| NONE_IMMERSIVE | 0 | Default appearance mode, not using immersive style.|
| IMMERSIVE | 1 | Immersive style, following the system color mode.|
| LIGHT_IMMERSIVE | 2 | Immersive style in light mode.|
| DARK_IMMERSIVE | 3 | Immersive style in dark mode.|

## InsertValue<sup>12+</sup>

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name   | Type                         | Mandatory| Description                                                        |
| ------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| insertOffset  | number | Yes  | Position of the inserted text.|
| insertValue  | string | Yes  | Content of the inserted text.|

## DeleteValue<sup>12+</sup>

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name   | Type                                                   | Mandatory| Description                                                   |
| ------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| deleteOffset  | number | Yes  | Position of the deleted text.|
| direction  | [TextDeleteDirection](#textdeletedirection12) | Yes  | Direction for deleting the text.|
| deleteValue  | string | Yes  | Content of the deleted text.|

## TextDataDetectorConfig<sup>11+</sup>

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type | Mandatory| Description |
| ------ | -------- | ---- | ------------------------------------------- |
| types   | [TextDataDetectorType](ts-text-common.md#textdatadetectortype11)[] | Yes  | Entity types for text recognition. Values **null** and **[]** indicate that all types of entities can be recognized.|
| onDetectResultUpdate   | (result: string) => void | No  | Callback invoked when text recognition succeeds.<br>- **result**: text recognition result, in JSON format.|
| color<sup>12+</sup>   | [ResourceColor](ts-types.md#resourcecolor) | No  | Entity color when text recognition succeeds.<br>Default value: **'#ff0a59f7'**|
| decoration<sup>12+</sup>  | [DecorationStyleInterface](ts-universal-styled-string.md#decorationstyleinterface)| No  | Style of the entity decorative line when text recognition succeeds.<br>Default value:<br>{<br> type: TextDecorationType.Underline,<br> color: same as the entity<br> style: TextDecorationStyle.SOLID <br>} |

## PreviewText<sup>12+</sup>

Preview text.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name    | Type                                            | Mandatory| Description                                                    |
| -------- | ------------------------------------------------ | ---- | -------------------------------------------------------- |
| offset | number | Yes  | Start position of the preview text.|
| value    | string         | Yes  | Content of the preview text.        |

## FontSettingOptions<sup>12+</sup>

Defines the font settings, including smooth and continuous adjustments for the font weight for components in your application.

**Widget capability**: This API can be used in ArkTS widgets since API version 12.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name    | Type                                            | Mandatory| Description                                                    |
| -------- | ------------------------------------------------ | ---- | -------------------------------------------------------- |
| enableVariableFontWeight | boolean | No  | Whether to support variable font weight adjustment.<br>Default value: **false**|

## OnDidChangeCallback<sup>12+</sup>

type OnDidChangeCallback = (rangeBefore: TextRange, rangeAfter: TextRange) => void

Represents the callback invoked after text changes.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type| Mandatory| Description|
| -- | -- | -- | -- |
| rangeBefore | [TextRange](#textrange12) | Yes| Range of the text to be changed.|
| rangeAfter | [TextRange](#textrange12) | Yes| Range of the text added.|

## StyledStringChangedListener<sup>12+</sup>

Defines the listener for changes of the styled string text content.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type| Mandatory| Description|
| -- | -- | -- | -- |
| onWillChange | Callback<[StyledStringChangeValue](#styledstringchangevalue12), boolean> | No| Callback invoked when text is about to change.|
| onDidChange | [OnDidChangeCallback](#ondidchangecallback12) | No| Callback invoked when text is changed.|

## StyledStringChangeValue<sup>12+</sup>

Describes the text changes of the styled string.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name| Type| Mandatory| Description|
| -- | -- | -- | -- |
| range | TextRange | Yes| Range of the styled string to be replaced in the original string.|
| replacementString | [StyledString](ts-universal-styled-string.md#styledstring) | Yes| Styled string used for replacement.|
| previewText | [StyledString](ts-universal-styled-string.md#styledstring) | No| Preview styled string.|

## TextBaseController<sup>12+</sup>

Defines a text selection controller.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### setSelection<sup>12+</sup>

setSelection(selectionStart: number, selectionEnd: number, options?: SelectionOptions): void

Sets the range of content selection. The selected content is highlighted.

If both **selectionStart** and **selectionEnd** are set to **-1**, the entire content is selected.

The component must be focused for the API call to have effect.

Since API version 12, on 2-in-1 devices, regardless of the value of **options**, calling the **setSelection** API will not display a menu; if a menu is already open, calling the API will close it.

On non-2-in-1 devices, when **options** is set to **MenuPolicy.DEFAULT**, the following rules apply after the API is called:

1. If the component has a menu with a selection handle, the menu remains open and is relocated according to the selection.

2. If the component has a menu without a selection handle, the menu remains open and its position remains unchanged.

3. If there is no menu open, no menu will appear after the selection.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name           | Type  | Mandatory  | Description   |
| -------------- | ------ | ---- | ------- |
| selectionStart | number | Yes   | Start position of the selection.|
| selectionEnd   | number | Yes   | End position of the selection.|
| options   | [SelectionOptions](ts-types.md#selectionoptions12) | No   | Configuration of options.|

### closeSelectionMenu<sup>12+</sup>

closeSelectionMenu(): void

Closes the custom or default text selection menu.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### getLayoutManager<sup>12+</sup>

getLayoutManager(): LayoutManager

Obtains a **LayoutManager** object.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type                                      | Description     |
| ---------------------------------------- | ------- |
| [LayoutManager](ts-text-common.md#layoutmanager12) | Implements a **LayoutManager** object.|

## TextEditControllerEx<sup>12+</sup>

Implements an extended text editing controller.

Inherits [TextBaseController](#textbasecontroller12).

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### isEditing<sup>12+</sup>

isEditing(): boolean

Obtains the editing status of the rich text.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type   | Description                         |
| ------- | ----------------------------- |
| boolean | Editing status of the rich text. **true** means that the text is in editable state, and **false** means the opposite.|

### stopEditing<sup>12+</sup>

stopEditing(): void

Stops editing.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### getCaretOffset<sup>12+</sup>

getCaretOffset(): number

Obtains the current position of the cursor.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type    | Description       |
| ------ | --------- |
| number | Position of the cursor.|

### setCaretOffset<sup>12+</sup>

setCaretOffset(offset: number): boolean

Sets the cursor offset.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name   | Type  | Mandatory  | Description               |
| ------ | ------ | ---- | -------------------- |
| offset | number | Yes   | Offset of the cursor. If the offset is outside the range of all content, the setting fails.|

**Return value**

| Type     | Description       |
| ------- | --------- |
| boolean | Whether the cursor is set successfully.|

### getPreviewText<sup>12+</sup>

getPreviewText?(): PreviewText

Obtains the preview text.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type                                      | Description     |
| ---------------------------------------- | ------- |
| [PreviewText](#previewtext12) | Preview text.|.

## StyledStringController<sup>12+</sup>

Defines a styled string controller.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

### setStyledString<sup>12+</sup>

setStyledString(styledString: StyledString): void

Sets the styled string displayed in the rich text component.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name  | Type  | Mandatory  | Description               |
| ----- | ------ | ---- | ------------------- |
| styledString | [StyledString](ts-universal-styled-string.md#styledstring) | Yes   | Styled string to set.<br>**NOTE**<br>The child class [MutableStyledString](ts-universal-styled-string.md#mutablestyledstring) of **StyledString** can also serve as the argument.|

### getStyledString<sup>12+</sup>

getStyledString(): MutableStyledString

Obtains the styled string displayed in the rich text component.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type   | Description                         |
| ------- | ----------------------------- |
| [MutableStyledString](ts-universal-styled-string.md#mutablestyledstring) | Styled string displayed in the rich text component.|

## DecorationStyleResult<sup>12+</sup>

Provides the text decorative line information returned by the backend.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name | Type                             | Mandatory| Description  |
| ------- | --------------------------------- | ---- | --------------------------------- |
| type | [TextDecorationType](ts-appendix-enums.md#textdecorationtype) | Yes  | Type of the text decorative line.|
| color | [ResourceColor](ts-types.md#resourcecolor) | Yes  | Color of the text decorative line.|
| style | [TextDecorationStyle](ts-appendix-enums.md#textdecorationstyle12) | No  | Style of the text decorative line.|

## LineMetrics<sup>12+</sup>

type LineMetrics = LineMetrics

Describes the measurement information of a single line of text in the text layout.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Type                             | Description  |
| --------------------------------- | --------------------------------- |
| [LineMetrics](../../apis-arkgraphics2d/js-apis-graphics-text.md#linemetrics) | Measurement information of a single line of text in the text layout.|

## Affinity<sup>12+</sup>

type Affinity = Affinity

Enumerates the affinity modes.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Type                             | Description  |
| --------------------------------- | --------------------------------- |
| [Affinity](../../apis-arkgraphics2d/js-apis-graphics-text.md#affinity) | Affinity mode enum.|

## TextBox<sup>14+</sup>

type TextBox = TextBox

Describes the rectangle that holds the text.

**Atomic service API**: This API can be used in atomic services since API version 14.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Type                             | Description  |
| --------------------------------- | --------------------------------- |
| [TextBox](../../apis-arkgraphics2d/js-apis-graphics-text.md#textbox) | Rectangle that holds the text.|

## RectHeightStyle<sup>14+</sup>

type RectHeightStyle = RectHeightStyle

Enumerates the rectangle height styles.

**Atomic service API**: This API can be used in atomic services since API version 14.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Type                             | Description  |
| --------------------------------- | --------------------------------- |
| [RectHeightStyle](../../apis-arkgraphics2d/js-apis-graphics-text.md#rectheightstyle) | Rectangle height style enum.|

## RectWidthStyle<sup>14+</sup>

type RectWidthStyle = RectWidthStyle

Enumerates the rectangle width styles.

**Atomic service API**: This API can be used in atomic services since API version 14.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Type                             | Description  |
| --------------------------------- | --------------------------------- |
| [RectWidthStyle](../../apis-arkgraphics2d/js-apis-graphics-text.md#rectwidthstyle) | Rectangle width style enum.|

## TextChangeOptions<sup>15+</sup>

Provides information about the text before and after a change, including the selection ranges.

**Atomic service API**: This API can be used in atomic services since API version 15.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name   | Type                                                   | Mandatory| Description                                                   |
| ------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| rangeBefore  | [TextRange](#textrange12) | Yes  | Selection range before the change.|
| rangeAfter  | [TextRange](#textrange12) | Yes  | Selection range after the change.|
| oldContent  | string | Yes  | Text content before the change.|
| oldPreviewText | [PreviewText](#previewtext12) | Yes| Preview text before the change.|

## EditableTextChangeValue<sup>15+</sup>

Provides detailed information of text changes, including preview text.

**Atomic service API**: This API can be used in atomic services since API version 15.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name   | Type                                                   | Mandatory| Description                                                   |
| ------- | ----------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| content  | string | Yes  | Current text content.|
| previewText  | [PreviewText](#previewtext12) | No  | Preview text.|
| options  | [TextChangeOptions](#textchangeoptions15) | No  | Information about the text change.|

