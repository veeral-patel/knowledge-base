# CH26 - System Evaluation and Assurance

From ["Security Engineering" by Ross Anderson](http://www.cl.cam.ac.uk/~rja14/book.html)

Problem: How do you obtain confidence that a system is secure?

## Security testing

- Look for common vulnerabilities (SQL injection, XSS, etc)
- Run static analysis tools - linters, detect-secrets, etc
- Read code and think of edge cases programmer forgot about
- Look for denial of service and side channel vulnerabilities
- Taint analysis
- Bug bounty programs
- Fuzzing
- Look for misconfigurations

## Formal methods

- Can be useful in verifying crypto and protocols

### Problems

- Can have issues in the implementation, rather than the design, of a system
- Proofs our proof relies on may be proven false
- The proof's may not be valid in real life (ie, a certain minimum key length)

## Fault Injection

- Idea: intentionally introduce vulnerabilities into software
- Then, measure how many of those vulnerabilities our security tester finds, to determine how effective our tester is
