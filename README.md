This is a repository that automatically builds GKI kernels

Non-GKI can try [SukiSU Cloud Drive] (https://alist.shirkneko.top) resources, does not support OnePlus ColorOS14,15
>
The first time you use it must be read in detail, and don't take up other people's time because of laziness!
>
> Last Updated: 1. One plus 8ELITE processor can use 6.6 cores (not tested), 2. Fix these GKI versions to compile error - [5.10.( 66, 81, 101, 5.15. 74, 94, 104)]
### Download
You can download your resources [here] (https://github.com/zzh20188/GKKernelSU_SUSFS/releases)
1. About Anyoneel3.zip, Download Now!
- Then use the swipe-in software, such as [HorizonKernelFlasher] (https://github.com/libxzr/HorizonKernelFlasher/releases) to swipe the kernel
2. For boot.img, download the format that matches your kernel format (uncompressed, gz, lz4), [reference] (https://kernelsu.org/en_CN/guide/installation.html#install-by-kernelsu-boot-image) **Find the right boot.img** section
- Use [FASTBOOT] (https://magiskcn.com/) to swipe in, or use swipe software to swipe to the boot partition of the ROOT slot (e.g., fun game console, Kernelflasher)

### Support
Functions | Descriptions |
| -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
| [KernelSU] (https://kernelsu.org/en_CN/) | Includes ** Original, MKSU, SUKISU, NEXT** |
| [SUSFS4] (https://gitlab.com/simonpunk/susfs4ksu) | Features of KSU's hidden features at the kernel level |
| [BBR](https://blog.thinkin.top/archives/ke-pu-bbrdao-di-shi-shi-me) | TCP Congestion Control Algorithm to Make the Web Faster? | |
| [Wireguard] (https://zh.wikipedia.org/wiki/WireGuard) | Refer to the wiki link on the left |
| [LZ4KD] (https://github.com/ShirkNeko/SukiSU_patch/tree/main/other) | I heard of the ZRAM algorithm from HUAWEI source, patched by [Cloud Maple] (http://www.coolapk.com/u/24963680) |

<details>

<summary> also supports these algorithms, which can be switched between Scene's ZRAM</summary>

LZ4K, LZ4HC, deflate, 842, ~zstdn~~, lz4k_oplus

</details>

The KSU Manager
After the compilation is complete, you will see a file like Next-Manager (12600), which is simply the latest manager uploaded with the kernel.
![ Example] (./assets/get_manager.gif)
Similarly, in [Release] (https://github.com/zzh20188/GKKernelSU_SUSFS/releases) also contains the latest manager***!
![ release](./assets/release_manager.gif)

Emergency assistance guidelines

> [! IMPORTANT]
> **Trigger conditions**  
> Rescue when the device cannot be started due to:  
> - Brush into the wrong/incompatible kernel
> - Kernel version adaptation exception (such as 5.10.66 brush 233 version of the kernel)
1. Go to Fastboot mode

- Physical key combination: power + volume - or ADB command: `adb reboot bootloader`

2. Execute the brushing command
"Bash"
$ fastboot flash boot <boot.img file full name>
"```
### The original mirror access
1. Extract from existing firmware

- Card swipe package: use [payload-dumper tool] after decompression (https://magiskcn.com/payload-dumper-go-boot.html)

- Wire brush package: directly unpack to get boot.img

2. Access to external resources

- Community platform search: Model + original boot (such as XDA/Cool)

- [Mobile online extraction remote acquisition] (https://magiskcn.com/payload-dumper-compose.html)

> [! TIP]
> ### Kernel Version Compatibility Instructions
> 
> **1. Cross-sub-version brushing rules**  
When the main version of the phone GKI is 5.10.x (such as 5.10.168), you can swipe the kernel of the same main version of the older sub-version (such as 5.10.198).  
> About the **X-lts** version, to `android12-5.10. X-lts-AnyKernel3.zip` for example:
> - **X-lts** indicates long-term support (maximum sub-version number, current example 5.10.236)
> - LTS with GKI source code updates, the compiled version number will continue to increase (other versions, such as 198, are permanently fixed)
> - ⚠️ Note: LTS is the latest, ** but the latest version ≠ is the most stable (such as 6.6.x exists automatically restarted BUG)
> 
> **2. Kernel version camouflage method**  
> Execute at the MT Manager terminal:
> "`bash"
> uname -r | sed 's/^[^-]*//'
>"
> Copy directly after getting it, and fill this version number into the Action compilation panel to enable kernel version camouflage.
> 
> **3. Compilation Optimization Suggestions**  
> Modify the [profile] (.github/workflows/kernel-a12-5.10.yml) (e.g. kernel-a12-5.10.yml):
> - ▶️ Delete/Recommended GKI version configuration (**accelerated compilation**)
> - ➕ Add the specified GKI version (see [custom guide] (https://www.coolapk.com/feed/62820671?) shareKey=OGMxYmZmNTk0YzIxNjgxNzM1MzI~&shareUid=11253396&shareFrom.apcoolk.market_15.2.2)
> - 📅 Kernel build time, with reference to [gki-kernel.yml] (.github/workflows/gki-kernel.yml) file **`Notes around line 490`**
