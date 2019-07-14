# CH3 - Protocols

From ["Security Engineering" by Ross Anderson](http://www.cl.cam.ac.uk/~rja14/book.html)

## What is a protocol?

A protocol specifies how principals (users, programs, computers, etc) communicate

The world’s payment system has dozens of protocols - between human and ATM, between ATM and bank, between banks, etc

## Car key fob protocol

- Electronic car key broadcasts a serial number in cleartext to open the car

### Problems:

1. The serial number is only 16 bits. If you have 300 cars in parking lot, you only need to guess one of 300 serial numbers
2. Serial number can be captured and played back later
3. Lots of people (DMV, insurance, etc) know the serial number

### Possible solutions:

1. Just encrypt the serial number with some shared key. Problem - Attacker can just replay the ciphertext!
2. Idea 1, but to mitigate capture/replay attacks, add a nonce

## Parking garage key protocol

Say you scan a card to open a parking garage.

1. Your card sends its serial number
2. Then, the card sends encrypt([serial number, nonce])

Here, we concatenate the serial number and nonce and encrypt it with a card-specific key.

_This note is incomplete._
