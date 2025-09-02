### This is a repository for automatically building the GKI kernel.

> Non-GKI users can try the resources from [SukiSU Cloud Disk](https://alist.shirkneko.top). OnePlus ColorOS 14 and 15 are not supported.
>
> First-time users, please **read** the following carefully. Don't waste other people's time out of laziness!
>
> Recent updates: 1. The OnePlus 8 ELITE processor can now use the 6.6 kernel (untested). 2. Fixed compilation errors with these GKI versions: [5.10. (66, 81, 101), 5.15. (74, 94, 104)].
### Download
You can download your resources [here](https://github.com/zzh20188/GKI_KernelSU_SUSFS/releases).
1. About Anykernel3.zip: Download and use it now!
- Then use flashing software such as [HorizonKernelFlasher](https://github.com/libxzr/HorizonKernelFlasher/releases) to flash the kernel.
2. Regarding the boot.img file, download the one that matches your kernel format (uncompressed, gz, lz4). Refer to the section "Finding the Right Boot.img" in [https://kernelsu.org/zh_CN/guide/installation.html#install-by-kernelsu-boot-image].
- Flash using [FASTBOOT](https://magiskcn.com/), or use flashing software such as Aiwanji or Kernelflasher to flash the kernel to the boot partition in the root slot.

### Supported
| Features | Description |
| --- | --- |
| [KernelSU](https://kernelsu.org/zh_CN/) | Includes **Original, MKSU, SUKISU, and NEXT** |
| [SUSFS4](https://gitlab.com/simonpunk/susfs4ksu) | Kernel-level patch to assist with KSU's hidden functionality |
| [BBR](https://blog.thinkin.top/archives/ke-pu-bbrdao-di-shi-shi-me) | TCP congestion control algorithm: making the network faster? |
| [Wireguard](https://zh.wikipedia.org/wiki/WireGuard) | See the wiki link on the left |
| [LZ4KD](https://github.com/ShirkNeko/SukiSU_patch/tree/main/other) | I heard this is a ZRAM algorithm from the HUAWEI source code. The patch was ported by [Cloud Maple](http://www.coolapk.com/u/24963680) |

<details>

<summary>These algorithms are also supported and can be switched in the ZRAM scene.</summary>

### LZ4K, LZ4HC, deflate, 842, ~~zstdn~~, lz4k_oplus

</details>

### KSU Manager
After the compilation is complete, you will see a file similar to `Next-Manager(12600)`. Simply put, this is the ***latest manager*** uploaded with the kernel.
![Example](./assets/get_manager.gif)
Similarly, the latest manager is also included in [Release](https://github.com/zzh20188/GKI_KernelSU_SUSFS/releases)!
![release](./assets/release_manager.gif)

### Emergency Rescue Guide

> [!IMPORTANT]
> **Trigger Conditions**
> Rescue is required when the device fails to boot due to the following reasons:
> - Flashing an incorrect/incompatible kernel
> - Kernel version mismatch (e.g., flashing kernel version 233 on 5.10.66)

1. Enter Fastboot mode

- Physical key combination: Power + Volume Up

Or ADB command: `adb reboot bootloader`

2. Execute the flash command
```bash
$ fastboot flash boot <full name of the boot.img file>
```
### Obtaining the Original Image
1. Extract from the existing firmware

- Flashing the package: Unzip and use the [payload-dumper tool](https://magiskcn.com/payload-dumper-go-boot.html)

- Flashing the package: Directly unzip and obtain the boot.img image.

2. Obtaining from external sources

- Search on community platforms: Model + Factory Boot (e.g., XDA/CoolAnk)

- [Mobile Online Extraction and Remote Access](https://magiskcn.com/payload-dumper-compose.html)

> [!TIP]
> ### Kernel Version Compatibility
>
> **1. Flashing across sub-versions**
> When the phone's GKI major version is 5.10.x (e.g., 5.10.168), you can flash a kernel with a higher sub-version of the same major version (e.g., 5.10.198).
> Regarding the **X-lts** version, using `android12-5.10.X-lts-AnyKernel3.zip` as an example:
> - **X-lts** indicates the long-term support release (with the highest sub-version number, currently 5.10.236).
> - The LTS build version number will continue to increase with GKI source code updates (other versions, such as 198, are permanently fixed).
> - ⚠️ Note: Although LTS is the latest, it is not necessarily the most stable (for example, 6.6.x has an automatic restart bug).
>
> **2. Kernel version camouflage method**
> In the MT Manager terminal, execute:
> ```bash
> uname -r | sed 's/^[^-]*//'
> ```
> Copy the obtained version number and enter it in the Action build panel to achieve kernel version camouflage.
>
> **3. Compilation Optimization Suggestions**
> Modify the [configuration file](.github/workflows/kernel-a12-5.10.yml) (e.g., kernel-a12-5.10.yml):
> - ▶️ Delete/comment out unnecessary GKI version configuration (**Speed ​​up compilation**)
> - ➕ Add a specific GKI version (refer to the [Customization Guide](https://www.coolapk.com/feed/62820671?shareKey=OGMxYmZmNTk0YzIxNjgxNzM1MzI~&shareUid=11253396&shareFrom=com.coolapk.market_15.2.2))
> - 📅 For kernel build time, refer to the comment around line 490 in the [gki-kernel.yml](.github/workflows/gki-kernel.yml) file and modify it.
