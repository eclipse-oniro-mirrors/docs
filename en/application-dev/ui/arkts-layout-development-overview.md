# Layout Overview


In declarative UI, page layout is the art of organizing custom components sequentially over a page. A well-designed layout can help you present information intuitively and effectively.


You design page layout by leveraging specific components or attributes to control the size and position of components on pages. The design process involves the following steps:


- Determine the layout structure of the page.

- Analyze the elements on the page.

- Select container components and attributes to control the position and size constraints of each element on the page.


## Layout Structure

A layout is generally in a hierarchical structure, which represents the overall architecture in the UI. Below is a common page structure.

  **Figure 1** Common page structure 

![common-page-structure](figures/common-page-structure.png)

To achieve the preceding effect, you need to declare the corresponding elements on the page. **Page** indicates the root node of the page, and other elements such as **Column** and **Row** are built-in components. ArkUI provides a wide variety of layout components, which you can draw on to implement different layouts. For example, you can use **Row** to implement a linear layout.


## Layout Elements

You can use layout-related container components to create a specific layout. For example, the **List** component can form a linear layout.

  **Figure 2** Layout elements 

![layout-element-omposition](figures/layout-element-omposition.png)

- Component area (blue block): size of the component and is determined by the width and height attributes.

- Component content area (yellow block): size of the component area minus the [border](../reference/arkui-ts/ts-universal-attributes-size.md) of the component. It serves as the layout constraint for calculating the size of the component content (or child component).

- Component content (green block): size of the component content, for example, size of the text content in the component. The component content may not match the component content area. For example, if fixed width and height values are set, the component content area is the size obtained with the width and height minus the paddings and border. The component content is the size calculated by the layout engine, which may be less than the component content area. When the component content and component content area do not match, the[align](../reference/arkui-ts/ts-universal-attributes-location.md) attribute takes effect, which defines the alignment mode of the component content in the component content area, for example, center aligned.

- Component layout bounds (dotted lines): component area plus the margins (if supplied).


## Layout Selection

The declarative UI provides eight common layouts. Choose a layout that best suits the use case.

| Layout                                      | Description                                    |
| ---------------------------------------- | ---------------------------------------- |
| [Linear layout](arkts-layout-development-linear.md) (Row and Column)| Use this layout when there are multiple child components and they can be arranged linearly.|
| [Stack layout](arkts-layout-development-stack-layout.md) (Stack)| Use this layout when you want to stack elements. The stacking does not occupy or affect the layout space of other child components in the same container. For example, when the [\<Panel>](../reference/arkui-ts/ts-container-panel.md) component is displayed as a child, superimposing it over other components makes more sense. In this case, the stack layout is preferred at the outer layer.|
| [Flex layout](arkts-layout-development-flex-layout.md) (Flex)| The flex layout is similar to the linear layout. However, it empowers the container to adjust the size of its child components to best fill the available space. Use this layout when you need elements to stretch or shrink to fit into the container.|
| [Relative layout](arkts-layout-development-relative-layout.md) (RelativeContainer)| The relative layout is a two-dimensional layout system. It does not need to comply with linear layout rules, and therefore exhibits more flexibility. By setting anchor rules (**AlignRules**) on a child component, you enable the component to position itself on the horizontal axis and vertical axis as relative to other child component in the container. Anchor rules support compression, stretching, stacking, and wrapping of child components. Use this layout when the distribution of elements is complex or when a linear layout may result in deeply nested components in the container.|
| [Responsive grid layout](arkts-layout-development-grid-layout.md) (GridRow and GridCol)| The responsive grid is an auxiliary positioning tool for a multi-device application, dividing space into rows and columns. Unlike the regular grid, the responsive grid is not allocating fixed-size space. Instead, it allows a layout to dynamically change based on the screen size. In this way, the design and development costs for adapting to different screen sizes are significantly reduced, and the overall design and development process is more orderly and rhythmic. In addition, the responsive grid offers a consistent display experience across devices. Use this layout when you are presenting the same content on different screen sizes.|
| [Media query](arkts-layout-development-media-query.md) (\@ohos.mediaquery)| You can use media queries to apply application styles based on the device type or device state. For example, you can apply specific layouts based on the attribute information of the target device and application, and update a page layout to reflect the dynamic screen changes.|
| [List](arkts-layout-development-create-list.md) (List)| Use lists to easily and efficiently display structured, scrollable information. In ArkUI, the list allows you to lay out elements in the horizontal or vertical layout and is able to adapt to the number of elements in the cross axis direction. It can scroll when the content overflows. Use this layout when you are presenting similar data types or data type sets, such as images and text.|
| [Grid](arkts-layout-development-create-grid.md) (Grid)| As an important adaptive layout, the grid excels at spacing elements evenly and defining the relationship between the elements. The grid layout controls the number of cells occupied by child components, number of rows or columns that child components span, and how the child components and spacing are adjusted proportionally when the grid container size changes. Use this layout in scenarios where space needs to be allocated evenly or based on a fixed proportion, such as calculators, albums, and calendars.|
| [Looping](arkts-layout-development-create-looping.md) (Swiper)| Use this layout when you want to implement ad rotation, image preview, or scrollable content.             |


## Layout Position

Attributes such as **position** and **offset** affect the position of the layout container relative to itself or other components.

| Positioning Capability| Description                                    | Implementation                                    |
| ---- | ---------------------------------------- | ---------------------------------------- |
| Absolute positioning| Absolute positioning is poor in adaptability to devices of different sizes, and is prone to screen adaptation errors.    | Use [position](../reference/arkui-ts/ts-universal-attributes-location.md) to implement absolute positioning and set the offset position of the upper left corner of an element relative to the upper left corner of the parent container. When laying out components, this attribute does not affect the layout of the parent component. It only adjusts the component position during drawing.|
| Relative positioning| Relative positioning keeps an element in the normal document flow, while allowing you to move it around relative to its original location.| You can use [offset](../reference/arkui-ts/ts-universal-attributes-location.md) to implement relative positioning and set the offset of an element relative to itself. This attribute does not affect the layout of the parent component. It only adjusts the component position during drawing.|


## Constraints on Child Components

| Constraint| Description                                    | Implementation                                    |
| --------- | ---------------------------------------- | ---------------------------------------- |
| Stretching       | When the size of a container component changes, the increased or decreased amount of space is allocated to the specified area in the container component.     | [flexGrow](../reference/arkui-ts/ts-universal-attributes-flex-layout.md) and [flexShrink](../reference/arkui-ts/ts-universal-attributes-flex-layout.md) attributes:<br>1. **flexGrow** defines the grow factor of a flex item.<br>2. **flexShrink** defines the shrink factor of a flex item.|
| Scaling       | The width and height of a child component change with the container component, with its aspect ratio fixed at the preset value.| The [aspectRatio](../reference/arkui-ts/ts-universal-attributes-layout-constraints.md) attribute specifies the aspect ratio of the current component. The formula is as follows: aspectRatio = width/height.|
| Proportion       | The proportion capability indicates that the width and height of child components change with the parent container component based on the preset proportion.         | Two implementation modes are available with the universal attributes:<br>1. Set the width and height of the child components to a percentage of the width and height of the parent component.<br>2. Use the [layoutWeight](../reference/arkui-ts/ts-universal-attributes-size.md) attribute to enable the child components to adaptively occupy the remaining space.|
| Hiding       | The hiding capability refers to that the visibility of a child component in a container component is subject to its preset display priority and the size of the container component. Child components with the same display priority are displayed or hidden at the same time.| The [displayPriority](../reference/arkui-ts/ts-universal-attributes-layout-constraints.md) attribute is used to control component visibility.|
