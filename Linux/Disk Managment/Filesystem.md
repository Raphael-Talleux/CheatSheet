# File System

## Overview

Linux supports many filesystems, but only some are recommended for general use and stability. It is advised to read up on a filesystem's features and support state before using experimental ones for important partitions. **XFS** is the recommended modern, all-purpose filesystem.  

| Filesystem | Description | Key Features | Notes / Limitations |
|------------|-------------|--------------|-------------------|
| **XFS**    | Filesystem with metadata journaling. | Scalable, supports reflinks, Copy on Write (CoW), modern features. | Partitions cannot be shrunk (work in progress). Requires ≥300MB. Recommended for general use. |
| **ext4**   | Reliable, all-purpose filesystem. | Stable, widely supported. | Lacks modern features like reflinks. |
| **VFAT / FAT32** | Interoperability filesystem for Windows/macOS. | Supported by Linux, used for EFI System Partition. | No UNIX permissions, limited attributes. Needed for UEFI boot. |
| **btrfs**  | New generation filesystem. | Snapshots, checksums, transparent compression, subvolumes, integrated RAID. | Kernels <5.4 may be unsafe. RAID5/6 and quota groups unsafe. |
| **F2FS**   | Flash-Friendly File System (by Samsung). | Optimized for NAND flash storage. | Good for microSD, USB drives, or flash-based devices. |
| **NTFS**   | Microsoft Windows filesystem. | Interoperability with Windows. | Does not support UNIX permissions. Not recommended as root filesystem. |
| **ZFS**    | Next-generation filesystem by Ahrens & Bonwick. | Data integrity, redundancy, snapshots, never offline for repair. | Pools can be created on minimal installation CD. More info: ZFS/rootfs. |


## Applying a Filesystem to a Partition

**Note:**  
Before creating a filesystem, ensure the relevant user-space utilities package for your chosen filesystem is installed. Any `mkfs` command will **erase existing data** on the partition—back up important data first.

| Filesystem | Creation Command  | Package |
|------------|-----------------|--------|
| **XFS**    | `mkfs.xfs`   | `sys-fs/xfsprogs` |
| **ext4**   | `mkfs.ext4`   | `sys-fs/e2fsprogs` |
| **VFAT / FAT32** | `mkfs.vfat`  | `sys-fs/dosfstools` |
| **btrfs**  | `mkfs.btrfs`   | `sys-fs/btrfs-progs` |
| **F2FS**   | `mkfs.f2fs` | `sys-fs/f2fs-tools` |
| **NTFS**   | `mkfs.ntfs` | `sys-fs/ntfs3g` |
| **ZFS**    | `zpool create ...`| `sys-fs/zfs` |

### Examples

* **EFI System Partition** (`/dev/sda1`) must be FAT32:

```bash
mkfs.vfat -F 32 /dev/sda1
```

* **Root partition as XFS** (`/dev/sda3`):  
```bash
mkfs.xfs -c options=/usr/share/xfsprogs/mkfs/lts_6.6.conf /dev/sda3
````

* **Legacy BIOS boot partition** with XFS:

```bash
mkfs.xfs -c options=/usr/share/xfsprogs/mkfs/lts_6.6.conf /dev/sda1
```

* **Small ext4 partitions** (<8 GiB) should use the `-T small` option to increase the number of inodes:

```bash
mkfs.ext4 -T small /dev/<device>
```

This reduces bytes-per-inode from 16 KiB → 4 KiB, quadrupling the number of inodes.
