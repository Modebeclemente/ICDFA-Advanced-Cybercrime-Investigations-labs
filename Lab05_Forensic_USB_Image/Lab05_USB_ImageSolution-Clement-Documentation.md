# Lab Report: USB Image Acquisition (Lab 5)

## Student Information

| Field | Details |
|---|---|
| Student Name | Clement Modebe |
| Student ID | aci2616123@icdfa.edu.ng |
| Course Code | ACI801 Digital Evidence Collection |
| Course Name | Introduction to Digital Forensics |
| Instructor Name | Mr. Aminu Idris, AMCPN |
| Lab Title | Lab 5 – USB Image Acquisition Across Windows and Linux Environments |
| Date of Submission | 16 May 2026 |

---

# Executive Summary (150–200 words)

This lab demonstrated the acquisition of a forensic image from a USB storage device using both Windows and Linux environments. The main objective was to create a bit-by-bit copy of the USB drive while maintaining forensic integrity through documentation and hashing. On Windows, FTK Imager was used to acquire a Raw-format image and verify the image using the built-in hash verification workflow. In addition, a Windows dd utility was used as an alternative command-line method to acquire an image based on the correct volume identifier.

On Kali Linux (Kali-Forensics VM), the USB device was identified using lsblk and acquired with dd using forensic-friendly options such as conv=noerror,sync and status=progress. Hash values (MD5/SHA1) were generated to evaluate integrity of the acquired outputs. Results showed that the FTK image verification confirmed a matching hash between the source and the image, supporting integrity. Although dd-based images were created successfully as files, the dd-derived outputs did not consistently match the source hashes in the documented verification steps. Overall, the lab reinforced best practices for evidence acquisition, careful device identification, and the importance of hashing as an integrity control.

---

# Lab Objectives

- Define a disk image and distinguish imaging a partition (volume) vs an entire device.
- Identify disk image formats mentioned in the study slides (open vs proprietary).
- Acquire a USB image in Windows using FTK Imager and document verification results.
- Acquire a USB image using the Windows dd alternative and record the correct Volume GUID.
- Acquire a USB image in Kali using dd (and dcfldd where available) and verify with hashing.
- Describe the network acquisition concept using nc as shown in the slides.
- Maintain forensic soundness: minimal writes to evidence, document paths, and verify hashes.

---

# Tools and Resources Used

- Windows host PC with dedicated D:\ drive for lab work
- FTK Imager (as referenced in course slides)
- Windows dd utility (dd-0.5.zip)
- Oracle VirtualBox + Kali-Forensics VM
- Kali shared folder: /media/sf_VM_Lab
- Linux tools: lsblk, dd, md5sum, nc (dcfldd referenced)

---

# Workspace / Evidence Storage

## Windows (host)
- D:\Lab05_USB_Image_Acquisition\Forensic_Working_Space\

## Kali (shared folder)
- /media/sf_VM_Lab/

---

# Methodology (End-to-End)

## Part 1 — Imaging Concepts (Theory)
1. Defined disk image and explained partition (volume) image vs entire device image.
2. Identified image formats (open vs proprietary) referenced in slides and tools.

## Part 2 — Windows Acquisition
### 2.1 FTK Imager (Primary Workflow)
3. Downloaded and installed FTK Imager.
4. Inserted USB and verified Windows could access it.
5. Opened FTK Imager and started Create Disk Image.
6. Selected Source Evidence Type (Physical Drive) to image the entire device.
7. Chose the correct USB physical drive.
8. Selected image type (Raw/dd and other options shown).
9. Completed Evidence Item Information.
10. Set destination folder and enabled “Verify images after they are created”.
11. Started acquisition and captured completion.
12. Verified the image using FTK “Verify Drive/Image...” and recorded hash results.

### 2.2 Windows dd (Alternative)
13. Downloaded/unzipped dd-0.5.zip and placed dd.exe in an accessible directory.
14. Identified the correct USB volume using dd --list and recorded the Volume GUID.
15. Acquired the image using dd if=<VolumeGUID> of=<output> and recorded results.
16. Verified hashes using FTK verification view for both the dd image and original USB.

