# Partition Tables

## GUID Partition Table (GPT)

- Uses **64-bit identifiers** for partitions.  
- Partition info storage is much larger than MBR's 512 bytes → practically unlimited partitions.  
- Maximum partition size: ~8 **ZiB** (zebibytes).  
- Required for **UEFI** boot systems.  
- Features **checksums and redundancy**:
  - CRC32 checksums detect errors in headers/tables.
  - Backup GPT at the disk end allows recovery of the primary GPT.  

**Caveats:**
- GPT on **BIOS**-based computers works, but Windows cannot boot from GPT in BIOS mode.  
- Some older BIOS firmware may fail to boot GPT-labeled disks.


## Master Boot Record (MBR)

- Also called **DOS disklabel** or **legacy BIOS boot**.  
- Introduced in 1983 with PC DOS 2.x.  
- Uses **32-bit identifiers** for start sector and length → max partition table size: 2 TiB.  
- Partition types:
  1. **Primary** – stored in MBR itself, max **4 primary partitions**.  
  2. **Extended** – one primary partition can become extended to house additional **logical partitions**.  

**Limitations:**
- Only **4 primary partitions** unless extended partitions are used.  
- No backup of the partition table → corruption leads to data loss.  
- Legacy hardware support; modern post-2010 motherboards consider MBR a legacy mode.  

**Use Cases:**
- Still supported in virtualized environments like AWS or older BIOS systems.  


## Quick Comparison Table

| Feature                     | GPT                     | MBR (DOS)            |
|------------------------------|------------------------|---------------------|
| Identifier Size             | 64-bit                 | 32-bit              |
| Max Partitions              | Practically unlimited  | 4 primary (+logical)|
| Max Partition Size          | ~8 ZiB                 | 2 TiB               |
| Boot Type                   | UEFI                   | BIOS (legacy)       |
| Backup/Redundancy           | Yes (CRC32 + backup)   | No                  |
| Modern Recommendation       | Preferred              | Legacy              |
