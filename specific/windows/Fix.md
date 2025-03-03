# Windows System File Repair Guide  
## Using `sfc /scannow` and `DISM`  

This guide explains how to fix corrupted system files in Windows using built-in tools.  

---

### Table of Contents  
1. [What Are These Tools?](#tools)  
2. [Using `sfc /scannow`](#sfc)  
3. [Using `DISM`](#dism)  
4. [Combined Approach](#combined)  
5. [Troubleshooting](#troubleshoot)  

---

## <a name="tools"></a>1. What Are These Tools?  
- **`sfc /scannow`** (System File Checker): Scans and repairs corrupted system files.  
- **`DISM`** (Deployment Image Servicing and Management): Repairs Windows system integrity by restoring missing files from the installation media.  

---

## <a name="sfc"></a>2. Using `sfc /scannow`  
**Steps**:  
1. Open **Command Prompt as Administrator**:  
   - Press `Win + X` > Select "Command Prompt (Admin)" or "PowerShell (Admin)".  
2. Run the scan:  
   ```cmd  
   sfc /scannow  
   ```
3. Wait for completion. The tool will:
   Scan all protected system files.
   Replace corrupted files.
   Display results: Windows Resource Protection did **not** find any problems (if no issues).
   Note : This tool requires sufficient disk space and read/write permissions.


## <a name="dism"></a>3. Using DISM

When to Use : If sfc /scannow fails (e.g., error 0x80070570) or system integrity is compromised.

**Steps :**

1. Open Command Prompt as Administrator .

   ```cmd  
    DISM /Online /Cleanup-Image /ScanHealth  
    DISM /Online /Cleanup-Image /RestoreHealth  
    ```

2. The tool will:
    Scan for errors.
    Download necessary files (connect to internet if prompted).
    Repair the Windows image.


## <a name="combined"></a>4. Combined Approach
For persistent issues, run both tools sequentially:

1. Run DISM first.
2. Then run sfc /scannow.

   ```cmd  
    DISM /Online /Cleanup-Image /RestoreHealth  
    sfc /scannow  
    ```


## <a name="troubleshoot"></a>5. Troubleshooting
Common Issues :

- Error 0x80070057 (sfc fails) :
 **Run chkdsk /f /x and restart.**

- Check for hardware issues (e.g., failing hard drive).

- Error 0x80070570 (sfc blocked) :
    **Ensure no third-party antivirus is interfering.**
    **Disable real-time protection temporarily.**

- Last Resort :
    If tools fail, perform a Windows Repair Installation [USB-Reset](https://github.com/ag7dev/pcfix-database/blob/main/specific/windows/reset/FULLRESET.md)