## Part 3 — Linux (Kali) Acquisition
17. Attached USB device to Kali VM using VirtualBox USB passthrough.
18. Confirmed device name with lsblk (e.g., /dev/sdb).
19. Acquired image using dd with status=progress and conv=noerror,sync.
20. Verified integrity using md5sum on the source device and acquired image.

## Part 4 — Network Acquisition Concept
21. Set up Windows listener with ncat to receive an image over the network.
22. Used dd piped to nc on Kali to send the image to Windows.
23. Verified integrity by comparing hashes between source and received file.

---

# Screenshots and Evidence (Using Provided Screenshot Filenames)

## Part 2 — Windows Acquisition (FTK Imager)

### Fig01 — firstname_lastname.txt saved on USB (Windows)
**Screenshot Filename:** Lab05_Fig01_Clement_Modebe_On_USB_Windows.png

![Screenshot](Screenshots/Lab05_Fig01_Clement_Modebe_On_USB_Windows.png)

### Fig02 — FTK Imager download page
**Screenshot Filename:** Lab05_Fig02_FTK_Imager_Download_Page.png

![Screenshot](Screenshots/Lab05_Fig02_FTK_Imager_Download_Page.png)

### Fig03 — USB detected in Windows File Explorer
**Screenshot Filename:** Lab05_Fig03_USB_Detected_Windows.png

![Screenshot](Screenshots/Lab05_Fig03_USB_Detected_Windows.png)

### Fig04 — FTK Imager Create Disk Image menu
**Screenshot Filename:** Lab05_Fig04_FTK_CreateDiskImage_Menu.png

![Screenshot](Screenshots/Lab05_Fig04_FTK_CreateDiskImage_Menu.png)

### Fig05 — Source evidence type: Physical Drive
**Screenshot Filename:** Lab05_Fig05_FTK_SourceType_PhysicalDrive.png

![Screenshot](Screenshots/Lab05_Fig05_FTK_SourceType_PhysicalDrive.png)

### Fig06 — Select USB physical drive
**Screenshot Filename:** Lab05_Fig06_FTK_Select_USB_PhysicalDrive.png

![Screenshot](Screenshots/Lab05_Fig06_FTK_Select_USB_PhysicalDrive.png)

### Fig07 — FTK Create Image window
**Screenshot Filename:** Lab05_Fig07_FTK_Create_Image.png

![Screenshot](Screenshots/Lab05_Fig07_FTK_Create_Image.png)

### Fig08 — Select image type (Raw/dd, SMART, E01, AFF)
**Screenshot Filename:** Lab05_Fig08_FTK_SelectImageType.png

![Screenshot](Screenshots/Lab05_Fig08_FTK_SelectImageType.png)

### Fig09 — Evidence Item Information completed
**Screenshot Filename:** Lab05_Fig09_FTK_EvidenceItemInfo.png

![Screenshot](Screenshots/Lab05_Fig09_FTK_EvidenceItemInfo.png)

### Fig10 — Destination settings + verify option enabled
**Screenshot Filename:** Lab05_Fig10_FTK_Destination_Settings.png

![Screenshot](Screenshots/Lab05_Fig10_FTK_Destination_Settings.png)

### Fig11 — FTK Create Image settings
**Screenshot Filename:** Lab05_Fig11_FTK_Create_Image.png

![Screenshot](Screenshots/Lab05_Fig11_FTK_Create_Image.png)

### Fig12 — FTK acquisition complete
**Screenshot Filename:** Lab05_Fig12_FTK_Acquisition_Complete.png

![Screenshot](Screenshots/Lab05_Fig12_FTK_Acquisition_Complete.png)

### Fig13 — FTK Verify Drive/Image hash results
**Screenshot Filename:** Lab05_Fig13_FTK_VerifyDriveImage_Hashes.png

![Screenshot](Screenshots/Lab05_Fig13_FTK_VerifyDriveImage_Hashes.png)

### Fig14 — FTK image file saved/copied
**Screenshot Filename:** Lab05_Fig14_FTK_USB_Image_Copy.png

![Screenshot](Screenshots/Lab05_Fig14_FTK_USB_Image_Copy.png)

