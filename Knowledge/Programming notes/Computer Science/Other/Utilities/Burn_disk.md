# 🔒 Securely Wipe a Disk Before Selling — Windows

> [!abstract] Overview **Goal:** Remove personal data before selling, donating, or giving away a computer or storage drive.
> 
> **Important:** A quick format or deleting files is not enough to reliably prevent data recovery. Choose a sanitization method appropriate for your storage device and the sensitivity of your data.

## 🧠 Understand the Difference

|Method|What it does|Suitable for selling?|
|---|---|---|
|Delete files|Removes file references|❌ No|
|Quick format|Recreates filesystem structures|❌ No|
|Full format in Windows|Writes zeros to sectors on supported Windows versions|⚠️ Depends on the device and threat|
|Windows Reset + Clean data|Removes personal files and makes recovery harder|✅ Good consumer option|
|Manufacturer Secure Erase / Sanitize|Uses a supported drive-level sanitization function|✅ Preferred for stronger SSD/HDD sanitization|

> [!warning] Remember **Formatting is not the same as secure erasure.** SSDs can retain inaccessible flash cells, and ordinary formatting may not sanitize every area of a drive.

## 🛡️ Step 1 — Prepare Before Wiping

Before starting, complete this checklist.

- [ ] Back up documents, photos, passwords, and other important files.
- [ ] Verify that your backup actually works.
- [ ] Save your BitLocker recovery key if device encryption is enabled.
- [ ] Sign out of accounts and deauthorize software where necessary.
- [ ] Disconnect external drives and USB storage you do not intend to erase.
- [ ] Identify every internal drive included in the sale.
- [ ] Connect a laptop to its power adapter.

> [!danger] Irreversible operation The following procedures can permanently destroy data. Double-check the selected disk, its capacity, and its model before proceeding.

## 💻 Method 1 — Reset Windows Before Selling a PC

**Best for:** Selling a Windows 11 or Windows 10 computer with its operating system included.

### Steps

1. Open **Settings**.
2. Navigate to:
    - Windows 11: `System → Recovery`
    - Windows 10: `Update & Security → Recovery`
3. Select **Reset this PC**.
4. Choose **Remove everything**.
5. Open the reset settings or **Change settings**, if available.
6. Enable **Clean data** or the option to clean the drive.
7. Choose **Cloud download** or **Local reinstall**.
8. Review the summary carefully and start the reset.
9. Allow the process to finish without interrupting it.

