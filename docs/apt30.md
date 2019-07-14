# APT30

## Overview

- Can infect air gapped networks using USBs
- First attacks observed in 2005
- Used the same few tools to target many organizations across Southeast Asia

## Systematic Malware Development

- Each backdoor has a version number. If less than reference number, then automatically update malware.
- Malware authors work in shifts and in teams
- Malware is modular and has been modified over time to create variants.
- 2 main branches of BACKSPACE backdoor, each with a different set of commands.

## Two Stage C2

- Backdoors are hardcoded with initial set of C2 domains
- By default, infected endpoints cannot be accessed interactively
- Only endpoints asked to connect to second stage C2 can connect to second stage C2
- Infected endpoints who connect to second stage C2 _can_ be accessed interactively
- This setup helps obfuscate the threat actor's important C2 beacons
