# DeviceInfo Adaptation

## DeviceInfo parameters and mapping APIs

| Parameter| API| Description|
|----------|------- |------|
| const.product.devicetype | const&nbsp;char\*&nbsp;GetDeviceType(void) | Obtains the device type.|
| const.product.manufacturer | const&nbsp;char\*&nbsp;GetManufacture(void) | Obtains the device manufacturer.|
| const.product.brand | const&nbsp;char\*&nbsp;GetBrand(void) | Obtains the device brand.|
| const.product.name | const&nbsp;char\*&nbsp;GetMarketName(void) | Obtains the device marketing name.|
| const.build.product | const&nbsp;char\*&nbsp;GetProductSeries(void) | Obtains the device series name.|
| const.product.model | const&nbsp;char\*&nbsp;GetProductModel(void) | Obtains the device authentication model.|
| const.software.model | const&nbsp;char\*&nbsp;GetSoftwareModel(void) | Obtains the device software model.|
| const.product.hardwareversion | const&nbsp;char\*&nbsp;GetHardwareModel(void) | Obtains the device hardware model.|
| const.product.hardwareprofile | const&nbsp;char\*&nbsp;GetHardwareProfile(void) | Obtains the device hardware profile.|
| ohos.boot.sn | const&nbsp;char\*&nbsp;GetSerial(void) | Obtains the serial number (SN) of the device.|
| const.product.software.version | const&nbsp;char\*&nbsp;GetDisplayVersion(void) | Obtains the software version visible to users.|
| const.product.bootloader.version | const&nbsp;char\*&nbsp;GetBootloaderVersion(void) | Obtains the bootloader version of the device.|
| const.product.udid | int&nbsp;GetDevUdid(char&nbsp;\*udid,&nbsp;int&nbsp;size) | Obtains the UDID of the device through **DeviceInfo** or through calculation if the attempt to obtain the UDID through **DeviceInfo** fails.|
| | const char *AclGetSerial(void); | Obtains the SN of the device (with ACL check).|
| | int AclGetDevUdid(char *udid, int size); | Obtains the UDID of the device (with ACL check).|

## DeviceInfo Source

### Adaptation of OHOS Fixed-value Parameters

- OHOS fixed-value parameters:

  ```
  const.ohos.version.security_patch
  const.ohos.releasetype
  const.ohos.apiversion
  const.ohos.fullname
  ```

- Description of adaptation:

  OHOS fixed-value parameters are filled by the OHOS and do not need to be adapted by vendors. Currently, these parameters are defined in the **/base/startup/init/services/etc/param/ohos_const/ohos.para** file.

### Adaptation of Vendor Fixed-value Parameters

- Vendor fixed-value parameters:

  ```
  const.product.devicetype
  const.product.manufacturer
  const.product.brand
  const.product.name
  const.build.product
  const.product.model
  const.software.model
  const.product.hardwareversion
  const.product.hardwareprofile
  const.product.software.version
  const.product.bootloader.version
  const.build.characteristics
  ... ...

  ```


- Description of adaptation:

  Adapt parameters in the **vendor** directory based on actual requirements.

   (1) Take RK3568 as an example for standard-system devices. Adapt parameters in the **/vendor/hihope/rk3568/etc/para/hardware_rk3568.para** file and install the file to the specified directory.

   ```
   ohos_prebuilt_etc("para_for_chip_prod") {
    source = "./para/hardware_rk3568.para"
    install_images = [ chip_prod_base_dir ]
    relative_install_dir = "para"
    part_name = "product_rk3568"
   }
   ```

   (2) For mini- and small-system devices, adapt parameters in the respective **hals/utils/sys_param/vendor.para** file. For example:

    ```
    const.product.manufacturer=Talkweb

    const.product.brand=Talkweb

    const.product.name=Niobe

    const.build.product=Niobe

    const.product.model=Niobe407

    const.software.model="2.0.0"

    const.product.hardwareversion="1.0.0"

    const.product.hardwareprofile="RAM:192K,ROM:1M,ETH:true"
    ... ...
    ```

### Adaptation of Vendor Dynamic-value Parameters

- Currently, three ways are provided to obtain vendor dynamic-value parameters: cmdline, macro definition, and **BUILD.gn** definition.

  1. cmdline: Values that are read from cmdline include **ohos.boot.hardware**, **ohos.boot.bootslots**, and **ohos.boot.sn**. The way to obtain **ohos.boot.sn** differs according to the system type as follows:

   (1) For standard-system devices: **ohos.boot.sn** is read from cmdline (generated by U-Boot). If the SN is obtained, the value is directly read; if the file path is obtained, the value is read from the file. If the preceding attempt fails, the value is read from the default SN files; that is, **/sys/block/mmcblk0/device/cid** and **/proc/bootdevice/cid**.

   (2) For mini- and small-system devices: These devices may come with their own special algorithms. Therefore, **HalGetSerial()** can be used to obtain the SN from the **hal_sys_param.c** file in the **hals/utils/sys_param** directory.

  2. Macro definition: Obtain parameter values by compiling macro definitions. Currently, this mode is available only for mini- and small-system devices. For example:

  ```
    defines = [
    "INCREMENTAL_VERSION=\"${ohos_version}\"",
    "BUILD_TYPE=\"${ohos_build_type}\"",
    "BUILD_USER=\"${ohos_build_user}\"",
    "BUILD_TIME=\"${ohos_build_time}\"",
    "BUILD_HOST=\"${ohos_build_host}\"",
    "BUILD_ROOTHASH=\"${ohos_build_roothash}\"",
  ]
  ```

  3. **BUILD.gn** definition: Obtain parameter values from the **/base/startup/init/services/etc/BUILD.gn** file. For example:

  ```
    if (target_cpu == "arm64") {
      extra_paras += [ "const.product.cpu.abilist=arm64-v8a" ]
    }
    if (build_variant == "user") {
      extra_paras += [
        "const.secure=1",
        "const.debuggable=0",
      ]
    } else if (build_variant == "root") {
      extra_paras += [
        "const.secure=0",
        "const.debuggable=1",
      ]
    }
    if (device_type != "default") {
      extra_paras += [
        "const.product.devicetype=${device_type}",
        "const.build.characteristics=${device_type}",
      ]
    }
    module_install_dir = "etc/param"
  }
  ```
#### Notes

  (1) For small-system devices, add the compilation of **vendor.para** to the **hals/utils/sys_param/BUILD.gn** file.

  ```
  copy("vendor.para") {
    sources = [ "./vendor.para" ]
    outputs = [ "$root_out_dir/vendor/etc/param/vendor.para" ]
  }
  ```

  (2) For mini-system devices, a file system is not available and therefore, the **hal_sys_param.c** and **vendor.para** files are converted into header files and are compiled to the system during compilation.