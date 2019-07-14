# Windows Artifacts

## Prefetch

- Windows keeps track of the applications opened the most often and preloads them into memory before they're executed
- Prefetch files (\*.pf) stored in `C:\Windows\Prefetch`
- For example, prefetch file for `calc.exe` named `calc.exe-<8 char hash of filepath>.pf`
- Body of prefetch file tells us when program was executed, how many times, from what path

## Shellbags

- Windows stores the size, icon, position of a folder when using Windows Explorer
- Persists after the folder is deleted
- Can be used to list deleted files and previously mounted volumes

## Windows Event Logs

- Application = events apps want to log
- Security = sign in/out, user creation, program execution, etc
- System = changes to system time, service runs, etc

## ShimCache

- Aka App Compatibility Cache
- Stored in registry
- Limited in size - overwrites itself when out of space
- Stores file paths and metadata of files that are browsed interactively in `explorer.exe` or executed
- Process execution flag indicates if file was executed

## LNK files

- Shortcut files. The Google Chrome "shortcut file" on the Desktop is a LNK file
- Created whenever an user opens a file -- not just when he creates a file!
- Useful if the original file is deleted

### Attributes

- MACE times of original file
- serial number of volume where original file was stored (useful if an USB was plugged in)
- original file's size when last opened
- a few other things

## NTFS MACE timestamps

- NTFS stores 2 sets of `Modified`, `Accessed`, `Created`, `MFT entry modified` timestamps

## MFT

- Stores metadata about every file in filesystem
- [Can look for anomalies using AnalyzeMFT](https://www.andreafortuna.org/dfir/using-mft-anomalies-to-spot-suspicious-files-in-forensic-analysis/)
- In a directory, files should have sequential MFT Record Numbers. Helps us identify newly added files to `C:\Windows`, for example

## Registry

### Registry structure

- Designed to centralize configuration files in Windows
- 5 main system hives: `System`, `Software`, `Security`, `SAM`, `Default`
- User specific hives: `NTUSER.DAT`, `USRCLASS.DAT`

### How are hives structured?

- Essentially, as folders of key-value pairs
- Keys = "folders"
- Values = "keys in each folder"
- Data = "values in each folder"
- Example: `HLKM\SOFTWARE\cygwin` is a key, `rootdir` is a value, `C:\cygwin64` is data
- Registry keys (folders) only store one timestamp: `LastWriteTime`
- Windows API doesn't have a function to set `LastWriteTime` for a registry key, so malware timestomping a registry key isn't common

### Auto-run keys

- Hundreds of them! Some still undocumented
- Run, RunOnce, AppInit_DLLs, a lot more

### Windows services

- Are executed by `svchost.exe`
- Look for a `ServiceMain` function!

### Volatile hives

- `HKEY_LOCAL_MACHINE` hive is erased after computer is shutdown, as it's only stored in memory

## Scenarios

[From the CountUponSecurity Blog](https://countuponsecurity.com/2018/06/20/digital-forensics-plugx-and-artifacts-left-behind/)

**Scenario 1: The attacker placed the filename “kas.exe” on the folder “c:\PerfLogs\Admin”. Which artifacts could record evidence about this action?**

MFT, USN, $LogFile, $INDX attributes

**Scenario 2: Which account did the attacker used to log into the system when he placed “kas.exe” on the file system?**

Windows Event Logs (Security)

**Scenario 3: Attacker executed the “kas.exe” binary. Which artifacts might record this evidence?**

ShimCache, Prefetch, Windows Event Logs (Security)

**Scenario 4: The execution of “kas.exe” dropped three files on disk that used DLL Search Order Hijacking to achieve persistence and install the malicious payload. Which artifacts might help identifying this technique?**

I didn't know. Correct - use a mixture of artifacts

**Scenario 5: The PlugX dropped files have the NTFS timestamps manipulated i.e., It copies the timestamps obtained from the operating system filename ntdll.dll to set the timestamps on the dropped files. What artifacts could be used to detect this?**

Check for inconsistencies between NTFS `$Standard_Information` and `$Filename` attributes.

Also, to identify dropped file, can look for MFT anomalies. Usually, files in a folder have sequential MFT Record Numbers. Dropped files will have later record numbers.

**Scenario 6: Attacker used the PlugX controller to Invoke a command shell and execute Windows built-in commands. Are there any artifacts left behind that could help understand commands executed?**

Use Volatility - `cmdscan`

**Scenario 7: Attacker established a persistence mechanism either using a Service or Registry Key.**

Use RegRipper. Check last modified timestamp for each registry key

**Scenario 8: The attacker accessed the Active Directory database using the “ntdsutil.exe” command. What could be used to detect this activity?**

Volatility `cmdscan`, ShimCache, Windows Event logs. (Can't use Prefetch - not enabled on servers!)
