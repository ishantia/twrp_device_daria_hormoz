# TWRP Recovery for Daria Bond II (hormoz)

An open-source custom recovery image based on Team Win Recovery Project (TWRP) for the **Daria Bond II (hormoz)**.

---

## Device Specifications

| Feature | Details |
| :--- | :--- |
| **Device** | Daria Bond II |
| **Codename** | hormoz |
| **SoC** | MediaTek Dimensity 8350 |
| **CPU** | Octa-Core (1×3.35 GHz + 3×3.2 GHz + 4×2.2 GHz) |
| **GPU** | Mali-G615 |
| **RAM** | 12GB LPDDR5X |
| **Storage** | 512GB UFS 4.0 |
| **Display** | 6.67" AMOLED, 120Hz (1220 × 2712) |
| **Battery** | 5000mAh |
| **Shipped OS** | DariaOS 5.0 (Android 14) |

---

## Build Status

*   **Current State:** Active Development / Testing
*   **TWRP Version:** 12.1 / 14 (AOSP-based)

### Status Matrix

| Component | Status | Notes |
| :--- | :--- | :--- |
| **Touchscreen** |  Working | Full touch response operational |
| **ADB Sideload** |  Working (With Bugs) | Functional, but encounters issues during active slot-switching |
| **MTP** |  Working | File transfer functional |
| **USB OTG** |  Working | OTG storage mount functional |
| **Fastbootd** |  Working | Fastbootd mode operational for dynamic partitions |
| **Vibrator** |  Working | Haptic feedback operational |
| **Brightness** |  Working | Brightness adjustment functional |
| **Battery Info** |  Working | Battery level and charging status reporting |
| **Backup / Restore** |  Working (Partial) | Fully operational for system/super/logical partitions; fails on /data due to encryption |
| **Data Mounting** |  Not Working | /data partition cannot be mounted (Decryption/FBE Issue) |

---

## How to Build

To initialize your local repository and build TWRP for Daria Bond II, follow these steps:

### 1. Initialize TWRP Minimal Manifest

repo init --depth=1 -u [https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git](https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git) -b twrp-12.1

2. Clone the Device Tree
Clone this repository into your build tree:

git clone [https://github.com/MorZeus/twrp_device_daria_hormoz.git](https://github.com/MorZeus/twrp_device_daria_hormoz.git) device/daria/hormoz

3. Build the Recovery Image

# Set up the build environment
source build/envsetup.sh

# Select the build target
lunch twrp_hormoz-eng

# Start the compilation
mka recoveryimage

Known Issues & Notes
FBE / Data Decryption: The /data partition currently fails to mount due to File-Based Encryption (FBE) implementation on MediaTek Dimensity 8350. Consequently, backup/restore operations for User Data are blocked until decryption libs/keys are correctly bound in the ramdisk.

Super/Logical Partition Backup: Backup and Restore functionalities are verified and fully working for metadata and raw sub-partitions inside the Super block.

A/B Slot-Switching: While adb sideload is operational, switching active boot slots (Slot A/B) during recovery operations may trigger intermittent mount errors or partition locks.

## Credits
* **TeamWin** - For the Custom Recovery Project
* **itisMahdi** - For the initial base device tree layout reference
* **Hovatech** - For MTK development guides and supplementary resources
* **DariaOS community** - For resources and support


