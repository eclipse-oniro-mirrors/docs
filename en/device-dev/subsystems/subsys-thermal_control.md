# Thermal Control Customization

## Overview

### Introduction

By default, OpenHarmony provides the thermal control feature. If a device becomes overheated during usage, thermal control measures need to be taken for the device. For example, if the battery temperature is too high during charging, then thermal control needs to be applied to the charging device. However, thermal control varies according to product specifications. To address this issue, OpenHarmony provides the thermal control customization function.

### Constraints

The configuration path for battery level customization is subject to the [configuration policy](https://gitee.com/openharmony/customization_config_policy). In this development guide, `/vendor` is used as an example of the configuration path. During actual development, you need to modify the customization path based on the product configuration policy.

## How to Develop

### Setting Up the Environment

**Hardware requirements:**

Development board running the standard system, for example, the DAYU200 or Hi3516D V300 open source suite.

**Environment requirements:**

For details about the requirements on the Linux environment, see [Quick Start](../quick-start/quickstart-overview.md).

### Getting Started with Development

The following uses [DAYU200](https://gitee.com/openharmony/vendor_hihope/tree/master/rk3568) as an example to illustrate thermal control customization.

1. Create the `thermal` folder in the product directory [/vendor/hihope/rk3568](https://gitee.com/openharmony/vendor_hihope/tree/master/rk3568).

2. Create a target folder by referring to the [default thermal control configuration folder](https://gitee.com/openharmony/powermgr_thermal_manager/tree/master/services/native/profile), and install it in `//vendor/hihope/rk3568/thermal`. The content is as follows:
     
    ```text
    profile
    ├── BUILD.gn
    ├── thermal_service_config.xml
    ```

3. Write the custom `thermal_service_config.xml` file by referring to the [thermal_service_config.xml](https://gitee.com/openharmony/powermgr_thermal_manager/blob/master/services/native/profile/thermal_service_config.xml) file in the default thermal control configuration folder. The following table describes the related configuration items.

    **Table 1** Configuration items for thermal control

    | Configuration Item| Description| Parameter| Parameter Description| Data Type|Value Range|
    | -------- | -------- | -------- | -------- | -------- | -------- |
    | name="cpu_big" | Big-core CPU control (big-core CPU frequency)| N/A| N/A| N/A| N/A|
    | name="cpu_med" | Medium-core CPU control (medium-core CPU frequency)| N/A| N/A| N/A| N/A|
    | name="cpu_lit" | Small-core CPU control (small-core CPU frequency)| N/A| N/A| N/A| N/A|
    | name="gpu" | GPU control (GPU frequency)| N/A| N/A| N/A| N/A|
    | name="lcd" | LCD control (screen brightness)| N/A| N/A| N/A| N/A|
    | name="volume" | Sound control (volume)| uid | User ID| int | Product-specific| 
    | name="current_xxx" | Charging current control (charging current during fast charging and slow charging)| protocol<br>param | Set **protocol** to **current** and **param** to a supported charging protocol, that is, fast charging (**sc**) or slow charging (**buck**).| string |protocol="current" param="sc" |
    | name="current_xxx" | Charging current control | event | - **1**: event sending enabled<br>-**0**: event sending disabled| int | 0 or 1|
    | name="voltage_xxx" | Charging voltage control (charging voltage during fast charging and slow charging)| protocol<br>param | Set **protocol** to **voltage** and **param** to a charging protocol, that is, fast charging (**sc**) or slow charging (**buck**).| string | protocol="voltage" param="buck" |
    | name="voltage_xxx" | Charging voltage control | event | - **1**: event sending enabled<br>-**0**: event sending disabled| int | 0 or 1|
    | name="process_ctrl" | Process control (survival status of foreground and background processes)| event | - **1**: event sending enabled<br>-**0**: event sending disabled<br>If this parameter is not set, the value is defaulted to **0**.| int | 0 or 1|
    | name="shut_down" | Shutdown control (device shutdown)| event | - **1**: event sending enabled<br>-**0**: event sending disabled| int | 0 or 1|
    | name="thermallevel" | Thermal level control (thermal level reporting)| event | - **1**: event sending enabled<br>-**0**: event sending disabled| int | 0 or 1|
    | name="popup" | Pop-up window control (pop-up window display)| N/A| N/A| N/A| N/A|
    | name="xxx" | Node thermal control action| protocol<br>param | Set **protocol** to **node**.<br>Set **param** to the node path and rollback value, which are separated by a comma (,).| string | N/A|

    ```shell
    <action>
        <item name="cpu_big"/>
        <item name="cpu_med"/>
        <item name="cpu_lit"/>
        <item name="gpu"/>
        <item name="lcd"/>
        <item name="volume" uid="2001,2002"/>
        <item name="current_sc" protocol="current" param="sc" event="1"/>
        <item name="voltage_buck" protocol="voltage" param="buck" event="1"/>
        <item name="process_ctrl" event=""/>
        <item name="shut_down" event="0"/>
        <item name="thermallevel" event="0"/>
        <item name="popup"/>
        <item name="(action_name)" protocol="node" param="/sys/class/thermal/xxx"/>
    </action>
    ```

4. Write the `BUILD.gn` file by referring to the [BUILD.gn](https://gitee.com/openharmony/powermgr_thermal_manager/blob/master/services/native/profile/BUILD.gn) file in the default thermal control configuration folder to pack the `thermal_service_config.xml` file to the `/vendor/etc/thermal_config` directory. The configuration is as follows:

    ```shell
    import("//build/ohos.gni")                      # Reference build/ohos.gni.

    ohos_prebuilt_etc("thermal_service_config") {
        source = "thermal_service_config.xml"
        relative_install_dir = "thermal_config"
        install_images = [ chipset_base_dir ]       # Required configuration for installing the thermal_service_config.xml file in the vendor directory.
        part_name = "product_rk3568"                # Set part_name to product_rk3568 for subsequent build. You can change it as required.
    }
    ```

5. Add the build target to `module_list` in [ohos.build](https://gitee.com/openharmony/vendor_hihope/blob/master/rk3568/ohos.build). For example:

    ```json
    {
        "parts": {
            "product_rk3568": {
                "module_list": [
                    "//vendor/hihope/rk3568/default_app_config:default_app_config",
                    "//vendor/hihope/rk3568/image_conf:custom_image_conf",
                    "//vendor/hihope/rk3568/preinstall-config:preinstall-config",
                    "//vendor/hihope/rk3568/resourceschedule:resourceschedule",
                    "//vendor/hihope/rk3568/etc:product_etc_conf",
                    "//vendor/hihope/rk3568/thermal/profile:thermal_service_config", // Add the configuration for building of thermal_service_config.
                ]
            }
        },
        "subsystem": "product_hihope"
    }
    ```
    In the preceding code, `//vendor/hihope/rk3568/thermal/` is the folder path, `profile` is the folder name, and `thermal_service_config` is the build target.

6. Build the customized version by referring to [Quick Start](../quick-start/quickstart-overview.md).

    ```shell
    ./build.sh --product-name rk3568 --ccache
    ```

7. Burn the customized version to the DAYU200 development board.

### Debugging and Verification

1. After startup, run the following command to launch the shell command line:
    ```shell
    hdc shell
    ```

2. Obtain the current thermal control information.
    ```shell
    hidumper -s 3303 -a -a
    ```

    The following is the reference thermal control result after customization:
    ```shell
    -------------------------------[ability]-------------------------------


    ----------------------------------ThermalService---------------------------------
    name: cpu_big	strict: 0	enableEvent: 0
    name: cpu_med	strict: 0	enableEvent: 0
    name: cpu_lit	strict: 0	enableEvent: 0
    name: gpu	strict: 0	enableEvent: 0
    name: boost	strict: 0	enableEvent: 0
    name: lcd	strict: 0	enableEvent: 0
    name: volume	uid: 2001,2002	strict: 0	enableEvent: 0
    name: current	protocol: sc,buck	strict: 0	enableEvent: 1
    name: voltage	protocol: sc,buck	strict: 0	enableEvent: 1
    name: process_ctrl	strict: 0	enableEvent: 0
    name: shut_down	strict: 0	enableEvent: 0
    name: thermallevel	strict: 0	enableEvent: 0
    name: popup	strict: 0	enableEvent: 0
    ```

## Reference
During development, you can refer to the [default thermal control configuration](https://gitee.com/openharmony/powermgr_thermal_manager/blob/master/services/native/profile/thermal_service_config.xml).

Packing path: `/vendor/etc/thermal_config/hdf`
