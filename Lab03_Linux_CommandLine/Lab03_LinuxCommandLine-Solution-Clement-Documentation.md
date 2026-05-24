# Lab Report: Linux Command Line Mastery for Digital Forensics (Lab 3)

## Student Information

| Field | Details |
|---|---|
| Student Name | Clement Modebe |
| Student ID | aci2616123@icdfa.edu.ng |
| Course Name | Advanced Cybercrime Investigation |
| Instructor Name | Mr. Aminu Idris |
| Date of Submission | 8 May 2026 |

---

# Executive Summary (150–200 words)

This lab introduced the Linux command line as a fundamental tool for digital forensics. The exercises covered basic navigation, file management, searching, networking, and standard input/output redirection. Using Kali Linux, I executed practical commands to demonstrate how investigators interact with systems, locate relevant artifacts, and document outputs as evidence.

The lab also included remote evidence acquisition concepts using Netcat-style tools for controlled file transfer and verification. In addition, shell concepts (bind shell vs. reverse shell) were discussed to understand how remote sessions work and why network controls can influence connection direction. The overall outcome demonstrated that Linux CLI tools support forensic workflows by enabling fast system exploration, repeatable evidence collection, and structured documentation. The lab strengthened my confidence in command syntax, logging outputs to files, and troubleshooting common issues such as networking configuration and tool availability.

---

# Lab Objectives

- Understand basic Linux navigation and file operations.
- Learn file searching and networking tools.
- Understand standard I/O redirection.
- Perform remote evidence acquisition using Netcat.

---

# Tools and Resources Used

- Kali Linux
- VirtualBox
- Linux Terminal (CLI)
- Netcat / Ncat (nc, ncat)
- wget
- grep
- Instructor tutorial slides referenced in the lab (Basic Tutorial PPT 3 and Advanced Tutorial PPT 4)

---

# Workspace / Evidence Storage

/media/sf_Lab03_LinuxCommandLine/  
/media/sf_Lab03_LinuxCommandLine/Screenshots/  
/media/sf_Lab03_LinuxCommandLine/Notes/  

---

# Methodology

1. Opened the terminal in Kali Linux.
2. Executed identification commands (e.g., pwd) and captured evidence.
3. Explored the filesystem and examined inode information.
4. Checked disk usage in human-readable format.
5. Created a working folder and evidence files, then copied/renamed them.
6. Checked file permissions and interpreted RWX bits.
7. Searched for keywords using grep and performed configuration searches in /etc.
8. Tested connectivity and viewed listening ports.
9. Practiced stdout/stderr redirection into evidence files.
10. Demonstrated remote transfer/acquisition concepts and verified received content.
11. Completed the challenge scenario of acquiring a Windows-created file onto Kali (documented commands and results).

---

# Screenshots and Evidence

## Part 1.1 — pwd Output (Current Working Directory)

**Screenshot Filename:** Part1_1_pwd.png

![Pwd](Screenshots/Part1_1_pwd.png)

---

## Part 1.2 — Inode Listing (ls -i) and Inode Explanation

**Screenshot Filename:** Part1_2_inode.png

![Inode](Screenshots/Part1_2_inode.png)

---

## Part 1.3 — Disk Usage (Human-Readable) using df -h

**Screenshot Filename:** Part1_3_disk.png

![Disk](Screenshots/Part1_3_disk.png)

---

## Parts 1.4 & 1.5 — Creating Forensics_Lab Directory in Home Folder

**Screenshot Filename:** Part1_4_create_folder.png

![Create Folder](Screenshots/Part1_4_create_folder.png)

**Screenshot Filename:** Part1_5_cd.png

![Cd](Screenshots/Part1_5_cd.png)

---

## Part 1.6 — Creating evidence.txt with echo

**Screenshot Filename:** Part1_6_echo.png

![Echo](Screenshots/Part1_6_echo.png)

---

## Part 1.7 — Copying evidence.txt to evidence_backup.txt

**Screenshot Filename:** Part1_7_copy.png

![Copy](Screenshots/Part1_7_copy.png)

---

## Part 1.8 — Renaming evidence_backup.txt to evidence_v2.txt using mv

**Screenshot Filename:** Part1_8_rename.png

![Rename](Screenshots/Part1_8_rename.png)

---

## Part 1.9 — Checking File Permissions (ls -l) and Identifying RWX Bits

**Screenshot Filename:** Part1_9_permissions.png

![Permissions](Screenshots/Part1_9_permissions.png)

---

## Part 2.1 — grep Search for "Evidence" with Line Numbers

