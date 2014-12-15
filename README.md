Copyright (C) Sony Mobile Communications 2014
=============================================

This is the Android device configuration for Xperia (yukon platform).

To setup a tree and build images for the device do the following:

`repo init` as described by Google over at:
http://source.android.com/source/downloading.html

Put the following snippet in `.repo/local_manifests/yukon.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<remote  name="sony" fetch="git://github.com/sonyxperiadev/" />

<remove-project name="platform/hardware/qcom/media" />
<remove-project name="platform/hardware/invensense" />
<remove-project name="platform/hardware/akm" />

<project path="device/sony/eagle" name="device-sony-eagle" groups="device" remote="sony" revision="master" />
<project path="device/sony/flamingo" name="device-sony-flamingo" groups="device" remote="sony" revision="master" />
<project path="device/sony/seagull" name="device-sony-seagull" groups="device" remote="sony" revision="master" />
<project path="device/sony/tianchi" name="device-sony-tianchi" groups="device" remote="sony" revision="master" />
<project path="device/sony/yukon" name="device-sony-yukon" groups="device" remote="sony" revision="master" />
</manifest>
```

Download the zip file with vendor binaries from:
http://developer.sonymobile.com/downloads/tool/software-binaries-for-xperia-z2-xperia-z1-and-xperia-z/

In the root of your Android code tree unzip the corresponding vendor zip.


You should now have vendor directories named in your tree.

* `repo sync`
* `source ./build/envsetup.sh`
* `lunch aosp_xxxx-userdebug`
* `make`

To flash the images produced make sure your device is unlocked, as described on
http://unlockbootloader.sonymobile.com/

Enter fastboot mode on the device by pressing volume up while inserting the USB
cable or execute `adb reboot bootloader`.

* `fastboot flash boot out/target/product/<device>/boot.img`
* `fastboot flash system out/target/product/<device>/system.img`
* `fastboot flash userdata out/target/product/<device>/userdata.img`

Reflashing userdata is not necessary every time, but incompatibilities with
previous content might result in a device that doesn't boot. If this happens
try to reflash just the userdata again.
