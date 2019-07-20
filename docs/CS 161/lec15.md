# Lecture 15: Denial of Service Attacks

[https://inst.eecs.berkeley.edu/~cs161/sp19/lectures/lec15_net_5.pdf](https://inst.eecs.berkeley.edu/~cs161/sp19/lectures/lec15_net_5.pdf)

## Single system DoS
- Resource consumption: run a fork bomb! Solution is for the system to
  enforce some quota on each user's resource usage.

## Network-based DoS

### Flooding
- Send as many small packets as possible, with the aim of surpassing the
  maximum number of packets the victim can receive at once
- Or send maximum-sized packets, with the aim of overwhelming the victim's
  bandwidth

### Flooding defenses
- Filter packets from the attacker's IP, using a firewall
- Block any packets that match a certain, suspicious pattern
- Use a DoS mitigation provider

### Circumventing these defenses
- Attacker can spoof the source IP address by setting it to a random 32-bit
  number (still use one host)
- Note: You can only flood and spoof using UDP packets. (TCP doesn't work because the victim may be unable to establish a TCP connection with the host at the spoofed IP. I'm excluding SYN flooding, as it's not based on sending lots of packets.)
- Use many hosts -- say a botnet -- to send traffic (DDoS). Mirai botnet took down Dyn DNS, which also took down Twitter and Reddit.
