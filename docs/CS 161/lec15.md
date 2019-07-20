# Lecture 15: Denial of Service Attacks

[https://inst.eecs.berkeley.edu/~cs161/sp19/lectures/lec15_net_5.pdf](https://inst.eecs.berkeley.edu/~cs161/sp19/lectures/lec15_net_5.pdf)

## To look into:
- TCP SYN flooding defenses
- SYN cookies

## Single system DoS
- Resource consumption: run a fork bomb! Solution is for the system to
  enforce some quota on each user's resource usage.

## Network-based DoS

### Flooding
- Send as many small packets as possible, with the aim of surpassing the
  maximum number of packets the victim can receive at once
- Or send maximum-sized packets, with the aim of overwhelming the victim's
  bandwidth
- Amplification: A DNS response is much larger than a DNS query, so send a lot of DNS queries to a DNS server, with the source IP set to the victim's IP. Also see NTP amplification

### Flooding defenses
- Filter packets from the attacker's IP, using a firewall
- Block any packets that match a certain, suspicious pattern
- Use a DoS mitigation provider

### Circumventing these defenses
- Attacker can spoof the source IP address by setting it to a random 32-bit
  number (still use one host)
- Note: You can only flood and spoof using UDP packets. (TCP doesn't work because the victim may be unable to establish a TCP connection with the host at the spoofed IP. I'm excluding SYN flooding, as it's not based on sending lots of packets.)
- Use many hosts -- say a botnet -- to send traffic (DDoS). Mirai botnet took down Dyn DNS, which also took down Twitter and Reddit.

## TCP SYN Flooding

- Attacker sends a SYN packet, victim sends a SYN/ACK, but the attacker
  doesn't send an ACK
- Each half-open TCP connection consumes some memory; the purpose of SYN
  flooding is to consume the victim host's memory
- Question: does SYN flooding seek to consume all of the victim host's
  memory, or exhaust the number of network connections the victim host can
  make?

### Defenses
- Add more memory to your servers
- Filter traffic using an IP reputation database
- SYN cookies

## Application layer DoS
- Algorithmic complexity attacks. Examples: using inputs that cause hashtable collisions and malicious GraphQL queries
- Writing scripts to increase application load. For example, writing a script to post thousands of comments per second on a blog. CAPTCHA and verifying people before granting API access are two defenses.
- Massive over-provisioning -- either yourself, or by paying a CDN
