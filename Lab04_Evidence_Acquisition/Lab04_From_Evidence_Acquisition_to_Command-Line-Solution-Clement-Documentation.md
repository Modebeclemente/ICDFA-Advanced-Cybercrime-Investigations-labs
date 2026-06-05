# Lab Report: Comprehensive Digital Forensics (Autopsy + The Sleuth Kit) — Lab 4

## Student Information

| Field | Details |
|---|---|
| Student Name | Clement Modebe |
| Student ID | aci2616123@icdfa.edu.ng |
| Course Code | ACI801 |
| Course Name | Introduction to Digital Forensics |
| Lab Title | Lab 4 – From Evidence Acquisition to Command-Line Analysis |
| Instructor Name | Mr. Aminu Idris, AMCPN |
| Date of Submission | 16 May 2026 |
| Tool Version (Autopsy) | 7.2.6 r172322 (Qt6.8.0 on Windows) |

---

# Executive Summary (150–200 words)

This lab focused on core digital forensics concepts and practical evidence analysis using both graphical and command-line forensic tools. The investigation followed standard digital forensics principles: identifying, collecting, examining, and analyzing data while preserving integrity and maintaining chain of custody. A forensic disk image (Ch01InChap01.dd) was examined using Autopsy to create a case, validate integrity with hashing, locate deleted files, tag evidence for reporting, recover artifacts, perform keyword searches, and generate a report. The Sleuth Kit (TSK) tools were then used to inspect image and file system details, list allocated and deleted files, recover deleted files by inode/blocks, and verify recovered outputs using hashing. Advanced steps included mounting the image via loop devices and documenting a new TSK command (tsk_gettimes) with an example usage for timeline-ready output. Overall, the lab demonstrates a repeatable workflow for defensible digital evidence analysis that combines GUI-driven review with low-level command-line verification and recovery.

---

# Lab Objectives

- Define digital forensics using the NIST definition and identify required integrity/chain-of-custody conditions.
- Differentiate between public-sector vs private-sector digital investigations and give examples of private-sector triggers.
- List and apply the five main steps of a digital investigation.
- Explain the difference between a bit-stream copy (image) and a standard backup copy, and why a bit-stream copy is essential.
- Perform graphical analysis in Autopsy: case creation, data source addition, deleted file recovery, tagging, keyword searching, and reporting.
- Perform command-line analysis with The Sleuth Kit (TSK): image/file system inspection, listing deleted entries, recovering files with icat/blkcat, and verifying results with hashing.
- Mount a disk image read-only using losetup and mount; validate access and explain relevant flags.
- Document one new TSK command not explicitly demonstrated and provide example usage.

---

# Tools and Resources Used

- Windows 11 Host (evidence storage on dedicated D:\ drive)
- Oracle VirtualBox (Kali-Forensics VM)
- Autopsy (GUI forensic tool)
- The Sleuth Kit (TSK) (img_stat, fsstat, fls, icat, istat, blkcat)
- Hashing utilities (e.g., md5file.com/calculator for quick verification)
- Evidence image: Ch01InChap01.dd
- Course slide decks: “Introduction to Digital Forensics” and “Sleuth Kit Tutorial”

---

# Workspace / Evidence Storage

## Windows host workspace (as used in the lab)

D:\VM_Lab\ICDFA_Labs\computerforensics_investigation_6ed\Lab_data\chapter_1\Ch01InChap01\
D:\VM_Lab\ICDFA_Labs\computerforensics_investigation_6ed\autopsy_case\chap01\InChap01\
D:\VM_Lab\ICDFA_Labs\ICDFA Study Material\ACI801 Digital Evidence Collection\ACI801 Digital Evidence Collection Latest\Assignments\Week 2 16 May 26\Lab 4 From Evidence Acquisition to Command-Line Analysis\Screenshots\

## Kali (shared-folder path referenced in commands)

/media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/

---

# Methodology (End-to-End)

## Part 1 — Digital Forensics Fundamentals (Theory)

1. Defined digital forensics using the NIST-aligned definition.
2. Differentiated public-sector vs private-sector investigations and listed private-sector triggers.
3. Listed the five main steps of a digital investigation.
4. Explained bit-stream imaging vs backup copying and why imaging is essential.

## Part 2 — Graphical Analysis with Autopsy

