# Lab Report: PC Introduction and Disk Analysis

## Student Information

| Field | Details |
|---|---|
| Student Name | Clement Modebe |
| Student ID | aci2616123@icdfa.edu.ng |
| Course Name | Advanced Cybercrime Investigations |
| Instructor Name | Mr. Aminu Idris |
| Date of Submission | 8 May 2026 |

---

# Executive Summary (150–200 words)

This lab introduced the basic structure of a PC system and demonstrated how disk and partition information can be examined at a low level for digital forensics. Using Oracle VirtualBox with a Kali-Forensics VM, I identified disks and partitions with tools such as `lsblk` and `fdisk`, then captured raw disk data from Sector 0 (the MBR) using `dd` and examined the bytes in hex using `xxd` and WinHex.

I extracted key partition-table fields—Starting LBA and Total Sectors—and used Python 3 to convert little-endian hex values into decimal and compute partition sizes in GB using the 512-bytes-per-sector formula. I also completed a disk geometry (CHS) calculation to estimate total disk size and reviewed the PC boot process, including BIOS vs UEFI.

The main findings were that partition-size calculations match expected sizes when endianness is handled correctly, and that GPT disks may show a protective MBR on Sector 0, meaning MBR values may not represent the actual GPT partitions directly.

---

# Lab Objectives

- Describe the layers of a computer system and explain why each layer can generate evidence.
- Explain the difference between a program, a process, and a thread.
- Understand HDD basics and compute disk size using CHS values.
- Describe the PC boot process and key differences between BIOS and UEFI.
- Locate and interpret partition table fields (Starting LBA and Total Sectors) from the MBR in hex.
- Manually compute partition sizes in GB and verify with OS-reported sizes.
- Identify common file systems and match them to operating systems.

---

# Tools and Resources Used

- Oracle VirtualBox
- Kali-Forensics (Linux VM)
- Linux CLI tools:
  - lsblk, fdisk -l, parted
  - dd
  - xxd (or hexdump)
- Python 3
- WinHex (hex editor)
- Instructor-provided slide deck:
  - 1_PC_Introduction.pptx
- ICDFA lab report guide / template structure

---

# Workspace / Evidence Storage

/media/sf_Lab02_PC_Introduction/
/media/sf_Lab02_PC_Introduction/Screenshots/
/media/sf_Lab02_PC_Introduction/Notes/

---

# Methodology

1. Started the Kali-Forensics VM and opened Terminal.
2. Confirmed shared folder location and created Screenshots and Notes folders.
3. Identified the main disk and partitions using lsblk and/or fdisk -l.
4. Captured raw Sector 0 (MBR) from the target disk using dd.
5. Viewed MBR bytes in hex using xxd and located the partition table area (0x1BE–0x1FD).
6. Extracted the Starting LBA and Total Sectors fields for Partition 1 and Partition 2.
7. Converted little-endian hex bytes into decimal values using Python 3.
8. Computed partition sizes in GB using: size_gb = total_sectors × 512 / 1024^3.
9. Compared computed sizes with OS-reported sizes (e.g., lsblk) and documented results.
10. Answered theory questions on system layers, boot process, and file systems.

---

# Screenshots and Evidence

## Figure 1 — Kali VM Running + Terminal Opened

**Screenshot Filename:** Fig--_-------.png

![-----](Fig--_--------.png)

---

## Figure 2 — Disk + Partition Identification (lsblk or fdisk -l)

**Screenshot Filename:** Fig--_-------.png

![-----](Fig--_--------.png)

---

## Figure 3 — dd Capturing Sector 0 (MBR) to a File

**Screenshot Filename:** Fig--_-------.png

![-----](Fig--_--------.png)

---

## Figure 4 — xxd Hex View Showing Partition Table Area (0x1BE – 0x1FD)

**Screenshot Filename:** Fig--_-------.png

![-----](Fig--_--------.png)

---

## Figure 5 — Partition 1 Fields Highlight (Starting LBA + Total Sectors)

**Screenshot Filename:** Fig--_-------.png

