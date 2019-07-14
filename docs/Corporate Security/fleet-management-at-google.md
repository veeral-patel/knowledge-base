# Fleet management at scale at Google

[Google whitepaper](https://services.google.com/fh/files/misc/fleet_management_at_scale_white_paper.pdf)

Google has 250k desktops and laptops - Windows, Macs, Linux, ChromeOS

## Imaging

1. Build image based on OS. Include Puppet in all images.
2. Push the image to computers

Tools:

- macOS - AutoDMG
- Windows - created glazier
- Linux - PXE netboot

## To install software

- Mac - created simian
- Linux - created Rapture
- Windows - SCCM, moving to rapture

## Encrypting devices

- Built [Cauliflower Vest](https://github.com/google/cauliflowervest) for disk encryption
  for Linux, Windows, Mac

## OS Updates

- OS updates nag employees with increasing frequently
- Worst case, block access to resources until employee updates
- Finally, can force OS updates remotely after a pop-up notification

## Binary whitelisting

- Santa (macOS)
- Carbon Black (Windows)

## Installing software

Employees can install any software they want as long as:

- it’s been pre-approved by IT
- or it passes automated security checks and another person signs off on it

IT proactively runs security checks on and pre-approves software that gets popular across fleet