5. Prepared lab workspace folders on Windows and placed Ch01InChap01.dd in the designated evidence directory.
6. Computed/recorded hashes for integrity verification.
7. Opened Autopsy and created a new case (name, case number, examiner).
8. Added Ch01InChap01.dd as a data source (raw .dd).
9. Enabled/configured ingest modules and completed ingest.
10. Browsed the file system, located deleted files, tagged relevant items, and recovered at least one deleted file to the “Recovered” folder.
11. Performed keyword searches and generated an Autopsy report.

## Part 3 — Command-Line Analysis with The Sleuth Kit (TSK)

12. Used img_stat to confirm image format and details.
13. Used fsstat to document file system layout/statistics.
14. Used fls to list allocated + deleted entries and fls -d to list deleted-only entries.
15. Counted deleted entries and recorded evidence.
16. Recovered deleted content using icat by inode, and validated metadata using istat.
17. Recovered content using blkcat based on block lists, then verified recovered outputs by hashing.

## Part 4 — Advanced Recovery + Mounting

18. Performed multi-method recovery of INCOME.XLS using:
    - fls + grep to identify inode
    - icat recovery
    - istat + blkcat recovery
19. Verified both recovered versions are identical using sha256sum.
20. Attached the image to a loop device read-only using:
    sudo losetup --partscan --find --show --read-only <image>
21. Created a mount point and mounted the image read-only.
22. Verified mounted content using ls.
23. Unmounted and detached loop devices after verification.

## Part 5 — Independent Exploration (New TSK Command)

24. Selected and documented a new TSK command: tsk_gettimes.
25. Explained purpose, minimum inputs, outputs, and provided example usage (redirecting output to a body file suitable for timeline tools like mactime).

---

# Screenshots and Evidence (Placeholders)

## Part 2 — Autopsy (GUI)

### Lab04_Fig01 — Evidence image placed in workspace folder
**Screenshot Filename:** Lab04_Screenshot_01.png

![Screenshot](Screenshots/Lab04_Fig01_EvidenceImageSaved.png)

### Lab04_Fig02 — Hash verification of evidence image
**Screenshot Filename:** Lab04_Screenshot_02.png

![Screenshot](Screenshots/Lab04_Fig02_ImageHashVerification.png)

### Lab04_Fig03 — Autopsy home screen
**Screenshot Filename:** Lab04_Screenshot_03.png

![Screenshot](Screenshots/Lab04_Fig03_AutopsyHome.png)

### Lab04_Fig04 — New case wizard
**Screenshot Filename:** Lab04_Screenshot_04.png

![Screenshot](Screenshots/Lab04_Fig04_AutopsyNewCaseWizard.png)

### Lab04_Fig05 — Case details entered
**Screenshot Filename:** Lab04_Screenshot_05.png

![Screenshot](Screenshots/Lab04_Fig05_NewCaseDetails.png)

### Lab04_Fig06 — Selecting disk image data source type
**Screenshot Filename:** Lab04_Screenshot_06.png

![Screenshot](Screenshots/Lab04_Fig06_Disk_Image_or_VM_File_Data_Format.png)

### Lab04_Fig07 — Selecting the .dd image file
**Screenshot Filename:** Lab04_Screenshot_07.png

![Screenshot](Screenshots/Lab04_Fig07_Choose_Image_File.png)

### Lab04_Fig08 — Adding raw (.dd) disk image
**Screenshot Filename:** Lab04_Screenshot_08.png

![Screenshot](Screenshots/Lab04_Fig08_AddDataSourceRawDD.png)

### Lab04_Fig09 — Configuring ingest modules
**Screenshot Filename:** Lab04_Screenshot_09.png

![Screenshot](Screenshots/Lab04_Fig09_ConfigureIngestWizard.png)

### Lab04_Fig10 — Data source added successfully
**Screenshot Filename:** Lab04_Screenshot_10.png

![Screenshot](Screenshots/Lab04_Fig10_DataSourceAddedWizard.png)

### Lab04_Fig11 — Deleted files view
**Screenshot Filename:** Lab04_Screenshot_11.png

![Screenshot](Screenshots/Lab04_Fig11_DeletedFilesView.png)

### Lab04_Fig12 — Tagging menu for evidence
**Screenshot Filename:** Lab04_Screenshot_12.png

![Screenshot](Screenshots/Lab04_Fig12_TagMenu.png)
![Screenshot](Screenshots/Lab04_Fig12i_TagMenu.png)

