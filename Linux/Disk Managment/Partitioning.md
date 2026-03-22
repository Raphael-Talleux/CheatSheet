
# Partitioning for UEFI and BIOS

## Recommended Partition Layout

| Device      | Mount Point | File System | DPS UUID (Type-UUID)                     | Description                  |
|------------|------------|------------|----------------------------------------|------------------------------|
| /dev/sda1  | /efi       | vfat       | c12a7328-f81f-11d2-ba4b-00a0c93ec93b  | EFI System Partition (ESP)   |
| /dev/sda2  | N/A        | swap       | 0657fd6d-a4ab-43c4-84e5-0933c84b4f4f  | Swap partition               |
| /dev/sda3  | /          | xfs        | 4f68bce3-e8cd-4db1-96e7-fbcaf984b709  | Root partition               |


## Viewing Current Partition Layout

```bash
fdisk /dev/sda
# press 'p' to print partition table
````

Example output:

```
Disk /dev/sda: 931.51 GiB
Disklabel type: gpt

Device     Start       End       Sectors   Size Type
/dev/sda1  2048        2099199   1G        EFI System
/dev/sda2  2099200     10487807  4G        Linux swap
/dev/sda3  10487808    1953523711 926.5G  Linux root (x86-64)
```

## Disk Labels

A **disk label** (or partition table) is metadata at the start of a disk that describes how the disk is divided into partitions.  
It tells the system:

- Where each partition starts and ends (sectors)
- The type of each partition (EFI, swap, Linux root, etc.)
- Optional unique identifiers for partitions or the disk itself

### Common Types

| Type | Description | Use Case |
|------|------------|----------|
| **MBR** | Legacy partition table, supports up to 2 TB and 4 primary partitions | BIOS systems, older hardware |
| **GPT** | Modern partition table, part of UEFI spec, supports large disks and many partitions | UEFI systems, Linux, Windows 64-bit |

