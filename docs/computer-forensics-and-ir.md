# "Computer Forensics and IR" (by Mandia et al)

[Link to Book on Amazon](https://www.amazon.com/Incident-Response-Computer-Forensics-Third/dp/0071798684)

## Investigation

```
1. Examine initial lead(s)

repeat:

2. IOC creation
3. Search environment with IOCs
4. Identify systems of interest
5. Collect evidence
6. Analyse data
```

### Common mistake: only looking for malware

- But malware is only one tool
- And when attacker gains credentials, he no longer needs malware

### IOCs

#### Types of IOCs

- Network IOCs = Snort rules
- Malware IOCs = YARA rules
- Host IOCs = OpenIOC, Cybox (not mature!)

#### Places we search for IOCs

- Hosts
- Packet captures
- Live traffic
- Malware samples
- Logs (Duo, firewall, Carbon Black, etc) - stored in SIEM!
- Internal threat intel tool
- External threat intel providers
- DNS logs

Now you have a list of systems you've found IOCs on…

### Categorize attackers' activities on each system

- Backdoor installed
- Data stolen
- etc

### Prioritize each system

- Based on system's owner (eg, CFO vs secretary)
- Based on what it's used for (Kubernetes server in production vs Raspberry Pi in lab)
- Interestingly - based on how much we'll learn from this system
  - Ie, whether it's a new kind of malware or the 20th identical rootkit

### Preserve evidence

- Until now, we haven't collected any evidence from the hosts
- Now, collect live artifacts, memory dump, hard disk image from host (without shutting down PC)
- Key - Automate the collection process. You want to minimize changes to the system
  as well as interaction time with system

#### Collecting live artifacts + memory dumps

- Windows: use Mandiant Redline for live artifacts, Memoryze for memory dumping
- UNIX: write a script for live artifacts, LiME for memory dumping
- MacOS - write a script for live artifacts (try OSXCollector!), Memoryze for memory dumping
- Can use gcore for dumping individual processes

### Analyze data

Some things to analyze:

- malware
- live response artifacts
- disk image
- packet captures
- memory dump

## Remediation

1. Posturing - eg, exchange contact info, designate responsibilities, etc
2. Tactical - short term - eg, change passwords, block IP addresses, re-image hacked systems
3. Strategic - long term. go through the attack's kill chain and add a protection against each step

## Tracking of significant info during incident

Have a naming scheme for each incident. Some possibilities:

- INCIDENT-333 (auto-generated)
- Stormy Seas (user created)
- MAC-Jan-3-A (unique but descriptive)

Significant information to track:

### List of evidence collected

For each piece of evidence, store:

- Source of data (eg a person - "Jill Matheson" or a system - "WIN-XP-338")
- Date time of collection
- Chain of custody

### List of affected systems

- Systems that were hacked into
- Systems that were accessed without authorization (not the same thing!

## Report Writing

- Know your audience. Are you writing a technical postmortem or a summary for the C-Suite?
- Just state the facts. Don't interject speculation or opinions.
- Mandiant writes reports in Word, according to the author