### Lab04_Fig13 — Tag applied to evidence item
**Screenshot Filename:** Lab04_Screenshot_13.png

![Screenshot](Screenshots/Lab04_Fig13_TagCreated.png)

### Lab04_Fig14 — Recover/Extract option
**Screenshot Filename:** Lab04_Screenshot_14.png

![Screenshot](Screenshots/Lab04_Fig14_ExtractFile(s)View.png)

### Lab04_Fig15 — Recovery destination/confirmation
**Screenshot Filename:** Lab04_Screenshot_15.png

![Screenshot](Screenshots/Lab04_Fig15_RecoveryExport.png)

### Lab04_Fig16 — Keyword search configuration
**Screenshot Filename:** Lab04_Screenshot_16.png

![Screenshot](Screenshots/Lab04_Fig16_KeywordsSearch.png)

### Lab04_Fig17 — Keyword search results
**Screenshot Filename:** Lab04_Screenshot_17.png

![Screenshot](Screenshots/Lab04_Fig17_KeywordResults.png)

### Lab04_Fig18 — Generating Autopsy report
**Screenshot Filename:** Lab04_Screenshot_18.png

![Screenshot](Screenshots/Lab04_Fig18_GenerateReport.png)

### Lab04_Fig19 — Report options/confirmation
**Screenshot Filename:** Lab04_Screenshot_19.png

![Screenshot](Screenshots/Lab04_Fig18i_GenerateReport.png)

## Part 3–4 — TSK (CLI)

### Lab04_Fig20 — fsstat output (file system statistics)
**Screenshot Filename:** Lab04_Screenshot_20.png

![Screenshot](Screenshots/Lab04_Fig20_fsstat.png)

### Lab04_Fig21 — img_stat output (image details)
**Screenshot Filename:** Lab04_Screenshot_21.png

![Screenshot](Screenshots/Lab04_Fig19_img_stat.png)

### Lab04_Fig22 — fls -d output (deleted entries only)
**Screenshot Filename:** Lab04_Screenshot_22.png

![Screenshot](Screenshots/Lab04_Fig22_fls_DeletedOnly.png)

### Lab04_Fig23 — Deleted entries count (fls piped to wc -l)
**Screenshot Filename:** Lab04_Screenshot_23.png

![Screenshot](Screenshots/Lab04_Fig22i_DeletedCount_wc_l.png)

### Lab04_Fig24 — icat recovery of inode 15
**Screenshot Filename:** Lab04_Screenshot_24.png

![Screenshot](Screenshots/Lab04_Fig22i_DeletedCount_wc_l.png)

### Lab04_Fig25 — istat output (inode 15 metadata)
**Screenshot Filename:** Lab04_Screenshot_25.png

![Screenshot](Screenshots/Lab04_Fig23_icat_Ch01InChap01_inode15_to_recovered_file.png) 

### Lab04_Fig26 — Identify INCOME.XLS inode via fls/grep
**Screenshot Filename:** Lab04_Screenshot_26.png

![Screenshot](Screenshots/Lab04_Fig24_istat_inode_metadata.png)
![Screenshot](Screenshots/Lab04_Fig25_INCOME_InodeIdentified.png)

### Lab04_Fig27 — Recover INCOME.XLS using icat
**Screenshot Filename:** Lab04_Screenshot_27.png

![Screenshot](Screenshots/Lab04_Fig26_INCOME_icat_Recover.png)

### Lab04_Fig28 — Recover INCOME.XLS using blkcat
**Screenshot Filename:** Lab04_Screenshot_28.png

![Screenshot](Screenshots/Lab04_Fig28_INCOME_blkcat_Recover.png)
![Screenshot](Screenshots/Lab04_Fig27__INCOME_istat_Sectors.png)

### Lab04_Fig29 — sha256sum comparison (INCOME recoveries)
**Screenshot Filename:** Lab04_Screenshot_29.png

![Screenshot](Screenshots/Lab04_Fig29_INCOME_HashCompare_SHA256.png)

### Lab04_Fig30 — losetup --partscan attaching image (read-only)
**Screenshot Filename:** Lab04_Screenshot_30.png

![Screenshot](Screenshots/Lab04_Fig30_losetup_partscan.png)

### Lab04_Fig31 — lsblk output showing loop device mapping
**Screenshot Filename:** Lab04_Screenshot_31.png

![Screenshot](Screenshots/Lab04_Fig31_ListPartitions_lsblk.png)

