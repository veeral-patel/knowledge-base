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

## Persistence

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

### DLL Search Order Hijacking

## Exfiltration

- Schedule transfer at certain times in day, to blend in with normal traffic
- Copy data onto removable drive
- Exfiltrate over bluetooth, cellular signal etc
- Exfiltrate over multiple channels
- Encrypt, split, compress files
- Steganography

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
- Process hollowing
- Timestomping
- Overwriting programs like `ls` and `ps`

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

## Command and Control

- Using a web service (like Twitter)
- Using a non-standard C&C protocol (like ICMP)
- ICMP could be useful if there's a local C&C server on the LAN
- Use a proxy. Can chain multiple proxies
- Split communication over multiple chaanels
- Encrypt C&C body, even while using HTTPS
