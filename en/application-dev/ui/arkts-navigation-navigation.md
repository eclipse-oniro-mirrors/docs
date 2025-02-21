# Navigation

Generally, the [\<Navigation>](../reference/apis-arkui/arkui-ts/ts-basic-components-navigation.md) component functions as the root container of a page and supports three display modes: single-page, column, and adaptive. It is applicable to page redirection within a module and useful in one-time development for multi-device deployment. Draw on this component's routing capability to create a smooth page transition experience, and explore its various title bar styles to present titles seamlessly linked with the content. In one-time development for multi-device deployment scenarios, the **\<Navigation>** component can automatically adapt to the window size; when the window is large enough, it automatically displays content in columns.

The pages of the **\<Navigation>** component include the home page and content page. The home page consists of the title bar, content area, and toolbar. You can use [\<NavRouter>](../reference/apis-arkui/arkui-ts/ts-basic-components-navrouter.md) as a child component in the content area to implement a navigation bar. The content page displays the content of the [\<NavDestination>](../reference/apis-arkui/arkui-ts/ts-basic-components-navdestination.md) child component.

As a special child component of **\<Navigation>**, **\<NavRouter>** provides default processing logic for responding to clicks, eliminating the need for manual logic definition. It has only two child components, the second of which must be **\<NavDestination>**. As a special child component of **\<NavRouter>**, **\<NavDestination>** makes up the content page of the **\<Navigation>** component. When the user clicks the **\<NavRouter>** component, the corresponding **\<NavDestination>** content area is displayed.


## Setting the Page Display Mode

The **\<Navigation>** component uses the **mode** attribute to set the page display mode.

- Adaptive Mode

  By default, the **\<Navigation>** component is in adaptive mode. In this case, the **mode** attribute is **NavigationMode.Auto**. In adaptive mode, when the device width is greater than 520 vp, the **\<Navigation>** component uses the column mode. Otherwise, the **\<Navigation>** component uses the single-page mode.


  ```
  Navigation() {
    ...
  }
  .mode(NavigationMode.Auto)
  ```

- Single-page mode

    **Figure 1** Single-page mode 

  ![en-us_image_0000001511740532](figures/en-us_image_0000001511740532.png)

  Set **mode** to **NavigationMode.Stack** so that the **\<Navigation>** component is displayed on a single page.


  ```ts
  Navigation() {
    ...
  }
  .mode(NavigationMode.Stack)
  ```

  ![single-page-1](figures/single-page-1.jpg)

- Column mode

  **Figure 2** Column mode

  ![en-us_image_0000001562820845](figures/en-us_image_0000001562820845.png)

  Set **mode** to **NavigationMode.Split** so that the **\<Navigation>** component is displayed in columns.


  ```ts
  @Entry
  @Component
  struct NavigationExample {
    @State TooTmp: ToolbarItem = {'value': "func", 'icon': "./image/ic_public_highlights.svg", 'action': ()=> {}}
    private arr: number[] = [1, 2, 3];
  
    build() {
      Column() {
        Navigation() {
          TextInput({ placeholder: 'search...' })
            .width("90%")
            .height(40)
            .backgroundColor('#FFFFFF')
  
          List({ space: 12 }) {
            ForEach(this.arr, (item:string) => {
              ListItem() {
                NavRouter() {
                  Text("NavRouter" + item)
                    .width("100%")
                    .height(72)
                    .backgroundColor('#FFFFFF')
                    .borderRadius(24)
                    .fontSize(16)
                    .fontWeight(500)
                    .textAlign(TextAlign.Center)
                  NavDestination() {
                    Text("NavDestinationContent" + item)
                  }
                  .title("NavDestinationTitle" + item)
                }
              }
            }, (item:string):string => item)
          }
          .width("90%")
          .margin({ top: 12 })
        }
        .title ("Main Title")
        .mode(NavigationMode.Split)
        .menus([
          {value: "", icon: "./image/ic_public_search.svg", action: ()=> {}},
          {value: "", icon: "./image/ic_public_add.svg", action: ()=> {}},
          {value: "", icon: "./image/ic_public_add.svg", action: ()=> {}},
          {value: "", icon: "./image/ic_public_add.svg", action: ()=> {}},
          {value: "", icon: "./image/ic_public_add.svg", action: ()=> {}}
        ])
        .toolbarConfiguration([this.TooTmp, this.TooTmp, this.TooTmp])
      }
      .height('100%')
      .width('100%')
      .backgroundColor('#F1F3F5')
    }
  }
  ```

  ![column](figures/column.jpg)


## Setting the Title Bar Mode

The title bar is on the top of the page and is used to display the page name and operation entry. The **\<Navigation>** component uses the **titleMode** attribute to set the title bar mode.

- Mini mode
  Applicable when the title of a level-1 page does not need to be highlighted.

  **Figure 3** Title bar in Mini mode 

  ![mini](figures/mini.jpg)


  ```ts
  Navigation() {
    ...
  }
  .titleMode(NavigationTitleMode.Mini)
  ```


- Full mode
  Applicable when the title of a level-1 page needs to be highlighted.

    **Figure 4** Title bar in Full mode 

  ![free1](figures/free1.jpg)


  ```ts
  Navigation() {
    ...
  }
  .titleMode(NavigationTitleMode.Full)
  ```


## Setting the Menu Bar

