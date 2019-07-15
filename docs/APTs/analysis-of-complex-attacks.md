# Threat Analysis of Complex Attacks (SANS DFIR 2015)

[Talk on YouTube](https://www.youtube.com/watch?v=Yh1XZf0hLS4)

## You can't prevent complex attacks

- When infected by a cyber criminal's malware, your job is just to get rid of the malware
- But for complex attackers, malware is just a tool. They can also hire people to infiltrate you, for example
- You can't prevent complex attacks

## Don't let APTs know once you detect them

- Don't submit to VirusTotal
- Don't publish Yara rules

If you do, they'll just create new malware and return. Remember, these are targeted attacks

### Instead...

- Limit their bandwidth
- Feed them false information
- This will buy you time to investigate the attacker

## A few ways to detect APTs

### Outgoing network traffic

- store DNS queries your endpoints make (use OpenDNS)
- capture full packet captures with Suricata
- why outgoing? malware must talk to C&C server over network
  - I wonder if malware could be controlled by a rogue employee regularly plugging in a USB drive

but APTs try bypassing this!

- Equation Group sends its outgoing traffic (responses to C&C server?) to US universities
  - these universities then somehow send the packets to Equation Group

### Honey docs

- Spin up a server, add documents to it, send alert whenever a doc is opened

### Technical analysis of samples

- APTs reuse code samples; after all, they spend a lot of money developing them
- You should be able to recognize attacker's code
- Have an internal threat intel tool
- For each bad IP or domain you see, write down who you think it is, all the times you saw them, etc
- Potentially, 2 threat actors will work together, or really be 2 campaigns of one threat actor. Detect this if 2 threat actors are using the same IPs

## Mapping victims

### Using VirusTotal

1. Write YARA rule
2. Setup VirusTotal to email you whenever a piece of malware, which matches your rule, is uploaded

### Using domains

- Register an domain name the APT used in malware
- Can find domain names hard-coded in malware
- Then, you'll get traffic from all the victims

## Attribution

- Attribution is easy to fake!
- Try recovering the passwords of the C2 server
  - May be hard-coded in the malware
  - Can then log into C2 server. If malware creator forgets to use a VPN, you can see what IP he has
- Have a linguistic expert on the team
  - He said a European person probably misspelled "exceeded" but that's not convincing
- Having a geopolitical expert could be useful to understand the attacker's motivations

## Protection

Austrialian Signals Directorate: To stop 85% of complex attacks, do:

1. Whitelisting executables and default deny
2. Patching apps
3. Patching OS
4. Restrict admin privileges

## Who are the threat actors?

- Insider threats - motivated by money or revenge
- Hacktivist networks - motivated by ideological reasons
- APTs - motivated by economic, military reasons
- Script Kiddies - motivated by reputation
- Cyber criminals - motivated by money
- Rogue hackers - motivated by reputation
