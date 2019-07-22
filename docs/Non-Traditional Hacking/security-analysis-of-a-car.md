# Experimental Security Analysis of a Modern Automobile

[Paper link](http://www.autosec.org/pubs/cars-oakland2010.pdf)

## Introduction

- Cars have 100 MB of binary code, or 100 million LOC
- Spread out 50-70 electronic control units
- ECUs connected by internal network buses
- This paper is about attacks once the attacker gains access to the car

## Attack surface

- On-Board Diagnostics Port
- User modifiable subsystems, like audio systems, are connected to internal networks
- So are short range wireless devices (bluetooth, etc)
- Telematics systems (crash response, stolen vehicle recovery) integrate internal networks with remote control center over cellular data
- “Car as a platform” — third party apps running on car
- Vehicle to vehicle communications
- Vehicle to infrastructure communications

## Background

- Some features require complex interactions across ECUs
  - For example, Electronic Stability Control
- Standardized digital buses: Controller Area Network (CAN)
- Standardized software architecture for ECUs: AUTOSAR
- Cars have a few buses with different purposes
  - High speed bus for real time data (like speed)
  - Low speed bus for car doors, lights, etc
- You’d expect these buses to be separated. But they are bridged, to allow rules like “if air bags deploy, unlock car doors”

## Related Work

- Potential vulnerabilities in cars
- V2V vulnerabilities 18
- Theft related access control 11, 16, 3

## Attack Vectors

- Or, how the attacker first gains access to the car
- Physical access
  - Plant rogue component in car’s internal network. Either permanently, or use it to install malware onto other ECUs
  - How to gain physical access?
    - Break into car using vulnerability (theft related ACL)
    - Convince friend/valet/trusted person
    - Disguise component as a harmless device and sell to owner
- Wireless interfaces in car
  - Some interfaces are short distance, but others have very high range
  - Compromise ECUs through network, then escalate privileges based on this paper’s results

## Test Environments

- Bench: extracted individual pieces of hardware and analyzed them
- Stationary car
- Moving car

## Controller Area Network (CAN) Attacks

### CAN Architecture

- No concept of network addresses
- Every message is sent to every node, which decides whether or not to process it (publish/subscribe model)
- Sometimes have separate, but bridged high-speed and low-speed physical layers

### CAN Vulnerabilities

- CAN broadcasts all packets to all nodes. This means malicious nodes can sniff other ECUs’ packets. Malicious nodes can also send spoofed packets to any other ECU.
- Vulnerable to DOS. First of all, packet flooding is easy due to broadcast. Second, a node can become “dominant” and block other nodes from getting packets.
- No authenticator fields. CAN packets don’t have any authentication field, or even a source field. Any ECU can indistinguishably send any packet to any other ECU. A single hacked ECU can attack or control any other ECU.

## ECU attacks

- Packet sniffing
- Targeted probing
- Fuzzing
- Reverse engineering

## Attackable devices

- Radio
- Instrument Panel Cluster
- Body Controller
- Engine
- Brakes
- HVAC
- Generic Denial of Service

## Attacks involving multiple components

- Speedometer
- Lights out
- Self destruct
- Bridging internal CAN networks
- Hosting code; wiping code
