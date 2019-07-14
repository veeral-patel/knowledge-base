# CH11 - Physical Protection

From ["Security Engineering" by Ross Anderson](http://www.cl.cam.ac.uk/~rja14/book.html)

## Building a secure system

1. Create a threat model (list all kinds of attacks you need to defend against)
2. Design the system
3. Test the system

Internalize the weakest link principle!

### Defense mechanisms within the system

1. Deter
2. Detect
3. Alarm
4. Delay
5. Respond

I would add "insure", as well.

### Need a systematic way to enumerate attacks

I've looked into threat modeling, but I can't find a systematic method for enumerating all possible
attacks against a system

- Say you're protecting against someone robbing a bank
- You may assume the robbers will walk in the front door with guns
- So you add human guards, CCTV cameras, etc
- But you don't consider that the attacker could take a person's family hostage
- Or spoof a cash pickup order from another bank

## Threat model

- Instead of asking "Is this system secure?", ask "Is this system secure against person X in environment Y?"

### Hierarchy of threat actors for a robbery

- Addict - unskilled
- Convicted felon - skilled
- Gentleman criminal - skilled with insider help
- Terrorist - highly skilled & lots of resources

## Deter

Say you want to deter car theft.

- You can address the root problem, say a person can't get home one day, by investing in public transit
- Or if people are selling cars for parts, the government can subsidize hidden trackers
  like Lojack and shut down the shops that buy stolen cars

### Defenses against physical attacks

- Deter - walls, security lighting, open spaces, moats, dogs, guards, razor fences, locks, warning signs, snipers, gates, natural barriers (rivers, mountains, etc)
- Detect - CCTV, motion sensors, guards

### Caveats regarding walls and barriers

- Most doors can be broken with a battering ram, sledgehammer, etc--no key required!
- Secure the door _and_ the roof! This is why datacenters, bank vaults, etc have reinforced concrete walls/floors/roofs with steel doorframes
- A thief working undisturbed all week can penetrate 8 inches of concrete, so detection is a must

## How to steal a painting

- Pull alarm constantly so people don't trust it
- Grabbing painting after hours and escaping through fire exit
- Cutting off electricity to disable alarm. (This is why failing closed matters!)
- Cutting off wire between sensors and alarm or telephone wires to police
- Substituting alarm with non-functioning alarm
