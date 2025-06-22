# <img src="https://i.postimg.cc/RVfnZc7N/FH63-XNDI504-TRGD.png" width="48"> USB Partition Cleaning Guide using PowerShell

This guide walks you through the process of **removing all partitions and formatting a USB drive** using PowerShell’s DiskPart tool on Windows. This is especially useful when your USB drive has multiple partitions created by tools like **BalenaEtcher** or **Rufus**, and you want to restore it to a single, usable partition.

---

## 🚀 Prerequisites
- Windows OS
- Basic familiarity with PowerShell
- Administrator privileges

---

## ⚡ Step-by-Step Instructions

### 1. Open PowerShell as Administrator
- Press `Windows + X` and select **Windows PowerShell (Admin)**.

---

### 2. Identify Your USB Drive
```powershell
diskpart
````

```powershell
list disk
```

Look carefully at the **Size** column to identify your USB drive. For example:

```text
Disk 3    Online         7580 MB  6555 MB
```

---

### 3. Select the USB Drive

```powershell
select disk 3
```

*(Replace `3` with the disk number of your USB drive.)*

---

### 4. Clean the USB Drive

This will **erase all partitions and data** from the USB.

```powershell
clean
```

---

### 5. Create a New Partition

```powershell
create partition primary
```

---

### 6. Format the Drive

```powershell
format fs=ntfs quick
```

*(You can replace `ntfs` with `fat32` if you need FAT32 format.)*

---

### 7. (Optional) Assign a Drive Letter

```powershell
assign
```

---

### ✅ Done!

Your USB drive should now be cleaned, formatted, and ready to use as a single partition.

---

## ⚠️ Important Notes

* **Double-check** the disk number before using the `clean` command to avoid wiping the wrong drive.
* If your USB needs to be bootable again, you can use tools like Rufus or BalenaEtcher after this process.

---

## 📂 License

This guide is provided under the MIT License.