---

## Part 2 — Windows Acquisition (dd Alternative)

### Fig15 — Windows dd utility unzipped on Desktop
**Screenshot Filename:** Lab05_Fig15_DD_Unzipped_On_Desktop.png

![Screenshot](Screenshots/Lab05_Fig15_DD_Unzipped_On_Desktop.png)

### Fig16 — dd --list output showing Volume GUID
**Screenshot Filename:** Lab05_Fig16_DD_List_Volumes.png

![Screenshot](Screenshots/Lab05_Fig16_DD_List_Volumes.png)

### Fig17 — dd acquisition complete output
**Screenshot Filename:** Lab05_Fig17_DD_Acquisition_Complete_Output.png

![Screenshot](Screenshots/Lab05_Fig17_DD_Acquisition_Complete_Output.png)

### Fig18 — usb_dd image created on D:\ root
**Screenshot Filename:** Lab05_Fig18_usb_dd_img_On_D_Root.png

![Screenshot](Screenshots/Lab05_Fig18_usb_dd_img_On_D_Root.png)

### Fig19 — usb_dd image stored in Forensic_Working_Space
**Screenshot Filename:** Lab05_Fig19_usb_dd_img_In_Forensic_Working_Space.png

![Screenshot](Screenshots/Lab05_Fig19_usb_dd_img_In_Forensic_Working_Space.png)

### Fig20i — FTK verify hash for usb_dd image
**Screenshot Filename:** Lab05_Fig20i_FTK_Verify_usb_dd_img_Hash.png

![Screenshot](Screenshots/Lab05_Fig20i_FTK_Verify_usb_dd_img_Hash.png)

### Fig20ii — FTK verify hash for original USB
**Screenshot Filename:** Lab05_Fig20ii_FTK_Verify_usb_original_hash.png

![Screenshot](Screenshots/Lab05_Fig20ii_FTK_Verify_usb_original_hash.png)

---

## Part 3 — Linux Acquisition (Kali)

### Fig21 — Kali desktop running
**Screenshot Filename:** Lab05_Fig21_Kali_Desktop.png

![Screenshot](Screenshots/Lab05_Fig21_Kali_Desktop.png)

### Fig21 (USB) — USB attached to Kali VM
**Screenshot Filename:** Lab05_Fig21_USB_Attached_Kali.png

![Screenshot](Screenshots/Lab05_Fig21_USB_Attached_Kali.png)

### Fig22 — lsblk output showing USB device
**Screenshot Filename:** Lab05_Fig22_lsblk_Output.png

![Screenshot](Screenshots/Lab05_Fig22_lsblk_Output.png)

### Fig23 — dd imaging status/progress
**Screenshot Filename:** Lab05_Fig23_dd_Imaging_StatusProgress.png

![Screenshot](Screenshots/Lab05_Fig23_dd_Imaging_StatusProgress.png)

### Fig24 — md5sum for source and image
**Screenshot Filename:** Lab05_Fig24_md5sum_Source_And_Image.png

![Screenshot](Screenshots/Lab05_Fig24_md5sum_Source_And_Image.png)

---

## Part 4 — Network Acquisition

### Fig25 — Windows ncat listener receiving image
**Screenshot Filename:** Lab05_Fig25_Windows_ncat_Listener_8080.png

![Screenshot](Screenshots/Lab05_Fig25_Windows_ncat_Listener_8080.png)

### Fig26 — Kali sending image over network (dd | nc)
**Screenshot Filename:** Lab05_Fig26_Kali_dd_to_nc_Send.png

![Screenshot](Screenshots/Lab05_Fig26_Kali_dd_to_nc_Send.png)

### Fig27 — Image received on Windows
**Screenshot Filename:** Lab05_Fig27_Windows_Received_usb_network_dd_File.png

![Screenshot](Screenshots/Lab05_Fig27_Windows_Received_usb_network_dd_File.png)

### Fig28i — Kali MD5 hash of original USB
**Screenshot Filename:** Lab05_Fig28i_Kali_MD5_Hash_Origninal_to_nc_Send.png