### Lab04_Fig32 — Verifying loop device mapping
**Screenshot Filename:** Lab04_Screenshot_32.png

![Screenshot](Screenshots/Lab04_Fig32ii_Verify_Loop_Device_loop0.png)

### Lab04_Fig33 — Creating mount point directory
**Screenshot Filename:** Lab04_Screenshot_33.png

![Screenshot](Screenshots/Lab04_Fig32i_Create_Mount_Point_tmp_usb.png)

### Lab04_Fig34 — Mounting loop device read-only
**Screenshot Filename:** Lab04_Screenshot_34.png

![Screenshot](Screenshots/Lab04_Fig32_Mount_loop0_ReadOnly.png)
![Screenshot](Screenshots/Lab04_Fig32iii_Mount_loop0_to_tmp_usb.png)

### Lab04_Fig35 — Verifying mounted contents (ls)
**Screenshot Filename:** Lab04_Screenshot_35.png

![Screenshot](Screenshots/Lab04_Fig32iv_Verify_Mount_ls_tmp_usb.png)

### Lab04_Fig36 — Running tsk_gettimes (new command) and previewing output
**Screenshot Filename:** Lab04_Screenshot_36.png

![Screenshot](Screenshots/Lab04_Fig33_tsk_gettimes_Run_Verify_OutputPreview.png)

### Lab04_Fig37 — Unmounting and detaching loop device
**Screenshot Filename:** Lab04_Screenshot_37.png

![Screenshot](Screenshots/Lab04_Fig32iv_Unmount_Detach_loop0.png)

---

# Analysis and Findings

# PART 1: Digital Forensics Fundamentals (Answers)

## 1) Define Digital Forensics (NIST-aligned)
Digital forensics is the application of science to the identification, collection, examination, and analysis of data while preserving the integrity of the information and maintaining a strict chain of custody.

## 2) Investigation Types (Public vs Private Sector)
- **Public-sector investigations** involve government agencies responsible for criminal investigations and prosecution.
- **Private-sector investigations** typically involve organizational policy violations and internal incidents such as e-mail harassment, falsification of data, discrimination, embezzlement, sabotage, and industrial espionage.

## 3) Five Main Steps of a Digital Investigation
1. Procedure of gathering evidence media (evidence media)
2. Acquiring an image of evidence media
3. Analyzing digital evidence
4. Producing a final report
5. Critiquing the case

## 4) Bit-stream Copy vs Backup Copy
A **bit-stream copy (image)** is a bit-by-bit copy of the original storage medium and can include deleted files and file fragments. A **backup copy** typically copies known files only and cannot capture deleted files or fragments. A bit-stream copy is essential because it preserves the full state of the medium for repeatable examination without altering the original.

---

# PART 2: Graphical Analysis with Autopsy (What Was Done)

## Case Creation + Hash Verification
- Created a new case in Autopsy (case name, case number, examiner).
- Verified hash of the image file to support integrity and defensible chain of custody.

## Data Source + Data Format for .dd
- Added the evidence as a **raw disk image** when selecting data source format for a .dd.

## Deleted File Recovery + Tagging
- Located deleted files in Autopsy’s deleted files view.
- Tagged relevant files for reporting.
- Recovered at least one deleted file using the extract/recover function to a separate recovery folder.

## Keyword Search + Reporting
- Configured and executed keyword searches.
- Generated an Autopsy report that captures tagged evidence and search results.

---

# PART 3: Command-Line Analysis with The Sleuth Kit (TSK)

## Key Concepts
- **File System Layer**: Interprets directories/files/metadata within file systems (FAT/NTFS, etc.).
- **Data Unit Layer**: Provides access to blocks/clusters/sectors to read content/metadata without relying on OS file system APIs.
- **Host Protected Area (HPA)**: Hidden disk area not normally visible to the OS; can be abused by rootkits. Some TSK tools can temporarily remove an HPA (it returns after reset).

## Practical Commands Executed (with examples)

### 1) Image Details
img_stat /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd

### 2) File System Statistics
fsstat /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd

### 3) Listing Entries (Allocated + Deleted)
fls /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd

### 4) Deleted Entries Only
fls -d /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd

### 5) Deleted Count (example pattern)
fls -i raw -r -d /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd | wc -l

### 6) Data Extraction (icat)
icat /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd 15 > recovered_file.txt

### 7) Metadata Statistics (istat)
istat /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd 15