**Screenshot Filename:** Part2_1_grep.png

![Grep](Screenshots/Part2_1_grep.png)

---

## Part 2.2 — Searching /etc Files for the String "network"

**Screenshot Filename:** Part2_2_search_etc.png

![Search Etc](Screenshots/Part2_2_search_etc.png)

---

## Part 2.3 — Network Connectivity Test (ping)

**Screenshot Filename:** Part2_3_ping.png

![Ping](Screenshots/Part2_3_ping.png)

---

## Part 2.4 — Listening TCP Ports (netstat -lnt)

**Screenshot Filename:** Part2_4_ports.png

![Ports](Screenshots/Part2_4_ports.png)

---

## Part 2.5 — Downloading a File using wget

**Screenshot Filename:** Part2_5_wget.png

![Wget](Screenshots/Part2_5_wget.png)

---

## Part 3.1 — Redirecting Standard Output (stdout) to root_list.txt

**Screenshot Filename:** Part3_1_stdout.png

![Stdout](Screenshots/Part3_1_stdout.png)

---

## Part 3.2 — Redirecting Standard Error (stderr) to error_log.txt

**Screenshot Filename:** Part3_2_error_content.png

![Error Content](Screenshots/Part3_2_error_content.png)

**Screenshot Filename:** Part3_2_error_created.png

![Error Created](Screenshots/Part3_2_error_created.png)

---

## Part 4.1 — Netcat Listener Setup (Evidence Transfer Concept)

**Screenshot Filename:** Part4_1_listener.png

![Listener](Screenshots/Part4_1_listener.png)

---

## Part 4.2 — Sending evidence.txt to Listener (Evidence Transfer Concept)

**Screenshot Filename:** Part4_2_sender.png

![Sender](Screenshots/Part4_2_sender.png)

---

## Part 4.3 — Verification that the File Was Received Correctly

**Screenshot Filename:** Part4_3_verify.png

![Verify](Screenshots/Part4_3_verify.png)

---

## Part 5.1 — Windows Evidence File Creation (Challenge Scenario)

**Screenshot Filename:** Part5_1_windows_file_created.png

![Windows File Created](Screenshots/Part5_1_windows_file_created.png)

---

## Part 5.2 — Kali Listener for Windows Acquisition (Challenge Scenario)

**Screenshot Filename:** Part5_2_kali_listener.png

![Kali Listener](Screenshots/Part5_2_kali_listener.png)

---

## Part 5.3 — Viewing Acquired Evidence on Kali (cat Verification)

**Screenshot Filename:** Part5_3_windows_send.png

![Windows Send](Screenshots/Part5_3_windows_send.png)

---

## Part 5.4 — Viewing Acquired Evidence on Kali (cat Verification)

**Screenshot Filename:** Part5_4_verify.png

![Verify](Screenshots/Part5_4_verify.png)

---

# Analysis and Findings

# PART 1: Basic Linux Navigation and File Management

## Exercise 1.1 — System Exploration

### 1) Current Location (pwd)
I used pwd to confirm my current directory. This is important in forensics to ensure that evidence files are created and stored in the correct location and that paths in documentation are accurate.

### 2) Inodes (ls -i) + Inode Explanation
I listed files with inode numbers. An inode is a filesystem structure that stores a file’s metadata (permissions, ownership, timestamps, and pointers to data blocks). The filename is separate from the inode, which is why inode examination is useful during forensic analysis.

### 3) Human-Readable Disk Space (df -h)
I used df -h to view disk usage and available space. This helps ensure there is enough storage capacity before collecting large artifacts or disk images.

---

## Exercise 1.2 — File Operations

### 4) Create Directory (Forensics_Lab)
I created a directory named Forensics_Lab in my home directory to keep lab artifacts organized.

### 5) Create File (evidence.txt)
Inside Forensics_Lab, I created evidence.txt containing:
“Confidential Evidence Data”.

### 6) Copy and Rename
- Copied evidence.txt to evidence_backup.txt to preserve a working copy.
- Renamed evidence_backup.txt to evidence_v2.txt to demonstrate versioning.

### 7) Permissions (ls -l) and RWX Interpretation
I checked file permissions and identified read/write/execute bits for User, Group, and Others. File permissions are important because they can explain why access succeeded/failed and help interpret user activity on a system.

---

# PART 2: Searching and Networking

## Exercise 2.1 — Grep and Search

### 8) Search for "Evidence" in evidence.txt with Line Number
I searched for the keyword “Evidence” inside evidence.txt and displayed the line number to demonstrate fast keyword triage.

