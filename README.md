# android_device_oneplus_dumpling
Tree for building TWRP for OnePlus 5T (Decryption works on Android 12.x ROMs)

## Device specifications

| Device       | OnePlus 5T                                      |
| -----------: | :---------------------------------------------- |
| SoC          | Qualcomm MSM8998 Snapdragon 835                 |
| CPU          | Quad-core 2.45GHz Kryo & quad-core 1.9GHz Kryo  |
| GPU          | 710MHz Adreno 540                               |
| Memory       | 6GB / 8GM RAM (LPDDR4X)                         |
| Shipped Android version | 7.1.1                                |
| Storage      | 64GB / 128GB (UFS 2.1 2-LANE Flash)             |
| Battery      | Non-removable Li-Po 3300 mAh                    |
| Dimensions   | 152.7 x 74.1 x 7.25 mm                          |
| Display      | 2160 x 1080 (18:9), 6 inch                      |
| Rear camera 1 | 16MP (IMX 398), 1.12-micron pixels, f/1.7 Dual LED flash, 4K 30 fps, 1080p 60 fps, 720p 120 fps video |
| Rear camera 2 | 20MP (IMX 376k), 1-micron pixels, f/1.7        |
| Front camera | 16MP (IMX 371), 1-micron pixels, f/2.0 1080p 30 fps video |

## Device picture

![OnePlus 5T](https://cdn.opstatics.com/store/20170907/assets/images/support/support-list/model-specs-list/details/5t-black.png "OnePlus 5T in black")

## Kernel

Kernel source: (prebuilt)
https://github.com/faoliveira78/android_kernel_oneplus_msm8998

## Compile

First repo init the TWRP 12.1 tree:

```
mkdir ~/android/twrp-12.1
cd ~/android/twrp-12.1
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1
```

Then add to a local manifest (if you don't have .repo/local_manifests then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="faoliveira78/android_kernel_oneplus_msm8998" path="kernel/oneplus/msm8998" remote="github" revision="lineage-19.1"/>
  <project name="faoliveira78/android_device_oneplus_dumpling" path="device/oneplus/dumpling" remote="github" revision="android-12.1"/>
</manifest>
```

Now you can sync your source:

```
repo sync
```

To be able to compile you need to cherry-pick the following commits:

```
source build/envsetup.sh
repopick 5405 5540
```
Finally execute these:

```
. build/envsetup.sh
export LC_ALL=C
lunch twrp_dumpling-eng
mka recoveryimage
```
