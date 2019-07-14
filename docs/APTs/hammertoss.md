# HAMMERTOSS

## Overview

- First observed in 2014
- Attributed to the Russian government
  - Work hours align with Moscow, St Petersberg work hours
  - Don't work on Russian holidays
- HAMMERTOSS uses anti-forensic techiques
- Monitors victim's efforts to get rid of malware and actively responds to them
- Quickly modifies malware to avoid detection

## Backdoor Has Many C&C Channels

- HAMMERTOSS's backdoor leverages tweets and steganographic images on GitHub for C&C
- It can also upload data to multiple cloud services
- This allows attackers to easily switch C&C sources without getting caught

## Attack Lifecycle

### 1. Everyday, each backdoor generates a unique Twitter handle

Say an infected endpoint is named `WORK01` and today's date is `09/11/98` => Twitter handle would be `09bob111998`

### 2. Everyday, APT operators manually register the Twitter handle for every infected endpoint

If the operators don't register the handle an infected endpoint one day, the backdoor does nothing
that day.

The operators tweet an URL and a hashtag.

### 3. The backdoor scrapes the Twitter page

- Finds the one (and only) tweet with the URL and hashtag
- The backdoor has certain restrictions to blend in with normal traffic.
- For example, it only checks twitter during work hours and doesn't check Twitter for the first X
  days after being installed

### 4. URL redirects to a GitHub page

- The backdoor downloads an steganographic image from the GitHub page.

### 5. HAMMERTOSS extracts encrypted data from the image

- The backdoor decrypts the data to get commands to execute.

### 6. HAMMERTOSS backdoor runs the commands

- Advantage of unique image for every client - can't detect it in VirusTotal
- This is a two stage C&C. Visit Twitter, get GitHub link, download image, execute commands.

## Full Example

This tweet:

```
Follow doctorhandbook.com #101docto
```

Means:

- Download the image from doctorhandbook.com (which redirects to a GitHub link)
- A hidden ZIP starts 101 bytes into the image.
- The ZIP's decryption password is "docto"
