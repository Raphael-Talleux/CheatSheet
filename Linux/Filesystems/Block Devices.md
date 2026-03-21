# Block Devices

## 1. Block Devices Overview

Block devices represent an abstract interface to storage drives. Programs interact with them as a series of contiguous, randomly-accessible 4 KB blocks, without worrying about the underlying hardware (SATA, SCSI, NVMe, etc.).

## 2. Common Block Device Types

| Device Type                       | Default Device Handle | Notes & Considerations |
|----------------------------------|---------------------|----------------------|
| IDE, SATA, SAS, SCSI, USB flash  | `/dev/sda`          | Found on hardware from ~2007 to present. Most common in Linux. Example: first partition on the first SATA device is `/dev/sda1`. |
| NVM Express (NVMe)                | `/dev/nvme0n1`      | PCI Express connected SSDs, very fast. Systems from ~2014+ may support NVMe. First partition: `/dev/nvme0n1p1`. |
| MMC, eMMC, SD                     | `/dev/mmcblk0`      | Embedded MMC, SD cards, and memory cards. Usually not suitable for active Linux installations; good for file transfer or short-term backups. |
| VirtIO                            | `/dev/vda`          | Virtualized device in QEMU/KVM VMs. `virtio_blk` driver allows access to host-allocated storage. Useful for testing Linux in virtual environments. |

## 3. Device Naming Conventions

- **SATA/SCSI/USB**: `/dev/sdXN`  
  - `X` = device letter (a, b, c…)  
  - `N` = partition number (1, 2, 3…)  
  - Example: `/dev/sda1` → first partition on first SATA/SCSI disk.

- **NVMe**: `/dev/nvmeXpY`  
  - `X` = NVMe controller number (0, 1…)  
  - `Y` = partition number (1, 2…)  
  - Example: `/dev/nvme0n1p1` → first partition on first NVMe disk.

- **MMC/eMMC/SD**: `/dev/mmcblkNpM`  
  - `N` = device number (0, 1…)  
  - `M` = partition number (1, 2…)  
  - Example: `/dev/mmcblk0p1`.

- **VirtIO**: `/dev/vdXN`  
  - `X` = device letter  
  - `N` = partition number  
  - Example: `/dev/vda1`.