![-----](Fig--_--------.png)

---

## Figure 6 — Partition 2 Fields Highlight (Starting LBA + Total Sectors)

**Screenshot Filename:** Fig--_-------.png

![-----](Fig--_--------.png)

---

## Figure 7 — Python Calculations (Hex → Decimal + Size in GB)

**Screenshot Filename:** Fig--_-------.png

![-----](Fig--_--------.png)

---

## Figure 8 — OS Verification (lsblk Size Output)

**Screenshot Filename:** Fig--_-------.png

![-----](Fig--_--------.png)

---

# Analysis and Findings

# PART 1: Computer Systems and Operations

## Exercise 1.1 — System Layers

### 1) What are the four layers of a computer system?
**Answer:** User, Applications, Operating System, and Hardware.

### 2) Why is it important (for forensics) that evidence is generated from each layer?
**Answer:** A single user action can create artifacts in multiple places (application logs, OS logs, memory artifacts, and disk traces). Investigators must understand each layer to avoid missing evidence.

---

## Exercise 1.2 — Programs, Processes, and Threads

### 3) Explain the difference between a Program, a Process, and a Thread
- **Program:** Stored code (example: a .py file).
- **Process:** A running instance of a program.
- **Thread:** A smaller execution unit inside a process that can run concurrently.

### 4) Why is computer forensics multi-disciplinary? Name at least three disciplines involved
**Answer:** Computer forensics combines fields such as criminal justice, law, and computer science.

---

# PART 2: Hard Disk Drive (HDD) Mechanics

## Exercise 2.1 — Disk Geometry (CHS) Calculations

**Given:**
- Cylinders (Tracks): 20,000  
- Heads: 16  
- Sectors per track: 63  
- Bytes per sector: 512  

### Step 1 — Total number of sectors
Total sectors = C × H × S  
= 20,000 × 16 × 63  
= **20,160,000 sectors**

### Step 2 — Total bytes
Total bytes = total sectors × 512  
= 20,160,000 × 512  
= **10,321,920,000 bytes**

### Step 3 — Convert bytes → KB → MB → GB (divide by 1024 each step)
- KB = 10,321,920,000 / 1024 = **10,080,000 KB**
- MB = 10,080,000 / 1024 = **9,843.75 MB**
- GB = 9,843.75 / 1024 ≈ **9.61 GB**

---

# PART 3: PC Booting and Partition Tables

## Exercise 3.1 — The Boot Process

### 5) Describe the steps of a computer booting up, from POST to the OS taking control
**Answer:** Power on → POST → BIOS boot sequence (settings stored in CMOS) → control passes to the MBR → MBR points to the boot record of the selected OS → boot manager/loader pre-loads OS → OS kernel loads from boot volume → OS takes control.

### 6) What is the main difference between BIOS and UEFI?
**Answer:** BIOS is a legacy firmware boot method commonly tied to classic MBR-based boot flows, while UEFI is a newer firmware interface designed for modern boot mechanisms and commonly supports GPT-based boot.

---

## Exercise 3.2 — Manual MBR Analysis (Practical)

### Partition 1 (Protective MBR context on GPT disk)

**Starting LBA bytes (offset 0x01C6–0x01C9):** 01 00 00 00  
- Reverse (little-endian): 00 00 00 01  
- Hex: **0x00000001**

**Total Sectors bytes (offset 0x01CA–0x01CD):** FF FF FF FF  
- Reverse: unchanged  
- Hex: **0xFFFFFFFF**

**Decimal total sectors:** **4,294,967,295**

**Partition size in GB (512 bytes/sector):**
- Bytes = 4,294,967,295 × 512 = 2,199,023,255,040 bytes
- KB = 2,199,023,255,040 / 1024 = 2,147,483,647,500 KB
- MB = 2,147,483,647,500 / 1024 = 2,097,151,999.51 MB
- GB = 2,097,151,999.51 / 1024 = **2048.00 GB**

**Note (Forensics):** If the disk is GPT, Sector 0 may contain a protective MBR. In that case, MBR partition entries may not reflect the real GPT partitions.

