# Environment: Device Environment Query


You may want your application to behave differently based on the device environment where the application is running, for example, switching to dark mode or a specific language. In this case, you need Environment for device environment query.


Environment is a singleton object created by the ArkUI framework at application startup. It provides a range of application state attributes to AppStorage that describe the device environment in which the application is running. Environment and its attributes are immutable. All property values are of simple types only.


## Environment Built-in Parameters

| Key| Data Type| Description                                     |
| ------------------ | ------------------ | ------------------ |
| accessibilityEnabled              | boolean                  | Whether to enable accessibility.                |
| colorMode              | ColorMode                  | Color mode. The options are as follows:<br>- **ColorMode.LIGHT**: light mode.<br>- **ColorMode.DARK**: dark mode.                |
| fontScale              | number                  | Font scale. Range: [0.85, 1.45].                |
| fontWeightScale              | number                  | Font weight scale. Range: [0.6, 1.6].               |
| layoutDirection              | LayoutDirection                  | Layout direction. The options are as follows:<br>- **LayoutDirection.LTR**: from left to right.<br>- **LayoutDirection.RTL**: from right to left.                |
| languageCode              | string                  | Current system language. The value is in lowercase, for example, **zh**.                |


## Use Scenarios


### Accessing Environment Parameters from UI

- Use **Environment.EnvProp** to save the environment variables of the device to AppStorage.

  ```ts
  // Save languageCode to AppStorage. The default value is en.
  Environment.EnvProp('languageCode', 'en');
  ```

- Decorate the variables with \@StorageProp to link them with components.

  ```ts
  @StorageProp('languageCode') lang : string = 'en';
  ```

The chain of updates is as follows: Environment > AppStorage > Component.

> **NOTE**
>
> An \@StorageProp decorated variable can be locally modified, but the change will not be updated to AppStorage. This is because the environment variable parameters are read-only to the application.


```ts
// Save the device language code to AppStorage.
Environment.EnvProp('languageCode', 'en');

@Entry
@Component
struct Index {
  @StorageProp('languageCode') languageCode: string = 'en';

  build() {
    Row() {
      Column() {
        // Output the current device language code.
        Text(this.languageCode)
      }
    }
  }
}
```


### Using Environment in Application Logic


```ts
// Use Environment.EnvProp to save the device language code to AppStorage.
Environment.EnvProp('languageCode', 'en');
// Obtain the one-way bound languageCode variable from AppStorage.
const lang: SubscribedAbstractProperty<string> = AppStorage.Prop('languageCode');

if (lang.get() === 'en') {
  console.info('Hi');
} else {
  console.info('Bonjour');
}
```
