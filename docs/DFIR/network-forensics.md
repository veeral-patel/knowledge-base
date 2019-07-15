# Network Forensics (SANS DFIR 2015)

[YouTube link](https://www.youtube.com/watch?v=cVbil4y702o)

## Brief history of computer forensics

1. Shut down PC and image the hard disk. (The Secret Service still does this)
2. Memory forensics
3. Network forensics

Network forensics augments, not replaces, #1 and #2

## Motivation

- Say a user Googles for "how to bury a body". But he never hits enter
- The search query wouldn't be in the browser history, but you'd see it in the packet capture

Google fires a request for every letter you type:

```
h
ho
how
how t
...
```

Also, most malware gets onto PCs via the network. Most malware also connects to C&C over network

## Sources of Evidence

Packet capture:

1. Headers only
2. Full content

Logs:

- From proxy servers - URLs requests
- Firewalls - packets accepted or denied
- Flow records - high level traffic overview

## Identifying malicious traffic

- Connections to suspicious IPs
- Activity at unusual times of day
- Large outbound file transfers
- Workstation to workstation communications
- Ideally, have a baseline and alert on anomalous network traffic

## DIY DNS DFIR

[Talk on YouTube](https://www.youtube.com/watch?v=ihxkxV80u6I)

From "SANS Threat Hunting Summit 2016"

### Free tools

- PassiveTotal
- ELK or Graylog (for storing DNS queries)

### Commercial tools

- PassiveTotal Enterprise
- DomainTools
- OpenDNS Investigate
