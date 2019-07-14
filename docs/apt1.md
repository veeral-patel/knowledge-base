# APT 1

[Original APT1 Report, from Mandiant](https://www.fireeye.com/content/dam/fireeye-www/services/pdfs/mandiant-apt1-report.pdf)

## Overview

- Stole 100's of TBs of data from 141 organizations since 2006
- Once they get into a network, they keep exfiltrating data over time
  - Maximum time APT1 has been in an environment has been 4+ years
- Targeted mostly the US (115 attacks vs <= 5 attacks on other countries)

## What do they steal?

- Info about products, like designs
- Manufacturing procedures
- Business plans
- Policy documents, like meeting notes from execs and papers
- Emails of top employees
- User credentials
- Network architecture details

## APT1's Attack Lifecycle

### Initial Compromise

- APT1 leverages attachment-based spearphishing
- Attached file installs a custom APT1 RAT (APT1 sometimes uses public backdoors like Poison Ivy and Ghost RAT)
- Sometimes, people reply asking if email is legit, APT1 says "yes" (of courses)
- APT1 uses Resource Hacker to change the attached file's icon to the PDF icon
- Also, APT1 sets the filename to something like `file.pdf <many spaces>.exe` to trick victims into thinking it's an PDF file

### Establish foothold

- Problem: now that we got in, how do we control the malware inside to do what we want?
- Solution: Have malware connect outbound to C&C server. Firewalls block inbound connections, but not outbound connections.
- APT1 first installs minimal backdoors, which are used to install fully functional backdoors

#### Beachhead Backdoors

- Goal: get the full standard backdoor on the PC
- Can only do simple tasks like send out local files, send out basic system info, download a standard RAT
- The WEBC2 backdoor is the most popular beachhead backdoor
  - Newer backdoors: download a webpage from C2 server, run the commands between special tags.
  - Older backdoors: read data between HTML comments (this is why APT1 was called Comment Crew)
- 400+ variants of WebC2

#### Standard Backdoors

- Communicate over HTTP or with custom protocol malware authors designed
- Can mimic MSN Messenger, Jabber, Gmail Calendar protocols
- Use SSL encryption

##### Functionality

- Upload/download files
- Create/delete directories
- List/start/stop processes
- Modify the system registry
- Take screenshots of the user’s desktop
- Capture keystrokes
- Capture mouse movement
- Start an interactive command shell
- Create a Remote desktop (i.e. graphical) interface
- Harvest passwords
- Enumerate users
- Enumerate other systems on the network
- Sleep (i.e. go inactive) for a specified amount of time
- Log off the current user
- Shut down the system

### Exfiltration

- ZIP or RAR the data to exfiltrate
- Use the backdoor channel, FTP, or custom file transfer tools to transfer the data out
- APT1 exfiltrates data slowly
