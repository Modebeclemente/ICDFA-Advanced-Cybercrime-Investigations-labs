# Lab Report: Number Systems and Digital Forensics Fundamentals

## Student Information

| Field | Details |
|---|---|
| Student Name | Clement Modebe |
| Student ID | aci2616123@icdfa.edu.ng |
| Course Name | Advanced Cybercrime Investigation |
| Instructor Name | Mr. Aminu Idris |
| Date of Submission | 8 May 2026 |
| Version | 1.0 |

---

# Executive Summary

This lab was designed to help me understand how computers store and represent information using number systems and common digital forensics formats. Using a Kali Linux virtual machine (Linux terminal/CLI) and Python 3, I practiced converting values between binary, decimal, and hexadecimal, first by hand and then with Linux commands and Python functions to verify accuracy.

I also worked with ASCII encoding to connect numbers to readable characters and used CLI/Python tools to translate strings into hexadecimal values commonly seen in forensic investigations. Additionally, I converted Unix epoch timestamps into human-readable dates and explored how different systems use different epoch starting points.

Finally, I reviewed how data is stored in memory using endianness and validated byte order with Python. Hashing concepts were also explored to reinforce evidence integrity principles.

---

# Lab Objectives

- Understand and manually convert between Binary, Decimal, and Hexadecimal number systems.
- Verify conversions using Linux CLI tools and Python 3.
- Work with ASCII encoding and text-to-hex conversions.
- Convert Unix timestamps to readable dates.
- Explain endianness and verify byte order in Python.
- Understand basic hashing and integrity verification concepts.

---

# Tools and Resources Used

- Oracle VirtualBox
- Kali-Forensics Linux VM
- Linux CLI tools:
  - `bash`
  - `printf`
  - `xxd`
  - `date`
  - `md5sum`
  - `sha256sum`
- Python 3
- Instructor-provided slide deck:
  - `0_Number_Systems.pptx`

---

# Workspace / Evidence Storage

```bash
/media/sf_Lab01_NumberSystems/
/media/sf_Lab01_NumberSystems/Screenshots/
/media/sf_Lab01_NumberSystems/Notes/
```

---

# Methodology

1. Started the Kali-Forensics VM in VirtualBox.
2. Opened the terminal and verified Python 3 installation.
3. Confirmed the shared folder mount path.
4. Created and verified the `Screenshots` and `Notes` folders.
5. Performed manual number system conversions.
6. Verified conversions using Linux CLI commands and Python.
7. Completed ASCII, timestamp, endianness, and hashing exercises.
8. Captured screenshots and saved terminal outputs.

---

# Screenshots and Evidence

## Figure 1 — Kali VM Started and Terminal Opened

**Screenshot Filename:** `Fig01_KaliVMStarted.png`

```markdown
![Figure 1 - Kali VM Started](Screenshots/Fig01_KaliVMStarted.png)
```

---

## Figure 2 — Python Version Verification

**Screenshot Filename:** `Fig02_CheckPythonVersion.png`

```markdown
![Figure 2 - Python Version](Screenshots/Fig02_CheckPythonVersion.png)
```

---

## Figure 3 — Shared Folder Verification

**Screenshot Filename:** `Fig03_SharedFolderExists.png`

```markdown
![Figure 3 - Shared Folder Exists](Screenshots/Fig03_SharedFolderExists.png)
```

---

## Figure 4 — CLI Conversion Output

**Screenshot Filename:** `Fig04_CLIConversions.png`

```markdown
![Figure 4 - CLI Conversions](Screenshots/Fig04_CLIConversions.png)
```

---

## Figure 5 — ASCII and xxd Output

**Screenshot Filename:** `Fig05_ASCII_xxd_Output.png`

```markdown
![Figure 5 - ASCII xxd Output](Screenshots/Fig05_ASCII_xxd_Output.png)
```

---

## Figure 6 — Unix Timestamp Conversion

**Screenshot Filename:** `Fig06_UnixTimestampConversion.png`

```markdown
![Figure 6 - Unix Timestamp Conversion](Screenshots/Fig06_UnixTimestampConversion.png)
```

---

## Figure 7 — Python sys.byteorder Output

**Screenshot Filename:** `Fig07_ByteOrderOutput.png`

```markdown
![Figure 7 - Byte Order Output](Screenshots/Fig07_ByteOrderOutput.png)
```

---

## Figure 8 — Hashing Output

**Screenshot Filename:** `Fig08_HashOutput.png`

```markdown
![Figure 8 - Hash Output](Screenshots/Fig08_HashOutput.png)
```

---

# Analysis and Findings

# PART 1: Number System Conversions

## Exercise 1.1 — Manual Conversions

### 1. Convert `101101₂` to Decimal

```text
(1×2⁰) + (0×2¹) + (1×2²) + (1×2³) + (0×2⁴) + (1×2⁵)
= 1 + 0 + 4 + 8 + 0 + 32
= 45
```

