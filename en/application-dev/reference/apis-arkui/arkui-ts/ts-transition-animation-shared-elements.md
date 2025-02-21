# Shared Element Transition (sharedTransition)

A shared element transition is a transition animation applied to a component that is present on two pages. This component is called the shared element and can be set in the **sharedTransition** attribute.

> **NOTE**
>
> The APIs of this module are supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Attributes


| Name            | Type         | Mandatory                                   | Description                                                    |
| ---------------- | -----------------|------------------------------------------- | ------------------------------------------------------------ |
|      id          |  string         | Yes                                        |    Transition of the shared element. If the same **id** value is configured for a component on the two pages, this component is considered as a shared element of the pages. If the **id** value is an empty string, no transition will be applied to the component.|
|     options          |  [sharedTransitionOptions](#sharedtransitionoptions)       | No    |  Parameters of the shared element transition animation.|

> **NOTE**
>
> **motionPath** is effective only when **type** is set to **SharedTransitionEffectType.Exchange**.

## sharedTransitionOptions

**Atomic service API**: This API can be used in atomic services since API version 11.

| Name             | Type     | Mandatory      | Description                                                     |
| ----------------- | -------------|-------------- | --------------------------------------------------------------|
| duration          |     number   |  No          | Animation duration.<br>Default value: **1000**<br>Unit: ms|
| curve             |      [Curve](ts-appendix-enums.md#curve) \| string \| [ICurve](../js-apis-curve.md#icurve9)<sup>10+</sup>  | No| Animation curve.<br>Default value: **Curve.Linear**|
| delay          |     number   |  No          | Delay of animation playback.<br>Default value: **0**<br>Unit: ms|
| motionPath          | [MotionPathOptions](./ts-motion-path-animation.md)  |  No          | Motion path.|
| zIndex          |     number   |  No             | Z-axis.|
| type           |     [SharedTransitionEffectType](ts-appendix-enums.md#sharedtransitioneffecttype)   |  No  | Animation type.<br>Default value: **SharedTransitionEffectType.Exchange**|


## Example

This example implements the custom transition of a shared image during redirection from one page to another, which is triggered by a click on the image.

```ts
// xxx.ets
@Entry
@Component
struct SharedTransitionExample {
  @State active: boolean = false

  build() {
    Column() {
      Navigator({ target: 'pages/PageB', type: NavigationType.Push }) {
        Image($r('app.media.ic_health_heart')).width(50).height(50)
          .sharedTransition('sharedImage', { duration: 800, curve: Curve.Linear, delay: 100 })
      }.padding({ left: 20, top: 20 })
      .onClick(() => {
        this.active = true
      })
    }
  }
}
```

```ts
// PageB.ets
@Entry
@Component
struct pageBExample {
  build() {
    Stack() {
      Image($r('app.media.ic_health_heart')).width(150).height(150)
        .sharedTransition('sharedImage', { duration: 800, curve: Curve.Linear, delay: 100 })
    }.width('100%').height('100%')
  }
}
```

![shared](figures/shared.gif)