The menu bar is in the upper right corner of the **\<Navigation>** component. You can set the menu bar through the **menus** attribute, which supports two parameter types: Array&lt;[NavigationMenuItem](../reference/apis-arkui/arkui-ts/ts-basic-components-navigation.md#navigationmenuitem)&gt; and CustomBuilder. When the Array\<NavigationMenuItem> type is used, a maximum of three icons can be displayed in portrait mode and a maximum of five icons can be displayed in landscape mode. Extra icons will be placed in the automatically generated More icons.

**Figure 5** Menu bar with three icons 

![menu-bar-2](figures/menu-bar-2.jpg)

```ts
let TooTmp: NavigationMenuItem = {'value': "", 'icon': "./image/ic_public_highlights.svg", 'action': ()=> {}}
Navigation() {
  ...
}
.menus([TooTmp,
  TooTmp,
  TooTmp])
```

You can also reference images in the **resources** folder.

```ts
let TooTmp: NavigationMenuItem = {'value': "", 'icon': "resources/base/media/ic_public_highlights.svg", 'action': ()=> {}}
Navigation() {
  ...
}
.menus([TooTmp,
  TooTmp,
  TooTmp])
```

**Figure 6** Menu bar with four icons 

![menu-bar](figures/menu-bar.jpg)

```ts
let TooTmp: NavigationMenuItem = {'value': "", 'icon': "./image/ic_public_highlights.svg", 'action': ()=> {}}
Navigation() {
  ...
}
.menus([TooTmp,
  TooTmp,
  TooTmp,
  TooTmp])
```


## Setting the Toolbar

The toolbar is located at the bottom of the **\<Navigation>** component. You can set the toolbar through the **toolbarConfiguration** attribute.


  **Figure 7** Toolbar 

![free3](figures/free3.jpg)

```ts
let TooTmp: ToolbarItem = {'value': "func", 'icon': "./image/ic_public_highlights.svg", 'action': ()=> {}}
let TooBar: ToolbarItem[] = [TooTmp,TooTmp,TooTmp]
Navigation() {
  ...
}
.toolbarConfiguration(TooBar)
```

## Setting the Subpage Mode

You can set the subpage mode through the **mode** attribute of **\<NavDestination>**, the root container of subpages.

- Standard mode

  By default, subpages in the **\<NavDestination>** component are in standard mode, which corresponds to the **NavDestinationMode.STANDARD** value of the **mode** attribute. In standard mode, where the lifecycle of **\<NavDestination>** changes with the standard destination in the **NavPathStack**.

- Dialog mode

  **Figure 8** Dialog mode

  ![dialog_navdes_1](figures/dialog_navdes_1.png)

  Set the **mode** attribute to **NavDestinationMode.DIALOG** to set subpages in the **\<NavDestination>** component to dialog mode, where the component is transparent. You can add different effects to the component, for example, add a background.

  ```ts
  // Index.ets
  @Component
  struct Page01 {

    @Consume('pageInfos') pageInfos: NavPathStack;

    build() {
      NavDestination() {
        Button('push Page01')
          .width('80%')
          .onClick(() => {
            this.pageInfos.pushPathByName('Page01', '');
          })
          .margin({top: 10, bottom: 10})
        Button('push Dialog01')
          .width('80%')
          .onClick(() => {
            this.pageInfos.pushPathByName('Dialog01', '');
          })
          .margin({top: 10, bottom: 10})
      }
      .title('Page01')
    }
  }

  @Component
  struct Dialog01 {

    @Consume('pageInfos') pageInfos: NavPathStack;

    build() {
      NavDestination() {
        Stack() {
          Column()
            .width('100%')
            .height('100%')
            .backgroundColor(Color.Gray)
            .opacity(0.1)
            .onClick(() => {
              this.pageInfos.pop();
            })
          // Add controls for business processing
          Column() {
            Text('Dialog01')
              .fontSize(30)
              .fontWeight(2)
            Button('push Page01')
              .width('80%')
              .onClick(() => {
                this.pageInfos.pushPathByName('Page01', '');
              })
              .margin({top: 10, bottom: 10})
            Button('push Dialog01')
              .width('80%')
              .onClick(() => {
                this.pageInfos.pushPathByName('Dialog01', '');
              })
              .margin({top: 10, bottom: 10})
            Button('pop')
              .width('80%')
              .onClick(() => {
                this.pageInfos.pop();
              })
              .margin({top: 10, bottom: 10})
          }
          .padding(10)
          .width(250)
          .backgroundColor(Color.White)
          .borderRadius(10)
        }
      }
      .hideTitleBar(true)
      // Set the mode property of this NavDestination to DIALOG
      .mode(NavDestinationMode.DIALOG)
    }
  }

  @Entry
  @Component
  struct Index {
    @Provide('pageInfos') pageInfos: NavPathStack = new NavPathStack()

    @Builder
    PagesMap(name: string) {
      if (name == 'Page01') {
        Page01()
      } else if (name == 'Dialog01') {
        Dialog01()
      }
    }

    build() {
      Navigation(this.pageInfos) {
        Button('push Page01')
          .width('80%')
          .onClick(() => {
            this.pageInfos.pushPathByName('Page01', '');
          })
      }
      .mode(NavigationMode.Stack)
      .titleMode(NavigationTitleMode.Mini)
      .title ('Home')
      .navDestination(this.PagesMap)
    }
  }
  ```

  ![dialog_navdes_2](figures/dialog_navdes_2.png)
