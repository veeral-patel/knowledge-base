# ATT&CK Framework

## Initial access

- Supply chain compromise
- Attachment spearphishing
- Credential phishing
- Spearphishing over a service (like Twitter)
- Sending an operative to work at the victim company
- Plugging in an infected USB drive
- Bribing or extorting an insider
- Obtaining secrets from an an GitHub repo
- Compromising a public web app
- Zero day
- Writing an exploit for a recently disclosed vulnerability
- Buying an infected host in network from a botnet owner
- Hardware keylogger, packet sniffer, etc
- Keylogging password for password manager

## Information gathering

From an endpoint, can gather:

- Accounts
- Open applications (Helps keylogger)
- Browser extensions
- Files/directories on disk
- Network shares
- Running processes
- Security software on machine
- System info (patches, OS version, etc)
- Network connections

Can also:

- Port scan other hosts
- Sniff network traffic
- Query registry

## Lateral Movement

- Use JAMF, Ansible etc to deploy malware
- Exploit vulnerable network services
- Pass the hash
- Pass the ticket
- Upload malicious files onto internal website
- Embed macros into shared documents
- Execute commands remotely using internally hosted software (eg, Carbon Black)
- Keylog user's password. Then execute commands remotely with winrm
- Copy adversary's tools to other PCs with FTP/SCP
- RDP session hijacking
- Log in with a legitimate RDP/SSH/other service password
- SSH hijacking

## Privilege escalation

- Scheduled tasks in older versions of Windows run as SYSTEM
- Stealing an admin's credentials
- Exploiting an program running as SYSTEM

## Persistence

- Autoruns in Windows Registry
- DLL Search Order Hijacking
- Shortcut Hijacking
- Bootkit
- `.bashrc` and `.bash_profile`
- Web shells
- Browser extensions
- Firmware
- Login item (macOS)

### Startup folders

- Each user has a startup folder
- When he logs in, every program in the folder gets executed
- Can add a LNK file to execute say a powershell command on startup

### Scheduled tasks

- Using `at` or `schtasks`
- Stored as \*.job files

### System binary modification

- Can use Windows Resource Protection to counter-act this
- Also, if a system binary changes, its hash will change
- And its digital signature will be invalidated

## Defense Evasion

- Access token manipulation - Security tokens determine who owns a process. If you're an administrator, you can use runas to run a process under a different user.
- Can pretend to be a sysadmin, for example, while port scanning hosts
- Binary padding. Add/remove bytes from malware, without changing its functionality, to change its hash. Evades signature based AV
- Clear `.bash_history`
- Clear Windows Event logs
- Edit Windows Event logs (Shadow Brokers)
- Kill Windows event log thread in lsasse.exe (Shadow Brokers)
- Sign malware with stolen certificates
- Obfuscating strings. Could help avoid detection from Yara. Eg, instead of "bad00string", write "bad" + "00string"
- Kill processes of security tools
- Or removing their registry keys so they don't start on startup
- Process injection
- Process hiding
- Not running in a VM
- Installing a root certificate
- Packing
- Timestomping
- Overwriting programs like `ls` and `ps`

### VM detection techniques

- [Check CPU temperature](https://www.andreafortuna.org/dfir/malware-analysis/malware-vm-detection-techniques-evolving-an-analysis-of-gravityrat/)
- Can check other hardware like Motherboard, Processor, etc
- Check for processes like VMWare Tools
- Check for driver files on disk
- Check for registry keys
- Check if MAC address of network adapter corresponds to VMWare, VirtualBox, etc
- Examine OS data structures in memory

### Process hollowing

- Launch a legitimate process like `calc.exe`, then suspend the process and replace the process's memory with the code of another program
- Causes Windows to think the original process is running, but it's not
- To detect: use Volatility to dump a process's code to an executable. Then, compare that executable with the original file on the filesystem

## Stealing credentials

- Creating admin accounts
- Checking .bash_history for usernames/passwords
- Checking employee's desk for written down asswords
- Finding credentials on GitHub or internal version control server
- Keylogging password for password manager
- Brute forcing (eg a web server)
- Dumping hashes (eg of /etc/shadow) then cracking them offline
- Keylogging
- Asking for password or TOTP token over phone
- Credential phishing
- Viewing saved passwords with Keychain
- Or revealing them in Google Chrome
- Faking an "password required" OS prompt

### Pass the hash

- Can read an NTLM hash from memory with mimikatz
- Or dump all hashes from NTDS.DIT on domain controller
- Attacker then puts the hash in his `lsass.exe` memory. Lets him access any service victim could with those credentials
- Attack is possible because NTLM challenge-response doesn't require a plaintext password, just the hash

## Command and Control

- Using a web service (like Twitter)
- Using a non-standard C&C protocol (like ICMP)
- ICMP could be useful if there's a local C&C server on the LAN
- Use a proxy. Can chain multiple proxies
- Split communication over multiple chaanels
- Encrypt C&C body, even while using HTTPS

## Exfiltration

- Schedule transfer at certain times in day, to blend in with normal traffic
- Copy data onto removable drive
- Exfiltrate over bluetooth, cellular signal etc
- Exfiltrate over multiple channels
- Encrypt, split, compress files
- Steganography
