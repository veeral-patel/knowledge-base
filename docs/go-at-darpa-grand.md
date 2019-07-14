# Go at the DARPA Grand Challenge (GopherCon 2017)

[Talk on YouTube](https://www.youtube.com/watch?v=lD0Qx7ZB_MU)

## About the 2016 Grand

- Each team is given vulnerable binaries
- Goal: prevent your binaries from being exploited by malicious inputs, and exploit other teams' binaries

## This team's idea

- Built an IDS which captured packets, flagged + blocked anomalous inputs, and stored these flagged inputs in a database
- Used gopacket to store and parse packets
- Problem - program dropping packets, due to too many incoming packets
- Solution - write goroutines for parsing, filtering, storing data. This way, you can operate on a lot of packets at once, in parallel
- Note: they only parallelized storing data, as that was their bottleneck
