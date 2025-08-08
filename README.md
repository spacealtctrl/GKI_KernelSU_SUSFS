### This is a repository for automatically building GKI kernels

> For non-GKI devices, you can try the resources from [SukiSU Cloud Drive](https://alist.shirkneko.top). OnePlus ColorOS 14 and 15 are not supported.
>
> If you are a first-time user, you must **read the following content in detail**. Don't waste others' time out of laziness!
>
> Recent updates: 1. OnePlus 8 with ELITE processor can use kernel 6.6 (untested). 2. Fixed compilation errors for these GKI versions: [5.10.(66, 81, 101), 5.15.(74, 94, 104)].

### Download
You can download your resources [here](https://github.com/zzh20188/GKI_KernelSU_SUSFS/releases).
1.  Regarding `Anykernel3.zip`, download and use it directly!
    * Then use a flashing tool, for example, [HorizonKernelFlasher](https://github.com/libxzr/HorizonKernelFlasher/releases), to flash the kernel.
2.  Regarding `boot.img`, download the one that matches your kernel format (uncompressed, gz, or lz4). [Refer to](https://kernelsu.org/guide/installation.html#install-with-boot-image) the **Find the correct boot.img** section.
    * Use [FASTBOOT](https://magiskcn.com/) to flash, or use a flashing tool to flash it to the boot partition of your ROOT slot (e.g., A-Play Machine, KernelFlasher).

### Support
| Feature | Description |
| --- | --- |
| [KernelSU](https://kernelsu.org/zh_CN/) | Includes **official, MKSU, SUKISU, and NEXT** versions. |
| [SUSFS4](https://gitlab.com/simonpunk/susfs4ksu) | A patch that assists KSU hiding functions at the kernel level. |
| [BBR](https://blog.thinkin.top/archives/ke-pu-bbrdao-di-shi-shi-me) | TCP congestion control algorithm. Does it make the network faster? |
| [Wireguard](https://en.wikipedia.org/wiki/WireGuard) | Refer to the wiki link on the left. |
| [LZ4KD](https://github.com/ShirkNeko/SukiSU_patch/tree/main/other) | Said to be a ZRAM algorithm from HUAWEI source. The patch was ported by [云彩之枫 (Maple of the Clouds)](http://www.coolapk.com/u/24963680). |

<details>
<summary>These algorithms are also supported and can be switched in scene's ZRAM</summary>

### LZ4K, LZ4HC, deflate, 842, ~~zstdn~~, lz4k_oplus

</details>

### KSU Manager
After the compilation is complete, you will see a file like `Next-Manager(12600)`. Simply put, this is the ***latest manager*** uploaded along with the kernel.
![Example](./assets/get_manager.gif)
Similarly, the [Releases](https://github.com/zzh20188/GKI_KernelSU_SUSFS/releases) page also contains the ***latest manager***!
![release](./assets/release_manager.gif)

### Emergency Rescue Guide

> [!IMPORTANT]
> **Trigger Conditions**
> Rescue is required when the device cannot boot due to the following reasons:
> - Flashed an incorrect/incompatible kernel
> - Kernel version mismatch (e.g., flashing a version 233 kernel on 5.10.66)
>
> 1.  Enter FASTBOOT mode
>     * Physical key combination: Power + Volume Down, or via ADB command: `adb reboot bootloader`
>
> 2.  Execute the flash command
> ```bash
> fastboot flash boot <full_boot.img_filename>
> ```

### How to get the original boot image
1.  Extract from existing firmware
    * For OTA zip packages: Unzip and use a [payload-dumper tool](https://magiskcn.com/payload-dumper-go-boot.html).
    * For fastboot packages: Unzip directly to get `boot.img`.
2.  Obtain from external resources
    * Search on community platforms: `device model + stock boot` (e.g., on XDA/CoolAPK).
    * [Extract remotely online from your mobile device](https://magiskcn.com/payload-dumper-compose.html).

> [!TIP]
> ### Kernel Version Compatibility Notes
>
> **1. Rules for flashing across minor versions**
> When your phone's main GKI version is 5.10.x (e.g., 5.10.168), you can flash kernels of the same main version with a higher minor version (e.g., 5.10.198).
> Regarding the **X-lts** version, taking `android12-5.10.X-lts-AnyKernel3.zip` as an example:
> - **X-lts** stands for Long-Term Support (has the highest minor version number, which is 5.10.236 in this example).
> - The LTS version number will continue to increase as the GKI source code is updated (other versions, like 198, are permanently fixed).
> - ⚠️ Note: Although LTS is the latest, **the latest version is not necessarily the most stable** (e.g., 6.6.x has a random reboot BUG).
>
> **2. Kernel version spoofing method**
> Execute in an MT Manager terminal:
> ```bash
> uname -r | sed 's/^[^-]*//'
> ```
> Copy the output directly and paste this version number into the Action compilation panel to achieve kernel version spoofing.
>
> **3. Compilation optimization suggestions**
> Modify the [configuration file](.github/workflows/kernel-a12-5.10.yml) (e.g., `kernel-a12-5.10.yml`):
> - ▶️ Delete/comment out unneeded GKI version configurations (**to speed up compilation**).
> - ➕ Add a specific GKI version (refer to the [Customization Guide](https://www.coolapk.com/feed/62820671?shareKey=OGMxYmZmNTk0YzIxNjgxNzM1MzI~&shareUid=11253396&shareFrom=com.coolapk.market_15.2.2)).
> - 📅 To modify the kernel build time, refer to the **`comment around line 490`** in the [gki-kernel.yml](.github/workflows/gki-kernel.yml) file.