![Screenshot](Screenshots/Lab05_Fig28i_Kali_MD5_Hash_Origninal_to_nc_Send.png)

### Fig28ii — Windows MD5 hash of received image (certutil)
**Screenshot Filename:** Lab05_Fig28ii_Windows_MD5_usb_network_dd.png

![Screenshot](Screenshots/Lab05_Fig28ii_Windows_MD5_usb_network_dd.png)

---

# Analysis and Findings

## Part 1: Concepts of Disk Imaging

- **Disk image definition:** A disk image is a computer file containing the contents and structure of a disk volume (partition) or an entire data storage device.
- **Volume image vs entire device image:** A volume image captures a partition only, while an entire device image captures the full device structure and contents.
- **File formats:** Open standard example: ISO. Proprietary examples referenced: EnCase, FTK. FTK-supported formats listed include Raw (dd), SMART, E01, and AFF.

## Part 2: Windows Acquisition Findings

- FTK Imager successfully created a forensic image (usb_image.001) and the verification step reported matching hash values between the source and the image.
- Windows dd successfully produced an image file; however, the documented verification views showed hash mismatches between the original USB and the dd-acquired image, meaning integrity could not be fully confirmed for that method in this run.

## Part 3: Linux Acquisition Findings

- Kali recognized the USB device through VirtualBox passthrough and lsblk identified the device node.
- dd imaging created an output file and md5sum was used to validate integrity.

## Part 4: Network Acquisition Findings

- A network listener was configured on Windows (ncat) and Kali transmitted data using dd piped to nc.
- Hash comparisons showed mismatches, indicating the transfer was incomplete or integrity was not preserved during the network acquisition attempt.

---

# Challenges and Solutions

| Challenge | Solution |
|---|---|
| dd command not recognized in Windows | Opened Command Prompt in the correct folder containing dd.exe (cd into dd-0.5 directory) before running dd. |
| Command prompt pause (QuickEdit mode) | Exited selection mode (Esc/Enter/right-click) and disabled QuickEdit to prevent interruption. |
| Slow/unresponsive dd imaging feedback on Windows | Confirmed progress by monitoring the output file size growth in File Explorer until completion. |

---

# Conclusion

This lab demonstrated USB forensic imaging using both Windows and Linux approaches. FTK Imager provided a clear, verifiable workflow and produced an image whose hashes matched the source, supporting forensic soundness. Command-line imaging using dd (Windows and Kali) successfully created image files and supported hashing, though the documented verification steps indicated mismatches for some dd-acquired outputs, highlighting the need for precise device identification, minimal system activity during acquisition, and careful verification.

The lab also reinforced network acquisition concepts using nc/ncat, showing the importance of end-to-end integrity checks when data is transmitted across a network. Overall, the work strengthened practical skills in evidence acquisition, documentation, and hash-based validation.

---

# Recommendations

- Use trusted imaging tools (FTK Imager, dd/dcfldd) and always document device identifiers clearly.
- Verify images immediately after acquisition with MD5/SHA1 (or stronger hashes where required) and keep hash logs.
- Prefer dd/dcfldd options such as status=progress, conv=noerror,sync, and hashing/logging to improve reliability.
- Ensure proper USB passthrough configuration in VirtualBox to avoid device recognition issues.
- Maintain structured documentation of steps, commands, paths, and outputs to improve reproducibility and defensibility.

---

# References

- FTK Imager download page (as referenced in slides): https://accessdata.com/product-download/ftk-imager-version-4-5
- Windows dd download (as referenced in slides): http://www.chrysocome.net/downloads/dd-0.5.zip
- SMART for Linux: http://www.asrdata.com/forensic-software/smart-for-linux
- Digital forensics lab reference: https://github.com/frankwxu/digital-forensics-lab
- VirtualBox USB access guide: https://www.linuxbabe.com/virtualbox/access-usb-from-virtualbox-guest-os
- Additional VirtualBox USB passthrough reference: https://www.net-usb.com/virtual-usb/virtualbox-usb-passthrough/virtualbox-usb-linux
- Video reference: https://www.youtube.com/watch?v=ULSFaGmIaUo
