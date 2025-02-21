# Previewing<a name="EN-US_TOPIC_0000001055394496"></a>

## When to Use<a name="en-us_topic_0000001051930577_section186634310418"></a>

Use the camera module APIs to generate and play video streams.

## Available APIs<a name="en-us_topic_0000001051930577_section125479541744"></a>

For details, see the available APIs described in development guidelines on photographing.

## Limitations and Constraints<a name="en-us_topic_0000001051930577_section1165911177314"></a>

None

## How to Develop<a name="en-us_topic_0000001051930577_section34171333656"></a>

1.  Perform step 1 through step 4 described in development guidelines on photographing.
2.  Set the preview area.

    ```
    Surface *surface = Surface::CreateSurface();
    /* Set the display area. */
    surface->SetUserData("region_position_x", "480"); // X-coordinate of the upper left corner of the rectangle
    surface->SetUserData("region_position_y", "270"); // Y-coordinate of the upper left corner of the rectangle
    surface->SetUserData("region_width", "960"); // Width
    surface->SetUserData("region_height", "540"); // Height
    
    fc->AddSurface(*surface);
    ```

3.  Start and stop previewing.

    ```
    stateCallback->camera_->TriggerLoopingCapture(*fc); // Start previewing.
    stateCallback->camera_->StopLoopingCapture(); // Stop previewing.
    ```