---

# PART 4: Advanced Recovery and Mounting

## Task 4.1 — Multi-Method File Recovery (INCOME.XLS)

### Step A: Identify inode
fls -r /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd | grep -i 'INCOME\.XLS'

### Step B: Recover using icat
icat -i raw "/media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd" 13 > INCOME_icat.xls

### Step C: Recover using istat + blkcat
1) Record block list:
istat /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd 13

2) Extract blocks:
blkcat -i raw "/media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd" 285 27 > INCOME_blkcat.xls

### Step D: Verify hashes match
sha256sum INCOME_icat.xls INCOME_blkcat.xls

## Task 4.2 — Mounting the Image (Read-Only)

### Attach image to loop device
sudo losetup --partscan --find --show --read-only /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd

**Flag notes:**
- **--partscan** scans the partition table and creates loop devices for partitions.
- **--find** selects the first available loop device.
- **--show** prints the loop device path used.
- **--read-only** prevents writes to the evidence image.

### Create mount point + mount read-only
sudo mkdir -p /tmp/usb
sudo mount -t vfat -o ro /dev/loop0 /tmp/usb
ls -al /tmp/usb

---

# PART 5: Independent Exploration (New TSK Command)

## New Command: tsk_gettimes

### What it does
tsk_gettimes examines a file system in a disk image and outputs timestamp metadata in MACtime “body file” format (timeline-ready output). The output can be used with tools like mactime to build a timeline of file activity.

### Minimum required input
- Disk image path (single image file, or multiple segments if split)

### Example usage (timeline body file)
tsk_gettimes -i raw -z UTC \
  /media/sf_VM_Lab/ICDFA_Labs/computerforensics_investigation_6ed/Lab_data/chapter_1/Ch01InChap01/Ch01InChap01.dd \>/tmp/timeline.body

ls -lh /tmp/timeline.body
head -n 5 /tmp/timeline.body

---

# Challenges and Solutions

| Challenge | Solution |
|---|---|
| “/mnt/usb: No such file or directory” during verification | Created the mount point directory first (or re-created it), then mounted and verified with ls. |
| “Read-only file system” when creating /mnt/usb | Used a writable mount location (e.g., /tmp/usb) and mounted the loop device read-only there. |
| No /dev/loop0p1 partition appeared after losetup --partscan | Used lsblk to identify available devices and mounted the correct node (mounting /dev/loop0 directly where appropriate). |

---

# Conclusion

This lab reinforced the standard workflow of a digital forensic investigation: gathering evidence, acquiring an image, analyzing artifacts, producing a final report, and reflecting on the process for improvement. Autopsy provided a structured GUI approach for case creation, deleted-file recovery, tagging for reporting, keyword searching, and report generation. The Sleuth Kit (TSK) supported command-line validation of the image and file system, listing deleted entries, and performing recovery using metadata structures and data units. Integrity and defensibility were emphasized through hashing, careful documentation, consistent screenshot handling, and read-only mounting of the evidence image—supporting repeatability and professional reporting standards.

---

# Recommendations

- Verify evidence integrity early by hashing the evidence image and documenting results before analysis.
- Use read-only techniques whenever possible (read-only losetup and read-only mounting) to avoid accidental modification.
- Keep outputs and screenshots organized using consistent folder structures and naming conventions.
- Save terminal output to files (e.g., via tee or redirection) to keep results reproducible and easy to attach to reports.
- When exploring new tools, consult help/man pages and document command purpose, inputs, and outputs.

---

# References

- Idris, A. (n.d.). *Introduction to Digital Forensics* (PowerPoint slides). International Cybersecurity and Digital Forensics Academy (ICDFA).
- Idris, A. (n.d.). *The Sleuth Kit (TSK) Tutorial* (PowerPoint slides). International Cybersecurity and Digital Forensics Academy (ICDFA).
- International Cybersecurity and Digital Forensics Academy. (n.d.). *Lab Assignment Template Guide* (PDF).
- Carrier, B. (n.d.). *tsk_gettimes — Collect MAC times from a disk image into a body file* (Manual page). The Sleuth Kit. http://www.sleuthkit.org/sleuthkit/man/tsk_gettimes.html
- Sleuthkit/Sleuthkit. (2017, October 24). *tsk_gettimes* (Wiki page). GitHub. https://github.com/sleuthkit/sleuthkit/wiki/tsk_gettimes
