# <img src="https://i.postimg.cc/RVfnZc7N/FH63-XNDI504-TRGD.png" width="69"> USB Partition Cleaning Guide using PowerShell

*A comprehensive guide to completely clean and format USB drives using PowerShell's DiskPart utility*

---

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Step-by-Step Guide](#step-by-step-guide)
  - [1. Launch PowerShell as Admin](#1-launch-powershell-as-admin)
  - [2. Start DiskPart and List Disks](#2-start-diskpart-and-list-disks)
  - [3. Identify Your USB Drive](#3-identify-your-usb-drive)
  - [4. Select and Clean the USB](#4-select-and-clean-the-usb)
  - [5. Create a New Primary Partition](#5-create-a-new-primary-partition)
  - [6. Format the Partition](#6-format-the-partition)
  - [7. Assign a Drive Letter](#7-assign-a-drive-letter)
  - [8. Exit DiskPart](#8-exit-diskpart)
  - [9. Verify in File Explorer](#9-verify-in-file-explorer)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Introduction

This guide provides a clear method to **remove all partitions and reformat USB drives** using Windows PowerShell. Perfect when:
- Your USB has multiple partitions from tools like BalenaEtcher or Rufus
- You need to restore the drive to a single, clean partition
- Windows Disk Management can't delete protected partitions

---

## Prerequisites

- Windows 7/8/10/11
- PowerShell with **Administrator privileges**
- Basic command-line knowledge
- The USB drive you want to clean

> **Warning:** This process will **permanently erase all data** on the selected drive.

---

## Step-by-Step Guide

### 1. Launch PowerShell as Admin
```powershell
Press Win+X → Select "Windows PowerShell (Admin)"
```

### 2. Start DiskPart and List Disks
```powershell
diskpart
list disk
```

### 3. Identify Your USB Drive
Check the size column carefully. Example output:
```
Disk ###  Status      Size     Free
Disk 0    Online      465 GB   0 B
Disk 1    Online      931 GB   0 B
Disk 2    Online      14 GB    0 B  ← Likely USB
```

### 4. Select and Clean the USB
```powershell
select disk 2  # Replace with your disk number
clean
```

### 5. Create a New Primary Partition
```powershell
create partition primary
```
*This creates a new partition using all available space on the disk*

### 6. Format the Partition
Choose **one** of these formatting commands based on your needs:

#### Option A: NTFS Format (Recommended for Windows)
```powershell
format fs=ntfs quick label="USB_DRIVE"
```
*Faster format, supports large files (>4GB)*

#### Option B: FAT32 Format (For maximum compatibility)
```powershell
format fs=fat32 quick label="USB_DRIVE"
```
*Works with all devices but has 4GB file limit*

> **Note:** The `quick` flag performs a fast format. Remove it for full format (takes longer but checks for bad sectors)

### 7. Assign a Drive Letter
```powershell
assign
```
*Automatically assigns the next available drive letter*

### 8. Exit DiskPart
```powershell
exit
```
*Safely exits the DiskPart utility*

### 9. Verify in File Explorer
1. Open File Explorer (`Win + E`)
2. Check for your USB drive with the new label
3. The drive should show full capacity as one partition

> If the drive doesn't appear, safely remove and reinsert it

---

## Troubleshooting

**Problem:** DiskPart shows "Access Denied"  
**Solution:** Run PowerShell as **Administrator**

**Problem:** USB not appearing in Explorer after format  
**Solution:** Use `assign` command or replug the USB

**Problem:** Need bootable USB again  
**Solution:** Use Rufus/Etcher after this process

---

## License
MIT License - Feel free to use and modify this guide!

---