Microsoft recommends the Remove everything and Clean data options when preparing a computer for sale or donation. However, this consumer feature does not meet every professional or industry sanitization standard. [Microsoft's reset guide](https://support.microsoft.com/en-us/windows/experience/backup-recovery/reset-your-pc)

> [!tip] Final step If you are selling the computer with Windows installed, stop at the initial Windows setup screen. Let the new owner complete setup.

## 💽 Method 2 — Erase a Secondary HDD Using DiskPart

**Best for:** A traditional hard disk drive (HDD) that you want to erase completely before selling separately.

DiskPart's `clean all` command writes zeros to every addressable sector on the selected disk. It takes considerably longer than a quick format and destroys the existing partition layout and data.

### Step 1 — Open an elevated terminal

Open **Command Prompt as administrator** or **Windows Terminal as administrator**.

### Step 2 — Start DiskPart

```
diskpart
```

### Step 3 — List available disks

```
list disk
```

Check the disk numbers and capacities carefully.

### Step 4 — Select the intended disk

```
select disk N
```

Replace `N` with the correct disk number.

### Step 5 — Verify your selection

```
detail disk
```

Confirm that this is the drive you intend to erase.

### Step 6 — Erase the disk

```
clean all
```

Wait for DiskPart to report that the operation completed successfully. Large drives can take hours.

### Step 7 — Exit DiskPart

```
exit
```

> [!danger] Critical warning `clean all` is destructive. Selecting the wrong disk can erase the wrong drive. It is not the recommended universal sanitization method for SSDs, and it may not address every hidden or remapped sector.

## ⚡ Method 3 — Securely Sanitize an SSD

**Best for:** SATA SSDs and NVMe SSDs.

For an SSD, prefer the drive manufacturer's supported **Secure Erase**, **Sanitize**, or **NVMe Format with User Data Erase** function.

### General procedure

1. Identify the SSD's exact model.
2. Visit the manufacturer's official support website.
3. Find its recommended secure-erasure utility or instructions.
4. Follow the procedure for your particular model and connection type.
5. Verify that the sanitization operation completed successfully.
6. If selling a complete PC, reinstall Windows or reset the computer afterward if needed.

Some drives support cryptographic erase, which makes previously stored encrypted data inaccessible by destroying or replacing the relevant encryption keys. This is appropriate only when the implementation and prior encryption meet the required security conditions.

> [!note] Why not use `clean all` for every SSD? Flash storage uses wear levelling and spare cells, so overwriting addressable sectors is not necessarily equivalent to sanitizing the entire device. Use a supported drive-level sanitization feature for stronger assurance.

For additional technical guidance, see the [NIST Guidelines for Media Sanitization](https://csrc.nist.gov/pubs/sp/800/88/r2/ipd).

## 🔌 Method 4 — Wipe a USB Flash Drive or External Disk

**Best for:** Selling or giving away removable storage.

1. Back up anything you need.
2. Identify whether the device uses an HDD, SSD, or flash memory.
3. For an external HDD, consider a suitable full overwrite.
4. For an external SSD or USB flash drive, check whether the manufacturer provides a reliable sanitization function.
5. Verify the result before handing the device over.

A quick format is not sufficient when you need to make recovery difficult. If the device contains highly sensitive information and does not support trustworthy sanitization, retaining or physically destroying it through an appropriate disposal service may be safer than reselling it.

## 🔍 Verify the Result

After erasure:

- [ ] Confirm that the operation completed without errors.
- [ ] Check that the expected partitions and files are no longer accessible.
- [ ] Confirm that the correct drive was erased.
- [ ] For a high-assurance wipe, use the manufacturer's verification procedure or an appropriate independent validation method.
- [ ] Reinstall Windows if the computer is being sold as a working PC.
- [ ] Leave the computer at the Windows initial setup screen.

**Important:** Seeing an empty drive or a fresh Windows installation does not, by itself, prove that all previous data is unrecoverable.

## 🧰 Quick Reference

|Situation|Recommended approach|
|---|---|
|Selling a Windows PC|Reset this PC → Remove everything → Clean data|
|Selling a secondary HDD|Full overwrite or an appropriate drive sanitization method|
|Selling an SSD|Manufacturer-supported Secure Erase or Sanitize|
|Selling a USB flash drive|Manufacturer-supported sanitization, if available|
|Highly sensitive data|Use a validated sanitization process appropriate to the risk|
|Drive cannot be sanitized reliably|Retain it or use secure physical destruction|

## 🔗 Related Notes

- [[ARP Command — Windows]]
- [[NET Command — Windows]]
- [[DiskPart — Windows]]
- [[BitLocker — Windows]]
- [[Windows Recovery Environment]]
- [[Data Backup and Recovery]]

## 📚 References

- [Microsoft — Reset your PC](https://support.microsoft.com/en-us/windows/experience/backup-recovery/reset-your-pc)
- [Microsoft — Before you recycle, sell, or gift your Windows PC](https://support.microsoft.com/en-us/accounts-billing/security/before-you-recycle-sell-or-gift-your-xbox-or-windows-pc)
- [NIST — Guidelines for Media Sanitization](https://csrc.nist.gov/pubs/sp/800/88/r2/ipd)

---

> [!summary] Key Takeaway **For a normal Windows PC sale:** use _Reset this PC → Remove everything → Clean data_.
> 
> **For a separate HDD:** consider a full overwrite or suitable sanitization method.
> 
> **For an SSD:** use the manufacturer's supported Secure Erase or Sanitize feature when stronger data protection is required.
> 
> Always back up your data and verify the target disk before starting.