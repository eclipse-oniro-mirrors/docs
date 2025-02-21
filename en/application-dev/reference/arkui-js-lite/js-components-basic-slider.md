# slider

The **\<Slider>** component is used to quickly adjust settings, such as the volume and brightness.

> **NOTE**
>
> This component is supported since API version 4. Updates will be marked with a superscript to indicate their earliest API version.


## Child Components

Not supported


## Attributes

| Name   | Type    | Default Value | Mandatory  | Description                                      |
| ----- | ------ | ---- | ---- | ---------------------------------------- |
| min   | number | 0    | No   | Minimum value of the slider.                              |
| max   | number | 100  | No   | Maximum value of the slider.                              |
| value | number | 0    | No   | Initial value of the slider.                              |
| id    | string | -    | No   | Unique ID of the component.                                |
| style | string | -    | No   | Style declaration of the component.                                |
| class | string | -    | No   | Style class of the component, which is used to refer to a style table.                         |
| ref   | string | -    | No   | Reference information of child elements, which is registered with the parent component on **$refs**.|


## Events

| Name                | Parameter                               | Description            |
| ------------------ | --------------------------------- | -------------- |
| change             | ChangeEvent                       | Triggered when the value changes.|
| click              | -                                 | Triggered when the component is clicked.    |
| longpress          | -                                 | Triggered when the component is long pressed.    |
| swipe<sup>5+</sup> | [SwipeEvent](js-common-events.md) | Triggered when a user quickly swipes on the component.   |

  **Table 1** ChangeEvent

| Attribute                                      | Type    | Description           |
| ---------------------------------------- | ------ | ------------- |
| progress<sup>(deprecated<sup>5+</sup>)</sup> | string | Current value of the slider.|
| value<sup>5+</sup>                       | number | Current value of the slider.|


## Styles

| Name                                | Type                                      | Default Value     | Mandatory  | Description                                      |
| ---------------------------------- | ---------------------------------------- | -------- | ---- | ---------------------------------------- |
| color                              | &lt;color&gt;                            | \#000000 | No   | Background color of the slider.                               |
| selected-color                     | &lt;color&gt;                            | \#ffffff | No   | Selected color of the slider.                              |
| width                              | &lt;length&gt; \| &lt;percentage&gt;<sup>5+</sup> | -        | No   | Component width.<br>If this attribute is not set, the default value **0** is used.       |
| height                             | &lt;length&gt; \| &lt;percentage&gt;<sup>5+</sup> | -        | No   | Component height.<br>If this attribute is not set, the default value **0** is used.       |
| padding                            | &lt;length&gt;                           | 0        | No   | Shorthand attribute to set the padding for all sides.<br>The attribute can have one to four values:<br>- If you set only one value, it specifies the padding for all the four sides.<br>- If you set two values, the first value specifies the top and bottom padding, and the second value specifies the left and right padding.<br>- If you set three values, the first value specifies the top padding, the second value specifies the left and right padding, and the third value specifies the bottom padding.<br>- If you set four values, they respectively specify the padding for top, right, bottom, and left sides (in clockwise order).|
| padding-[left\|top\|right\|bottom] | &lt;length&gt;                           | 0        | No   | Left, top, right, and bottom padding.                         |
| margin                             | &lt;length&gt; \| &lt;percentage&gt;<sup>5+</sup> | 0        | No   | Shorthand attribute to set the margin for all sides. The attribute can have one to four values:<br>- If you set only one value, it specifies the margin for all the four sides.<br>- If you set two values, the first value specifies the top and bottom margins, and the second value specifies the left and right margins.<br>- If you set three values, the first value specifies the top margin, the second value specifies the left and right margins, and the third value specifies the bottom margin.<br>- If you set four values, they respectively specify the margin for top, right, bottom, and left sides (in clockwise order).|
| margin-[left\|top\|right\|bottom]  | &lt;length&gt; \| &lt;percentage&gt;<sup>5+</sup> | 0        | No   | Left, top, right, and bottom margins.                         |
| border-width                       | &lt;length&gt;                           | 0        | No   | Shorthand attribute to set the margin for all sides.                      |
| border-color                       | &lt;color&gt;                            | black    | No   | Shorthand attribute to set the color for all borders.                      |
| border-radius                      | &lt;length&gt;                           | -        | No   | Radius of round-corner borders.           |
| background-color                   | &lt;color&gt;                            | -        | No   | Background color.                                 |
| display                            | string                                   | flex     | No   | How and whether to display the box containing an element. Available values are as follows:<br>- **flex**: flexible layout<br>- **none**: not rendered|
| [left\|top]                        | &lt;length&gt; \| &lt;percentage&gt;<sup>6+</sup> | -        | No   | Edge of the element.<br>- **left**: left edge position of the element. This attribute defines the offset between the left edge of the margin area of a positioned element and left edge of its containing block.<br>- **top**: top edge position of the element. This attribute defines the offset between the top edge of a positioned element and that of a block included in the element.|

## Example

```html
<!-- xxx.hml -->
<div class="container">
  <text>slider start value is {{startValue}}</text>
  <text>slider current value is {{currentValue}}</text>
  <text>slider end value is {{endValue}}</text>
  <slider min="0" max="100" value="{{value}}" onchange="setvalue" style="width: 20%;height: 10%"></slider>
</div>
```

```css
/* xxx.css */
.container {
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}
```

```javascript
// xxx.js
export default {
  data: {
    value: 0,
    startValue: 0,
    currentValue: 0,
    endValue: 100,
  },
  setvalue(e) {
    this.currentValue = e.value;
  }
}
```

![slider](figures/slider.png)
