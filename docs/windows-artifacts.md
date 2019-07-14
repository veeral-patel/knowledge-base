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