---

### Partition 2 (Protective MBR context on GPT disk)

**Starting LBA bytes:** 00 00 00 00  
- Reverse: unchanged  
- Hex: **0x00000000**
- Decimal: **0**

**Partition size:** 0 GB (based on the shown MBR values in this protective MBR context).

---

# PART 4: File Systems

## Exercise 4.1 — File System Identification

Match the file system to its primary operating system:

- **NTFS** → Windows  
- **EXT4** → Linux  
- **APFS / HFS+** → macOS  
- **FAT32** → Windows (also supported on Linux/macOS; common for flash drives)

---

# PART 5: Lab Challenge (Major Assignment)

**Task:** Verify the size of at least two partitions using a hex editor (WinHex) without using templates.

## Partition 1 — Manual Hex Extraction and Size Calculation

**Starting LBA bytes (offset 0x01C6–0x01C9):** 3F 00 00 00  
- Reverse: 00 00 00 3F  
- Hex: **0x0000003F**  
- Decimal: **63**

**Total Sectors bytes (offset 0x01CA–0x01CD):** 5F 5A 07 00  
- Reverse: 00 07 5A 5F  
- Hex: **0x00075A5F**  
- Decimal: **481,887**

**Partition size in GB:**
- Bytes = 481,887 × 512 = 246,726,144 bytes
- KB = 246,726,144 / 1024 = 240,943.5 KB
- MB = 240,943.5 / 1024 = 235.29638671875 MB
- GB = 235.29638671875 / 1024 = **0.2297816276550293 GB**

---

## Partition 2 — Manual Hex Extraction and Size Calculation

**Starting LBA bytes (offset 0x01D6–0x01D9):** DD 5A 07 00
- Reverse: 00 07 5A DD  
- Hex: **0x00075ADD**  
- Decimal: **482,013**

**Total Sectors bytes (offset 0x01DA–0x01DD):** 37 90 F8 00  
- Reverse: 00 F8 90 37  
- Hex: **0x00F89037**  
- Decimal: **16,289,847**

**Partition size in GB:**
- Bytes = 16,289,847 × 512 = 8,340,401,664 bytes
- KB = 8,340,401,664 / 1024 = 8,144,923.5 KB
- MB = 8,144,923.5 / 1024 = 7,954.02685546875 MB
- GB = 7,954.02685546875 / 1024 = **7.767604351043701 GB**

---

# Challenges and Solutions

| Challenge | Solution |
|---|---|
| WinHex license restrictions interrupted workflow | Focused on required manual offset extraction from Sector 0 and captured quick screenshots of the exact offset blocks (0x01C6, 0x01CA, 0x01D6, 0x01DA). |
| Endianness confusion when interpreting bytes | Consistently reversed byte order (little-endian) before converting hex → decimal and validated results against OS/tool outputs (allowing for rounding). |

---

# Conclusion

This lab helped me understand how digital evidence is tied to the low-level structure of a computer system, especially how storage devices are organized and how partition information is stored. By manually locating the MBR at Sector 0 and extracting partition fields using exact offsets, I learned that forensic work depends on precision with raw bytes rather than relying only on tool summaries.

The most important lesson was that small details change interpretation: MBR vs GPT affects where partition data truly lives, and little-endian storage affects how bytes must be read. Correct handling of these concepts allowed accurate partition size calculations and reliable verification against OS-reported values.

---

# Recommendations

- Always confirm whether a disk uses **MBR or GPT** before interpreting partition fields.
- Always account for **little-endian** byte order when converting raw hex values.
- Verify calculated partition sizes against OS tools to catch mistakes early.

---

# References (No External Links)

- Idris, A. — 1_PC_Introduction.pptx (Instructor-provided slide deck)
- ICDFA — Lab Assignment Template Guide (course document)
- WinHex — User Guide/Documentation (tool documentation)
- Python 3 — Documentation (local/reference documentation)
- GNU Bash — Documentation (shell/reference documentation)
