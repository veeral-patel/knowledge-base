# Code Security and Access Control

## Access control basics
### Access control matrix

Can edit
```
      Alice's wall | Bob's wall
Alice| true        | false
Bob  | false       | true
```

Have access control matrices for can read, can edit, can delete, etc

### Permission matrix

```
      Alice's wall | Bob's wall
Alice| read, write | read
 Bob  | read       | read, write
```

## Complete mediation
- Fancy way for saying all operations should undergo an access control check
  that can't be bypassed
- Also means you shouldn't access control decisions

### Reference monitor
- The reference monitor mediates all access to data
- Subject cannot access directly; operations must go through the reference
  monitor
- Example: All memory accesses are mediated by the memory controller, which
  enforces limits on what memory each process can access

#### Reference monitor criteria
- Unbypassable
- Tamper resistance
- Its correctness should be **verifiable**

## Trusted computing base (TCB)
- The TCB is the subset of a system that must be correct for some security goal to be achieved
- A reference monitor is part of the trusted computing base for ensuring
  people can't access resources they're not authorized to access
- Make the reference monitor as small as possible

## Privilege separation in Chrome
- Problem: drive-by malware can exploit a browser bug to read/write local
  files
- Solution: Chrome separates the rendering engine, where most of the bugs are, from the browser kernel, which can read/write to the filesystem
- The browser kernel is the TCB for ensuring drive by malware cannot
  read/write local files
- By isolating the browser kernel from the rendering engine, we've made the TCB as small as possible (in addition to separating privileges)!

## Time-to-Use vs Time-To-Check
- Idea: between the time you can check something and the time you use it, the check decision may get invalidated
- For example: you check if the user has enough balance, then you let him
  withdraw money. but between your check and his withdrawal, he might've
withdrawn money from somewhere else!
