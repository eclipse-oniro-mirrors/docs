# \@Link Decorator: Two-Way Synchronization Between Parent and Child Components


An \@Link decorated variable creates two-way synchronization with a variable of its parent component.


> **NOTE**
>
> Since API version 9, this decorator is supported in ArkTS widgets.


## Overview

An \@Link decorated variable in a child component shares the same value with a variable in its parent component.


## Restrictions

- The \@Link decorator cannot be used in custom components decorated by \@Entry.


## Rules of Use

| \@Link Decorator| Description                                      |
| ----------- | ---------------------------------------- |
| Decorator parameters      | None.                                       |
| Synchronization type       | Two-way:<br>from an \@State, \@StorageLink, or \@Link decorated variable in the parent component to this variable; and the other way around.|
| Allowed variable types  | Object, class, string, number, Boolean, enum, and array of these types. For details about the scenarios of nested types, see [Observed Changes](#observed-changes).<br>The type must be specified and must be the same as that of the counterpart variable of the parent component.<br>**any** is not supported. A combination of simple and complex types is not supported. The **undefined** and **null** values are not allowed.<br>**NOTE**<br>The Length, ResourceStr, and ResourceColor types are a combination of simple and complex types and therefore not supported.|
| Initial value for the decorated variable  | Forbidden.                              |


## Variable Transfer/Access Rules

| Transfer/Access     | Description                                      |
| ---------- | ---------------------------------------- |
| Initialization and update from the parent component| Mandatory. A two-way synchronization relationship can be established with the @State, @StorageLink, or \@Link decorated variable in the parent component. An \@Link decorated variable can be initialized from an \@State, \@Link, \@Prop, \@Provide, \@Consume, \@ObjectLink, \@StorageLink, \@StorageProp, \@LocalStorageLink, or \@LocalStorageProp decorated variable in the parent component.<br>Since API version 9, the syntax is **Comp({&nbsp;aLink:&nbsp;this.aState&nbsp;})** for initializing an \@Link decorated variable in the child component from an @State decorated variable in its parent component. The **Comp({aLink:&nbsp;$aState})** syntax is also supported|
| Child component initialization  | Supported; can be used to initialize a regular variable or \@State, \@Link, \@Prop, or \@Provide decorated variable in the child component.|
| Access | Private, accessible only within the component.                          |

  **Figure 1** Initialization rule 

![en-us_image_0000001502092556](figures/en-us_image_0000001502092556.png)


## Observed Changes and Behavior


### Observed Changes

- When the decorated variable is of the Boolean, string, or number type, its value change can be observed. For details, see [Example for @Link with Simple and Class Types](#example-for-link-with-simple-and-class-types).

- When the decorated variable is of the class or Object type, its value change and value changes of all its attributes, that is, the attributes that **Object.keys(observedObject)** returns. For details, see [Example for @Link with Simple and Class Types](#example-for-link-with-simple-and-class-types).

- When the decorated variable is of the array type, the addition, deletion, and updates of array items can be observed. For details, see [Array Type \@Link](#array-type-link).


### Framework Behavior

An \@Link decorated variable shares the lifecycle of its owning component.

To understand the value initialization and update mechanism of the \@Link decorated variable, it is necessary to consider the parent component and the initial render and update process of the child component that owns the \@Link decorated variable (in this example, the \@State decorated variable in the parent component is used).

1. Initial render: The execution of the parent component's **build()** function creates a new instance of the child component. The initialization process is as follows:
   1. An \@State decorated variable of the parent component must be specified to initialize the child component's \@Link decorated variable. The child component's \@Link decorated variable value and its source variable are kept in sync (two-way data synchronization).
   2. The \@State state variable wrapper class of the parent component is passed to the child component through the build function. After obtaining the \@State state variable of the parent component, the \@Link wrapper class of the child component registers the **this** pointer to the current \@Link wrapper class with the \@State variable of the parent component.

2. Update of the \@Link source: When the state variable in the parent component is updated, the \@Link decorated variable in the related child component is updated. Processing steps:
   1. As indicated in the initial rendering step, the child component's \@Link wrapper class registers the current **this** pointer with the parent component. When the \@State decorated variable in the parent component is changed, all system components (**elementid**) and state variables (such as the \@Link wrapper class) that depend on the parent component are traversed and updated.
   2. After the \@Link wrapper class is updated, all system components (**elementId**) that depend on the \@Link decorated variable in the child component are notified of the update. In this way, the parent component has the state data of the child components synchronized.

3. Update of \@Link: After the \@Link decorated variable in the child component is updated, the following steps are performed (the \@State decorated variable in the parent component is used):
   1. After the \@Link decorated variable is updated, the **set** method of the \@State wrapper class in the parent component is called to synchronize the updated value back to the parent component.
   2. The \@Link in the child component and \@State in the parent component traverse the dependent system components and update the corresponding UI. In this way, the \@Link decorated variable in the child component is synchronized back to the \@State decorated variable in the parent component.


## Usage Scenarios


### Example for @Link with Simple and Class Types

In the following example, after **Parent View: Set yellowButton** and **Parent View: Set GreenButton** of the parent component **ShufflingContainer** are clicked, the change in the parent component is synchronized to the child components.

  1. After buttons of the child components **GreenButton** and **YellowButton** are clicked, the child components (@Link decorated variables) change accordingly. Due to the two-way synchronization relationship between @Link and @State, the changes are synchronized to the parent component.
  
  2. When a button in the parent component **ShufflingContainer** is clicked, the parent component (@State decorated variable) changes, and the changes are synchronized to the child components, which are then updated accordingly.

```ts
class GreenButtonState {
  width: number = 0;

  constructor(width: number) {
    this.width = width;
  }
}

@Component
struct GreenButton {
  @Link greenButtonState: GreenButtonState;

  build() {
    Button('Green Button')
      .width(this.greenButtonState.width)
      .height(40)
      .backgroundColor('#64bb5c')
      .fontColor('#FFFFFF, 90%')
      .onClick(() => {
        if (this.greenButtonState.width < 700) {
          // Update the attribute of the class. The change can be observed and synchronized back to the parent component.
          this.greenButtonState.width += 60;
        } else {
          // Update the class. The change can be observed and synchronized back to the parent component.
          this.greenButtonState = new GreenButtonState(180);
        }
      })
  }
}

@Component
struct YellowButton {
  @Link yellowButtonState: number;

  build() {
    Button('Yellow Button')
      .width(this.yellowButtonState)
      .height(40)
      .backgroundColor('#f7ce00')
      .fontColor('#FFFFFF, 90%')
      .onClick(() => {
        // The change of the decorated variable of a simple type in the child component can be synchronized back to the parent component.
        this.yellowButtonState += 40.0;
      })
  }
}

@Entry
@Component
struct ShufflingContainer {
  @State greenButtonState: GreenButtonState = new GreenButtonState(180);
  @State yellowButtonProp: number = 180;

  build() {
    Column() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center }) {
        // Simple type @Link in the child component synchronized from @State in the parent component.
        Button('Parent View: Set yellowButton')
          .width(312)
          .height(40)
          .margin(12)
          .fontColor('#FFFFFF, 90%')
          .onClick(() => {
            this.yellowButtonProp = (this.yellowButtonProp < 700) ? this.yellowButtonProp + 40 : 100;
          })
        // Class type @Link in the child component synchronized from @State in the parent component.
        Button('Parent View: Set GreenButton')
          .width(312)
          .height(40)
          .margin(12)
          .fontColor('#FFFFFF, 90%')
          .onClick(() => {
            this.greenButtonState.width = (this.greenButtonState.width < 700) ? this.greenButtonState.width + 100 : 100;
          })
        // Initialize the class type @Link.
        GreenButton({ greenButtonState: $greenButtonState }).margin(12)
        // Initialize the simple type @Link.
        YellowButton({ yellowButtonState: $yellowButtonProp }).margin(12)
      }
    }
  }
}
```

![Video-link-UsageScenario-one](figures/Video-link-UsageScenario-one.gif)

### Array Type \@Link


```ts
@Component
struct Child {
  @Link items: number[];

  build() {
    Column() {
      Button(`Button1: push`)
        .margin(12)
        .width(312)
        .height(40)
        .fontColor('#FFFFFF, 90%')
        .onClick(() => {
          this.items.push(this.items.length + 1);
        })
      Button(`Button2: replace whole item`)
        .margin(12)
        .width(312)
        .height(40)
        .fontColor('#FFFFFF, 90%')
        .onClick(() => {
          this.items = [100, 200, 300];
        })
    }
  }
}

@Entry
@Component
struct Parent {
  @State arr: number[] = [1, 2, 3];

  build() {
    Column() {
      Child({ items: $arr })
        .margin(12)
      ForEach(this.arr,
        (item: number) => {
          Button(`${item}`)
            .margin(12)
            .width(312)
            .height(40)
            .backgroundColor('#11a2a2a2')
            .fontColor('#e6000000')
        },
        (item: ForEachInterface) => item.toString()
      )
    }
  }
}
```

![Video-link-UsageScenario-two](figures/Video-link-UsageScenario-two.gif)

As described above, the ArkUI framework can observe the addition, deletion, and replacement of array items. It should be noted that, in the preceding example, the type of the \@Link and \@State decorated variables is the same: number[]. It is not allowed to define the \@Link decorated variable in the child component as type number (**\@Link item: number**), and create child components for each array item in the \@State decorated array in the parent component. [\@Prop](arkts-prop.md) or \@Observed should be used depending on application semantics.
<!--no_check-->