### 2. Convert `255₁₀` to Hexadecimal

```text
255 ÷ 16 = 15 remainder 15
15 ÷ 16 = 0 remainder 15

15 = F in hexadecimal

Result = FF₁₆
```

### 3. Convert `0x1A3₁₆` to Decimal

```text
(3×16⁰) + (10×16¹) + (1×16²)
= 3 + 160 + 256
= 419
```

### 4. Convert `1110 1011₂` to Hexadecimal

```text
1110 = E
1011 = B

Result = EB₁₆
```

---

## Exercise 1.2 — Linux CLI and Python

### 5. Shell Arithmetic Conversion

```bash
echo $((0x4F))
```

Output:

```text
79
```

### 6. Python Binary Conversion

```python
int("110011", 2)
```

Output:

```text
51
```

### 7. Linux printf Command

```bash
printf "%X\n" 1024
```

Output:

```text
400
```

---

# PART 2: ASCII and Text Encoding

## Exercise 2.1 — Character Conversion

| Decimal | Hexadecimal | ASCII Character |
|---|---|---|
| 65 | 41 | A |
| 104 | 68 | h |
| 33 | 21 | ! |
| 48 | 30 | 0 |

---

## Exercise 2.2 — CLI and Python Tools

### 8. Hexadecimal Representation of "Forensics"

```bash
echo -n "Forensics" | xxd
```

Output:

```text
00000000: 466f 7265 6e73 6963 73
```

### 9. Python chr() and ord()

```python
chr(82)
ord('Z')
```

Output:

```text
R
90
```

---

# PART 3: Epoch Time and Timestamps

## Exercise 3.1 — Unix Timestamp Conversion

### 10. Unix Epoch Date

```text
00:00:00 UTC on 1 January 1970
```

### 11. Convert Unix Timestamp

```bash
date -d @1714550400
```

Output:

```text
Wed 01 May 2024 08:00:00 UTC
```

### 12. Current UTC Time in Python

```python
from datetime import datetime, timezone
datetime.now(timezone.utc)
```

---

## Exercise 3.2 — Forensics Comparison

### Difference Between Unix Epoch and Mac Cocoa Core Date

- Unix Epoch starts at:
  - `1 January 1970 UTC`
- Mac Cocoa Core Date starts at:
  - `1 January 2001 UTC`

Difference:

```text
978,307,200 seconds
```

### Why This Matters in Forensics

Using the wrong epoch can produce incorrect timelines. This may:

- Make files appear to be created decades earlier or later.
- Corrupt investigation timelines.
- Produce unreliable forensic evidence.

Investigators must always identify the correct timestamp format before analysis.

---

# PART 4: Data Storage and Endianness

## Exercise 4.1 — Endianness Identification

### 13. Define Little-endian and Big-endian

- **Little-endian:** Least significant byte stored first.
- **Big-endian:** Most significant byte stored first.

### 14. Little-endian Byte Order of `0x12345678`

```text
78 56 34 12
```

### 15. Python sys.byteorder

```python
import sys
sys.byteorder
```

Output:

```text
little
```

---

# PART 5: Hash Codes (Optional / Bonus)

## 16. Generate MD5 and SHA256 Hashes

```bash
echo -n "DigitalEvidence" | md5sum
echo -n "DigitalEvidence" | sha256sum
```

### MD5 Output

```text
3df79ba6a3504ef82b9ea1d8603097b8
```

### SHA256 Output

```text
c590ad5eab615d1df0b9ea606c1a2a8d265067ad
```

---

## 17. Importance of `-n` with echo

The `-n` flag prevents `echo` from adding a newline character.

Without `-n`, the newline becomes part of the hashed data, producing a completely different hash value.

---

# Challenges and Solutions

| Challenge | Solution |
|---|---|
| Shared folder missing in Kali | Installed VirtualBox Guest Tools and rebooted |
| No internet connectivity in Kali | Configured NAT networking |
| apt update signature errors | Disabled problematic Elastic repository |
| Duplicate shared folder mounts | Used working mount and verified permissions |

---

# Conclusion

This lab improved my understanding of how computers represent and store digital information. I practiced converting between binary, decimal, and hexadecimal systems manually and verified results using Linux and Python tools.

I also learned how ASCII encoding works, how timestamps differ across operating systems, and why endianness matters when interpreting raw data. Hashing exercises reinforced the importance of integrity verification in digital forensics investigations.

These concepts are directly applicable to real-world forensic analysis where investigators regularly work with raw binary and hexadecimal evidence.

---

# Recommendations

- Always verify the number base before converting values.
- Identify timestamp formats and epochs before analysis.
- Use proper hashing methods to maintain evidence integrity.
- Document screenshots and terminal outputs carefully during investigations.

---

# References

- Idris, A. — `0_Number_Systems.pptx`
- GNU Bash Documentation
- Python 3 Documentation
- Kali Linux Documentation
