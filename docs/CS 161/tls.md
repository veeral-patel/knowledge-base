# SSL/TLS

[Slides from CS 161](http://www-inst.cs.berkeley.edu/~cs161/sp18/slides/2.22.TLS.pdf)

## Goal: a secure end-to-end channel
- End-to-end: client trusts server, with no need to trust any intermediate
  nodes
- Threats: eavesdropping (solve with encryption), manipulation (solve with
  integrity), replay attacks, DoS attacks, impersonation (solve with
  signatures) 

## SSL vs TLS

SSL and TLS are used interchangeably, but technically TLS is the correct term

- SSL = Secure Sockets Layer (predecessor)
- TLS = Transport Layer Security (current)

Caveat: TLS encrypts any TCP traffic, it sits on top of TCP. It's NOT only for HTTP