### 9) Search /etc for "network"
I searched configuration files under /etc for the string “network” to demonstrate locating configuration-related evidence.

---

## Exercise 2.2 — Network Utilities

### 10) Connectivity Test (ping)
I ran ping to confirm network connectivity and documented the output.

### 11) Listening Ports (netstat -lnt) and SSH
I used netstat -lnt to display listening TCP ports. At the time of execution, no active listening ports were shown, indicating that services such as SSH were not running at that moment. (SSH commonly uses TCP port 22, but it must be actively listening to appear in `netstat` output.)

### 12) Download Using wget
I used wget to download a file and documented the successful retrieval as part of basic acquisition practice.

---

# PART 3: Standard I/O and Redirection

## Exercise 3.1 — File Descriptors and Redirection

### 13) Redirect stdout (1) to root_list.txt
I redirected standard output into root_list.txt to preserve results as an evidence artifact.

### 14) Redirect stderr (2) to error_log.txt
I attempted to read a non-existent file and redirected the error output into error_log.txt to preserve execution errors for documentation and troubleshooting.

### 15) Combine stdout and stderr (2>&1)
I redirected both stdout and stderr into a single file using 2>&1 to keep complete execution logs in one place.

---

# PART 4: Remote Evidence Acquisition and Shell Concepts

## Exercise 4.1 — Remote Transfer (Netcat Concept)

### 16) Listener Setup
I set up a listener on a chosen port to receive incoming data as part of remote acquisition practice.

### 17) Sending an Evidence File
From a second terminal/system, I transmitted the evidence file to the listener to simulate controlled remote collection.

### 18) Verification
I verified that the received file matched expectations by checking the output and/or file content on the receiving end.

---

## Exercise 4.2 — Bind Shell vs. Reverse Shell (Conceptual)

### 19) Bind Shell (Backdoor) Explanation
A bind shell is when the target system listens on a port and provides a command interface to whoever connects. The key idea is that the target “waits” for an inbound connection.

### 20) Why Reverse Shells Can Be More Effective with Firewalls
A reverse shell often succeeds in restricted environments because the connection is initiated from the target outward. Many firewalls block inbound connections but allow outbound traffic, making reverse connections more likely to pass.

### 21) Demonstration Commands (Redacted / Use Your Lab Notes)
- Attacker listener command: [REDACTED — insert from your lab notes if required]
- Victim connect-back command: [REDACTED — insert from your lab notes if required]

---

# PART 5: Lab Challenge — Remote Acquisition (Windows → Kali)

## Scenario Summary
A file was created on a Windows machine and had to be acquired remotely on Kali Linux without touching the Windows system after creation.

### Windows Side (Creation + Send)
- Created the evidence file with a greeting message.
- Sent the file content over the network to the Kali listener.

### Kali Side (Receive + Verify)
- Started a listener to save incoming data into evidence_from_windows.txt.
- Verified the received content using cat evidence_from_windows.txt.

**Finding:** The file content was successfully displayed on Kali, confirming that remote acquisition was completed and verified.

---

# Challenges and Solutions

| Challenge | Solution |
|---|---|
| Windows host could not communicate with Kali VM due to network configuration | Reconfigured VirtualBox networking (Host-Only Adapter) to enable direct communication between systems. |
| “Command not found” errors with nc/ncat | Installed the required tools/packages so Netcat commands were available on both systems. |
| Evidence file not found on Windows due to wrong directory | Navigated to the correct directory and confirmed the file existed before transfer. |
| Syntax mistakes during redirection/transfer | Reviewed command structure carefully and corrected redirection operators and command formatting. |

---

# Conclusion

This lab enhanced my understanding of Linux command-line operations and their application in digital forensics. I practiced navigation, file management, searching, networking utilities, and output redirection to create repeatable workflows and preserve results as evidence artifacts.

The remote acquisition activities reinforced controlled collection and verification procedures. The Windows-to-Kali challenge demonstrated a realistic scenario where investigators must acquire data remotely while minimizing interaction with the target system. Overall, the lab improved my confidence in Linux CLI usage and strengthened my ability to document forensic actions clearly and accurately.

---

# Recommendations

- Practice Linux CLI commands frequently to improve speed and accuracy.
- Learn VirtualBox networking modes (NAT, Bridged, Host-Only) to reduce connectivity issues during labs.
- Document terminal outputs and steps carefully to support troubleshooting and produce strong forensic reports.

---

# References

- Instructor tutorials: Basic Tutorial (PPT 3) and Advanced Tutorial (PPT 4)
- Course-provided lab materials and slides used during exercises
