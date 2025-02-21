# \@BuilderParam Decorator: @Builder Function Reference


In certain circumstances, you may need to add a specific feature, such as a click-to-jump action, to a custom component. However, embedding an event method directly in a component will add the feature to all places where the component is imported. This is where the \@BuilderParam decorator comes into the picture. \@BuilderParam is used to decorate a custom component variable of type Reference to an \@Builder method. When initializing a custom component, you can add the specific feature to it by assigning a value to the variable. This decorator can be used to declare an element of any UI description, similar to a slot placeholder.


> **NOTE**
>
> Since API version 9, this decorator is supported in ArkTS widgets.


## Rules of Use


### Initializing \@BuilderParam Decorated Methods

An \@BuilderParam decorated method can be initialized only by an \@Builder function reference.

- Local initialization with the owning component's custom \@Builder function reference or a global \@Builder function reference

  ```ts
  @Builder function overBuilder() {}

  @Component
  struct Child {
    @Builder doNothingBuilder() {};

    // Use the custom builder function of the custom component for \@BuilderParam initialization.
    @BuilderParam customBuilderParam: () => void = this.doNothingBuilder;
    // Use the global custom builder function for \@BuilderParam initialization.
    @BuilderParam customOverBuilderParam: () => void = overBuilder;
    build(){}
  }
  ```

- Initialization from the parent component

  ```ts
  @Component
  struct Child {
    // Use the \@Builder decorated method in the parent component for \@BuilderParam initialization.
    @BuilderParam customBuilderParam: () => void;

    build() {
      Column() {
        this.customBuilderParam()
      }
    }
  }

  @Entry
  @Component
  struct Parent {
    @Builder componentBuilder() {
      Text(`Parent builder `)
    }

    build() {
      Column() {
        Child({ customBuilderParam: this.componentBuilder })
      }
    }
  }
  ```

  ![f1b703f7-2f2d-43af-b11d-fdc9542d8361](figures/f1b703f7-2f2d-43af-b11d-fdc9542d8361.png)

- **this** in the function body must point to the correct object.

  In the following example, when the **Parent** component calls **this.componentBuilder()**, **this** points to the owning component, that is, **Parent**. With **\@BuilderParam customBuilderParam** passed to the **Child** component from **\@Builder componentBuilder()**, when the **Child** component calls **this.customBuilderParam()**, **this** points to the label of the **Child** component, that is, **Child**.

   >  **NOTE**
   >
   >  Exercise caution when using **bind** to change the context of function invoking, which may cause **this** to point to an incorrect object.

  ```ts
  @Component
  struct Child {
    label: string = `Child`
    @BuilderParam customBuilderParam: () => void;

    build() {
      Column() {
        this.customBuilderParam()
      }
    }
  }

  @Entry
  @Component
  struct Parent {
    label: string = `Parent`

    @Builder componentBuilder() {
      Text(`${this.label}`)
    }

    build() {
      Column() {
        this.componentBuilder()
        Child({ customBuilderParam: this.componentBuilder })
      }
    }
  }
  ```

  ![3f17235e-57e6-4058-8729-a19127a3b007](figures/3f17235e-57e6-4058-8729-a19127a3b007.png)


## Use Scenarios


### Component Initialization Through Parameters

An \@BuilderParam decorated method can be a method with or without parameters. Whether it contains parameters should match that of the assigned \@Builder method. The type of the \@BuilderParam decorated method must also match that of the assigned \@Builder method.


```ts
@Builder function overBuilder($$ : {label: string }) {
  Text($$.label)
    .width(400)
    .height(50)
    .backgroundColor(Color.Green)
}

@Component
struct Child {
  label: string = 'Child'
  // Without parameters. The pointed componentBuilder is also without parameters.
  @BuilderParam customBuilderParam: () => void;
  // With parameters. The pointed GlobalBuilder1 is also with parameters.
  @BuilderParam customOverBuilderParam: ($$ : { label : string}) => void;

  build() {
    Column() {
      this.customBuilderParam()
      this.customOverBuilderParam({label: 'global Builder label' } )
    }
  }
}

@Entry
@Component
struct Parent {
  label: string = 'Parent'

  @Builder componentBuilder() {
    Text(`${this.label}`)
  }

  build() {
    Column() {
      this.componentBuilder()
      Child({ customBuilderParam: this.componentBuilder, customOverBuilderParam: overBuilder })
    }
  }
}
```

![3869e265-4d12-44ff-93ef-e84473c68c97](figures/3869e265-4d12-44ff-93ef-e84473c68c97.png)


### Component Initialization Through Trailing Closure

In a custom component, the \@BuilderParam decorated attribute can be initialized using a trailing closure. During initialization, the component name is followed by a pair of braces ({}) to form a trailing closure.

> **NOTE**
>
> In this scenario, the custom component can have only one \@BuilderParam decorated attribute.

You can pass the content in the trailing closure to \@BuilderParam as an \@Builder decorated method. Example:


```ts
// xxx.ets
@Component
struct CustomContainer {
  @Prop header: string;
  // Use the trailing closure {} (@Builder decorated method) of the parent component for @BuilderParam initialization.
  @BuilderParam closer: () => void

  build() {
    Column() {
      Text(this.header)
        .fontSize(30)
      this.closer()
    }
  }
}

@Builder function specificParam(label1: string, label2: string) {
  Column() {
    Text(label1)
      .fontSize(30)
    Text(label2)
      .fontSize(30)
  }
}

@Entry
@Component
struct CustomContainerUser {
  @State text: string = 'header';

  build() {
    Column() {
      // Create the CustomContainer component. During initialization, append a pair of braces ({}) to the component name to form a trailing closure.
      // Used as the parameter passed to CustomContainer @BuilderParam closer: () => void.
      CustomContainer({ header: this.text }) {
        Column() {
          specificParam('testA', 'testB')
        }.backgroundColor(Color.Yellow)
        .onClick(() => {
          this.text = 'changeHeader';
        })
      }
    }
  }
}
```

![7ae8ed5e-fc23-49ea-be3b-08a672a7b817](figures/7ae8ed5e-fc23-49ea-be3b-08a672a7b817.png)
