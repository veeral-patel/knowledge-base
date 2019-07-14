# Living in the Shadow of the Shadow Brokers (SANS 2018)

Talk by Jake Williams at SANS DFIR Summit 2018

[Talk on YouTube](https://www.youtube.com/watch?v=xuUMlNx72xI)

## Background

- The Shadow Brokers stole exploits, most notably ETERNALBLUE, from the Equation Group (NSA) in 2017
- We don't know who Shadow Brokers are
- Generally, to attribute a threat actor, examine its `Intent`, `Opportunity`, and `Capability`

## How did the Shadow Brokers get the exploits?

We don't know, but some possibilities:

- An insider leaked them
- Hack of NSA's networks
- An employee took files home (like Harold Martin, who took 50 TB home from the NSA), then the files were stolen

## EternalBlue (MS017-010) Released

- A leaked exploit, used in WannaCry and NotPetya
- An zero day vulnerability in Server Message Block (SMB)

## Tool to Stop/Modify Windows Event Logs Released

- To stop Windows Event logging, the tool finds the thread in `lsass` that logs events, then suspends it

### Windows Event Log edits can be detected, though

- Attacker may edit a Windows logon event, but forget to edit the corresponding logout event
- Defenders can also examine other forensics artifacts, instead of event logs

## Look at the dump!

- The Shadow Brokers dump included IOCs of other nation-states, for counter intelligence
- Attackers are looking at them and copying code from them
- 1 undergrad student hacked a university network, then used code from the Shadow Brokers to edit event logs

## Shadow Brokers broke threat models

- You may assume governments may never target you, and you may be correct, but due to leaks like this, nation-state capabilities are democratized
- Your threat model will no longer protect you
- Question to self: what are some other times threat models can be broken, like they were here?
